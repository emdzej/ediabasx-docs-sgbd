# DDE40KW0.prg

- Jobs: [281](#jobs)
- Tables: [7](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | DDE 4.0 fuer M57 |
| ORIGIN | BMW TI-431 Semmler |
| REVISION | 1.61 |
| AUTHOR | BMW TP-421 Weber, BMW TI-433 Schiefer, BMW ZM-E-31 Lexmueller, BMW TI-433 Schaller, BMW TI-431 Semmler |
| COMMENT | N/A |
| PACKAGE | 0.11 |
| SPRACHE | deutsch |

## Jobs

### Index

- [initialisierung](#job-initialisierung) - Default Init-Job
- [INFO](#job-info) - Information SGBD
- [UPROG_EIN](#job-uprog-ein) - Programmierspannung einschalten
- [UPROG_AUS](#job-uprog-aus) - Programmierspannung ausschalten
- [BLOCKLAENGE_MAX](#job-blocklaenge-max) - maximale Blocklaenge
- [DATEN_REFERENZ](#job-daten-referenz) - Job DATEN-Referenz
- [HW_REFERENZ](#job-hw-referenz) - Job HW-Referenz
- [ZIF](#job-zif) - Job ZIF
- [ZIF_BACKUP](#job-zif-backup) - Job ZIF_BACKUP
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender-Info-Feldes
- [IDENT_AIF](#job-ident-aif) - Ident und AIF zusammen lesen
- [ECU_CONFIG](#job-ecu-config) - Ident-Daten fuer DME
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Indentifikation, AIF, FS_Codes ShadowFS_Codes, ShadowFS_lang
- [GET_CURRAIFADR](#job-get-curraifadr) - ermittelt die Adresse des Momentan gueltigen AIF-Eintrags
- [AIF_SCHREIBEN](#job-aif-schreiben) - ermittelt die Adresse des Momentan gueltigen AIF-Eintrags
- [FLASH_LESEN](#job-flash-lesen) - Beliebige FLASH - Zellen auslesen
- [START_DIAGNOSTIC_SESSION](#job-start-diagnostic-session) - Status
- [FLASH_PROG_STATUS](#job-flash-prog-status) - Status
- [FLASH_LOESCHEN](#job-flash-loeschen) - Flash  - Zellen loeschen
- [FLASH_SCHREIBEN_ADRESSE](#job-flash-schreiben-adresse) - Beliebige Flash Zellen mit 02 beschreiben
- [FLASH_SCHREIBEN](#job-flash-schreiben) - Beliebige Flash Zellen  beschreiben
- [FLASH_SCHREIBEN_ENDE](#job-flash-schreiben-ende) - Beliebige EPROM - Zellen auslesen
- [SEED_KEY](#job-seed-key) - Schutzmechanismus SEED_KEY
- [IDENT](#job-ident) - Ident-Daten fuer DME
- [FS_LESEN_STATUS](#job-fs-lesen-status) - Auslesen des Fehlerspeichers
- [FS_SELEKTIV_LOESCHEN](#job-fs-selektiv-loeschen) - Auslesen des Fehlerspeichers
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers
- [FS_SHADOW_LESEN](#job-fs-shadow-lesen) - Auslesen des Fehlerspeichers
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [STATUS_CODIER_CHECKSUMME](#job-status-codier-checksumme) - Codier - Checksumme abfragen
- [ABGLEICH_LESEN_STARTMENGE](#job-abgleich-lesen-startmenge) - Startmengen-Abgleich lesen
- [ABGLEICH_LESEN_INJEKTOR_KLASSIERUNG](#job-abgleich-lesen-injektor-klassierung)
- [ABGLEICH_VERSTELLEN_INJEKTOR_KLASSIERUNG](#job-abgleich-verstellen-injektor-klassierung)
- [ABGLEICH_PROG_INJEKTOR_KLASSIERUNG](#job-abgleich-prog-injektor-klassierung)
- [ABGLEICH_LESEN_VERBR_KORFAKTOR](#job-abgleich-lesen-verbr-korfaktor)
- [ABGLEICH_VERSTELLEN_VERBR_KORFAKTOR](#job-abgleich-verstellen-verbr-korfaktor)
- [ABGLEICH_PROG_VERBR_KORFAKTOR](#job-abgleich-prog-verbr-korfaktor)
- [ABGLEICH_VERSTELLEN_STARTMENGE](#job-abgleich-verstellen-startmenge) - Startmenge Abgleich verstellen
- [ABGLEICH_PROG_STARTMENGE](#job-abgleich-prog-startmenge) - Startmenge Abgleich programmieren
- [ABGLEICH_LESEN_BEGR_MENGE](#job-abgleich-lesen-begr-menge) - BEGR_MENGEn-Abgleich lesen
- [ABGLEICH_VERSTELLEN_BEGR_MENGE](#job-abgleich-verstellen-begr-menge) - BEGR_MENGE Abgleich verstellen
- [ABGLEICH_PROG_BEGR_MENGE](#job-abgleich-prog-begr-menge) - BEGR_MENGE Abgleich programmieren
- [ABGLEICH_LESEN_BEGR_MENGE_ROH](#job-abgleich-lesen-begr-menge-roh) - BEGR_MENGEn-Abgleich lesen
- [ABGLEICH_VERSTELLEN_BEGR_MENGE_ROH](#job-abgleich-verstellen-begr-menge-roh) - BEGR_MENGE Abgleich verstellen
- [ABGLEICH_LESEN_LL_REGELUNG](#job-abgleich-lesen-ll-regelung) - LL-Regelung-Abgleich lesen
- [ABGLEICH_VERSTELLEN_LL_REGELUNG](#job-abgleich-verstellen-ll-regelung) - LL_REGELUNG Abgleich verstellen
- [ABGLEICH_PROG_LL_REGELUNG](#job-abgleich-prog-ll-regelung) - LL_REGELUNG Abgleich programmieren
- [ABGLEICH_LESEN_LLPN_REGELUNG](#job-abgleich-lesen-llpn-regelung) - LL-Regelung-Abgleich lesen
- [ABGLEICH_VERSTELLEN_LLPN_REGELUNG](#job-abgleich-verstellen-llpn-regelung) - LL_REGELUNG Abgleich verstellen
- [ABGLEICH_PROG_LLPN_REGELUNG](#job-abgleich-prog-llpn-regelung) - LL_REGELUNG Abgleich programmieren
- [ABGLEICH_LESEN_AGR_RUECK](#job-abgleich-lesen-agr-rueck) - AGR_RUECKn-Abgleich lesen
- [ABGLEICH_VERSTELLEN_AGR_RUECK](#job-abgleich-verstellen-agr-rueck) - AGR_RUECK Abgleich verstellen
- [ABGLEICH_PROG_AGR_RUECK](#job-abgleich-prog-agr-rueck) - AGR_RUECK Abgleich programmieren
- [ABGLEICH_LESEN_VOLL_MENGE](#job-abgleich-lesen-voll-menge) - BEGR_MENGEn-Abgleich lesen
- [ABGLEICH_VERSTELLEN_VOLL_MENGE](#job-abgleich-verstellen-voll-menge) - BEGR_MENGE Abgleich verstellen
- [ABGLEICH_PROG_VOLL_MENGE](#job-abgleich-prog-voll-menge) - BEGR_MENGE Abgleich programmieren
- [ABGLEICH_LESEN_ABGLEICHMENGE](#job-abgleich-lesen-abgleichmenge) - LADEDRUCK-Abgleich lesen
- [ABGLEICH_VERSTELLEN_ABGLEICHMENGE](#job-abgleich-verstellen-abgleichmenge) - LADEDRUCK Abgleich verstellen
- [ABGLEICH_PROG_ABGLEICHMENGE](#job-abgleich-prog-abgleichmenge) - LADEDRUCK Abgleich programmieren
- [ABGLEICH_LESEN_ABGLEICH_FLAG](#job-abgleich-lesen-abgleich-flag) - Kennung M_ABGLEICH_FLAG lesen
- [ABGLEICH_VERSTELLEN_ABGLEICH_FLAG](#job-abgleich-verstellen-abgleich-flag) - Kennung M_ABGLEICH_FLAG verstellen, 0 = nicht verbaut, 0xff = verbaut
- [ABGLEICH_PROG_ABGLEICH_FLAG](#job-abgleich-prog-abgleich-flag) - Kennung M_ABGLEICH_FLAG programmieren
- [ABGLEICHWERTE_LESEN](#job-abgleichwerte-lesen) - Lesen der Motorabgleichwerte
- [ABGLEICHWERTE_SCHREIBEN](#job-abgleichwerte-schreiben) - Beschreiben des internen Speichers mit den motorspezifischen Abgleichdaten
- [ABGLEICHFLAG_SCHREIBEN](#job-abgleichflag-schreiben) - Beschreiben des internen Speichers mit den motorspezifischen Abgleichdaten
- [ABGLEICHFLAG_LESEN](#job-abgleichflag-lesen) - Lesen des EEPROM-Speichers ab Adresse 0x0032
- [ABGLEICH_LESEN_MENGENDRIFT](#job-abgleich-lesen-mengendrift) - Mengendrift-Abgleich lesen
- [ABGLEICH_VERSTELLEN_MENGENDRIFT](#job-abgleich-verstellen-mengendrift) - Mengendrift Abgleich verstellen
- [ABGLEICH_PROG_MENGENDRIFT](#job-abgleich-prog-mengendrift) - LADEDRUCK Abgleich programmieren
- [HOLE_EMA_FELD](#job-hole-ema-feld)
- [ABGLEICH_LESEN_FGR_KLIMA](#job-abgleich-lesen-fgr-klima) - Kennung M_ABGLEICH_FLAG lesen
- [ABGLEICH_PROG_FGR_KLIMA](#job-abgleich-prog-fgr-klima) - Kennung M_ABGLEICH_FLAG programmieren
- [ABGLEICH_LESEN_FGR_VARIANTE](#job-abgleich-lesen-fgr-variante) - FGR-Variante-Abgleich lesen
- [ABGLEICH_VERSTELLEN_FGR_VARIANTE](#job-abgleich-verstellen-fgr-variante) - FGR_VARIANTE_Abgleich verstellen
- [ABGLEICH_PROG_FGR_VARIANTE](#job-abgleich-prog-fgr-variante) - FGR_VARIANTE_Abgleich programmieren
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [STEUERN_SYNC_MODE](#job-steuern-sync-mode)
- [WECHSELCODE_SYNC_DME](#job-wechselcode-sync-dme) - Wechselcodesynchronisation EWS 3 - DME anstossen
- [STATUS_SYNC_MODE](#job-status-sync-mode)
- [STEUERN_AGR_STELLER](#job-steuern-agr-steller) - ARF - Steller  ansteuern ,  - - 10%%
- [STEUERN_EKP](#job-steuern-ekp) - ARF-Steller ansteuern ,  0 oder 100%
- [STEUERN_GLUEHRELAIS](#job-steuern-gluehrelais) - Gluegrelais ansteuern ,  0 oder 100%
- [STEUERN_KLIMAKOMPRESSOR](#job-steuern-klimakompressor) - StellerKlimakompressor ansteuern ,  0 oder 100
- [STEUERN_LADEDRUCKSTELLER](#job-steuern-ladedrucksteller) - Ladedrucksteller ansteuern ,  5-95%
- [STEUERN_E_LUEFTER](#job-steuern-e-luefter) - E-Luefter ansteuern ,  5-95%
- [STEUERN_MOTORLAGER](#job-steuern-motorlager) - Motorlager ansteuern ,  0 oder 100%
- [STEUERN_OELDRUCKSCHALTER](#job-steuern-oeldruckschalter) - Oeldruckschalteranzeige ansteuern ,  0 oder 100%
- [STEUERN_DRALLKLAPPE](#job-steuern-drallklappe) - Drallklappe ansteuern ,  ,  0 oder 100%
- [STEUERN_KUEHLWASSERHEIZUNG](#job-steuern-kuehlwasserheizung) - Elektrische Kuehlwasserheizung ,  5 bis 95%
- [STEUERN_KS_HDPUMPE_ABSCHALTUNG](#job-steuern-ks-hdpumpe-abschaltung) - Railhochdruckpumpe Elementabschaltung   ansteuern ,  0 oder 100%
- [STEUERN_ENDE_SELECTIV](#job-steuern-ende-selectiv)
- [START_SYSTEMCHECK_ZYL_SEL_MENGENKOR](#job-start-systemcheck-zyl-sel-mengenkor) - Start zylinderselektive Mengenkorrekturen
- [START_SYSTEMCHECK_ZYL_SEL_DREHZAHL](#job-start-systemcheck-zyl-sel-drehzahl) - Start zylinderselektive Drehzhahlen lesen
- [STOP_SYSTEMCHECK](#job-stop-systemcheck) - Stop Systemtest
- [MW_SELECT_LESEN](#job-mw-select-lesen) - Messwerteblock selectiv lesen
- [TEL_ROH](#job-tel-roh) - Rohtelegramm ohne Header lesen
- [STATUS_DIGITAL](#job-status-digital) - Status Schalteingaenge
- [STATUS_DIGITAL1](#job-status-digital1) - Status Schalteingaenge
- [STATUS_DIGITAL2](#job-status-digital2) - Status Schalteingaenge
- [STATUS_DIGITAL3](#job-status-digital3) - Status Schalteingaenge
- [STATUS_DIGITAL4](#job-status-digital4) - Status Schalteingaenge
- [STATUS_LAUFUNRUHE_LLR_MENGE](#job-status-laufunruhe-llr-menge) - Auslesen selektive Mengenkorrektur
- [STATUS_LAUFUNRUHE_DREHZAHL](#job-status-laufunruhe-drehzahl) - Auslesen selektive Mengenkorrektur
- [ABGLEICH_KIC_VERSTELLEN_PROGRAMMIEREN](#job-abgleich-kic-verstellen-programmieren) - FGR-Funktion und Mainswitch konfigurieren
- [MW_SELECT_LESEN_NORM](#job-mw-select-lesen-norm) - Messwerteblock selectiv lesen
- [MW_SELECT_LESEN_NORM_EINZEL](#job-mw-select-lesen-norm-einzel) - Messwerteblock selectiv lesen
- [MW_SELECT_LESEN_NORM2](#job-mw-select-lesen-norm2) - Messwerteblock selectiv lesen
- [STATUS_ANMPWG](#job-status-anmpwg) - PWG Pedalwertgeber Poti 1
- [STATUS_ANMUBT](#job-status-anmubt) - UBT Batteriespannung
- [STATUS_ANMVDF](#job-status-anmvdf) - VDF Vorfoerderdruck
- [STATUS_ANMWTF](#job-status-anmwtf) - WTF Wassertemperatur
- [STATUS_ARMM_LIST](#job-status-armm-list) - M_L aktuelle Luftmasse
- [STATUS_ARMM_LSOLL](#job-status-armm-lsoll) - M_L Sollwert fuer AGR-Regelung
- [STATUS_DZMNMIT](#job-status-dzmnmit) - N Drehzahl
- [STATUS_EHMFARS](#job-status-ehmfars) - Tastverhaeltnis Ansteuerung AGR-Steller
- [STATUS_EHMFEKP](#job-status-ehmfekp) - Tastverhaeltnis Ansteuerung Vorfoerderpumpe
- [STATUS_EHMFGRS](#job-status-ehmfgrs) - Tastverhaeltnis Ansteuerung Gluehrelais
- [STATUS_EHMFKDR](#job-status-ehmfkdr) - Tastverhaeltnis Ansteuerung Raildruckregelventil
- [STATUS_EHMFKLI](#job-status-ehmfkli) - Tastverhaeltnis Ansteuerung Klimakompressor
- [STATUS_EHMFLDS](#job-status-ehmflds) - Tastverhaeltnis Ansteuerung Ladedrucksteller
- [STATUS_EHMFMLS](#job-status-ehmfmls) - Tastverhaeltnis Ansteuerung Elektroluefter
- [STATUS_EHMFMML](#job-status-ehmfmml) - Tastverhaeltnis Ansteuerung Motorlager
- [STATUS_LDMP_LLIN](#job-status-ldmp-llin) - aktueller Ladedruck  / Luftdruck
- [STATUS_LDMP_LSOLL](#job-status-ldmp-lsoll) - Sollwert Ladedruck
- [STATUS_MRMM_EFAHR](#job-status-mrmm-efahr) - M_E Fahrmenge nach Laufruheregler
- [STATUS_ZUMP_RAIL](#job-status-zump-rail) - Raildruck fuer Mengenzumessung
- [STATUS_ZUMPQSOLL](#job-status-zumpqsoll) - Raildruck Sollwert
- [STATUS_ADMADF](#job-status-admadf) - ADF Rohwert Atmosphaerendruck
- [STATUS_ADMIDV](#job-status-admidv) - IDV Rohwert Istwert Stromregelung Druckregelventil
- [STATUS_ADMKDF](#job-status-admkdf) - KDF Rohwert Raildruck
- [STATUS_ADMLDF](#job-status-admldf) - LDF Rohwert Ladedruck
- [STATUS_ADMLMM](#job-status-admlmm) - LMM Rohwert Luftmasse
- [STATUS_ADMLTF](#job-status-admltf) - LTF Rohwert Lufttemperatur
- [STATUS_ADMPGS](#job-status-admpgs) - PGS Rohwert Pedalwertgeber Poti 2
- [STATUS_ADMPWG](#job-status-admpwg) - PWG Rohwert Pedalwertgeber Poti 1
- [STATUS_ADMUBT](#job-status-admubt) - UBT Rohwert Batteriespannung
- [STATUS_ADMUC1](#job-status-admuc1) - UC1 Rohwert Kondensatorspannung 1 fuer Zylinder 1,2,3
- [STATUS_ADMUC2](#job-status-admuc2) - UC2 Rohwert Kondensatorspannung 2 fuer Zylinder 4,5,6
- [STATUS_ADMUG1](#job-status-admug1) - UG1 Rohwert Speisespannung 1 fuer Pedalwertgeber 2, Ladedruckfuehler, Luftmassenmesser
- [STATUS_ADMUG2](#job-status-admug2) - UG2 Rohwert Speisespannung 2 fuer Pedalwertgeber 1, Kraftstoff- ,Vorfoerderdruckfuehler
- [STATUS_ADMVDF](#job-status-admvdf) - VDF Rohwert Vorfoerderdruck
- [STATUS_ADMWTF](#job-status-admwtf) - WTF Rohwert Wassertemperatur
- [STATUS_ANMADF](#job-status-anmadf) - ADF Atmosphaerendruck
- [STATUS_ANMIDV](#job-status-anmidv) - IDV Istwert Stromregelung Druckregelventil
- [STATUS_ANMKDF](#job-status-anmkdf) - KDF Raildruck
- [STATUS_ANMLDF](#job-status-anmldf) - LDF Ladedruck
- [STATUS_ANMLMM](#job-status-anmlmm) - LMM Luftmasse
- [STATUS_ANMLTF](#job-status-anmltf) - LTF Lufttemperatur
- [STATUS_ANMPGS](#job-status-anmpgs) - PGS Pedalwertgeber Poti 2
- [STATUS_ANMUC1](#job-status-anmuc1) - UC1 Kondensatorspannung 1 fuer Zylinder 1,2,3
- [STATUS_ANMUC2](#job-status-anmuc2) - UC2 Kondensatorspannung 2 fuer Zylinder 4,5,6
- [STATUS_ANMUG1](#job-status-anmug1) - UG1 Speisespannung 1 fuer Pedalwertgeber 2, Ladedruckfuehler, Luftmassenmesser
- [STATUS_ANMUG2](#job-status-anmug2) - UG2 Speisespannung 2 fuer Pedalwertgeber 1, Kraftstoff- ,Vorfoerderdruckfuehler
- [STATUS_ANOU_ADF](#job-status-anou-adf) - ADF Spannung Atmosphaerendruckfuehler
- [STATUS_ANOU_IDV](#job-status-anou-idv) - IDV Spannung zur Strommessung Druckregelventil
- [STATUS_ANOU_KDF](#job-status-anou-kdf) - KDF Spannung Raildruckfuehler
- [STATUS_ANOU_LDF](#job-status-anou-ldf) - LDF Spannung Ladedruckfuehler
- [STATUS_ANOU_LMM](#job-status-anou-lmm) - LMM Spannung Luftmassenmesser
- [STATUS_ANOU_LTF](#job-status-anou-ltf) - LTF Spannung Lufttemperaturfuehler
- [STATUS_ANOU_PGS](#job-status-anou-pgs) - PGS Spannung Pedalwertgeber Poti 2
- [STATUS_ANOU_PWG](#job-status-anou-pwg) - PWG Spannung Pedalwertgeber Poti 1
- [STATUS_ANOU_UBT](#job-status-anou-ubt) - UBT Spannung Batteriespannung
- [STATUS_ANOU_UC1](#job-status-anou-uc1) - UC1 Spannung Kondensatorspannung 1 fuer Zylinder 1,2,3
- [STATUS_ANOU_UC2](#job-status-anou-uc2) - UC2 Spannung Kondensatorspannung 2 fuer Zylinder 4,5,6
- [STATUS_ANOU_UG1](#job-status-anou-ug1) - UG1 Spannung Speisespannung 1 fuer Pedalwertgeber 2, Ladedruckfuehler, Luftmassenmesser
- [STATUS_ANOU_UG2](#job-status-anou-ug2) - UG2 Spannung Speisespannung 2 fuer Pedalwertgeber 1, Kraftstoff- ,Vorfoerderdruckfuehler
- [STATUS_ANOU_VDF](#job-status-anou-vdf) - VDF Spannung Vorfoerderdruckfuehler
- [STATUS_ANOU_WTF](#job-status-anou-wtf) - WTF Spannung Wassertemperaturfuehler
- [STATUS_AROIST_5](#job-status-aroist-5) - M_L normierte Luftmasse (nicht T_L/P_ADF-korrig.)
- [STATUS_AROREG_2](#job-status-aroreg-2) - AGR-Status  Regelung / Steuerung / Abschaltung
- [STATUS_AROSOLL_5](#job-status-arosoll-5) - M_L Luft-Sollwert nach Sollwertbegrenzung
- [STATUS_CAMN_EL](#job-status-camn-el) - MLS Drehzahlstufe E-Luefter
- [STATUS_CAMS_AC](#job-status-cams-ac) - Schalter Klimabereitschaft
- [STATUS_CAMS_KO](#job-status-cams-ko) - Schalter Klimakompressor
- [STATUS_CAOVERB](#job-status-caoverb) - Kraftstoffverbrauch fuer CAN DDE4-VERBRAUCH
- [STATUS_COMGTR_OPT](#job-status-comgtr-opt) - Identifikation Handschalter/Automatik
- [STATUS_DIMDIG_0](#job-status-dimdig-0) - Auf logisch 0 erkannte Digitaleingaenge
- [STATUS_DIMDIG_1](#job-status-dimdig-1) - Auf logisch 1 erkannte Digitaleingaenge
- [STATUS_DIMDIGPREL](#job-status-dimdigprel) - Entprellte logische Zustaende der digitalen Eingaenge
- [STATUS_DIMF_MFL](#job-status-dimf-mfl) - FGR Multifunktionslenkrad
- [STATUS_DZMNAKT](#job-status-dzmnakt) - N aktuelle Drehzahl aus letzter Periode
- [STATUS_DZMZMK1](#job-status-dzmzmk1) - Selektive Mengenkorrektur Zylinder 1
- [STATUS_DZMZMK2](#job-status-dzmzmk2) - Selektive Mengenkorrektur Zylinder 2
- [STATUS_DZMZMK3](#job-status-dzmzmk3) - Selektive Mengenkorrektur Zylinder 3
- [STATUS_DZMZMK4](#job-status-dzmzmk4) - Selektive Mengenkorrektur Zylinder 4
- [STATUS_DZMZMK5](#job-status-dzmzmk5) - Selektive Mengenkorrektur Zylinder 5
- [STATUS_DZMZMK6](#job-status-dzmzmk6) - Selektive Mengenkorrektur Zylinder 6
- [STATUS_DZMZN1](#job-status-dzmzn1) - Selektive Drehzahl Zylinder 1
- [STATUS_DZMZN2](#job-status-dzmzn2) - Selektive Drehzahl Zylinder 2
- [STATUS_DZMZN3](#job-status-dzmzn3) - Selektive Drehzahl Zylinder 3
- [STATUS_DZMZN4](#job-status-dzmzn4) - Selektive Drehzahl Zylinder 4
- [STATUS_DZMZN5](#job-status-dzmzn5) - Selektive Drehzahl Zylinder 5
- [STATUS_DZMZN6](#job-status-dzmzn6) - Selektive Drehzahl Zylinder 6
- [STATUS_EDMRSTCD](#job-status-edmrstcd) - Restart Code
- [STATUS_FBMBSTZ_UB](#job-status-fbmbstz-ub) - UB Betriebsstunden
- [STATUS_FBMDIA_C](#job-status-fbmdia-c) - Diagnoselampe ueber CAN
- [STATUS_FBMMIL_C](#job-status-fbmmil-c) - MIL Malfunction Indikator Lamp ueber CAN
- [STATUS_FBMSDIAL](#job-status-fbmsdial) - Anforderung Diagnoselampe aus Fehlerbehandlung (0:Aus,1:Ein,2:Blinken)
- [STATUS_FBODIALA](#job-status-fbodiala) - Diagnose - Lampe Status (255 = EIN)
- [STATUS_FBOS_00](#job-status-fbos-00) - Defekte Pfade 1 bis 16
- [STATUS_FBOS_02](#job-status-fbos-02) - Defekte Pfade 17 bis 32
- [STATUS_FBOS_04](#job-status-fbos-04) - Defekte Pfade 33 bis 48
- [STATUS_FBOS_06](#job-status-fbos-06) - Defekte Pfade 49 bis 64
- [STATUS_FBOS_08](#job-status-fbos-08) - Defekte Pfade 65 bis 80
- [STATUS_FGM_VZUN](#job-status-fgm-vzun) - Verhaeltnis Geschwindigkeit/Drehzahl (V/N aktuell)
- [STATUS_FGMBESCH](#job-status-fgmbesch) - Beschleunigung
- [STATUS_FGMFGAKT](#job-status-fgmfgakt) - aktuelle Geschwindigkeit
- [STATUS_GSOGS_PHA](#job-status-gsogs-pha) - Gluehzeitsteuerung Gluehphase
- [STATUS_LDMADF](#job-status-ldmadf) - aktueller Atmosphaerendruck
- [STATUS_LDMT_LTGG](#job-status-ldmt-ltgg) - Errechnete Lufttemperatur
- [STATUS_LDOTVSTEU](#job-status-ldotvsteu) - Tastverhaeltnis Steuerung
- [STATUS_MRMCASE_A](#job-status-mrmcase-a) - ARD Zustand-Bits der aktiven Ruckeldaempfung
- [STATUS_MRMCASE_L](#job-status-mrmcase-l) - LLR Zustand-Bits der Leerlaufregelung
- [STATUS_MRMF_GANG](#job-status-mrmf-gang) - FGR aktuelle Gangstufe
- [STATUS_MRMFG_SOLL](#job-status-mrmfg-soll) - V Sollwert Fahrgeschwindigkeit von FGR
- [STATUS_MRMKM_AKT](#job-status-mrmkm-akt) - aktueller km-Stand von Kombiinstrument
- [STATUS_MRML_FGR](#job-status-mrml-fgr) - FGR-Status-Indicator-Lampe ueber CAN
- [STATUS_MRMLLRIANT](#job-status-mrmllriant) - M_E Menge aus I-Anteil des PI-Leerlaufreglers
- [STATUS_MRMLLRPANT](#job-status-mrmllrpant) - M_E Menge aus P-Anteil des PI-Leerlaufreglers
- [STATUS_MRMM_DXMSR](#job-status-mrmm-dxmsr) - M_E externer Momenteneingriff MSR
- [STATUS_MRMM_EAKT](#job-status-mrmm-eakt) - M_E Aktuelle Einspritzmenge (ohne ARD)
- [STATUS_MRMM_EARD](#job-status-mrmm-eard) - M_E Menge ARD - Gesamt vor Begrenzung
- [STATUS_MRMM_EBEGR](#job-status-mrmm-ebegr) - M_E resultierende Begrenzungsmenge
- [STATUS_MRMM_EDELB](#job-status-mrmm-edelb) - M_E begrenzte Abgleichmenge
- [STATUS_MRMM_EFGR](#job-status-mrmm-efgr) - M_E Wunschmenge aus Fahrgeschwindigkeitsregelung
- [STATUS_MRMM_EKORR](#job-status-mrmm-ekorr) - M_E Fahrmenge korrigiert mit Vollast- und Mengenabgleich
- [STATUS_MRMM_ELLR](#job-status-mrmm-ellr) - M_E Menge aus Leerlaufregelung
- [STATUS_MRMM_ELRR](#job-status-mrmm-elrr) - M_E Menge aus Laufruheregler
- [STATUS_MRMM_EMOT](#job-status-mrmm-emot) - M_E Einspritzmenge nach ARD
- [STATUS_MRMM_EPWG](#job-status-mrmm-epwg) - M_E Wunschmenge = f(PWG) aus Fahrverhaltenkennfeld
- [STATUS_MRMM_ESTAR](#job-status-mrmm-estar) - M_E resultierender Startmengen-Sollwert
- [STATUS_MRMM_EWUN](#job-status-mrmm-ewun) - M_E Fahrerwunschmenge nach externem Mengeneingriff
- [STATUS_MRMM_EWUNF](#job-status-mrmm-ewunf) - M_E Fahrerwunschmenge aus PWG oder FGR
- [STATUS_MRMN_LLBAS](#job-status-mrmn-llbas) - N Leerlaufsolldrehzahl
- [STATUS_MRMPWGFI](#job-status-mrmpwgfi) - PWG gefilterte Pedalwertgeber-Position
- [STATUS_MRMSTATUS](#job-status-mrmstatus) - Status Motorbetriebsphase
- [STATUS_MROFABZUST](#job-status-mrofabzust) - Zustand Ablaufsteuerung
- [STATUS_MROFGR_ABN](#job-status-mrofgr-abn) - FGR Abschalt-Bedingungen
- [STATUS_MROKICKDWN](#job-status-mrokickdwn) - Schalter Kickdown
- [STATUS_MROLLRDANT](#job-status-mrollrdant) - M_E Menge aus Leerlaufregler-DT1-Vorsteuerung
- [STATUS_MROLRRREG](#job-status-mrolrrreg) - Nsegm Segmentdrehzahl-Regelabweichung fuer Laufruheregler
- [STATUS_MROM_ARDFF](#job-status-mrom-ardff) - M_E Menge ARD - Fuehrungsformer
- [STATUS_MROMD_FAHR](#job-status-mromd-fahr) - Fahrerwunschmoment
- [STATUS_MROMD_REIB](#job-status-mromd-reib) - Reibmoment
- [STATUS_MROMD_SOLL](#job-status-mromd-soll) - Sollmoment
- [STATUS_XCMZ_E](#job-status-xcmz-e) - EWS Uebertragungsfehlerzaehler
- [STATUS_ZHOSYNC_ST](#job-status-zhosync-st) - Synchronisationsstatus des Zumesshandlers
- [STATUS_ZUMAB_HE](#job-status-zumab-he) - Ansteuerbeginn Haupteinspritzung
- [STATUS_ZUMAB_NE](#job-status-zumab-ne) - Ansteuerbeginn Nacheinspritzung
- [STATUS_ZUMAD_NE](#job-status-zumad-ne) - Ansteuerdauer Nacheinspritzung
- [STATUS_ZUOAB_VE1](#job-status-zuoab-ve1) - Ansteuerbeginn Voreinspritzung
- [STATUS_ZUOAD_HE](#job-status-zuoad-he) - Ansteuerdauer Haupteinspritzung
- [STATUS_ZUOAD_VE1](#job-status-zuoad-ve1) - Ansteuerdauer Voreinspritzung
- [STATUS_ZUOME_VE](#job-status-zuome-ve) - M_E Menge Voreinspritzung
- [STATUS_ZUOMEHE](#job-status-zuomehe) - M_E Menge Haupteinspritzung
- [STATUS_ZUOMEVGW](#job-status-zuomevgw) - GW-Kennfeld Menge Voreinspritzung
- [STATUS_ZUOVE_STAT](#job-status-zuove-stat) - Voreinspritzung - Schalter
- [STATUS_AN_LUFTTEMPERATUR](#job-status-an-lufttemperatur) - LTF Lufttemperatur
- [STATUS_LADEDRUCK](#job-status-ladedruck) - LDF Ladedruck
- [STATUS_MOTORDREHZAHL](#job-status-motordrehzahl) - N Drehzahl
- [STATUS_MOTORTEMPERATUR](#job-status-motortemperatur) - WTF Wassertemperatur
- [STATUS_PWG_FAHRERWUNSCH](#job-status-pwg-fahrerwunsch) - PWG Pedalwertgeber Poti 1
- [STATUS_PWG_POTI_SPANNUNG](#job-status-pwg-poti-spannung) - PWG Spannung Pedalwertgeber Poti 1
- [STEUERN_CHECK_ZUHEIZER](#job-steuern-check-zuheizer)
- [STEUERN_CHECK_ZUHEIZER_ECOS](#job-steuern-check-zuheizer-ecos)
- [STATUS_RAILDRUCK](#job-status-raildruck) - KDF Raildruck
- [STATUS_UBATT](#job-status-ubatt) - UBT Batteriespannung
- [STATUS_VORFOERDERDRUCK](#job-status-vorfoerderdruck) - VDF Vorfoerderdruck
- [STATUS_EHMFDRA](#job-status-ehmfdra) - Tastverhaeltnis Ansteuerung Drallklappe
- [ABGLEICH_VERSTELLEN_VERBR_KORFAKTOR_ROH](#job-abgleich-verstellen-verbr-korfaktor-roh)
- [ABGLEICH_LESEN_KDF_KENNLINIE](#job-abgleich-lesen-kdf-kennlinie) - Raildrucksensor Kennlinien -Abgleich lesen
- [ABGLEICH_VERSTELLEN_KDF_KENNLINIE](#job-abgleich-verstellen-kdf-kennlinie) - Mengendrift Abgleich verstellen
- [ABGLEICH_VERSTELLEN_KDF_KENNLINIE_ROH](#job-abgleich-verstellen-kdf-kennlinie-roh) - Mengendrift Abgleich verstellen
- [ABGLEICH_PROG_KDF_KENNLINIE](#job-abgleich-prog-kdf-kennlinie) - RAILDRUCHSENSOR Abgleich programmieren
- [ABGLEICH_LESEN_HFM](#job-abgleich-lesen-hfm) - HFM-Abgleich lesen
- [ABGLEICH_VERSTELLEN_HFM](#job-abgleich-verstellen-hfm) - HFM Abgleich verstellen
- [ABGLEICH_VERSTELLEN_HFM_ROH](#job-abgleich-verstellen-hfm-roh) - HFM Abgleich verstellen
- [ABGLEICH_PROG_HFM](#job-abgleich-prog-hfm) - HFM Abgleich programmieren
- [STATUS_LMM_MASSE](#job-status-lmm-masse) - LMM Spannung Luftmassenmesser

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
| ECU | string | Steuergerät im Klartext |
| ORIGIN | string | Steuergeräte-Verantwortlicher |
| REVISION | string | Versions-Nummer |
| AUTHOR | string | Namen aller Autoren |
| COMMENT | string | wichtige Hinweise |
| PACKAGE | string | Include-Paket-Nummer |
| SPRACHE | string | deutsch, english |

<a id="job-uprog-ein"></a>
### UPROG_EIN

Programmierspannung einschalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STATUS_UPROG_WERT | real | Programmierspannung als Info zurueck |
| STATUS_UPROG_EINH | string | Einheit V |

<a id="job-uprog-aus"></a>
### UPROG_AUS

Programmierspannung ausschalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-blocklaenge-max"></a>
### BLOCKLAENGE_MAX

maximale Blocklaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| BLOCKLAENGE_MAX_WERT | int | Blocklaenge fuer Telegramm |

<a id="job-daten-referenz"></a>
### DATEN_REFERENZ

Job DATEN-Referenz

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| DATEN_REF_SG_KENNUNG | string | SG-Kennung z.B. 011 fuer BMW |
| DATEN_REF_PROJEKT | string | Projektkennzeichnung |
| DATEN_REF_PROGRAMM_STAND | string | Programmstand |
| DATEN_REF_DATENSATZ | string | Datensatzkennung |
| DATEN_REF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |

<a id="job-hw-referenz"></a>
### HW_REFERENZ

Job HW-Referenz

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| HW_REF_SG_KENNUNG | string | SG-Kennung z.B. 011 fuer BMW |
| HW_REF_PROJEKT | string | Projektkennzeichnung |
| HW_REF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |

<a id="job-zif"></a>
### ZIF

Job ZIF

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ZIF_SG_KENNUNG | string | SG-Kennung z.B. 011 fuer BMW |
| ZIF_PROJEKT | string | Projektkennzeichnung |
| ZIF_PROGRAMM_STAND | string | Programmstand |
| ZIF_BMW_HW | string | BMW HW |
| ZIF_BMW_PST | string | BMW Programmstand |
| ZIF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |

<a id="job-zif-backup"></a>
### ZIF_BACKUP

Job ZIF_BACKUP

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ZIF_BACKUP_SG_KENNUNG | string | SG-Kennung z.B. 011 fuer BMW |
| ZIF_BACKUP_PROJEKT | string | Projektkennzeichnung |
| ZIF_BACKUP_PROGRAMM_STAND | string | Programmstand |
| ZIF_BACKUP_BMW_HW | string | BMW HW |
| ZIF_BACKUP_BMW_PST | string | BMW Programmstand |
| ZIF_BACKUP_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |

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

<a id="job-ident-aif"></a>
### IDENT_AIF

Ident und AIF zusammen lesen

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
| EGS_VORHANDEN | int | EGS vorhanden 1=ja ,  0=nein , 0xff=nicht unterstuetzt |

<a id="job-pruefcode-lesen"></a>
### PRUEFCODE_LESEN

Indentifikation, AIF, FS_Codes ShadowFS_Codes, ShadowFS_lang

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| PRUEFCODE | binary | Indentifikation, AIF, FS_Codes ShadowFS_Codes, ShadowFS_lang |

<a id="job-get-curraifadr"></a>
### GET_CURRAIFADR

ermittelt die Adresse des Momentan gueltigen AIF-Eintrags

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| AIF_ADRESSE | long | AIF Basisadresse |

<a id="job-aif-schreiben"></a>
### AIF_SCHREIBEN

ermittelt die Adresse des Momentan gueltigen AIF-Eintrags

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FAHRGESTELLNR | string |  |
| BMW_FERTIGUNGSDAT | string |  |
| BMW_SWNR | string |  |
| BMW_TYPPRUEFNR | long |  |
| BMW_ZBNR | long |  |
| PRG_GERAET_SER_NR | string |  |
| WERKSCODE | int |  |
| KM | int |  |
| PRG_STANDSNR | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| VERIFYBYTE | int |  |

<a id="job-flash-lesen"></a>
### FLASH_LESEN

Beliebige FLASH - Zellen auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_LESEN_ADRESSE | long | Uebergabeparameter, Startadresse High-Middle-Low HEX |
| FLASH_LESEN_ANZAHL_BYTE | int | Uebergabeparameter, Anzahl der auszulesenden BYTES |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| FLASH_LESEN_WERT | binary | nichts |

<a id="job-start-diagnostic-session"></a>
### START_DIAGNOSTIC_SESSION

Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| START_DIAGNOSTIC_SESSION_MODE | int | nichts |

<a id="job-flash-prog-status"></a>
### FLASH_PROG_STATUS

Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| FLASH_PROG_STATUS | int | nichts |

<a id="job-flash-loeschen"></a>
### FLASH_LOESCHEN

Flash  - Zellen loeschen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_LOESCHEN_ADRESSE | long | Uebergabeparameter, Startadresse High-Middle-Low |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| FLASH_LOESCHEN_STATUS | int | nichts |

<a id="job-flash-schreiben-adresse"></a>
### FLASH_SCHREIBEN_ADRESSE

Beliebige Flash Zellen mit 02 beschreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_SCHREIBEN_ADRESSE_ANFANG | long | Uebergabeparameter, Startadresse High-Middle-Low und Daten |
| FLASH_SCHREIBEN_ADRESSE_ENDE | long | Uebergabeparameter, Endadresse High-Middle-Low und Daten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| FLASH_SCHREIBEN_STATUS | int | nichts |

<a id="job-flash-schreiben"></a>
### FLASH_SCHREIBEN

Beliebige Flash Zellen  beschreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_SCHREIBEN_DATEN | binary | Uebergabeparameter, Startadresse High-Middle-Low und Daten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| FLASH_SCHREIBEN_STATUS | int | nichts |
| FLASH_SCHREIBEN_ANZAHL | int | nichts |

<a id="job-flash-schreiben-ende"></a>
### FLASH_SCHREIBEN_ENDE

Beliebige EPROM - Zellen auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

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

<a id="job-fs-lesen-status"></a>
### FS_LESEN_STATUS

Auslesen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_CODEHEX | binary | alle Fehlerbyte |

<a id="job-fs-selektiv-loeschen"></a>
### FS_SELEKTIV_LOESCHEN

Auslesen des Fehlerspeichers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FEHLER_0 | int | 0-65535 |
| FEHLER_1 | int | 0-65535 |
| FEHLER_2 | int | 0-65535 |
| FEHLER_3 | int | 0-65535 |
| FEHLER_4 | int | 0-65535 |
| FEHLER_5 | int | 0-65535 |
| FEHLER_6 | int | 0-65535 |
| FEHLER_7 | int | 0-65535 |
| FEHLER_8 | int | 0-65535 |
| FEHLER_9 | int | 0-65535 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-fs-lesen"></a>
### FS_LESEN

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
| F_ART9_NR | int | Fehlerart 9 Index |
| F_ART9_TEXT | string | Fehlerart 9 Text |
| F_ART10_NR | int | Fehlerart 10 Index |
| F_ART10_TEXT | string | Fehlerart 10 Text |
| F_ART11_NR | int | Fehlerart 11 Index |
| F_ART11_TEXT | string | Fehlerart 11 Text |
| F_ART12_NR | int | Fehlerart 12 Index |
| F_ART12_TEXT | string | Fehlerart 12 Text |
| F_ART13_NR | int | Fehlerart 13 Index |
| F_ART13_TEXT | string | Fehlerart 13 Text |
| F_ART14_NR | int | Fehlerart 14 Index |
| F_ART14_TEXT | string | Fehlerart 14 Text |
| F_ART15_NR | int | Fehlerart 15 Index |
| F_ART15_TEXT | string | Fehlerart 15 Text |
| F_ART16_NR | int | Fehlerart 16 Index |
| F_ART16_TEXT | string | Fehlerart 16  Text |
| F_VORHANDEN | int | Statusbit Fehler vorhanden |
| F_ART_BYTE | long | Fehlerartbyte als Rohwert ausgeben |
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

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Loeschen des Fehlerspeichers

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

<a id="job-abgleich-lesen-startmenge"></a>
### ABGLEICH_LESEN_STARTMENGE

Startmengen-Abgleich lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_LESEN_STARTMENGE_WERT | real | Aktuellen Abgleichwert |
| ABGLEICH_LESEN_STARTMENGE_STATUS | int | Rueckmeldebyte |

<a id="job-abgleich-lesen-injektor-klassierung"></a>
### ABGLEICH_LESEN_INJEKTOR_KLASSIERUNG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_LESEN_INJEKTOR_KLASSIERUNG_WERT | long | Aktuellen Abgleichwert |
| ABGLEICH_LESEN_INJEKTOR_KLASSIERUNG_STATUS | int | Rueckmeldebyte |

<a id="job-abgleich-verstellen-injektor-klassierung"></a>
### ABGLEICH_VERSTELLEN_INJEKTOR_KLASSIERUNG

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_VERSTELLEN_INJEKTOR_KLASSIERUNG_ROH_WERT | int | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_VERSTELLEN_INJEKTOR_KLASSIERUNG_ROH_STATUS | int | Status |

<a id="job-abgleich-prog-injektor-klassierung"></a>
### ABGLEICH_PROG_INJEKTOR_KLASSIERUNG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_PROG_INJEKTOR_KLASSIERUNG_STATUS | int | Status |

<a id="job-abgleich-lesen-verbr-korfaktor"></a>
### ABGLEICH_LESEN_VERBR_KORFAKTOR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_LESEN_VERBR_KORFAKTOR_ROH_WERT | int | Aktuellen Abgleichwert roh |
| ABGLEICH_LESEN_VERBR_KORFAKTOR_WERT | real | Aktuellen Abgleichwert |
| ABGLEICH_LESEN_VERBR_KORFAKTOR_STATUS | int | Rueckmeldebyte |

<a id="job-abgleich-verstellen-verbr-korfaktor"></a>
### ABGLEICH_VERSTELLEN_VERBR_KORFAKTOR

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_VERSTELLEN_VERBR_KORFAKTOR_WERT | real | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_VERSTELLEN_VERBR_KORFAKTOR_STATUS | int | Status |

<a id="job-abgleich-prog-verbr-korfaktor"></a>
### ABGLEICH_PROG_VERBR_KORFAKTOR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_PROG_VERBR_KORFAKTOR_STATUS | int | Status |

<a id="job-abgleich-verstellen-startmenge"></a>
### ABGLEICH_VERSTELLEN_STARTMENGE

Startmenge Abgleich verstellen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_VERSTELLEN_STARTMENGE_WERT | real | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_VERSTELLEN_STARTMENGE_STATUS | int | Status |

<a id="job-abgleich-prog-startmenge"></a>
### ABGLEICH_PROG_STARTMENGE

Startmenge Abgleich programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_PROG_STARTMENGE_STATUS | int | Status |

<a id="job-abgleich-lesen-begr-menge"></a>
### ABGLEICH_LESEN_BEGR_MENGE

BEGR_MENGEn-Abgleich lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_LESEN_BEGR_MENGE_WERT | real | Aktuellen Abgleichwert |
| ABGLEICH_LESEN_BEGR_MENGE_STATUS | int | Rueckmeldebyte |

<a id="job-abgleich-verstellen-begr-menge"></a>
### ABGLEICH_VERSTELLEN_BEGR_MENGE

BEGR_MENGE Abgleich verstellen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_VERSTELLEN_BEGR_MENGE_WERT | real | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_VERSTELLEN_BEGR_MENGE_STATUS | int | Status |

<a id="job-abgleich-prog-begr-menge"></a>
### ABGLEICH_PROG_BEGR_MENGE

BEGR_MENGE Abgleich programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_PROG_BEGR_MENGE_STATUS | int | Status |

<a id="job-abgleich-lesen-begr-menge-roh"></a>
### ABGLEICH_LESEN_BEGR_MENGE_ROH

BEGR_MENGEn-Abgleich lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_LESEN_BEGR_MENGE_ROH_WERT | int | Aktuellen Abgleichwert |
| ABGLEICH_LESEN_BEGR_MENGE_ROH_STATUS | int | Rueckmeldebyte |

<a id="job-abgleich-verstellen-begr-menge-roh"></a>
### ABGLEICH_VERSTELLEN_BEGR_MENGE_ROH

BEGR_MENGE Abgleich verstellen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_VERSTELLEN_BEGR_MENGE_ROH_WERT | int | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_VERSTELLEN_BEGR_MENGE_ROH_STATUS | int | Status |

<a id="job-abgleich-lesen-ll-regelung"></a>
### ABGLEICH_LESEN_LL_REGELUNG

LL-Regelung-Abgleich lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_LESEN_LL_REGELUNG_WERT | real | Aktuellen Abgleichwert |
| ABGLEICH_LESEN_LL_REGELUNG_STATUS | int | Rueckmeldebyte |

<a id="job-abgleich-verstellen-ll-regelung"></a>
### ABGLEICH_VERSTELLEN_LL_REGELUNG

LL_REGELUNG Abgleich verstellen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_VERSTELLEN_LL_REGELUNG_WERT | real | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_VERSTELLEN_LL_REGELUNG_STATUS | int | Status |

<a id="job-abgleich-prog-ll-regelung"></a>
### ABGLEICH_PROG_LL_REGELUNG

LL_REGELUNG Abgleich programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_PROG_LL_REGELUNG_STATUS | int | Status |

<a id="job-abgleich-lesen-llpn-regelung"></a>
### ABGLEICH_LESEN_LLPN_REGELUNG

LL-Regelung-Abgleich lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_LESEN_LLPN_REGELUNG_WERT | real | Aktuellen Abgleichwert |
| ABGLEICH_LESEN_LLPN_REGELUNG_STATUS | int | Rueckmeldebyte |

<a id="job-abgleich-verstellen-llpn-regelung"></a>
### ABGLEICH_VERSTELLEN_LLPN_REGELUNG

LL_REGELUNG Abgleich verstellen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_VERSTELLEN_LLPN_REGELUNG_WERT | real | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_VERSTELLEN_LLPN_REGELUNG_STATUS | int | Status |

<a id="job-abgleich-prog-llpn-regelung"></a>
### ABGLEICH_PROG_LLPN_REGELUNG

LL_REGELUNG Abgleich programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_PROG_LLPN_REGELUNG_STATUS | int | Status |

<a id="job-abgleich-lesen-agr-rueck"></a>
### ABGLEICH_LESEN_AGR_RUECK

AGR_RUECKn-Abgleich lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_LESEN_AGR_RUECK_WERT | real | Aktuellen Abgleichwert |
| ABGLEICH_LESEN_AGR_RUECK_STATUS | int | Rueckmeldebyte |

<a id="job-abgleich-verstellen-agr-rueck"></a>
### ABGLEICH_VERSTELLEN_AGR_RUECK

AGR_RUECK Abgleich verstellen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_VERSTELLEN_AGR_RUECK_WERT | real | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_VERSTELLEN_AGR_RUECK_STATUS | int | Status |

<a id="job-abgleich-prog-agr-rueck"></a>
### ABGLEICH_PROG_AGR_RUECK

AGR_RUECK Abgleich programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_PROG_AGR_RUECK_STATUS | int | Status |

<a id="job-abgleich-lesen-voll-menge"></a>
### ABGLEICH_LESEN_VOLL_MENGE

BEGR_MENGEn-Abgleich lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_LESEN_VOLL_MENGE_WERT | real | Aktuellen Abgleichwert |
| ABGLEICH_LESEN_VOLL_MENGE_STATUS | int | Rueckmeldebyte |

<a id="job-abgleich-verstellen-voll-menge"></a>
### ABGLEICH_VERSTELLEN_VOLL_MENGE

BEGR_MENGE Abgleich verstellen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_VERSTELLEN_VOLL_MENGE_WERT | real | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_VERSTELLEN_VOLL_MENGE_STATUS | int | Status |

<a id="job-abgleich-prog-voll-menge"></a>
### ABGLEICH_PROG_VOLL_MENGE

BEGR_MENGE Abgleich programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_PROG_VOLL_MENGE_STATUS | int | Status |

<a id="job-abgleich-lesen-abgleichmenge"></a>
### ABGLEICH_LESEN_ABGLEICHMENGE

LADEDRUCK-Abgleich lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_1 | real | Aktuellen Abgleichwert Nr 1 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_2 | real | Aktuellen Abgleichwert Nr 2 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_3 | real | Aktuellen Abgleichwert Nr 3 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_4 | real | Aktuellen Abgleichwert Nr 4 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_5 | real | Aktuellen Abgleichwert Nr 5 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_6 | real | Aktuellen Abgleichwert Nr 6 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_7 | real | Aktuellen Abgleichwert Nr 7 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_8 | real | Aktuellen Abgleichwert Nr 8 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_9 | real | Aktuellen Abgleichwert Nr 9 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_10 | real | Aktuellen Abgleichwert Nr 10 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_11 | real | Aktuellen Abgleichwert Nr 11 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_12 | real | Aktuellen Abgleichwert Nr 12 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_13 | real | Aktuellen Abgleichwert Nr 13 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_14 | real | Aktuellen Abgleichwert Nr 14 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_15 | real | Aktuellen Abgleichwert Nr 15 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_16 | real | Aktuellen Abgleichwert Nr 16 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_17 | real | Aktuellen Abgleichwert Nr 17 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_18 | real | Aktuellen Abgleichwert Nr 18 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_19 | real | Aktuellen Abgleichwert Nr 19 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_20 | real | Aktuellen Abgleichwert Nr 20 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_21 | real | Aktuellen Abgleichwert Nr 21 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_22 | real | Aktuellen Abgleichwert Nr 22 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_23 | real | Aktuellen Abgleichwert Nr 23 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_24 | real | Aktuellen Abgleichwert Nr 24 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_25 | real | Aktuellen Abgleichwert Nr 25 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_26 | real | Aktuellen Abgleichwert Nr 26 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_27 | real | Aktuellen Abgleichwert Nr 27 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_28 | real | Aktuellen Abgleichwert Nr 28 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_29 | real | Aktuellen Abgleichwert Nr 29 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_30 | real | Aktuellen Abgleichwert Nr 30 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_31 | real | Aktuellen Abgleichwert Nr 31 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_32 | real | Aktuellen Abgleichwert Nr 32 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_33 | real | Aktuellen Abgleichwert Nr 33 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_34 | real | Aktuellen Abgleichwert Nr 34 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_35 | real | Aktuellen Abgleichwert Nr 35 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_36 | real | Aktuellen Abgleichwert Nr 36 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_37 | real | Aktuellen Abgleichwert Nr 37 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_38 | real | Aktuellen Abgleichwert Nr 38 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_39 | real | Aktuellen Abgleichwert Nr 39 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_40 | real | Aktuellen Abgleichwert Nr 40 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_41 | real | Aktuellen Abgleichwert Nr 41 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_42 | real | Aktuellen Abgleichwert Nr 42 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_43 | real | Aktuellen Abgleichwert Nr 43 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_44 | real | Aktuellen Abgleichwert Nr 44 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_45 | real | Aktuellen Abgleichwert Nr 45 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_46 | real | Aktuellen Abgleichwert Nr 46 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_47 | real | Aktuellen Abgleichwert Nr 47 |
| ABGLEICH_LESEN_ABGLEICHMENGE_WERT_48 | real | Aktuellen Abgleichwert Nr 48 |
| ABGLEICH_LESEN_ABGLEICHMENGE_STATUS | int | Rueckmeldebyte |

<a id="job-abgleich-verstellen-abgleichmenge"></a>
### ABGLEICH_VERSTELLEN_ABGLEICHMENGE

LADEDRUCK Abgleich verstellen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_1 | real | Neuer Verstellwert 1 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_2 | real | Neuer Verstellwert 2 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_3 | real | Neuer Verstellwert 3 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_4 | real | Neuer Verstellwert 4 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_5 | real | Neuer Verstellwert 5 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_6 | real | Neuer Verstellwert 6 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_7 | real | Neuer Verstellwert 7 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_8 | real | Neuer Verstellwert 8 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_9 | real | Neuer Verstellwert 9 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_10 | real | Neuer Verstellwert 10 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_11 | real | Neuer Verstellwert 11 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_12 | real | Neuer Verstellwert 12 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_13 | real | Neuer Verstellwert 13 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_14 | real | Neuer Verstellwert 14 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_15 | real | Neuer Verstellwert 15 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_16 | real | Neuer Verstellwert 16 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_17 | real | Neuer Verstellwert 17 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_18 | real | Neuer Verstellwert 18 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_19 | real | Neuer Verstellwert 19 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_20 | real | Neuer Verstellwert 20 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_21 | real | Neuer Verstellwert 21 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_22 | real | Neuer Verstellwert 22 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_23 | real | Neuer Verstellwert 23 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_24 | real | Neuer Verstellwert 24 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_25 | real | Neuer Verstellwert 25 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_26 | real | Neuer Verstellwert 26 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_27 | real | Neuer Verstellwert 27 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_28 | real | Neuer Verstellwert 28 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_29 | real | Neuer Verstellwert 29 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_30 | real | Neuer Verstellwert 30 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_31 | real | Neuer Verstellwert 31 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_32 | real | Neuer Verstellwert 32 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_33 | real | Neuer Verstellwert 33 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_34 | real | Neuer Verstellwert 34 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_35 | real | Neuer Verstellwert 35 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_36 | real | Neuer Verstellwert 36 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_37 | real | Neuer Verstellwert 37 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_38 | real | Neuer Verstellwert 38 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_39 | real | Neuer Verstellwert 39 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_40 | real | Neuer Verstellwert 40 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_41 | real | Neuer Verstellwert 41 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_42 | real | Neuer Verstellwert 42 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_43 | real | Neuer Verstellwert 43 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_44 | real | Neuer Verstellwert 44 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_45 | real | Neuer Verstellwert 45 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_46 | real | Neuer Verstellwert 46 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_47 | real | Neuer Verstellwert 47 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_48 | real | Neuer Verstellwert 48 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_STATUS | int | Status |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_CS | int | Checksumme |

<a id="job-abgleich-prog-abgleichmenge"></a>
### ABGLEICH_PROG_ABGLEICHMENGE

LADEDRUCK Abgleich programmieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_PROG_ABGLEICHMENGE_CS | int | Zum Programmieren muss die CS aus Abgleichwerte vorgeben mit uebergeben werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_PROG_ABGLEICHMENGE_STATUS | int | Status |

<a id="job-abgleich-lesen-abgleich-flag"></a>
### ABGLEICH_LESEN_ABGLEICH_FLAG

Kennung M_ABGLEICH_FLAG lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_LESEN_ABGLEICH_FLAG_WERT | int | Aktuellen Abgleichwert |
| ABGLEICH_LESEN_ABGLEICH_FLAG_STATUS | int | Rueckmeldebyte |

<a id="job-abgleich-verstellen-abgleich-flag"></a>
### ABGLEICH_VERSTELLEN_ABGLEICH_FLAG

Kennung M_ABGLEICH_FLAG verstellen, 0 = nicht verbaut, 0xff = verbaut

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_VERSTELLEN_ABGLEICH_FLAG_WERT | int | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_VERSTELLEN_ABGLEICH_FLAG_STATUS | int | Status |

<a id="job-abgleich-prog-abgleich-flag"></a>
### ABGLEICH_PROG_ABGLEICH_FLAG

Kennung M_ABGLEICH_FLAG programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_PROG_ABGLEICH_FLAG_STATUS | int | Status |

<a id="job-abgleichwerte-lesen"></a>
### ABGLEICHWERTE_LESEN

Lesen der Motorabgleichwerte

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHWERTE_LESEN_ANZAHL | int | Anzahl der zu lesenden Bytes, =12 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHWERTE_LESEN_DATEN | string | aus dem Steuergeraet ausgelesene Daten im Format z.B.: "01 A5 FE" |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_..., wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-abgleichwerte-schreiben"></a>
### ABGLEICHWERTE_SCHREIBEN

Beschreiben des internen Speichers mit den motorspezifischen Abgleichdaten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHWERTE_SCHREIBEN_ANZAHL | int | Anzahl der zu schreibenden Abgleichdatenbytes ohne die Pruefziffer |
| ABGLEICHWERTE_SCHREIBEN_DATEN | string | Abgleichdaten in folgendem Format z.B. 01 02 AB FF ... &lt;PZ&gt; Datenbytes - 2-stellige Hex-Werte, jeweils gefolgt von einem (1) Leerzeichen - Wertebereich: 00 - FF - nur Grossbuchstaben A - F sind erlaubt Pruefziffer &lt;PZ&gt;: - 1-stelliges Zeichen - Wertebereich: 0 - 9, A - Z - nur Grossbuchstaben A - Z sind erlaubt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_... , wenn argument nicht uebergeben oder ausser Bereich |
| ABGLEICHWERTE_SCHREIBEN_ABGLEICHDATEN | string | Abgleichdaten zum Steuergeraet |
| ABGLEICHWERTE_SCHREIBEN_PRUEFZEICHEN | string | das im Job berechnete Pruefzeichen |

<a id="job-abgleichflag-schreiben"></a>
### ABGLEICHFLAG_SCHREIBEN

Beschreiben des internen Speichers mit den motorspezifischen Abgleichdaten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHFLAG_SCHREIBEN_FLAG | string | ABGLEICH_IO : 0x01 ABGLEICH_NIO: 0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_..., wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-abgleichflag-lesen"></a>
### ABGLEICHFLAG_LESEN

Lesen des EEPROM-Speichers ab Adresse 0x0032

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHFLAG_LESEN_WERT | string | 0x01 --&gt; ABGLEICH_IO 0xFF --&gt; ABGLEICH_NIO |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_..., wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-abgleich-lesen-mengendrift"></a>
### ABGLEICH_LESEN_MENGENDRIFT

Mengendrift-Abgleich lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_LESEN_MENGENDRIFT_MIN_WERT | real | Aktueller MIN - Wert |
| ABGLEICH_LESEN_MENGENDRIFT_MAX_WERT | real | Aktueller MIN - Wert |
| ABGLEICH_LESEN_MENGENDRIFT_STATUS | int | Rueckmeldebyte |

<a id="job-abgleich-verstellen-mengendrift"></a>
### ABGLEICH_VERSTELLEN_MENGENDRIFT

Mengendrift Abgleich verstellen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_VERSTELLEN_MENGENDRIFT_MIN_WERT | real | Neuer Verstellwert |
| ABGLEICH_VERSTELLEN_MENGENDRIFT_MAX_WERT | real | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_VERSTELLEN_MENGENDRIFT_STATUS | int | Status |
| ABGLEICH_VERSTELLEN_MENGENDRIFT_CS | int | Checksumme |

<a id="job-abgleich-prog-mengendrift"></a>
### ABGLEICH_PROG_MENGENDRIFT

LADEDRUCK Abgleich programmieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_PROG_MENGENDRIFT_CS | int | Zum Programmieren muss die CS aus Abgleichwerte vorgeben mit uebergeben werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_PROG_MENGENDRIFT_STATUS | int | Status |

<a id="job-hole-ema-feld"></a>
### HOLE_EMA_FELD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| EMA_FAK1 | real | Faktor 1 |
| EMA_FAK2 | real | faktor 2 |
| EMA_WERT3 | real | Wert 3 |

<a id="job-abgleich-lesen-fgr-klima"></a>
### ABGLEICH_LESEN_FGR_KLIMA

Kennung M_ABGLEICH_FLAG lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_LESEN_FGR_KLIMA_WERT | int | Aktuellen Abgleichwert |
| ABGLEICH_LESEN_FGR_KLIMA_STATUS | int | Rueckmeldebyte |

<a id="job-abgleich-prog-fgr-klima"></a>
### ABGLEICH_PROG_FGR_KLIMA

Kennung M_ABGLEICH_FLAG programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_PROG_FGR_KLIMA_STATUS | int | Status |

<a id="job-abgleich-lesen-fgr-variante"></a>
### ABGLEICH_LESEN_FGR_VARIANTE

FGR-Variante-Abgleich lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_LESEN_FGR_VARIANTE_WERT | int | Aktuellen Abgleichwert |
| ABGLEICH_LESEN_FGR_VARIANTE_STATUS | int | Rueckmeldebyte |

<a id="job-abgleich-verstellen-fgr-variante"></a>
### ABGLEICH_VERSTELLEN_FGR_VARIANTE

FGR_VARIANTE_Abgleich verstellen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_VERSTELLEN_FGR_VARIANTE_WERT | int | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_VERSTELLEN_FGR_VARIANTE_STATUS | int | Status |

<a id="job-abgleich-prog-fgr-variante"></a>
### ABGLEICH_PROG_FGR_VARIANTE

FGR_VARIANTE_Abgleich programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_PROG_FGR_VARIANTE_STATUS | int | Status |

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

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

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

<a id="job-steuern-agr-steller"></a>
### STEUERN_AGR_STELLER

ARF - Steller  ansteuern ,  - - 10%%

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | Verstellwert 5 - 95 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ekp"></a>
### STEUERN_EKP

ARF-Steller ansteuern ,  0 oder 100%

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | Verstellwert 0=AUS oder 1=EIN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-gluehrelais"></a>
### STEUERN_GLUEHRELAIS

Gluegrelais ansteuern ,  0 oder 100%

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | Verstellwert 0=Aus oder 100=EIN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-klimakompressor"></a>
### STEUERN_KLIMAKOMPRESSOR

StellerKlimakompressor ansteuern ,  0 oder 100

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | Verstellwert 0=Aus oder 100=Ein |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ladedrucksteller"></a>
### STEUERN_LADEDRUCKSTELLER

Ladedrucksteller ansteuern ,  5-95%

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | Verstellwert 5 - 95 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-e-luefter"></a>
### STEUERN_E_LUEFTER

E-Luefter ansteuern ,  5-95%

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | Verstellwert 5 - 95 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-motorlager"></a>
### STEUERN_MOTORLAGER

Motorlager ansteuern ,  0 oder 100%

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | Verstellwert 0=Aus oder 100=Ein |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-oeldruckschalter"></a>
### STEUERN_OELDRUCKSCHALTER

Oeldruckschalteranzeige ansteuern ,  0 oder 100%

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | Verstellwert 0=Aus oder 100=Ein |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-drallklappe"></a>
### STEUERN_DRALLKLAPPE

Drallklappe ansteuern ,  ,  0 oder 100%

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | Verstellwert 0=Aus oder 100=Ein |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-kuehlwasserheizung"></a>
### STEUERN_KUEHLWASSERHEIZUNG

Elektrische Kuehlwasserheizung ,  5 bis 95%

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ks-hdpumpe-abschaltung"></a>
### STEUERN_KS_HDPUMPE_ABSCHALTUNG

Railhochdruckpumpe Elementabschaltung   ansteuern ,  0 oder 100%

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | Verstellwert 0 oder 100 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ende-selectiv"></a>
### STEUERN_ENDE_SELECTIV

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STELLGLIED | int | Stellglied |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-start-systemcheck-zyl-sel-mengenkor"></a>
### START_SYSTEMCHECK_ZYL_SEL_MENGENKOR

Start zylinderselektive Mengenkorrekturen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-start-systemcheck-zyl-sel-drehzahl"></a>
### START_SYSTEMCHECK_ZYL_SEL_DREHZAHL

Start zylinderselektive Drehzhahlen lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-stop-systemcheck"></a>
### STOP_SYSTEMCHECK

Stop Systemtest

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-mw-select-lesen"></a>
### MW_SELECT_LESEN

Messwerteblock selectiv lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MW_SELECT_LESEN_MNR | binary | Telegrammaufbau MSG - Nr |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| MW_SELECT_LESEN_WERT | binary | 1 Byte = Status, MW Wert |

<a id="job-tel-roh"></a>
### TEL_ROH

Rohtelegramm ohne Header lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| REQUEST | binary | Daten ohne Header |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| RESPONSE | binary | Daten ohne Header |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

Status Schalteingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_GETRIEBEART_HAND_EIN | int | Status Getriebeart 0=Automatik / 1=Handschalter |
| STAT_BREMS_TEST_SCHALTER_EIN | int | Status Bremstestschalter 0=Aus / 1=Ein |
| STAT_BREMS_LICHT_SCHALTER_EIN | int | Status Bremslichtschalter 0=Aus / 1=Ein |
| STAT_GLUEHZEIT_SG_EIN | int | Status Gluehzeitsteuergeraet 0=Ein / 1=Aus |
| STAT_KUP_EIN | int | Schalter Kupplung aktiv 0=Nein / 1=Ja |
| STAT_BLS_EIN | int | Schalter BLS aktiv 0=Nein / 1=Ja |
| STAT_BLTS_EIN | int | Schalter BLTS aktiv 0=Nein / 1=Ja |
| STAT_KO_EIN | int | Klima-Anforderung 0=Nein / 1=Ja |
| STAT_AC_EIN | int | Anforderung Klimabereitschaft 0=Nein / 1=Ja |
| STAT_ODS_EIN | int | Status Oeldruckschalter 0=Nein / 1=Ja |
| STAT_HEIZ_EIN | int | Status Kuehlwasserheizung angefordert 0=Nein / 1=Ja |
| STAT_TEMPOMAT_VERZ_EIN | int | MFL Ein -  0=AUS / 1=EIN |
| STAT_TEMPOMAT_BESCHL_EIN | int | MFL Ein +  0=AUS / 1=EIN |
| STAT_TEMPOMAT_WIEDERAUF_EIN | int | MFL Wiederaufnahme  0=AUS / 1=EIN |
| STAT_TEMPOMAT_AUS_EIN | int | MFL AUS  0=AUS / 1=EIN |

<a id="job-status-digital1"></a>
### STATUS_DIGITAL1

Status Schalteingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_DIGITAL1_TEXT | string | Beschreibung Eingang |
| STATUS_DIGITAL1_STATUS | string | Status Eingang |

<a id="job-status-digital2"></a>
### STATUS_DIGITAL2

Status Schalteingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_DIGITAL2_TEXT | string | Beschreibung Eingang |
| STATUS_DIGITAL2_STATUS | string | Status Eingang |

<a id="job-status-digital3"></a>
### STATUS_DIGITAL3

Status Schalteingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_DIGITAL3_TEXT | string | Beschreibung Eingang |
| STATUS_DIGITAL3_STATUS | string | Status Eingang |

<a id="job-status-digital4"></a>
### STATUS_DIGITAL4

Status Schalteingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_DIGITAL4_TEXT | string | Beschreibung Eingang |
| STATUS_DIGITAL4_STATUS | string | Status Eingang |

<a id="job-status-laufunruhe-llr-menge"></a>
### STATUS_LAUFUNRUHE_LLR_MENGE

Auslesen selektive Mengenkorrektur

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_LAUFUNRUHE_LLR_MENGE_ZYL1_WERT | real |  |
| STAT_LAUFUNRUHE_LLR_MENGE_ZYL2_WERT | real |  |
| STAT_LAUFUNRUHE_LLR_MENGE_ZYL3_WERT | real |  |
| STAT_LAUFUNRUHE_LLR_MENGE_ZYL4_WERT | real |  |
| STAT_LAUFUNRUHE_LLR_MENGE_ZYL5_WERT | real |  |
| STAT_LAUFUNRUHE_LLR_MENGE_ZYL6_WERT | real |  |
| STAT_LAUFUNRUHE_LLR_MENGE_EINH | string |  |

<a id="job-status-laufunruhe-drehzahl"></a>
### STATUS_LAUFUNRUHE_DREHZAHL

Auslesen selektive Mengenkorrektur

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_LAUFUNRUHE_DREHZAHL_ZYL1_WERT | real |  |
| STAT_LAUFUNRUHE_DREHZAHL_ZYL2_WERT | real |  |
| STAT_LAUFUNRUHE_DREHZAHL_ZYL3_WERT | real |  |
| STAT_LAUFUNRUHE_DREHZAHL_ZYL4_WERT | real |  |
| STAT_LAUFUNRUHE_DREHZAHL_ZYL5_WERT | real |  |
| STAT_LAUFUNRUHE_DREHZAHL_ZYL6_WERT | real |  |
| STAT_LAUFUNRUHE_DREHZAHL_EINH | string |  |

<a id="job-abgleich-kic-verstellen-programmieren"></a>
### ABGLEICH_KIC_VERSTELLEN_PROGRAMMIEREN

FGR-Funktion und Mainswitch konfigurieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_KIC_VERSTELLEN_PROGRAMMIEREN_WERT | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_KIC_VERSTELLEN_PROGRAMMIEREN_STATUS | int | Status |

<a id="job-mw-select-lesen-norm"></a>
### MW_SELECT_LESEN_NORM

Messwerteblock selectiv lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MW_SELECT_LESEN_MNR | binary | Telegrammaufbau MSG - Nr |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-mw-select-lesen-norm-einzel"></a>
### MW_SELECT_LESEN_NORM_EINZEL

Messwerteblock selectiv lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MW_SELECT_LESEN_MNR | binary | Telegrammaufbau MSG - Nr |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_WERT | real | Ergebnis |
| STAT_EINH | string | Einheit |

<a id="job-mw-select-lesen-norm2"></a>
### MW_SELECT_LESEN_NORM2

Messwerteblock selectiv lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MW_SELECT_LESEN_MNR | binary | Telegrammaufbau MSG - Nr |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-status-anmpwg"></a>
### STATUS_ANMPWG

PWG Pedalwertgeber Poti 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANMPWG_WERT | real | Ergebnis |
| STAT_ANMPWG_EINH | string | Einheit |

<a id="job-status-anmubt"></a>
### STATUS_ANMUBT

UBT Batteriespannung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANMUBT_WERT | real | Ergebnis |
| STAT_ANMUBT_EINH | string | Einheit |

<a id="job-status-anmvdf"></a>
### STATUS_ANMVDF

VDF Vorfoerderdruck

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANMVDF_WERT | real | Ergebnis |
| STAT_ANMVDF_EINH | string | Einheit |

<a id="job-status-anmwtf"></a>
### STATUS_ANMWTF

WTF Wassertemperatur

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANMWTF_WERT | real | Ergebnis |
| STAT_ANMWTF_EINH | string | Einheit |

<a id="job-status-armm-list"></a>
### STATUS_ARMM_LIST

M_L aktuelle Luftmasse

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ARMM_LIST_WERT | real | Ergebnis |
| STAT_ARMM_LIST_EINH | string | Einheit |

<a id="job-status-armm-lsoll"></a>
### STATUS_ARMM_LSOLL

M_L Sollwert fuer AGR-Regelung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ARMM_LSOLL_WERT | real | Ergebnis |
| STAT_ARMM_LSOLL_EINH | string | Einheit |

<a id="job-status-dzmnmit"></a>
### STATUS_DZMNMIT

N Drehzahl

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DZMNMIT_WERT | real | Ergebnis |
| STAT_DZMNMIT_EINH | string | Einheit |

<a id="job-status-ehmfars"></a>
### STATUS_EHMFARS

Tastverhaeltnis Ansteuerung AGR-Steller

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_EHMFARS_WERT | real | Ergebnis |
| STAT_EHMFARS_EINH | string | Einheit |

<a id="job-status-ehmfekp"></a>
### STATUS_EHMFEKP

Tastverhaeltnis Ansteuerung Vorfoerderpumpe

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_EHMFEKP_WERT | real | Ergebnis |
| STAT_EHMFEKP_EINH | string | Einheit |

<a id="job-status-ehmfgrs"></a>
### STATUS_EHMFGRS

Tastverhaeltnis Ansteuerung Gluehrelais

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_EHMFGRS_WERT | real | Ergebnis |
| STAT_EHMFGRS_EINH | string | Einheit |

<a id="job-status-ehmfkdr"></a>
### STATUS_EHMFKDR

Tastverhaeltnis Ansteuerung Raildruckregelventil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_EHMFKDR_WERT | real | Ergebnis |
| STAT_EHMFKDR_EINH | string | Einheit |

<a id="job-status-ehmfkli"></a>
### STATUS_EHMFKLI

Tastverhaeltnis Ansteuerung Klimakompressor

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_EHMFKLI_WERT | real | Ergebnis |
| STAT_EHMFKLI_EINH | string | Einheit |

<a id="job-status-ehmflds"></a>
### STATUS_EHMFLDS

Tastverhaeltnis Ansteuerung Ladedrucksteller

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_EHMFLDS_WERT | real | Ergebnis |
| STAT_EHMFLDS_EINH | string | Einheit |

<a id="job-status-ehmfmls"></a>
### STATUS_EHMFMLS

Tastverhaeltnis Ansteuerung Elektroluefter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_EHMFMLS_WERT | real | Ergebnis |
| STAT_EHMFMLS_EINH | string | Einheit |

<a id="job-status-ehmfmml"></a>
### STATUS_EHMFMML

Tastverhaeltnis Ansteuerung Motorlager

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_EHMFMML_WERT | real | Ergebnis |
| STAT_EHMFMML_EINH | string | Einheit |

<a id="job-status-ldmp-llin"></a>
### STATUS_LDMP_LLIN

aktueller Ladedruck  / Luftdruck

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LDMP_LLIN_WERT | real | Ergebnis |
| STAT_LDMP_LLIN_EINH | string | Einheit |

<a id="job-status-ldmp-lsoll"></a>
### STATUS_LDMP_LSOLL

Sollwert Ladedruck

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LDMP_LSOLL_WERT | real | Ergebnis |
| STAT_LDMP_LSOLL_EINH | string | Einheit |

<a id="job-status-mrmm-efahr"></a>
### STATUS_MRMM_EFAHR

M_E Fahrmenge nach Laufruheregler

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMM_EFAHR_WERT | real | Ergebnis |
| STAT_MRMM_EFAHR_EINH | string | Einheit |

<a id="job-status-zump-rail"></a>
### STATUS_ZUMP_RAIL

Raildruck fuer Mengenzumessung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ZUMP_RAIL_WERT | real | Ergebnis |
| STAT_ZUMP_RAIL_EINH | string | Einheit |

<a id="job-status-zumpqsoll"></a>
### STATUS_ZUMPQSOLL

Raildruck Sollwert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ZUMPQSOLL_WERT | real | Ergebnis |
| STAT_ZUMPQSOLL_EINH | string | Einheit |

<a id="job-status-admadf"></a>
### STATUS_ADMADF

ADF Rohwert Atmosphaerendruck

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ADMADF_WERT | real | Ergebnis |
| STAT_ADMADF_EINH | string | Einheit |

<a id="job-status-admidv"></a>
### STATUS_ADMIDV

IDV Rohwert Istwert Stromregelung Druckregelventil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ADMIDV_WERT | real | Ergebnis |
| STAT_ADMIDV_EINH | string | Einheit |

<a id="job-status-admkdf"></a>
### STATUS_ADMKDF

KDF Rohwert Raildruck

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ADMKDF_WERT | real | Ergebnis |
| STAT_ADMKDF_EINH | string | Einheit |

<a id="job-status-admldf"></a>
### STATUS_ADMLDF

LDF Rohwert Ladedruck

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ADMLDF_WERT | real | Ergebnis |
| STAT_ADMLDF_EINH | string | Einheit |

<a id="job-status-admlmm"></a>
### STATUS_ADMLMM

LMM Rohwert Luftmasse

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ADMLMM_WERT | real | Ergebnis |
| STAT_ADMLMM_EINH | string | Einheit |

<a id="job-status-admltf"></a>
### STATUS_ADMLTF

LTF Rohwert Lufttemperatur

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ADMLTF_WERT | real | Ergebnis |
| STAT_ADMLTF_EINH | string | Einheit |

<a id="job-status-admpgs"></a>
### STATUS_ADMPGS

PGS Rohwert Pedalwertgeber Poti 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ADMPGS_WERT | real | Ergebnis |
| STAT_ADMPGS_EINH | string | Einheit |

<a id="job-status-admpwg"></a>
### STATUS_ADMPWG

PWG Rohwert Pedalwertgeber Poti 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ADMPWG_WERT | real | Ergebnis |
| STAT_ADMPWG_EINH | string | Einheit |

<a id="job-status-admubt"></a>
### STATUS_ADMUBT

UBT Rohwert Batteriespannung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ADMUBT_WERT | real | Ergebnis |
| STAT_ADMUBT_EINH | string | Einheit |

<a id="job-status-admuc1"></a>
### STATUS_ADMUC1

UC1 Rohwert Kondensatorspannung 1 fuer Zylinder 1,2,3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ADMUC1_WERT | real | Ergebnis |
| STAT_ADMUC1_EINH | string | Einheit |

<a id="job-status-admuc2"></a>
### STATUS_ADMUC2

UC2 Rohwert Kondensatorspannung 2 fuer Zylinder 4,5,6

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ADMUC2_WERT | real | Ergebnis |
| STAT_ADMUC2_EINH | string | Einheit |

<a id="job-status-admug1"></a>
### STATUS_ADMUG1

UG1 Rohwert Speisespannung 1 fuer Pedalwertgeber 2, Ladedruckfuehler, Luftmassenmesser

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ADMUG1_WERT | real | Ergebnis |
| STAT_ADMUG1_EINH | string | Einheit |

<a id="job-status-admug2"></a>
### STATUS_ADMUG2

UG2 Rohwert Speisespannung 2 fuer Pedalwertgeber 1, Kraftstoff- ,Vorfoerderdruckfuehler

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ADMUG2_WERT | real | Ergebnis |
| STAT_ADMUG2_EINH | string | Einheit |

<a id="job-status-admvdf"></a>
### STATUS_ADMVDF

VDF Rohwert Vorfoerderdruck

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ADMVDF_WERT | real | Ergebnis |
| STAT_ADMVDF_EINH | string | Einheit |

<a id="job-status-admwtf"></a>
### STATUS_ADMWTF

WTF Rohwert Wassertemperatur

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ADMWTF_WERT | real | Ergebnis |
| STAT_ADMWTF_EINH | string | Einheit |

<a id="job-status-anmadf"></a>
### STATUS_ANMADF

ADF Atmosphaerendruck

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANMADF_WERT | real | Ergebnis |
| STAT_ANMADF_EINH | string | Einheit |

<a id="job-status-anmidv"></a>
### STATUS_ANMIDV

IDV Istwert Stromregelung Druckregelventil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANMIDV_WERT | real | Ergebnis |
| STAT_ANMIDV_EINH | string | Einheit |

<a id="job-status-anmkdf"></a>
### STATUS_ANMKDF

KDF Raildruck

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANMKDF_WERT | real | Ergebnis |
| STAT_ANMKDF_EINH | string | Einheit |

<a id="job-status-anmldf"></a>
### STATUS_ANMLDF

LDF Ladedruck

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANMLDF_WERT | real | Ergebnis |
| STAT_ANMLDF_EINH | string | Einheit |

<a id="job-status-anmlmm"></a>
### STATUS_ANMLMM

LMM Luftmasse

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANMLMM_WERT | real | Ergebnis |
| STAT_ANMLMM_EINH | string | Einheit |

<a id="job-status-anmltf"></a>
### STATUS_ANMLTF

LTF Lufttemperatur

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANMLTF_WERT | real | Ergebnis |
| STAT_ANMLTF_EINH | string | Einheit |

<a id="job-status-anmpgs"></a>
### STATUS_ANMPGS

PGS Pedalwertgeber Poti 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANMPGS_WERT | real | Ergebnis |
| STAT_ANMPGS_EINH | string | Einheit |

<a id="job-status-anmuc1"></a>
### STATUS_ANMUC1

UC1 Kondensatorspannung 1 fuer Zylinder 1,2,3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANMUC1_WERT | real | Ergebnis |
| STAT_ANMUC1_EINH | string | Einheit |

<a id="job-status-anmuc2"></a>
### STATUS_ANMUC2

UC2 Kondensatorspannung 2 fuer Zylinder 4,5,6

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANMUC2_WERT | real | Ergebnis |
| STAT_ANMUC2_EINH | string | Einheit |

<a id="job-status-anmug1"></a>
### STATUS_ANMUG1

UG1 Speisespannung 1 fuer Pedalwertgeber 2, Ladedruckfuehler, Luftmassenmesser

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANMUG1_WERT | real | Ergebnis |
| STAT_ANMUG1_EINH | string | Einheit |

<a id="job-status-anmug2"></a>
### STATUS_ANMUG2

UG2 Speisespannung 2 fuer Pedalwertgeber 1, Kraftstoff- ,Vorfoerderdruckfuehler

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANMUG2_WERT | real | Ergebnis |
| STAT_ANMUG2_EINH | string | Einheit |

<a id="job-status-anou-adf"></a>
### STATUS_ANOU_ADF

ADF Spannung Atmosphaerendruckfuehler

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANOU_ADF_WERT | real | Ergebnis |
| STAT_ANOU_ADF_EINH | string | Einheit |

<a id="job-status-anou-idv"></a>
### STATUS_ANOU_IDV

IDV Spannung zur Strommessung Druckregelventil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANOU_IDV_WERT | real | Ergebnis |
| STAT_ANOU_IDV_EINH | string | Einheit |

<a id="job-status-anou-kdf"></a>
### STATUS_ANOU_KDF

KDF Spannung Raildruckfuehler

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANOU_KDF_WERT | real | Ergebnis |
| STAT_ANOU_KDF_EINH | string | Einheit |

<a id="job-status-anou-ldf"></a>
### STATUS_ANOU_LDF

LDF Spannung Ladedruckfuehler

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANOU_LDF_WERT | real | Ergebnis |
| STAT_ANOU_LDF_EINH | string | Einheit |

<a id="job-status-anou-lmm"></a>
### STATUS_ANOU_LMM

LMM Spannung Luftmassenmesser

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANOU_LMM_WERT | real | Ergebnis |
| STAT_ANOU_LMM_EINH | string | Einheit |

<a id="job-status-anou-ltf"></a>
### STATUS_ANOU_LTF

LTF Spannung Lufttemperaturfuehler

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANOU_LTF_WERT | real | Ergebnis |
| STAT_ANOU_LTF_EINH | string | Einheit |

<a id="job-status-anou-pgs"></a>
### STATUS_ANOU_PGS

PGS Spannung Pedalwertgeber Poti 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANOU_PGS_WERT | real | Ergebnis |
| STAT_ANOU_PGS_EINH | string | Einheit |

<a id="job-status-anou-pwg"></a>
### STATUS_ANOU_PWG

PWG Spannung Pedalwertgeber Poti 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANOU_PWG_WERT | real | Ergebnis |
| STAT_ANOU_PWG_EINH | string | Einheit |

<a id="job-status-anou-ubt"></a>
### STATUS_ANOU_UBT

UBT Spannung Batteriespannung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANOU_UBT_WERT | real | Ergebnis |
| STAT_ANOU_UBT_EINH | string | Einheit |

<a id="job-status-anou-uc1"></a>
### STATUS_ANOU_UC1

UC1 Spannung Kondensatorspannung 1 fuer Zylinder 1,2,3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANOU_UC1_WERT | real | Ergebnis |
| STAT_ANOU_UC1_EINH | string | Einheit |

<a id="job-status-anou-uc2"></a>
### STATUS_ANOU_UC2

UC2 Spannung Kondensatorspannung 2 fuer Zylinder 4,5,6

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANOU_UC2_WERT | real | Ergebnis |
| STAT_ANOU_UC2_EINH | string | Einheit |

<a id="job-status-anou-ug1"></a>
### STATUS_ANOU_UG1

UG1 Spannung Speisespannung 1 fuer Pedalwertgeber 2, Ladedruckfuehler, Luftmassenmesser

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANOU_UG1_WERT | real | Ergebnis |
| STAT_ANOU_UG1_EINH | string | Einheit |

<a id="job-status-anou-ug2"></a>
### STATUS_ANOU_UG2

UG2 Spannung Speisespannung 2 fuer Pedalwertgeber 1, Kraftstoff- ,Vorfoerderdruckfuehler

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANOU_UG2_WERT | real | Ergebnis |
| STAT_ANOU_UG2_EINH | string | Einheit |

<a id="job-status-anou-vdf"></a>
### STATUS_ANOU_VDF

VDF Spannung Vorfoerderdruckfuehler

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANOU_VDF_WERT | real | Ergebnis |
| STAT_ANOU_VDF_EINH | string | Einheit |

<a id="job-status-anou-wtf"></a>
### STATUS_ANOU_WTF

WTF Spannung Wassertemperaturfuehler

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANOU_WTF_WERT | real | Ergebnis |
| STAT_ANOU_WTF_EINH | string | Einheit |

<a id="job-status-aroist-5"></a>
### STATUS_AROIST_5

M_L normierte Luftmasse (nicht T_L/P_ADF-korrig.)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_AROIST_5_WERT | real | Ergebnis |
| STAT_AROIST_5_EINH | string | Einheit |

<a id="job-status-aroreg-2"></a>
### STATUS_AROREG_2

AGR-Status  Regelung / Steuerung / Abschaltung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_AROREG_2_WERT | real | Ergebnis |
| STAT_AROREG_2_EINH | string | Einheit |

<a id="job-status-arosoll-5"></a>
### STATUS_AROSOLL_5

M_L Luft-Sollwert nach Sollwertbegrenzung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_AROSOLL_5_WERT | real | Ergebnis |
| STAT_AROSOLL_5_EINH | string | Einheit |

<a id="job-status-camn-el"></a>
### STATUS_CAMN_EL

MLS Drehzahlstufe E-Luefter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_CAMN_EL_WERT | real | Ergebnis |
| STAT_CAMN_EL_EINH | string | Einheit |

<a id="job-status-cams-ac"></a>
### STATUS_CAMS_AC

Schalter Klimabereitschaft

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_CAMS_AC_WERT | real | Ergebnis |
| STAT_CAMS_AC_EINH | string | Einheit |

<a id="job-status-cams-ko"></a>
### STATUS_CAMS_KO

Schalter Klimakompressor

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_CAMS_KO_WERT | real | Ergebnis |
| STAT_CAMS_KO_EINH | string | Einheit |

<a id="job-status-caoverb"></a>
### STATUS_CAOVERB

Kraftstoffverbrauch fuer CAN DDE4-VERBRAUCH

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_CAOVERB_WERT | real | Ergebnis |
| STAT_CAOVERB_EINH | string | Einheit |

<a id="job-status-comgtr-opt"></a>
### STATUS_COMGTR_OPT

Identifikation Handschalter/Automatik

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_COMGTR_OPT_WERT | real | Ergebnis |
| STAT_COMGTR_OPT_EINH | string | Einheit |

<a id="job-status-dimdig-0"></a>
### STATUS_DIMDIG_0

Auf logisch 0 erkannte Digitaleingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DIMDIG_0_WERT | real | Ergebnis |
| STAT_DIMDIG_0_EINH | string | Einheit |

<a id="job-status-dimdig-1"></a>
### STATUS_DIMDIG_1

Auf logisch 1 erkannte Digitaleingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DIMDIG_1_WERT | real | Ergebnis |
| STAT_DIMDIG_1_EINH | string | Einheit |

<a id="job-status-dimdigprel"></a>
### STATUS_DIMDIGPREL

Entprellte logische Zustaende der digitalen Eingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DIMDIGPREL_WERT | real | Ergebnis |
| STAT_DIMDIGPREL_EINH | string | Einheit |

<a id="job-status-dimf-mfl"></a>
### STATUS_DIMF_MFL

FGR Multifunktionslenkrad

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DIMF_MFL_WERT | real | Ergebnis |
| STAT_DIMF_MFL_EINH | string | Einheit |

<a id="job-status-dzmnakt"></a>
### STATUS_DZMNAKT

N aktuelle Drehzahl aus letzter Periode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DZMNAKT_WERT | real | Ergebnis |
| STAT_DZMNAKT_EINH | string | Einheit |

<a id="job-status-dzmzmk1"></a>
### STATUS_DZMZMK1

Selektive Mengenkorrektur Zylinder 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DZMZMK1_WERT | real | Ergebnis |
| STAT_DZMZMK1_EINH | string | Einheit |

<a id="job-status-dzmzmk2"></a>
### STATUS_DZMZMK2

Selektive Mengenkorrektur Zylinder 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DZMZMK2_WERT | real | Ergebnis |
| STAT_DZMZMK2_EINH | string | Einheit |

<a id="job-status-dzmzmk3"></a>
### STATUS_DZMZMK3

Selektive Mengenkorrektur Zylinder 3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DZMZMK3_WERT | real | Ergebnis |
| STAT_DZMZMK3_EINH | string | Einheit |

<a id="job-status-dzmzmk4"></a>
### STATUS_DZMZMK4

Selektive Mengenkorrektur Zylinder 4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DZMZMK4_WERT | real | Ergebnis |
| STAT_DZMZMK4_EINH | string | Einheit |

<a id="job-status-dzmzmk5"></a>
### STATUS_DZMZMK5

Selektive Mengenkorrektur Zylinder 5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DZMZMK5_WERT | real | Ergebnis |
| STAT_DZMZMK5_EINH | string | Einheit |

<a id="job-status-dzmzmk6"></a>
### STATUS_DZMZMK6

Selektive Mengenkorrektur Zylinder 6

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DZMZMK6_WERT | real | Ergebnis |
| STAT_DZMZMK6_EINH | string | Einheit |

<a id="job-status-dzmzn1"></a>
### STATUS_DZMZN1

Selektive Drehzahl Zylinder 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DZMZN1_WERT | real | Ergebnis |
| STAT_DZMZN1_EINH | string | Einheit |

<a id="job-status-dzmzn2"></a>
### STATUS_DZMZN2

Selektive Drehzahl Zylinder 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DZMZN2_WERT | real | Ergebnis |
| STAT_DZMZN2_EINH | string | Einheit |

<a id="job-status-dzmzn3"></a>
### STATUS_DZMZN3

Selektive Drehzahl Zylinder 3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DZMZN3_WERT | real | Ergebnis |
| STAT_DZMZN3_EINH | string | Einheit |

<a id="job-status-dzmzn4"></a>
### STATUS_DZMZN4

Selektive Drehzahl Zylinder 4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DZMZN4_WERT | real | Ergebnis |
| STAT_DZMZN4_EINH | string | Einheit |

<a id="job-status-dzmzn5"></a>
### STATUS_DZMZN5

Selektive Drehzahl Zylinder 5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DZMZN5_WERT | real | Ergebnis |
| STAT_DZMZN5_EINH | string | Einheit |

<a id="job-status-dzmzn6"></a>
### STATUS_DZMZN6

Selektive Drehzahl Zylinder 6

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DZMZN6_WERT | real | Ergebnis |
| STAT_DZMZN6_EINH | string | Einheit |

<a id="job-status-edmrstcd"></a>
### STATUS_EDMRSTCD

Restart Code

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_EDMRSTCD_WERT | real | Ergebnis |
| STAT_EDMRSTCD_EINH | string | Einheit |

<a id="job-status-fbmbstz-ub"></a>
### STATUS_FBMBSTZ_UB

UB Betriebsstunden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_FBMBSTZ_UB_WERT | real | Ergebnis |
| STAT_FBMBSTZ_UB_EINH | string | Einheit |

<a id="job-status-fbmdia-c"></a>
### STATUS_FBMDIA_C

Diagnoselampe ueber CAN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_FBMDIA_C_WERT | real | Ergebnis |
| STAT_FBMDIA_C_EINH | string | Einheit |

<a id="job-status-fbmmil-c"></a>
### STATUS_FBMMIL_C

MIL Malfunction Indikator Lamp ueber CAN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_FBMMIL_C_WERT | real | Ergebnis |
| STAT_FBMMIL_C_EINH | string | Einheit |

<a id="job-status-fbmsdial"></a>
### STATUS_FBMSDIAL

Anforderung Diagnoselampe aus Fehlerbehandlung (0:Aus,1:Ein,2:Blinken)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_FBMSDIAL_WERT | real | Ergebnis |
| STAT_FBMSDIAL_EINH | string | Einheit |

<a id="job-status-fbodiala"></a>
### STATUS_FBODIALA

Diagnose - Lampe Status (255 = EIN)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_FBODIALA_WERT | real | Ergebnis |
| STAT_FBODIALA_EINH | string | Einheit |

<a id="job-status-fbos-00"></a>
### STATUS_FBOS_00

Defekte Pfade 1 bis 16

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_FBOS_00_WERT | real | Ergebnis |
| STAT_FBOS_00_EINH | string | Einheit |

<a id="job-status-fbos-02"></a>
### STATUS_FBOS_02

Defekte Pfade 17 bis 32

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_FBOS_02_WERT | real | Ergebnis |
| STAT_FBOS_02_EINH | string | Einheit |

<a id="job-status-fbos-04"></a>
### STATUS_FBOS_04

Defekte Pfade 33 bis 48

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_FBOS_04_WERT | real | Ergebnis |
| STAT_FBOS_04_EINH | string | Einheit |

<a id="job-status-fbos-06"></a>
### STATUS_FBOS_06

Defekte Pfade 49 bis 64

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_FBOS_06_WERT | real | Ergebnis |
| STAT_FBOS_06_EINH | string | Einheit |

<a id="job-status-fbos-08"></a>
### STATUS_FBOS_08

Defekte Pfade 65 bis 80

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_FBOS_08_WERT | real | Ergebnis |
| STAT_FBOS_08_EINH | string | Einheit |

<a id="job-status-fgm-vzun"></a>
### STATUS_FGM_VZUN

Verhaeltnis Geschwindigkeit/Drehzahl (V/N aktuell)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_FGM_VZUN_WERT | real | Ergebnis |
| STAT_FGM_VZUN_EINH | string | Einheit |

<a id="job-status-fgmbesch"></a>
### STATUS_FGMBESCH

Beschleunigung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_FGMBESCH_WERT | real | Ergebnis |
| STAT_FGMBESCH_EINH | string | Einheit |

<a id="job-status-fgmfgakt"></a>
### STATUS_FGMFGAKT

aktuelle Geschwindigkeit

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_FGMFGAKT_WERT | real | Ergebnis |
| STAT_FGMFGAKT_EINH | string | Einheit |

<a id="job-status-gsogs-pha"></a>
### STATUS_GSOGS_PHA

Gluehzeitsteuerung Gluehphase

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_GSOGS_PHA_WERT | real | Ergebnis |
| STAT_GSOGS_PHA_EINH | string | Einheit |

<a id="job-status-ldmadf"></a>
### STATUS_LDMADF

aktueller Atmosphaerendruck

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LDMADF_WERT | real | Ergebnis |
| STAT_LDMADF_EINH | string | Einheit |

<a id="job-status-ldmt-ltgg"></a>
### STATUS_LDMT_LTGG

Errechnete Lufttemperatur

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LDMT_LTGG_WERT | real | Ergebnis |
| STAT_LDMT_LTGG_EINH | string | Einheit |

<a id="job-status-ldotvsteu"></a>
### STATUS_LDOTVSTEU

Tastverhaeltnis Steuerung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LDOTVSTEU_WERT | real | Ergebnis |
| STAT_LDOTVSTEU_EINH | string | Einheit |

<a id="job-status-mrmcase-a"></a>
### STATUS_MRMCASE_A

ARD Zustand-Bits der aktiven Ruckeldaempfung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMCASE_A_WERT | real | Ergebnis |
| STAT_MRMCASE_A_EINH | string | Einheit |

<a id="job-status-mrmcase-l"></a>
### STATUS_MRMCASE_L

LLR Zustand-Bits der Leerlaufregelung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMCASE_L_WERT | real | Ergebnis |
| STAT_MRMCASE_L_EINH | string | Einheit |

<a id="job-status-mrmf-gang"></a>
### STATUS_MRMF_GANG

FGR aktuelle Gangstufe

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMF_GANG_WERT | real | Ergebnis |
| STAT_MRMF_GANG_EINH | string | Einheit |

<a id="job-status-mrmfg-soll"></a>
### STATUS_MRMFG_SOLL

V Sollwert Fahrgeschwindigkeit von FGR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMFG_SOLL_WERT | real | Ergebnis |
| STAT_MRMFG_SOLL_EINH | string | Einheit |

<a id="job-status-mrmkm-akt"></a>
### STATUS_MRMKM_AKT

aktueller km-Stand von Kombiinstrument

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMKM_AKT_WERT | real | Ergebnis |
| STAT_MRMKM_AKT_EINH | string | Einheit |

<a id="job-status-mrml-fgr"></a>
### STATUS_MRML_FGR

FGR-Status-Indicator-Lampe ueber CAN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRML_FGR_WERT | real | Ergebnis |
| STAT_MRML_FGR_EINH | string | Einheit |

<a id="job-status-mrmllriant"></a>
### STATUS_MRMLLRIANT

M_E Menge aus I-Anteil des PI-Leerlaufreglers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMLLRIANT_WERT | real | Ergebnis |
| STAT_MRMLLRIANT_EINH | string | Einheit |

<a id="job-status-mrmllrpant"></a>
### STATUS_MRMLLRPANT

M_E Menge aus P-Anteil des PI-Leerlaufreglers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMLLRPANT_WERT | real | Ergebnis |
| STAT_MRMLLRPANT_EINH | string | Einheit |

<a id="job-status-mrmm-dxmsr"></a>
### STATUS_MRMM_DXMSR

M_E externer Momenteneingriff MSR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMM_DXMSR_WERT | real | Ergebnis |
| STAT_MRMM_DXMSR_EINH | string | Einheit |

<a id="job-status-mrmm-eakt"></a>
### STATUS_MRMM_EAKT

M_E Aktuelle Einspritzmenge (ohne ARD)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMM_EAKT_WERT | real | Ergebnis |
| STAT_MRMM_EAKT_EINH | string | Einheit |

<a id="job-status-mrmm-eard"></a>
### STATUS_MRMM_EARD

M_E Menge ARD - Gesamt vor Begrenzung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMM_EARD_WERT | real | Ergebnis |
| STAT_MRMM_EARD_EINH | string | Einheit |

<a id="job-status-mrmm-ebegr"></a>
### STATUS_MRMM_EBEGR

M_E resultierende Begrenzungsmenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMM_EBEGR_WERT | real | Ergebnis |
| STAT_MRMM_EBEGR_EINH | string | Einheit |

<a id="job-status-mrmm-edelb"></a>
### STATUS_MRMM_EDELB

M_E begrenzte Abgleichmenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMM_EDELB_WERT | real | Ergebnis |
| STAT_MRMM_EDELB_EINH | string | Einheit |

<a id="job-status-mrmm-efgr"></a>
### STATUS_MRMM_EFGR

M_E Wunschmenge aus Fahrgeschwindigkeitsregelung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMM_EFGR_WERT | real | Ergebnis |
| STAT_MRMM_EFGR_EINH | string | Einheit |

<a id="job-status-mrmm-ekorr"></a>
### STATUS_MRMM_EKORR

M_E Fahrmenge korrigiert mit Vollast- und Mengenabgleich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMM_EKORR_WERT | real | Ergebnis |
| STAT_MRMM_EKORR_EINH | string | Einheit |

<a id="job-status-mrmm-ellr"></a>
### STATUS_MRMM_ELLR

M_E Menge aus Leerlaufregelung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMM_ELLR_WERT | real | Ergebnis |
| STAT_MRMM_ELLR_EINH | string | Einheit |

<a id="job-status-mrmm-elrr"></a>
### STATUS_MRMM_ELRR

M_E Menge aus Laufruheregler

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMM_ELRR_WERT | real | Ergebnis |
| STAT_MRMM_ELRR_EINH | string | Einheit |

<a id="job-status-mrmm-emot"></a>
### STATUS_MRMM_EMOT

M_E Einspritzmenge nach ARD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMM_EMOT_WERT | real | Ergebnis |
| STAT_MRMM_EMOT_EINH | string | Einheit |

<a id="job-status-mrmm-epwg"></a>
### STATUS_MRMM_EPWG

M_E Wunschmenge = f(PWG) aus Fahrverhaltenkennfeld

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMM_EPWG_WERT | real | Ergebnis |
| STAT_MRMM_EPWG_EINH | string | Einheit |

<a id="job-status-mrmm-estar"></a>
### STATUS_MRMM_ESTAR

M_E resultierender Startmengen-Sollwert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMM_ESTAR_WERT | real | Ergebnis |
| STAT_MRMM_ESTAR_EINH | string | Einheit |

<a id="job-status-mrmm-ewun"></a>
### STATUS_MRMM_EWUN

M_E Fahrerwunschmenge nach externem Mengeneingriff

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMM_EWUN_WERT | real | Ergebnis |
| STAT_MRMM_EWUN_EINH | string | Einheit |

<a id="job-status-mrmm-ewunf"></a>
### STATUS_MRMM_EWUNF

M_E Fahrerwunschmenge aus PWG oder FGR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMM_EWUNF_WERT | real | Ergebnis |
| STAT_MRMM_EWUNF_EINH | string | Einheit |

<a id="job-status-mrmn-llbas"></a>
### STATUS_MRMN_LLBAS

N Leerlaufsolldrehzahl

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMN_LLBAS_WERT | real | Ergebnis |
| STAT_MRMN_LLBAS_EINH | string | Einheit |

<a id="job-status-mrmpwgfi"></a>
### STATUS_MRMPWGFI

PWG gefilterte Pedalwertgeber-Position

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMPWGFI_WERT | real | Ergebnis |
| STAT_MRMPWGFI_EINH | string | Einheit |

<a id="job-status-mrmstatus"></a>
### STATUS_MRMSTATUS

Status Motorbetriebsphase

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMSTATUS_WERT | real | Ergebnis |
| STAT_MRMSTATUS_EINH | string | Einheit |

<a id="job-status-mrofabzust"></a>
### STATUS_MROFABZUST

Zustand Ablaufsteuerung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MROFABZUST_WERT | real | Ergebnis |
| STAT_MROFABZUST_EINH | string | Einheit |

<a id="job-status-mrofgr-abn"></a>
### STATUS_MROFGR_ABN

FGR Abschalt-Bedingungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MROFGR_ABN_WERT | real | Ergebnis |
| STAT_MROFGR_ABN_EINH | string | Einheit |

<a id="job-status-mrokickdwn"></a>
### STATUS_MROKICKDWN

Schalter Kickdown

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MROKICKDWN_WERT | real | Ergebnis |
| STAT_MROKICKDWN_EINH | string | Einheit |

<a id="job-status-mrollrdant"></a>
### STATUS_MROLLRDANT

M_E Menge aus Leerlaufregler-DT1-Vorsteuerung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MROLLRDANT_WERT | real | Ergebnis |
| STAT_MROLLRDANT_EINH | string | Einheit |

<a id="job-status-mrolrrreg"></a>
### STATUS_MROLRRREG

Nsegm Segmentdrehzahl-Regelabweichung fuer Laufruheregler

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MROLRRREG_WERT | real | Ergebnis |
| STAT_MROLRRREG_EINH | string | Einheit |

<a id="job-status-mrom-ardff"></a>
### STATUS_MROM_ARDFF

M_E Menge ARD - Fuehrungsformer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MROM_ARDFF_WERT | real | Ergebnis |
| STAT_MROM_ARDFF_EINH | string | Einheit |

<a id="job-status-mromd-fahr"></a>
### STATUS_MROMD_FAHR

Fahrerwunschmoment

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MROMD_FAHR_WERT | real | Ergebnis |
| STAT_MROMD_FAHR_EINH | string | Einheit |

<a id="job-status-mromd-reib"></a>
### STATUS_MROMD_REIB

Reibmoment

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MROMD_REIB_WERT | real | Ergebnis |
| STAT_MROMD_REIB_EINH | string | Einheit |

<a id="job-status-mromd-soll"></a>
### STATUS_MROMD_SOLL

Sollmoment

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MROMD_SOLL_WERT | real | Ergebnis |
| STAT_MROMD_SOLL_EINH | string | Einheit |

<a id="job-status-xcmz-e"></a>
### STATUS_XCMZ_E

EWS Uebertragungsfehlerzaehler

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_XCMZ_E_WERT | real | Ergebnis |
| STAT_XCMZ_E_EINH | string | Einheit |

<a id="job-status-zhosync-st"></a>
### STATUS_ZHOSYNC_ST

Synchronisationsstatus des Zumesshandlers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ZHOSYNC_ST_WERT | real | Ergebnis |
| STAT_ZHOSYNC_ST_EINH | string | Einheit |

<a id="job-status-zumab-he"></a>
### STATUS_ZUMAB_HE

Ansteuerbeginn Haupteinspritzung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ZUMAB_HE_WERT | real | Ergebnis |
| STAT_ZUMAB_HE_EINH | string | Einheit |

<a id="job-status-zumab-ne"></a>
### STATUS_ZUMAB_NE

Ansteuerbeginn Nacheinspritzung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ZUMAB_NE_WERT | real | Ergebnis |
| STAT_ZUMAB_NE_EINH | string | Einheit |

<a id="job-status-zumad-ne"></a>
### STATUS_ZUMAD_NE

Ansteuerdauer Nacheinspritzung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ZUMAD_NE_WERT | real | Ergebnis |
| STAT_ZUMAD_NE_EINH | string | Einheit |

<a id="job-status-zuoab-ve1"></a>
### STATUS_ZUOAB_VE1

Ansteuerbeginn Voreinspritzung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ZUOAB_VE1_WERT | real | Ergebnis |
| STAT_ZUOAB_VE1_EINH | string | Einheit |

<a id="job-status-zuoad-he"></a>
### STATUS_ZUOAD_HE

Ansteuerdauer Haupteinspritzung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ZUOAD_HE_WERT | real | Ergebnis |
| STAT_ZUOAD_HE_EINH | string | Einheit |

<a id="job-status-zuoad-ve1"></a>
### STATUS_ZUOAD_VE1

Ansteuerdauer Voreinspritzung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ZUOAD_VE1_WERT | real | Ergebnis |
| STAT_ZUOAD_VE1_EINH | string | Einheit |

<a id="job-status-zuome-ve"></a>
### STATUS_ZUOME_VE

M_E Menge Voreinspritzung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ZUOME_VE_WERT | real | Ergebnis |
| STAT_ZUOME_VE_EINH | string | Einheit |

<a id="job-status-zuomehe"></a>
### STATUS_ZUOMEHE

M_E Menge Haupteinspritzung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ZUOMEHE_WERT | real | Ergebnis |
| STAT_ZUOMEHE_EINH | string | Einheit |

<a id="job-status-zuomevgw"></a>
### STATUS_ZUOMEVGW

GW-Kennfeld Menge Voreinspritzung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ZUOMEVGW_WERT | real | Ergebnis |
| STAT_ZUOMEVGW_EINH | string | Einheit |

<a id="job-status-zuove-stat"></a>
### STATUS_ZUOVE_STAT

Voreinspritzung - Schalter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ZUOVE_STAT_WERT | real | Ergebnis |
| STAT_ZUOVE_STAT_EINH | string | Einheit |

<a id="job-status-an-lufttemperatur"></a>
### STATUS_AN_LUFTTEMPERATUR

LTF Lufttemperatur

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_AN_LUFTTEMPERATUR_WERT | real | Ergebnis |
| STAT_AN_LUFTTEMPERATUR_EINH | string | Einheit |

<a id="job-status-ladedruck"></a>
### STATUS_LADEDRUCK

LDF Ladedruck

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LADEDRUCK_WERT | real | Ergebnis |
| STAT_LADEDRUCK_EINH | string | Einheit |

<a id="job-status-motordrehzahl"></a>
### STATUS_MOTORDREHZAHL

N Drehzahl

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MOTORDREHZAHL_WERT | real | Ergebnis |
| STAT_MOTORDREHZAHL_EINH | string | Einheit |

<a id="job-status-motortemperatur"></a>
### STATUS_MOTORTEMPERATUR

WTF Wassertemperatur

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MOTORTEMPERATUR_WERT | real | Ergebnis |
| STAT_MOTORTEMPERATUR_EINH | string | Einheit |

<a id="job-status-pwg-fahrerwunsch"></a>
### STATUS_PWG_FAHRERWUNSCH

PWG Pedalwertgeber Poti 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_PWG_FAHRERWUNSCH_WERT | real | Ergebnis |
| STAT_PWG_FAHRERWUNSCH_EINH | string | Einheit |

<a id="job-status-pwg-poti-spannung"></a>
### STATUS_PWG_POTI_SPANNUNG

PWG Spannung Pedalwertgeber Poti 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_PWG_POTI_SPANNUNG_WERT | real | Ergebnis |
| STAT_PWG_POTI_SPANNUNG_1_WERT | real | Ergebnis |
| STAT_ROHWERT1 | int | Ergebnis |
| STAT_ROHWERT2 | int | Ergebnis |
| STAT_PWG_POTI_SPANNUNG_EINH | string | Einheit |

<a id="job-steuern-check-zuheizer"></a>
### STEUERN_CHECK_ZUHEIZER

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-check-zuheizer-ecos"></a>
### STEUERN_CHECK_ZUHEIZER_ECOS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-status-raildruck"></a>
### STATUS_RAILDRUCK

KDF Raildruck

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_RAILDRUCK_WERT | real | Ergebnis |
| STAT_RAILDRUCK_EINH | string | Einheit |

<a id="job-status-ubatt"></a>
### STATUS_UBATT

UBT Batteriespannung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_UBATT_WERT | real | Ergebnis |
| STAT_UBATT_EINH | string | Einheit |

<a id="job-status-vorfoerderdruck"></a>
### STATUS_VORFOERDERDRUCK

VDF Vorfoerderdruck

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_VORFOERDERDRUCK_WERT | real | Ergebnis |
| STAT_VORFOERDERDRUCK_EINH | string | Einheit |

<a id="job-status-ehmfdra"></a>
### STATUS_EHMFDRA

Tastverhaeltnis Ansteuerung Drallklappe

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_EHMFDRA_WERT | real | Ergebnis |
| STAT_EHMFDRA_EINH | string | Einheit |

<a id="job-abgleich-verstellen-verbr-korfaktor-roh"></a>
### ABGLEICH_VERSTELLEN_VERBR_KORFAKTOR_ROH

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_VERSTELLEN_VERBR_KORFAKTOR_ROH_WERT | int | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_VERSTELLEN_VERBR_KORFAKTOR_ROH_STATUS | int | Status |

<a id="job-abgleich-lesen-kdf-kennlinie"></a>
### ABGLEICH_LESEN_KDF_KENNLINIE

Raildrucksensor Kennlinien -Abgleich lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_LESEN_KDF_KENNLINIE_W1 | real | Aktueller Erster - Wert |
| ABGLEICH_LESEN_KDF_KENNLINIE_W2 | real | Aktueller Zweiter - Wert |
| ABGLEICH_LESEN_KDF_KENNLINIE_W1_ROH | int | Aktueller Erster - Roh-Wert |
| ABGLEICH_LESEN_KDF_KENNLINIE_W2_ROH | int | Aktueller Zweiter - Roh-Wert |
| ABGLEICH_LESEN_KDF_KENNLINIE_STATUS | int | Rueckmeldebyte |

<a id="job-abgleich-verstellen-kdf-kennlinie"></a>
### ABGLEICH_VERSTELLEN_KDF_KENNLINIE

Mengendrift Abgleich verstellen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_VERSTELLEN_KDF_KENNLINIE_W1 | real | Neuer Verstellwert |
| ABGLEICH_VERSTELLEN_KDF_KENNLINIE_W2 | real | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_VERSTELLEN_KDF_KENNLINIE_STATUS | int | Status |

<a id="job-abgleich-verstellen-kdf-kennlinie-roh"></a>
### ABGLEICH_VERSTELLEN_KDF_KENNLINIE_ROH

Mengendrift Abgleich verstellen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_VERSTELLEN_KDF_KENNLINIE_W1_ROH | int | Neuer Verstellwert |
| ABGLEICH_VERSTELLEN_KDF_KENNLINIE_W2_ROH | int | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_VERSTELLEN_KDF_KENNLINIE_STATUS_ROH | int | Status |

<a id="job-abgleich-prog-kdf-kennlinie"></a>
### ABGLEICH_PROG_KDF_KENNLINIE

RAILDRUCHSENSOR Abgleich programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_PROG_KDF_KENNLINIE_STATUS | int | Status |

<a id="job-abgleich-lesen-hfm"></a>
### ABGLEICH_LESEN_HFM

HFM-Abgleich lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_LESEN_HFM_NULL_WERT | real | Nullpunktabgleich - Wert |
| ABGLEICH_LESEN_HFM_LL_WERT | real | Leerlaufabgleich - Wert |
| ABGLEICH_LESEN_HFM_LAST_WERT | real | Lastabgleich - Wert |
| ABGLEICH_LESEN_HFM_NULL_WERT_ROH | int | Nullpunktabgleich - Wert_ROH |
| ABGLEICH_LESEN_HFM_LL_WERT_ROH | int | Leerlaufabgleich - Wert_ROH |
| ABGLEICH_LESEN_HFM_LAST_WERT_ROH | int | Lastabgleich - Wert_ROH |
| ABGLEICH_LESEN_HFM_STATUS | int | Rueckmeldebyte |

<a id="job-abgleich-verstellen-hfm"></a>
### ABGLEICH_VERSTELLEN_HFM

HFM Abgleich verstellen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_VERSTELLEN_HFM_NULL_WERT | real | Neuer Verstellwert |
| ABGLEICH_VERSTELLEN_HFM_LL_WERT | real | Neuer Verstellwert |
| ABGLEICH_VERSTELLEN_HFM_LAST_WERT | real | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_VERSTELLEN_HFM_STATUS | int | Status |

<a id="job-abgleich-verstellen-hfm-roh"></a>
### ABGLEICH_VERSTELLEN_HFM_ROH

HFM Abgleich verstellen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_VERSTELLEN_HFM_NULL_WERT_ROH | int | Neuer Verstellwert |
| ABGLEICH_VERSTELLEN_HFM_LL_WERT_ROH | int | Neuer Verstellwert |
| ABGLEICH_VERSTELLEN_HFM_LAST_WERT_ROH | int | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_VERSTELLEN_HFM_STATUS_ROH | int | Status |

<a id="job-abgleich-prog-hfm"></a>
### ABGLEICH_PROG_HFM

HFM Abgleich programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_PROG_HFM_STATUS | int | Status |

<a id="job-status-lmm-masse"></a>
### STATUS_LMM_MASSE

LMM Spannung Luftmassenmesser

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LMM_MASSE_WERT | real | Ergebnis |
| STAT_LMM_MASSE_EINH | string | Einheit |

## Tables

### Index

- [BETRIEBSWTAB](#table-betriebswtab) (167 × 17)
- [BITS](#table-bits) (39 × 9)
- [JOBRESULT](#table-jobresult) (37 × 2)
- [FORTTEXTE](#table-forttexte) (58 × 6)
- [FARTMATRIX](#table-fartmatrix) (57 × 33)
- [FARTTEXTE](#table-farttexte) (108 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (18 × 5)

<a id="table-betriebswtab"></a>
### BETRIEBSWTAB

Dimensions: 167 rows × 17 columns

| NAME | TELEGRAM | POS_ADR | LEN_ADR | ADR | BYTE | DATA_TYPE | COMPU_TYPE | FACT_A | FACT_B | MASK | VALUE | ANZ | MEAS | RANGE | JOBNAME | LNAME |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| anmPWG | B812F1042C100000 | 06 | 2 | 0x0F60 | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | % | -- | anmPWG | PWG Pedalwertgeber Poti 1 |
| anmUBT | B812F1042C100000 | 06 | 2 | 0x0F65 | 06 | 5 | -- | 0.0236197458 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anmUBT | UBT Batteriespannung |
| anmVDF | B812F1042C100000 | 06 | 2 | 0x1F06 | 06 | 5 | -- | 0.001 | 0 | 0x00 | 0x00 | 6.2f | bar | -- | anmVDF | VDF Vorfoerderdruck |
| anmWTF | B812F1042C100000 | 06 | 2 | 0x0F00 | 06 | 5 | -- | 0.1 | -273.14 | 0x00 | 0x00 | 6.2f | Grad C | -- | anmWTF | WTF Wassertemperatur |
| armM_List | B812F1042C100000 | 06 | 2 | 0x0F30 | 06 | 5 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | mg/Hub Luft | -- | armM_List | M_L aktuelle Luftmasse |
| armM_Lsoll | B812F1042C100000 | 06 | 2 | 0x0F32 | 06 | 5 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | mg/Hub Luft | -- | armM_Lsoll | M_L Sollwert fuer AGR-Regelung |
| dzmNmit | B812F1042C100000 | 06 | 2 | 0x0F10 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min | -- | dzmNmit | N Drehzahl |
| ehmFKLI | B812F1042C100000 | 06 | 2 | 0x0E91 | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | % | -- | ehmFKLI | Tastverhaeltnis Ansteuerung Klimakompressor |
| ehmFARS | B812F1042C100000 | 06 | 2 | 0x0E80 | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | % | -- | ehmFARS | Tastverhaeltnis Ansteuerung AGR-Steller |
| ehmFEKP | B812F1042C100000 | 06 | 2 | 0x0EA6 | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | % | -- | ehmFEKP | Tastverhaeltnis Ansteuerung Vorfoerderpumpe |
| ehmFDRA | B812F1042C100000 | 06 | 2 | 0x0E9A | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | % | -- | ehmFDRA | Tastverhaeltnis Ansteuerung Drallklappe |
| ehmFGRS | B812F1042C100000 | 06 | 2 | 0x0E87 | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | % | -- | ehmFGRS | Tastverhaeltnis Ansteuerung Gluehrelais |
| ehmFKWH | B812F1042C100000 | 06 | 2 | 0x0E9B | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | % | -- | ehmFKWH | Tastverhaeltnis Ansteuerung Kuehlwasserheizung |
| ehmFKDR | B812F1042C100000 | 06 | 2 | 0x0EA5 | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | % | -- | ehmFKDR | Tastverhaeltnis Ansteuerung Raildruckregelventil |
| ehmFLDS | B812F1042C100000 | 06 | 2 | 0x0E81 | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | % | -- | ehmFLDS | Tastverhaeltnis Ansteuerung Ladedrucksteller |
| ehmFMLS | B812F1042C100000 | 06 | 2 | 0x0EA2 | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | % | -- | ehmFMLS | Tastverhaeltnis Ansteuerung Elektroluefter |
| ehmFMML | B812F1042C100000 | 06 | 2 | 0x0E9F | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | % | -- | ehmFMML | Tastverhaeltnis Ansteuerung Motorlager |
| ldmP_Llin | B812F1042C100000 | 06 | 2 | 0x0F40 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | mbar | -- | ldmP_Llin | aktueller Ladedruck  / Luftdruck |
| ldmP_Lsoll | B812F1042C100000 | 06 | 2 | 0x0F42 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | mbar | -- | ldmP_Lsoll | Sollwert Ladedruck |
| mrmM_EFAHR | B812F1042C100000 | 06 | 2 | 0xDC86 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmM_EFAHR | M_E Fahrmenge nach Laufruheregler |
| zumP_RAIL | B812F1042C100000 | 06 | 2 | 0x1F5D | 06 | 5 | -- | 10.235414 | 0 | 0x00 | 0x00 | 6.2f | bar | -- | zumP_RAIL | Raildruck fuer Mengenzumessung |
| zumPQsoll | B812F1042C100000 | 06 | 2 | 0x1F5E | 06 | 5 | -- | 10.235414 | 0 | 0x00 | 0x00 | 6.2f | bar | -- | zumPQsoll | Raildruck Sollwert |
| admADF | B812F1042C100000 | 06 | 2 | 0x2041 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | mbar | -- | admADF | ADF Rohwert Atmosphaerendruck |
| admIDV | B812F1042C100000 | 06 | 2 | 0x2FFE | 06 | 5 | -- | 4.995005 | 0 | 0x00 | 0x00 | 6.2f | mA | -- | admIDV | IDV Rohwert Istwert Stromregelung Druckregelventil |
| admKDF | B812F1042C100000 | 06 | 2 | 0x2FFC | 06 | 5 | -- | 10.235414 | 0 | 0x00 | 0x00 | 6.2f | bar | -- | admKDF | KDF Rohwert Raildruck |
| admLDF | B812F1042C100000 | 06 | 2 | 0x2042 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | mbar | -- | admLDF | LDF Rohwert Ladedruck |
| admLMM | B812F1042C100000 | 06 | 2 | 0x2061 | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | % | -- | admLMM | LMM Rohwert Luftmasse |
| admLTF | B812F1042C100000 | 06 | 2 | 0x2001 | 06 | 5 | -- | 0.1 | -273.14 | 0x00 | 0x00 | 6.2f | Grad C | -- | admLTF | LTF Rohwert Lufttemperatur |
| admPGS | B812F1042C100000 | 06 | 2 | 0x2FFA | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | % | -- | admPGS | PGS Rohwert Pedalwertgeber Poti 2 |
| admPWG | B812F1042C100000 | 06 | 2 | 0x2060 | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | % | -- | admPWG | PWG Rohwert Pedalwertgeber Poti 1 |
| admUBT | B812F1042C100000 | 06 | 2 | 0x2065 | 06 | 5 | -- | 0.0236197458 | 0 | 0x00 | 0x00 | 6.2f | V | -- | admUBT | UBT Rohwert Batteriespannung |
| admUC1 | B812F1042C100000 | 06 | 2 | 0x2FF8 | 06 | 5 | -- | 0.0205718988 | 0 | 0x00 | 0x00 | 6.2f | V | -- | admUC1 | UC1 Rohwert Kondensatorspannung 1 fuer Zylinder 1,2,3 |
| admUC2 | B812F1042C100000 | 06 | 2 | 0x2FF9 | 06 | 5 | -- | 0.0205718988 | 0 | 0x00 | 0x00 | 6.2f | V | -- | admUC2 | UC2 Rohwert Kondensatorspannung 2 fuer Zylinder 4,5,6 |
| admUG1 | B812F1042C100000 | 06 | 2 | 0x2FF6 | 06 | 5 | -- | 0.01764418377 | 0 | 0x00 | 0x00 | 6.2f | V | -- | admUG1 | UG1 Rohwert Speisespannung 1 fuer Pedalwertgeber 2, Ladedruckfuehler, Luftmassenmesser |
| admUG2 | B812F1042C100000 | 06 | 2 | 0x2FF7 | 06 | 5 | -- | 0.01764418377 | 0 | 0x00 | 0x00 | 6.2f | V | -- | admUG2 | UG2 Rohwert Speisespannung 2 fuer Pedalwertgeber 1, Kraftstoff- ,Vorfoerderdruckfuehler |
| admVDF | B812F1042C100000 | 06 | 2 | 0x2006 | 06 | 5 | -- | 0.001 | 0 | 0x00 | 0x00 | 6.2f | bar | -- | admVDF | VDF Rohwert Vorfoerderdruck |
| admWTF | B812F1042C100000 | 06 | 2 | 0x2000 | 06 | 5 | -- | 0.1 | -273.14 | 0x00 | 0x00 | 6.2f | Grad C | -- | admWTF | WTF Rohwert Wassertemperatur |
| anmADF | B812F1042C100000 | 06 | 2 | 0x0F63 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | mbar | -- | anmADF | ADF Atmosphaerendruck |
| anmIDV | B812F1042C100000 | 06 | 2 | 0x0FFE | 06 | 5 | -- | 4.995005 | 0 | 0x00 | 0x00 | 6.2f | mA | -- | anmIDV | IDV Istwert Stromregelung Druckregelventil |
| anmKDF | B812F1042C100000 | 06 | 2 | 0x0FFC | 06 | 5 | -- | 10.235414 | 0 | 0x00 | 0x00 | 6.2f | bar | -- | anmKDF | KDF Raildruck |
| anmLDF | B812F1042C100000 | 06 | 2 | 0x0F62 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | mbar | -- | anmLDF | LDF Ladedruck |
| anmLMM | B812F1042C100000 | 06 | 2 | 0x0F61 | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | % | -- | anmLMM | LMM Luftmasse |
| anmLTF | B812F1042C100000 | 06 | 2 | 0x0F01 | 06 | 5 | -- | 0.1 | -273.14 | 0x00 | 0x00 | 6.2f | Grad C | -- | anmLTF | LTF Lufttemperatur |
| anmPGS | B812F1042C100000 | 06 | 2 | 0x0FFA | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | % | -- | anmPGS | PGS Pedalwertgeber Poti 2 |
| anmUC1 | B812F1042C100000 | 06 | 2 | 0x0FF8 | 06 | 5 | -- | 0.0205718988 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anmUC1 | UC1 Kondensatorspannung 1 fuer Zylinder 1,2,3 |
| anmUC2 | B812F1042C100000 | 06 | 2 | 0x0FF9 | 06 | 5 | -- | 0.0205718988 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anmUC2 | UC2 Kondensatorspannung 2 fuer Zylinder 4,5,6 |
| anmUG1 | B812F1042C100000 | 06 | 2 | 0x0FF6 | 06 | 5 | -- | 0.01764418377 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anmUG1 | UG1 Speisespannung 1 fuer Pedalwertgeber 2, Ladedruckfuehler, Luftmassenmesser |
| anmUG2 | B812F1042C100000 | 06 | 2 | 0x0FF7 | 06 | 5 | -- | 0.01764418377 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anmUG2 | UG2 Speisespannung 2 fuer Pedalwertgeber 1, Kraftstoff- ,Vorfoerderdruckfuehler |
| anoU_ADF | B812F1042C100000 | 06 | 2 | 0x3011 | 06 | 5 | -- | 0.0048875855 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anoU_ADF | ADF Spannung Atmosphaerendruckfuehler |
| anoU_IDV | B812F1042C100000 | 06 | 2 | 0x300C | 06 | 5 | -- | 0.0048875855 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anoU_IDV | IDV Spannung zur Strommessung Druckregelventil |
| anoU_KDF | B812F1042C100000 | 06 | 2 | 0x300A | 06 | 5 | -- | 0.0048875855 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anoU_KDF | KDF Spannung Raildruckfuehler |
| anoU_LDF | B812F1042C100000 | 06 | 2 | 0x3004 | 06 | 5 | -- | 0.0048875855 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anoU_LDF | LDF Spannung Ladedruckfuehler |
| anoU_LMM | B812F1042C100000 | 06 | 2 | 0x0F34 | 06 | 5 | -- | 0.0048875855 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anoU_LMM | LMM Spannung Luftmassenmesser |
| anoU_LTF | B812F1042C100000 | 06 | 2 | 0x300E | 06 | 5 | -- | 0.0048875855 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anoU_LTF | LTF Spannung Lufttemperaturfuehler |
| anoU_PGS | B812F1042C100000 | 06 | 2 | 0x3006 | 06 | 5 | -- | 0.0048875855 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anoU_PGS | PGS Spannung Pedalwertgeber Poti 2 |
| anoU_PWG | B812F1042C100000 | 06 | 2 | 0x0F35 | 06 | 5 | -- | 0.0048875855 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anoU_PWG | PWG Spannung Pedalwertgeber Poti 1 |
| anoU_UBT | B812F1042C100000 | 06 | 2 | 0x3013 | 06 | 5 | -- | 0.0048875855 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anoU_UBT | UBT Spannung Batteriespannung |
| anoU_UC1 | B812F1042C100000 | 06 | 2 | 0x3008 | 06 | 5 | -- | 0.0048875855 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anoU_UC1 | UC1 Spannung Kondensatorspannung 1 fuer Zylinder 1,2,3 |
| anoU_UC2 | B812F1042C100000 | 06 | 2 | 0x3009 | 06 | 5 | -- | 0.0048875855 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anoU_UC2 | UC2 Spannung Kondensatorspannung 2 fuer Zylinder 4,5,6 |
| anoU_UG1 | B812F1042C100000 | 06 | 2 | 0x3016 | 06 | 5 | -- | 0.01764418377 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anoU_UG1 | UG1 Spannung Speisespannung 1 fuer Pedalwertgeber 2, Ladedruckfuehler, Luftmassenmesser |
| anoU_UG2 | B812F1042C100000 | 06 | 2 | 0x3017 | 06 | 5 | -- | 0.01764418377 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anoU_UG2 | UG2 Spannung Speisespannung 2 fuer Pedalwertgeber 1, Kraftstoff- ,Vorfoerderdruckfuehler |
| anoU_VDF | B812F1042C100000 | 06 | 2 | 0x301A | 06 | 5 | -- | 0.0048875855 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anoU_VDF | VDF Spannung Vorfoerderdruckfuehler |
| anoU_WTF | B812F1042C100000 | 06 | 2 | 0x3002 | 06 | 5 | -- | 0.0048875855 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anoU_WTF | WTF Spannung Wassertemperaturfuehler |
| aroIST_4 | B812F1042C100000 | 06 | 2 | 0x0010 | 06 | 5 | -- | 0.0359929742 | 0 | 0x00 | 0x00 | 6.2f | kg/h | -- | aroIST_4 | MLt Luftmassenstrom n. Linearisierung u. Mittelung |
| aroIST_5 | B812F1042C100000 | 06 | 2 | 0xDF0E | 06 | 5 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | mg/Hub Luft | -- | aroIST_5 | M_L normierte Luftmasse (nicht T_L/P_ADF-korrig.) |
| aroREG_2 | B812F1042C100000 | 06 | 2 | 0x0EE0 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | aroREG_2 | AGR-Status  Regelung / Steuerung / Abschaltung |
| aroSOLL_5 | B812F1042C100000 | 06 | 2 | 0x0F31 | 06 | 5 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | mg/Hub Luft | -- | aroSOLL_5 | M_L Luft-Sollwert nach Sollwertbegrenzung |
| camN_EL | B812F1042C100000 | 06 | 2 | 0x2220 | 06 | 5 | -- | 0.0915555284 | 0 | 0x00 | 0x00 | 6.2f | 1/min | -- | camN_EL | MLS Drehzahlstufe E-Luefter |
| camS_AC | B812F1042C100000 | 06 | 2 | 0x1FB1 | 06 | 2 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | camS_AC | Schalter Klimabereitschaft |
| camS_HZL | B812F1042C100000 | 06 | 2 | 0xE4D1 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | camS_HZL | Anforderung Heizleistung von Klimasteuergeraet |
| camS_KO | B812F1042C100000 | 06 | 2 | 0x1FB0 | 06 | 2 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | camS_KO | Schalter Klimakompressor |
| camT_UMG | B812F1042C100000 | 06 | 2 | 0xE4D0 | 06 | 5 | -- | 0.1 | -273.14 | 0x00 | 0x00 | 6.2f | Grad C | -- | camT_UMG | Umgebungstemperatur aus CAN |
| caoVERB | B812F1042C100000 | 06 | 2 | 0x2160 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | ul | -- | caoVERB | Kraftstoffverbrauch fuer CAN DDE4-VERBRAUCH |
| comGTR_opt | B812F1042C100000 | 06 | 2 | 0x1C00 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | comGTR_opt | Identifikation Handschalter/Automatik |
| dimDIG_0 | B812F1042C100000 | 06 | 2 | 0x0F6C | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | dimDIG_0 | Auf logisch 0 erkannte Digitaleingaenge |
| dimDIG_1 | B812F1042C100000 | 06 | 2 | 0x0F6D | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | dimDIG_1 | Auf logisch 1 erkannte Digitaleingaenge |
| dimDIGprel | B812F1042C100000 | 06 | 2 | 0x0F70 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | dimDIGprel | Entprellte logische Zustaende der digitalen Eingaenge |
| dimF_MFL | B812F1042C100000 | 06 | 2 | 0x2F74 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | dimF_MFL | FGR Multifunktionslenkrad |
| dzmNakt | B812F1042C100000 | 06 | 2 | 0x0F12 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min | -- | dzmNakt | N aktuelle Drehzahl aus letzter Periode |
| dzmzMk1 | B812F1042C100000 | 06 | 2 | 0x0F19 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | dzmzMk1 | Selektive Mengenkorrektur Zylinder 1 |
| dzmzMk2 | B812F1042C100000 | 06 | 2 | 0x0F1A | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | dzmzMk2 | Selektive Mengenkorrektur Zylinder 2 |
| dzmzMk3 | B812F1042C100000 | 06 | 2 | 0x0F1B | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | dzmzMk3 | Selektive Mengenkorrektur Zylinder 3 |
| dzmzMk4 | B812F1042C100000 | 06 | 2 | 0x0F1C | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | dzmzMk4 | Selektive Mengenkorrektur Zylinder 4 |
| dzmzMk5 | B812F1042C100000 | 06 | 2 | 0x0F1D | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | dzmzMk5 | Selektive Mengenkorrektur Zylinder 5 |
| dzmzMk6 | B812F1042C100000 | 06 | 2 | 0x0F1E | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | dzmzMk6 | Selektive Mengenkorrektur Zylinder 6 |
| dzmzN1 | B812F1042C100000 | 06 | 2 | 0x0F13 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min | -- | dzmzN1 | Selektive Drehzahl Zylinder 1 |
| dzmzN2 | B812F1042C100000 | 06 | 2 | 0x0F14 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min | -- | dzmzN2 | Selektive Drehzahl Zylinder 2 |
| dzmzN3 | B812F1042C100000 | 06 | 2 | 0x0F15 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min | -- | dzmzN3 | Selektive Drehzahl Zylinder 3 |
| dzmzN4 | B812F1042C100000 | 06 | 2 | 0x0F16 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min | -- | dzmzN4 | Selektive Drehzahl Zylinder 4 |
| dzmzN5 | B812F1042C100000 | 06 | 2 | 0x0F17 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min | -- | dzmzN5 | Selektive Drehzahl Zylinder 5 |
| dzmzN6 | B812F1042C100000 | 06 | 2 | 0x0F18 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min | -- | dzmzN6 | Selektive Drehzahl Zylinder 6 |
| edmRSTCD | B812F1042C100000 | 06 | 2 | 0x0E00 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | edmRSTCD | Restart Code |
| fbmBSTZ_UB | B812F1042C100000 | 06 | 2 | 0x1300 | 06 | 5 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | h | -- | fbmBSTZ_UB | UB Betriebsstunden |
| fbmDIA_C | B812F1042C100000 | 06 | 2 | 0xDF01 | 06 | 2 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | fbmDIA_C | Diagnoselampe ueber CAN |
| fbmMIL_C | B812F1042C100000 | 06 | 2 | 0xDF02 | 06 | 2 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | fbmMIL_C | MIL Malfunction Indikator Lamp ueber CAN |
| fbmSDIAL | B812F1042C100000 | 06 | 2 | 0x1000 | 06 | 2 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | fbmSDIAL | Anforderung Diagnoselampe aus Fehlerbehandlung (0:Aus,1:Ein,2:Blinken) |
| fboDIALA | B812F1042C100000 | 06 | 2 | 0xDF00 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | fboDIALA | Diagnose - Lampe Status (255 = EIN) |
| fboS_00 | B812F1042C100000 | 06 | 2 | 0xDF70 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | fboS_00 | Defekte Pfade 1 bis 16 |
| fboS_02 | B812F1042C100000 | 06 | 2 | 0xDF72 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | fboS_02 | Defekte Pfade 17 bis 32 |
| fboS_04 | B812F1042C100000 | 06 | 2 | 0xDF74 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | fboS_04 | Defekte Pfade 33 bis 48 |
| fboS_06 | B812F1042C100000 | 06 | 2 | 0xDF76 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | fboS_06 | Defekte Pfade 49 bis 64 |
| fboS_08 | B812F1042C100000 | 06 | 2 | 0xDF78 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | fboS_08 | Defekte Pfade 65 bis 80 |
| fgm_VzuN | B812F1042C100000 | 06 | 2 | 0x0F0B | 06 | 5 | -- | 0.0000391 | 0 | 0x00 | 0x00 | 6.2f | (km/h)/(1/min) | -- | fgm_VzuN | Verhaeltnis Geschwindigkeit/Drehzahl (V/N aktuell)  |
| fgmBESCH | B812F1042C100000 | 06 | 2 | 0x0F0A | 06 | 7 | -- | 0.0847711 | -10.8506944 | 0x00 | 0x00 | 6.2f | m/s^2 | -- | fgmBESCH | Beschleunigung |
| fgmFGAKT | B812F1042C100000 | 06 | 2 | 0x0F08 | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | km/h | -- | fgmFGAKT | aktuelle Geschwindigkeit |
| gsoGS_Pha | B812F1042C100000 | 06 | 2 | 0x2152 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | gsoGS_Pha | Gluehzeitsteuerung Gluehphase |
| khoGENLAST | B812F1042C100000 | 06 | 2 | 0x0ECC | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | % | -- | khoGENLAST | Generatorlast |
| khoNOR_AB | B812F1042C100000 | 06 | 2 | 0x0FB7 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | khoNOR_AB | Zustand und Abschaltbedingungen der Kuehlmittelheizung |
| klmKLI_GEF | B812F1042C100000 | 06 | 2 | 0xE4D2 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | klmKLI_GEF | Klimaanlage verbaut |
| ldmADF | B812F1042C100000 | 06 | 2 | 0x0F41 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | mbar | -- | ldmADF | aktueller Atmosphaerendruck |
| ldmT_LTGG | B812F1042C100000 | 06 | 2 | 0x0F48 | 06 | 5 | -- | 0.1 | -273.14 | 0x00 | 0x00 | 6.2f | Grad C | -- | ldmT_LTGG | Errechnete Lufttemperatur |
| ldoTVsteu | B812F1042C100000 | 06 | 2 | 0x0F49 | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | % | -- | ldoTVsteu | LDR Tastverhaeltnis Steuerung |
| mrmCASE_A | B812F1042C100000 | 06 | 2 | 0xDF21 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | mrmCASE_A | ARD Zustand-Bits der aktiven Ruckeldaempfung |
| mrmCASE_L | B812F1042C100000 | 06 | 2 | 0xDF20 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | mrmCASE_L | LLR Zustand-Bits der Leerlaufregelung |
| mrmF_GANG | B812F1042C100000 | 06 | 2 | 0x0F7E | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | mrmF_GANG | FGR aktuelle Gangstufe |
| mrmFG_SOLL | B812F1042C100000 | 06 | 2 | 0x0F09 | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | km/h | -- | mrmFG_SOLL | V Sollwert Fahrgeschwindigkeit von FGR |
| mrmKM_akt | B812F1042C100000 | 06 | 2 | 0x0FD0 | 06 | 5 | -- | 10 | 0 | 0x00 | 0x00 | 6.2f | km | -- | mrmKM_akt | aktueller km-Stand von Kombiinstrument |
| mrmL_FGR | B812F1042C100000 | 06 | 2 | 0x2F75 | 06 | 2 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | mrmL_FGR | FGR-Status-Indicator-Lampe ueber CAN |
| mrmLLRIAnt | B812F1042C100000 | 06 | 2 | 0xDF13 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmLLRIAnt | M_E Menge aus I-Anteil des PI-Leerlaufreglers |
| mrmLLRPAnt | B812F1042C100000 | 06 | 2 | 0xDF14 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmLLRPAnt | M_E Menge aus P-Anteil des PI-Leerlaufreglers |
| mrmM_DXMSR | B812F1042C100000 | 06 | 2 | 0x0F89 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmM_DXMSR | M_E externer Momenteneingriff MSR |
| mrmM_EAKT | B812F1042C100000 | 06 | 2 | 0x0F80 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmM_EAKT | M_E Aktuelle Einspritzmenge (ohne ARD) |
| mrmM_EARD | B812F1042C100000 | 06 | 2 | 0xDC88 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmM_EARD | M_E Menge ARD - Gesamt vor Begrenzung |
| mrmM_EBEGR | B812F1042C100000 | 06 | 2 | 0x0F8A | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmM_EBEGR | M_E resultierende Begrenzungsmenge |
| mrmM_EDELB | B812F1042C100000 | 06 | 2 | 0x1F8E | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmM_EDELB | M_E begrenzte Abgleichmenge |
| mrmM_EFGR | B812F1042C100000 | 06 | 2 | 0x0F85 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmM_EFGR | M_E Wunschmenge aus Fahrgeschwindigkeitsregelung |
| mrmM_EKORR | B812F1042C100000 | 06 | 2 | 0x0F8E | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmM_EKORR | M_E Fahrmenge korrigiert mit Vollast- und Mengenabgleich |
| mrmM_ELLR | B812F1042C100000 | 06 | 2 | 0x0F8D | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmM_ELLR | M_E Menge aus Leerlaufregelung |
| mrmM_ELRR | B812F1042C100000 | 06 | 2 | 0xDC87 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmM_ELRR | M_E Menge aus Laufruheregler |
| mrmM_EMOT | B812F1042C100000 | 06 | 2 | 0x0F8C | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmM_EMOT | M_E Einspritzmenge nach ARD |
| mrmM_EPWG | B812F1042C100000 | 06 | 2 | 0x0F84 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmM_EPWG | M_E Wunschmenge = f(PWG) aus Fahrverhaltenkennfeld |
| mrmM_ESTAR | B812F1042C100000 | 06 | 2 | 0x0F82 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmM_ESTAR | M_E resultierender Startmengen-Sollwert |
| mrmM_EWUN | B812F1042C100000 | 06 | 2 | 0x0F8B | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmM_EWUN | M_E Fahrerwunschmenge nach externem Mengeneingriff |
| mrmM_EWUNF | B812F1042C100000 | 06 | 2 | 0x0F86 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmM_EWUNF | M_E Fahrerwunschmenge aus PWG oder FGR |
| mrmN_LLBAS | B812F1042C100000 | 06 | 2 | 0x0E02 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min | -- | mrmN_LLBAS | N Leerlaufsolldrehzahl |
| mrmPWGfi | B812F1042C100000 | 06 | 2 | 0x0F83 | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | % | -- | mrmPWGfi | PWG gefilterte Pedalwertgeber-Position |
| mrmSTATUS | B812F1042C100000 | 06 | 2 | 0x0F7F | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | mrmSTATUS | Status Motorbetriebsphase |
| mroFABZUST | B812F1042C100000 | 06 | 2 | 0x0F9A | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | mroFABZUST | Zustand Ablaufsteuerung |
| mroFGR_ABN | B812F1042C100000 | 06 | 2 | 0xDF08 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | mroFGR_ABN | FGR Abschalt-Bedingungen |
| mroKickDwn | B812F1042C100000 | 06 | 2 | 0x1F9A | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | mroKickDwn | Schalter Kickdown |
| mroLLRDAnt | B812F1042C100000 | 06 | 2 | 0xDF15 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mroLLRDAnt | M_E Menge aus Leerlaufregler-DT1-Vorsteuerung |
| mroLRRReg | B812F1042C100000 | 06 | 2 | 0xDC90 | 06 | 7 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min | -- | mroLRRReg | Nsegm Segmentdrehzahl-Regelabweichung fuer Laufruheregler |
| mroM_ARDFF | B812F1042C100000 | 06 | 2 | 0xDC89 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mroM_ARDFF | M_E Menge ARD - Fuehrungsformer |
| mroMD_FAHR | B812F1042C100000 | 06 | 2 | 0x2211 | 06 | 5 | -- | 2 | 0 | 0x00 | 0x00 | 6.2f | Nm | -- | mroMD_FAHR | Fahrerwunschmoment |
| mroMD_REIB | B812F1042C100000 | 06 | 2 | 0x2212 | 06 | 5 | -- | 2 | 0 | 0x00 | 0x00 | 6.2f | Nm | -- | mroMD_REIB | Reibmoment |
| mroMD_SOLL | B812F1042C100000 | 06 | 2 | 0x2210 | 06 | 5 | -- | 2 | 0 | 0x00 | 0x00 | 6.2f | Nm | -- | mroMD_SOLL | Sollmoment |
| xcmZ_E | B812F1042C100000 | 06 | 2 | 0x0FAE | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | xcmZ_E | EWS Uebertragungsfehlerzaehler |
| zhoSYNC_ST | B812F1042C100000 | 06 | 2 | 0x1F50 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | zhoSYNC_ST | Synchronisationsstatus des Zumesshandlers |
| zumAB_HE | B812F1042C100000 | 06 | 2 | 0x1F5A | 06 | 7 | -- | 0.0234375 | 0 | 0x00 | 0x00 | 6.2f | Grad KW | -- | zumAB_HE | Ansteuerbeginn Haupteinspritzung |
| zumAB_NE | B812F1042C100000 | 06 | 2 | 0x1F60 | 06 | 7 | -- | 0.0234375 | 0 | 0x00 | 0x00 | 6.2f | Grad KW | -- | zumAB_NE | Ansteuerbeginn Nacheinspritzung |
| zumAD_NE | B812F1042C100000 | 06 | 2 | 0x1F61 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | uS | -- | zumAD_NE | Ansteuerdauer Nacheinspritzung |
| zuoAB_VE1 | B812F1042C100000 | 06 | 2 | 0x1F51 | 06 | 7 | -- | 0.0234375 | 0 | 0x00 | 0x00 | 6.2f | Grad KW | -- | zuoAB_VE1 | Ansteuerbeginn Voreinspritzung |
| zuoAD_HE | B812F1042C100000 | 06 | 2 | 0x1F5B | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | uS | -- | zuoAD_HE | Ansteuerdauer Haupteinspritzung |
| zuoAD_VE1 | B812F1042C100000 | 06 | 2 | 0x1F52 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | uS | -- | zuoAD_VE1 | Ansteuerdauer Voreinspritzung |
| zuoME_VE | B812F1042C100000 | 06 | 2 | 0x1F53 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | zuoME_VE | M_E Menge Voreinspritzung |
| zuoMEHE | B812F1042C100000 | 06 | 2 | 0x1F5C | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | zuoMEHE | M_E Menge Haupteinspritzung |
| zuoMEVGW | B812F1042C100000 | 06 | 2 | 0x1F57 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | zuoMEVGW | GW-Kennfeld Menge Voreinspritzung |
| zuoVE_STAT | B812F1042C100000 | 06 | 2 | 0x1F55 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | zuoVE_STAT | Voreinspritzung - Schalter |
| anmLTF | B812F1042C100000 | 06 | 2 | 0x0F01 | 06 | 5 | -- | 0.1 | -273.14 | 0x00 | 0x00 | 6.2f | Grad C | -- | AN_LUFTTEMPERATUR | LTF Lufttemperatur |
| anmLDF | B812F1042C100000 | 06 | 2 | 0x0F62 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | mbar | -- | LADEDRUCK | LDF Ladedruck |
| dzmNmit | B812F1042C100000 | 06 | 2 | 0x0F10 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min | -- | MOTORDREHZAHL | N Drehzahl |
| anmWTF | B812F1042C100000 | 06 | 2 | 0x0F00 | 06 | 5 | -- | 0.1 | -273.14 | 0x00 | 0x00 | 6.2f | Grad C | -- | MOTORTEMPERATUR | WTF Wassertemperatur |
| anmPWG | B812F1042C100000 | 06 | 2 | 0x0F60 | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | % | -- | PWG_FAHRERWUNSCH | PWG Pedalwertgeber Poti 1 |
| anoU_PWG | B812F1042C100000 | 06 | 2 | 0x0F35 | 06 | 5 | -- | 0.0048875855 | 0 | 0x00 | 0x00 | 6.2f | V | -- | PWG_POTI_SPANNUNG | PWG Spannung Pedalwertgeber Poti 1 |
| anmKDF | B812F1042C100000 | 06 | 2 | 0x0FFC | 06 | 5 | -- | 10.235414 | 0 | 0x00 | 0x00 | 6.2f | bar | -- | RAILDRUCK | KDF Raildruck |
| anmUBT | B812F1042C100000 | 06 | 2 | 0x0F65 | 06 | 5 | -- | 0.0236197458 | 0 | 0x00 | 0x00 | 6.2f | V | -- | UBATT | UBT Batteriespannung |
| anmVDF | B812F1042C100000 | 06 | 2 | 0x1F06 | 06 | 5 | -- | 0.001 | 0 | 0x00 | 0x00 | 6.2f | bar | -- | VORFOERDERDRUCK | VDF Vorfoerderdruck |

<a id="table-bits"></a>
### BITS

Dimensions: 39 rows × 9 columns

| TELNAME | TELEGRAMM | NAME | BYTE | MASK | VALUE | LNAME | TEXT_0 | TEXT_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| dimDIGprel | 0F70 | S_BRL | 6 | 0x01 | 0x01 | Eingang Bremslichtschalter | Pedal nicht betaetigt (Masse) | Pedal betaetigt (Ubatt) |
| dimDIGprel | 0F70 | S_BRT | 6 | 0x02 | 0x02 | Eingang Bremslichttestschalter | Pedal nicht betaetigt (Masse) | Pedal betaetigt (Ubatt) |
| dimDIGprel | 0F70 | S_GZS | 6 | 0x10 | 0x10 | Eingang Gluehzeitrelais Diagnose | HIGH (Ubatt) = GLUEHEN EIN wenn System ok | LOW (Masse) = GLUEHEN AUS wenn System ok |
| dimDIGprel | 0F70 | S_KUP | 7 | 0x20 | 0x20 | Eingang Kupplungsschalter | Pedal nicht betaetigt (Masse) | Pedal betaetigt (Ubatt) |
| dimDIGprel | 0F70 | S_ODS | 7 | 0x08 | 0x08 | Eingang Oeldruckschalter | Oeldruck io (Ubatt) | Oeldruck zu niedrig (Masse) |
| comGTR_opt | 1C00 | S_EGS | 9 | 0x01 | 0x01 | Getriebe | Automat | Handschalt |
| mroKickDwn | 1F9A | S_KD | 17 | 0x01 | 0x01 | Kick Down | nicht betaetigt | betaetigt |
| camS_KO | 1FB0 | S_KO | 19 | 0x01 | 0x01 | Schalter Klimakompressor KO (CAN) | nicht betaetigt | betaetigt |
| camS_AC | 1FB1 | S_AC | 21 | 0x01 | 0x01 | Schalter Klimabereitschaft AC (CAN) | nicht betaetigt | betaetigt |
| fbmDIA_C | DF01 | S_DIALA | 13 | 0x01 | 0x01 | Status Diagnoselampe (CAN) | nicht angesteuert | angesteuert |
| dimF_MFL | 2F74 | S_MFLWA | 11 | 0x09 | 0x09 | MFL Bedienteil WA Wiederaufnahme | betaetigt | nicht betaetigt |
| dimF_MFL | 2F74 | S_MFLEINP | 11 | 0x12 | 0x12 | MFL Bedienteil EIN + | betaetigt | nicht betaetigt |
| dimF_MFL | 2F74 | S_MFLAUS | 11 | 0x20 | 0x20 | MFL Bedienteil AUS | betaetigt | nicht betaetigt |
| dimF_MFL | 2F74 | S_MFLEINM | 11 | 0x40 | 0x40 | MFL Bedienteil EIN - | betaetigt | nicht betaetigt |
| dimF_MFL | 2F74 | S_MFLTGL | 11 | 0x80 | 0x80 | MFL Bedienteil Togglebit | Zustand 0 | Zustand 1 |
| mroFGR_ABN | DF08 | S_RFGRKUP | 15 | 0x01 | 0x01 | Reversible FGR Abschaltbedingung | io (Kupplung betaetigt) | durch Kupplung betaetigt |
| mroFGR_ABN | DF08 | S_RFGRVNM | 15 | 0x02 | 0x02 | Reversible FGR Abschaltbedingung | io (Hochdrehen) | durch Hochdrehen |
| mroFGR_ABN | DF08 | S_RFGRBRK | 15 | 0x04 | 0x04 | Reversible FGR Abschaltbedingung | io (Bremse betaetigt) | durch Bremse betaetigt |
| mroFGR_ABN | DF08 | S_RFGRVMN | 15 | 0x08 | 0x08 | Reversible FGR Abschaltbedingung | io (Geschwindigkeit zu klein) | durch Geschwindigkeit zu klein |
| mroFGR_ABN | DF08 | S_RFGRVZG | 15 | 0x10 | 0x10 | Reversible FGR Abschaltbedingung | io (Verzoegerung zu gross) | durch Verzoegerung zu gross |
| mroFGR_ABN | DF08 | S_RFGRUEB | 15 | 0x20 | 0x20 | Reversible FGR Abschaltbedingung | io (Geschwindigkeit zu gross) | durch  Geschwindigkeit zu gross |
| mroFGR_ABN | DF08 | S_RFGRVMR | 15 | 0x40 | 0x40 | Reversible FGR Abschaltbedingung | io (Einschaltgeschwindigkeit zu gering) | Einschaltgeschwindigkeit zu gering |
| mroFGR_ABN | DF08 | S_RFGRMSW | 15 | 0x80 | 0x80 | Reversible FGR Abschaltbedingung | io (Mainswitch) | Mainswitch nicht eingeschaltet |
| mroFGR_ABN | DF08 | S_RFGRGNG | 14 | 0x01 | 0x01 | Reversible FGR Abschaltbedingung | io (kein gueltiger Gang) | kein gueltiger Gang |
| mroFGR_ABN | DF08 | S_RFGRABS | 14 | 0x02 | 0x02 | Reversible FGR Abschaltbedingung | io (Abschaltung aktiv) | Abschaltung aktiv |
| mroFGR_ABN | DF08 | S_IKUP | 14 | 0x10 | 0x10 | Irreversible FGR Abschaltbedingung | io (Fehler Kupplung) | Fehler Kupplung |
| mroFGR_ABN | DF08 | S_IBRE | 14 | 0x20 | 0x20 | Irreversible FGR Abschaltbedingung | io (Fehler Bremse) | Fehler Bremse |
| mroFGR_ABN | DF08 | S_IMFLTGL | 14 | 0x40 | 0x40 | Irreversible FGR Abschaltbedingung | io (Fehler MFL Togglebit) | Fehler MFL Togglebit |
| mroFGR_ABN | DF08 | S_IOPT | 14 | 0x80 | 0x80 | Irreversible FGR Abschaltbedingung | io (FGR nicht variantencodiert) | FGR nicht variantencodiert |
| camS_HZL | E4D1 | S_KLIANF | 23 | 0x01 | 0x01 | Anforderung Heizleistung von Klimasteuergeraet (CAN) | keine angefordert | angefordert |
| khoNOR_AB | 0FB7 | S_KWH_WTF | 25 | 0x01 | 0x01 | Abschaltbedingung Kuehlmittelheizung | io (Wassertemperatur ausreichend) | Wassertemperatur ausreichend |
| khoNOR_AB | 0FB7 | S_KWH_GEN1 | 25 | 0x02 | 0x02 | Abschaltbedingung Kuehlmittelheizung | io (Generatorlastfehler) | Generatorlastfehler |
| khoNOR_AB | 0FB7 | S_KWH_UBATT | 25 | 0x04 | 0x04 | Abschaltbedingung Kuehlmittelheizung | io (Batteriespannung zu niedrig) | Batteriespannung zu niedrig |
| khoNOR_AB | 0FB7 | S_KWH_N | 25 | 0x08 | 0x08 | Abschaltbedingung Kuehlmittelheizung | io (Motordrehzahl zu niedrig) | Motordrehzahl zu niedrig |
| khoNOR_AB | 0FB7 | S_KWH_START | 25 | 0x10 | 0x10 | Abschaltbedingung Kuehlmittelheizung | io (Startverzoegerung aktiv) | Startverzoegerung aktiv |
| khoNOR_AB | 0FB7 | S_KWH_SENSDEF | 25 | 0x20 | 0x20 | Abschaltbedingung Kuehlmittelheizung | io (WTF, UTF oder Endstufe defekt) | WTF, UTF oder Endstufe defekt |
| khoNOR_AB | 0FB7 | S_KWH_IKHA | 25 | 0x80 | 0x80 | Abschaltbedingung Kuehlmittelheizung | io (keine Heizleistungsanforderung von IHKA) | keine Heizleistungsanforderung von IHKA |
| khoNOR_AB | 0FB7 | S_KWH_GENSRC | 24 | 0x08 | 0x08 | Abschaltbedingung Kuehlmittelheizung | io (Generatorlast Null Prozent) | Generatorlast Null Prozent |
| khoNOR_AB | 0FB7 | S_KWH_APPL | 24 | 0x80 | 0x80 | Abschaltbedingung Kuehlmittelheizung | io (Wegappliziert) | Wegappliziert |

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 37 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0X00 | ERROR_ECU_RESERVED_BY_DOCUMENT |
| 0X10 | ERROR_ECU_GENERAL_REJECT |
| 0X11 | ERROR_ECU_SERVICE_NOT_SUPPORTED |
| 0X12 | ERROR_ECU_SUBFUNCTION_NOT_SUPPORTED_INVALID_FORMAT |
| 0X21 | ERROR_ECU_BUSY_REPEAT_REQUEST |
| 0X22 | ERROR_ECU_CONDITIONS_NOT_CORRECT_OR_REQUEST_SEQUENCE_ERROR |
| 0X23 | ERROR_ECU_ROUTINE_NOT_COMPLETE |
| 0X31 | ERROR_ECU_REQUEST_OUT_OF_RANGE |
| 0X33 | ERROR_ECU_SECURITY_ACCESS_DENIED_SECURITY_ACCESS_REQUESTED |
| 0X35 | ERROR_ECU_INVALID_KEY |
| 0X36 | ERROR_ECU_EXCEED_NUMBER_OF_ATTEMPTS |
| 0X37 | ERROR_ECU_REQUIRED_TIME_DELAY_NOT_EXPIRED |
| 0X40 | ERROR_ECU_DOWNLOAD_NOT_ACCEPTED |
| 0X41 | ERROR_ECU_IMPROPER_DOWNLOAD_TYPE |
| 0X42 | ERROR_ECU_CANNOT_DOWNLOAD_TO_SPECIFIED_ADDRESS |
| 0X43 | ERROR_ECU_CANNOT_DOWNLOAD_NUMBER_OF_BYTES_REQUESTED |
| 0X50 | ERROR_ECU_UPLOAD_NOT_ACCEPTED |
| 0X51 | ERROR_ECU_IMPROPER_UPLOAD_TYPE |
| 0X52 | ERROR_ECU_CANNOT_UPLOAD_FROM_SPECIFIED_ADDRESS |
| 0X53 | ERROR_ECU_CANNOT_UPLOAD_NUMBER_OF_BYTES_REQUESTED |
| 0X71 | ERROR_ECU_TRANSFER_SUSPENDED |
| 0X72 | ERROR_ECU_TRANSFER_ABORTED |
| 0X74 | ERROR_ECU_ILLEGAL_ADDRESS_IN_BLOCK_TRANSFER |
| 0X75 | ERROR_ECU_ILLEGAL_BYTE_COUNT_IN_BLOCK_TRANSFER |
| 0X76 | ERROR_ECU_ILLEGAL_BLOCK_TRANSFER_TYPE |
| 0X77 | ERROR_ECU_BLOCKTRANSFER_DATA_CHECKSUM_ERROR |
| 0X78 | ERROR_ECU_REQ_CORRECTLY_RCVD_RSP_PENDING |
| 0X79 | ERROR_ECU_INCORRECT_BYTE_COUNT_DURING_BLOCK_TRANSFER |
| 0X80 | ERROR_ECU_SERVICE_NOT_SUPPORTED_IN_ACTIVE_DIGNOSTICMODE |
| 0XF9 | ERROR_ECU_VEHICLE_MANUFACTURER_SPECIFIC |
| 0XFE | ERROR_ECU_SYSTEM_SUPPLIER_SPECIFIC |
| 0XFF | ERROR_ECU_RESERVED_BY_DOCUMENT |
| ?01? | OKAY |
| ?02? | BUSY |
| ?03? | AIF_NICHT_PROGRAMMIERT |
| ?04? | KEIN AIF MEHR FREI |
| 0xXY | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 58 rows × 6 columns

| ORT | ORTTEXT | UW_1 | UW_2 | UW_3 | UW_4 |
| --- | --- | --- | --- | --- | --- |
| 0x0100 | Luftmassenmesser | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x0105 | Atmosphaerendruckfuehler (im Steuergeraet verbaut) | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x0110 | Lufttemperaturfuehler | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x0115 | Kuehlmitteltemperaturfuehler | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x0120 | Pedalwertgeber | 0x01 | 0x05 | 0x09 | 0x10 |
| 0x0190 | Raildrucksensor | 0x01 | 0x11 | 0x03 | 0x04 |
| 0x0200 | Injektor Zylinder 1 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x0201 | Injektor Zylinder 5 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x0202 | Injektor Zylinder 3 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x0203 | Injektor Zylinder 6 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x0204 | Injektor Zylinder 2 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x0205 | Injektor Zylinder 4 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x0206 | Injektor 41(nicht verwendet) | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x0220 | Pedalwertgeber PGS | 0x01 | 0x05 | 0x08 | 0x10 |
| 0x0235 | Ladedruckfuehler | 0x01 | 0x02 | 0x03 | 0x16 |
| 0x0335 | Drehzahl Kurbelwelle | 0x01 | 0x02 | 0x03 | 0x05 |
| 0x0400 | Abgasrueckfuehr-Regelung oder Abgasrueckfuehrsteller | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x0404 | Abgasrueckfuehr-Regelung | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x0480 | Elektroluefter | 0x01 | 0x02 | 0x05 | 0x12 |
| 0x0500 | Fahrgeschwindigkeitssignal | 0x01 | 0x02 | 0x06 | 0x08 |
| 0x0560 | Referenzspannung intern | 0x01 | 0x02 | 0x05 | 0x04 |
| 0x0600 | Steuergeraet DDE (CAN-Controller) | 0x01 | 0x05 | 0x03 | 0x10 |
| 0x0605 | Steuergeraet DDE (Microcontroller) | 0x01 | 0x14 | 0x03 | 0x05 |
| 0x09F6 | Raildruckueberwachung im Start | 0x01 | 0x11 | 0x03 | 0x04 |
| 0x1190 | Raildruck-Plausibilitaet | 0x01 | 0x11 | 0x03 | 0x04 |
| 0x1195 | Raildruckregelventil | 0x01 | 0x11 | 0x05 | 0x04 |
| 0x1250 | Relais Vorfoerderpumpe | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x1255 | Vorfoerderdruckfuehler | 0x01 | 0x06 | 0x03 | 0x04 |
| 0x1260 | Vorfoerderdruck-Ueberwachung | 0x01 | 0x06 | 0x03 | 0x11 |
| 0x1470 | Ladedruck-Regelung | 0x01 | 0x02 | 0x03 | 0x07 |
| 0x1612 | Diagnoselampe | 0x01 | 0x11 | 0x03 | 0x04 |
| 0x1613 | Laufruheregler | 0x01 | 0x02 | 0x03 | 0x05 |
| 0x1640 | Steuergeraet DDE (EEPROM und Konfiguration) | 0x01 | 0x02 | 0x03 | 0x05 |
| 0x19E6 | Oeldruckkontrollampe | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x1A04 | Kuehlmittelheizung | 0x01 | 0x02 | 0x03 | 0x05 |
| 0x1A0E | Generatorlastsignal | 0x01 | 0x02 | 0x03 | 0x05 |
| 0x1A18 | Umgebungstemperatur | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x1A22 | Drallklappe           | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x1DF5 | Elektronische Wegfahrsperre (EWS) | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x1E00 | CAN-Bus           | 0x01 | 0x05 | 0x03 | 0x10 |
| 0x1E05 | Bedienteil Fahrgeschwindigkeitsregelung | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x1E25 | Ueberwachung Drehzahlgeber | 0x01 | 0x02 | 0x03 | 0x05 |
| 0x1E30 | Ladedruck-Regelung oder Ladedrucksteller | 0x01 | 0x02 | 0x03 | 0x07 |
| 0x1E35 | Fehler im Nachlauf beim Abstellen ueber Off oder Nullmenge | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x1E40 | Analog / Digital Wandler-Testspannung | 0x01 | 0x09 | 0x05 | 0x08 |
| 0x1E45 | Kondensatorspannung 1 fuer Zylinder 1,2,3 | 0x01 | 0x02 | 0x03 | 0x05 |
| 0x1E50 | Kondensatorspannung 2 fuer Zylinder 4,5,6 | 0x01 | 0x02 | 0x03 | 0x05 |
| 0x1E55 | Speisespannung fuer Pedalwertgeber, Ladedruckfuehler, Luftmassenmesser | 0x01 | 0x02 | 0x05 | 0x09 |
| 0x1E60 | Speisespannung fuer Pedalwertgeber, Raildrucksensor, Vorfoerderdruckfuehler | 0x01 | 0x02 | 0x05 | 0x08 |
| 0x2800 | Versorgungsspannung | 0x01 | 0x02 | 0x03 | 0x15 |
| 0x3000 | Bremslicht- / Bremstestschalter | 0x01 | 0x05 | 0x08 | 0x10 |
| 0x3005 | Klemme 15           | 0x01 | 0x02 | 0x06 | 0x05 |
| 0x3010 | Kupplungsschalter | 0x01 | 0x10 | 0x03 | 0x08 |
| 0x3505 | Gluehanlage           | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x3510 | DDE-Hauptrelais | 0x01 | 0x02 | 0x05 | 0x04 |
| 0x3515 | Klimaleistungsausgang | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x3520 | Motorlagersteuerung | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x0000 | unbekannter Fehlerort | 0x00 | 0x00 | 0x00 | 0x00 |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 57 rows × 33 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 | A6_0 | A6_1 | A7_0 | A7_1 | A8_0 | A8_1 | A9_0 | A9_1 | A10_0 | A10_1 | A11_0 | A11_1 | A12_0 | A12_1 | A13_0 | A13_1 | A14_0 | A14_1 | A15_0 | A15_1 | A16_0 | A16_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x0100 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x3 | 0x00 | 0x2 | 0x00 | 0x42 | 0x00 | 0x1 | 0x00 | 0x3F | 0x00 | 0x3C | 0x00 | 0x00 | 0x00 | 0x20 |
| 0x0105 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x3F | 0x00 | 0x3C | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x0110 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x3D | 0x00 | 0x3E | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x0115 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x3D | 0x00 | 0x3E | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x0120 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x3C | 0x00 | 0x42 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x0190 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x1C | 0x00 | 0x47 | 0x00 | 0x42 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x0200 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x44 | 0x00 | 0x00 | 0x00 | 0x43 | 0x00 | 0x1D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x39 | 0x00 | 0x00 |
| 0x0201 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x44 | 0x00 | 0x00 | 0x00 | 0x43 | 0x00 | 0x1D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x39 | 0x00 | 0x00 |
| 0x0202 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x44 | 0x00 | 0x00 | 0x00 | 0x43 | 0x00 | 0x1D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x39 | 0x00 | 0x00 |
| 0x0203 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x44 | 0x00 | 0x00 | 0x00 | 0x43 | 0x00 | 0x1D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x39 | 0x00 | 0x00 |
| 0x0204 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x44 | 0x00 | 0x00 | 0x00 | 0x43 | 0x00 | 0x1D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x39 | 0x00 | 0x00 |
| 0x0205 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x44 | 0x00 | 0x00 | 0x00 | 0x43 | 0x00 | 0x1D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x39 | 0x00 | 0x00 |
| 0x0206 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x44 | 0x00 | 0x00 | 0x00 | 0x43 | 0x00 | 0x1D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x39 | 0x00 | 0x00 |
| 0x0220 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x1B | 0x00 | 0x42 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x30 |
| 0x0235 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x3F | 0x00 | 0x3C | 0x00 | 0x42 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x2D |
| 0x0335 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x27 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x0400 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x5 | 0x00 | 0x6 | 0x00 | 0x32 | 0x00 | 0x29 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x0404 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x29 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x0480 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x52 | 0x00 | 0x53 | 0x00 | 0x5 | 0x00 | 0x6 | 0x00 | 0x00 | 0x00 | 0x54 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x0500 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x00 | 0x00 | 0x3B | 0x00 | 0x00 | 0x00 | 0x50 | 0x00 | 0x00 | 0x00 | 0x2E |
| 0x0560 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x49 | 0x00 | 0x2B | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x0600 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0xA | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x0605 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x34 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x55 | 0x00 | 0x35 | 0x00 | 0x13 | 0x00 | 0x25 | 0x00 | 0x00 |
| 0x09F6 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x5E | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1190 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x22 | 0x00 | 0x26 | 0x00 | 0x00 | 0x00 | 0x33 | 0x00 | 0x1E | 0x00 | 0x36 | 0x00 | 0x00 | 0x00 | 0x5D |
| 0x1195 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x1B | 0x00 | 0x48 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF |
| 0x1250 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x1B | 0x00 | 0x48 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1255 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x1C | 0x00 | 0x47 | 0x00 | 0x42 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1260 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x24 | 0x00 | 0x00 | 0x00 | 0x4D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1470 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x28 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1612 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x58 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1613 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x51 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1640 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x4 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x19 | 0x00 | 0x17 | 0x00 | 0x23 | 0x00 | 0x00 |
| 0x19E6 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x1B | 0x00 | 0x48 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1A04 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x59 | 0x00 | 0x5A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x5B | 0x00 | 0x1B | 0x00 | 0x48 |
| 0x1A0E | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x14 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x14 | 0x00 | 0x00 |
| 0x1A18 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x12 | 0x00 | 0x00 |
| 0x1A22 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x1B | 0x00 | 0x48 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1DF5 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x21 | 0x00 | 0x46 | 0x00 | 0x45 | 0x00 | 0x4A | 0x00 | 0x4E | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1E00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0xC | 0x00 | 0xB | 0x00 | 0xE | 0x00 | 0xD | 0x00 | 0x56 | 0x00 | 0x57 | 0x00 | 0x9 | 0x00 | 0x00 |
| 0x1E05 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x18 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1E25 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x2A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x7 | 0x00 | 0x1A | 0x00 | 0x8 | 0x00 | 0x00 |
| 0x1E30 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x5 | 0x00 | 0x6 | 0x00 | 0x31 | 0x00 | 0x28 | 0x00 | 0x5C | 0x00 | 0x00 |
| 0x1E35 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x11 | 0x00 | 0x10 |
| 0x1E40 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x48 | 0x00 | 0x1B | 0x00 | 0x00 | 0x00 | 0x1F | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1E45 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x40 | 0x00 | 0x41 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1E50 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x40 | 0x00 | 0x41 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1E55 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x48 | 0x00 | 0x1B | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1E60 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x48 | 0x00 | 0x1B | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x2800 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x4C | 0x00 | 0x4B | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x3000 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x2C |
| 0x3005 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x4F |
| 0x3010 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x2F |
| 0x3505 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x5 | 0x00 | 0x6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x16 |
| 0x3510 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x37 | 0x00 | 0x38 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x3515 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x1B | 0x00 | 0x48 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x3520 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0xF1 | 0xF2 | 0xF3 | 0xF4 | 0xF5 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3C | 0x00 | 0x3F | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 108 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x1 | Abgleichfehler Lastabgleich |
| 0x2 | Abgleichfehler Leerlaufabgleich |
| 0x3 | Abgleichfehler Nullpunktabgleich |
| 0x4 | Allgemeine Abgleiche Checksumme |
| 0x5 | Ansteuerung Kurzschluss nach B+ |
| 0x6 | Ansteuerung Unterbrechung oder Kurzschluss nach B- |
| 0x7 | Ausfall Drehzahlgebersignal Kurbelwelle |
| 0x8 | Ausfall Nockenwellengebersignal |
| 0x9 | CAN-Bus abgeschaltet |
| 0xA | CAN-Bus Baustein defekt |
| 0xB | Empfangsfehler ASC |
| 0xC | Empfangsfehler Elektronische Getriebesteuerung (EGS) |
| 0xD | Empfangsfehler Kombi-Instrument (INSTR2) |
| 0xE | Empfangsfehler Kombi-Instrument (INSTR3) |
| 0xF | Endstufenfehler |
| 0x10 | Fehler beim Abstellen ueber Injektor Endstufe (OFF) |
| 0x11 | Fehler beim Abstellen ueber Nullmenge |
| 0x12 | Fehlererkennung |
| 0x13 | Gate-Array Mengenstop |
| 0x14 | Generatorlast 0% |
| 0x15 | Geschwindigkeit zu gross |
| 0x16 | Gluehsystem - Gluehkerzen oder Gluehrelais |
| 0x17 | Injektorabgleich Checksumme |
| 0x18 | kein Signal vom Multifunktionslenkrad |
| 0x19 | Kommunikation mit EEPROM |
| 0x1A | Kurbelwellengebersignal dynamisch unplausibel |
| 0x1B | Kurzschluss nach B+ |
| 0x1C | Kurzschluss nach B- |
| 0x1D | Lastabfall |
| 0x1E | Leckage |
| 0x1F | Leerlauf-Testimpuls-Fehler |
| 0x20 | Luftmasse zu gering |
| 0x21 | Manipulationsversuch |
| 0x22 | Maximaldruck ueberschritten |
| 0x23 | Mengendriftkompensation Checksumme |
| 0x24 | Mengenreduktion wegen geringem Vorfoerderdruck |
| 0x25 | Microcontroller (Gate-Array Kommunikation) |
| 0x26 | Minimaldruck ueber Motordrehzahl zu klein |
| 0x27 | Motor hat ueberdreht |
| 0x28 | Negative Regelabweichung / Ladedruck zu hoch |
| 0x29 | Negative Regelabweichung / Luftmasse zu hoch |
| 0x2A | Nockenwellengebersignal Frequenz zu hoch |
| 0x2B | obere Referenzspannungsgrenze ueberschritten |
| 0x2C | Plausibilitaet der Bremssignale im Fahrbetrieb |
| 0x2D | Plausibilitaet mit Atmosphaerendruckfuehler bei Leerlauf |
| 0x2E | Plausibilitaet mit Einspritzmenge und Motordrehzahl |
| 0x2F | Plausibilitaet mit Fahrgeschwindigkeit |
| 0x30 | Plausibilitaet zwischen Poti 1 und 2 verletzt |
| 0x31 | Positive Regelabweichung / Ladedruck zu niedrig |
| 0x32 | Positive Regelabweichung / Luftmasse zu niedrig |
| 0x33 | Raildruckregelventil klemmt |
| 0x34 | Recovery aufgetreten |
| 0x35 | redundante Schubueberwachung |
| 0x36 | Regelabweichung ueber Motordrehzahl zu gross |
| 0x37 | Relais schaltet zu frueh ab |
| 0x38 | Relais schaltet zu spaet ab |
| 0x39 | Schnell-Loeschfehler |
| 0x3A | Signal dynamisch unplausibel |
| 0x3B | Signal fehlerhaft |
| 0x3C | Signal Kurzschluss nach B+ |
| 0x3D | Signal Kurzschluss nach B- |
| 0x3E | Signal Unterbrechung oder Kurzschluss nach B+ |
| 0x3F | Signal Unterbrechung oder Kurzschluss nach B- |
| 0x40 | Spannung zu hoch |
| 0x41 | Spannung zu niedrig |
| 0x42 | Speisespannungsfehler |
| 0x43 | Strom an High Side zu gross |
| 0x44 | Strom an Low Side zu gross |
| 0x45 | Timeout abgelaufen |
| 0x46 | Uebertragungsfehler |
| 0x47 | Unterbrechung oder Kurzschluss nach B+ |
| 0x48 | Unterbrechung oder Kurzschluss nach B- |
| 0x49 | untere Referenzspannungsgrenze unterschritten |
| 0x4A | Urcode (UC) im EEPROM defekt |
| 0x4B | Versorgungsspannung DDE ueberschritten |
| 0x4C | Versorgungsspannung DDE unterschritten |
| 0x4D | Vorfoerderdruck unter Mindestwert fuer Motorstart |
| 0x4E | Wechselcode (WC) im EEPROM defekt |
| 0x4F | Zuendstellung 2 Plausibilitaet nach Steuergeraet-Initialisierung |
| 0x50 | Fahrgeschwindigkeit von CAN ungueltig |
| 0x51 | Korrekturmenge zu gross |
| 0x52 | Blockiererkennung |
| 0x53 | Blockiererkennung2 |
| 0x54 | Blockiererkennung3 |
| 0x55 | ASCET Bypass Schnittstellenfehler |
| 0x56 | Empfangsfehler Untersetzungsgetriebe (TXU1) |
| 0x57 | Empfangsfehler ASC3 |
| 0x58 | Ansteuerung wegen Fehler Raildruck-Plausibilitaet |
| 0x59 | Uebertemperaturerkennung |
| 0x5A | Uebertemperaturerkennung2 |
| 0x5B | Uebertemperaturerkennung3 |
| 0x5C | Abgefallener Ladeluftschlauch |
| 0x5D | Raildruckueberhoehung |
| 0x5E | Kein Raildruckaufbau |
| 0xEB | Fehler momentan nicht vorhanden |
| 0xEC | Fehler momentan vorhanden |
| 0xED | -- |
| 0xEE | sporadischer Fehler |
| 0xEF | -- |
| 0xF0 | -- |
| 0xF1 | -- |
| 0xF2 | -- |
| 0xF3 | -- |
| 0xF4 | -- |
| 0xF5 | -- |
| 0xF6 | -- |
| 0xFF | unbekannte Fehlerart |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 18 rows × 5 columns

| UWNR | UWTEXT | UW_EINH | UWF_A | UWF_B |
| --- | --- | --- | --- | --- |
| 0x00 | -- | ---- | 1 | 0 |
| 0x01 | Motordrehzahl | 1/min | 24,975025 | 0,0 |
| 0x02 | Kuehlmitteltemperatur | Grad C | 0,6826871 | -41,0264009 |
| 0x03 | Einspritzmenge | mm^3 | 0,5120328 | 0,0 |
| 0x04 | Raildruck | bar | 6,0240963855 | 0,0 |
| 0x05 | Versorgungsspannung | V | 0,1157263393 | 0,0 |
| 0x06 | Lufttemperatur | Grad C | 0,6826871 | -41,0264009 |
| 0x07 | Ladedruck | mbar | 16,0 | 0,0 |
| 0x08 | Position Pedalwertgeber1 | % | 0,3938558 | 0,0 |
| 0x09 | Position Pedalwertgeber2 | % | 0,3938558 | 0,0 |
| 0x10 | Fahrgeschwindigkeit | km/h | 1,0235415 | 0,0 |
| 0x11 | Kraftstoffvorfoerderdruck | bar | 0,016 | 0,0 |
| 0x12 | Tastverhaeltnis Elektroluefteransteuerung | % | 0,3938558 | 0,0 |
| 0x13 | aktueller km-Stand | km | 10,0 | 0,0 |
| 0x14 | Restart-Code | - | 1,0 | 0,0 |
| 0x15 | Versorgungsspannung | V | 0,0967467 | 0,0 |
| 0x16 | Atmosphaerendruck | mbar | 16,0 | 0,0 |
| 0x17 | unbekannte Umweltbedingung | ---- | 1 | 0 |
