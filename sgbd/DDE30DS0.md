# DDE30DS0.prg

- Jobs: [177](#jobs)
- Tables: [9](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | DDE 3.0 fuer M47 |
| ORIGIN | BMW TI-433 Schiefer |
| REVISION | 1.36 |
| AUTHOR | BMW TP-421 Weber, BMW TI-433 Schiefer, ZM-E-31 Lexmueller, BMW TI-433 Schaller |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [EDIC_RESET](#job-edic-reset) - EDIC-Reset
- [initialisierung](#job-initialisierung) - Default Init-Job
- [INFO](#job-info) - Information SGBD
- [IDENT](#job-ident) - Ident-Daten fuer DME
- [EEPROM_LESEN](#job-eeprom-lesen) - Beliebige EPROM - Zellen auslesen
- [SEED_KEY](#job-seed-key) - Schutzmechanismus SEED_KEY
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender-Info-Feldes
- [IDENT_AIF](#job-ident-aif) - Ident und AIF zusammen lesen
- [CODIER_VARIANTE_LESEN](#job-codier-variante-lesen) - Auslesen des Varianten - Steuerwort
- [STATUS_CODIER_CHECKSUMME](#job-status-codier-checksumme) - Codier - Checksumme abfragen
- [FS_QUICK_LESEN](#job-fs-quick-lesen) - Auslesen des QUICK Fehlerspeichers
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [FS_SHADOW_LESEN](#job-fs-shadow-lesen) - Auslesen des Fehlerspeichers
- [STATUS_MW2](#job-status-mw2) - Messwerte (einzelne RAM - Zellen) auslesen
- [STATUS_MW3](#job-status-mw3) - Messwerte (einzelne RAM - Zellen) auslesen
- [STATUS_MW4](#job-status-mw4) - Messwerte (einzelne RAM - Zellen) auslesen
- [STATUS_MW5](#job-status-mw5) - Messwerte (einzelne RAM - Zellen) auslesen
- [STATUS_DIGITAL](#job-status-digital) - Status Schalteingaenge
- [STATUS_DIGITAL1](#job-status-digital1) - Status Schalteingaenge
- [STATUS_DIGITAL2](#job-status-digital2) - Status Schalteingaenge
- [STATUS_DIGITAL4](#job-status-digital4) - Status Schalteingaenge
- [STEUERN_CHECK_ZUHEIZER](#job-steuern-check-zuheizer)
- [STEUERN_CHECK_ZUHEIZER_ECOS](#job-steuern-check-zuheizer-ecos)
- [STEUERN_ABLUFTKLAPPE](#job-steuern-abluftklappe) - Abluftklappe ansteuern ,  0 oder 100%
- [STEUERN_AGR_STELLER](#job-steuern-agr-steller) - ARF - Steller  ansteuern ,  5-95%
- [STEUERN_GLUEHRELAIS](#job-steuern-gluehrelais) - Gluegrelais ansteuern ,  0 oder 100%
- [STEUERN_LADEDRUCKSTELLER](#job-steuern-ladedrucksteller) - Ladedrucksteller ansteuern ,  5-95%
- [STEUERN_E_LUEFTER](#job-steuern-e-luefter) - E-Luefter ansteuern ,  5-95%
- [STEUERN_KLIMAKOMPRESSOR](#job-steuern-klimakompressor) - ARF-Steller ansteuern ,  0 oder 100%
- [STEUERN_EKP](#job-steuern-ekp) - ARF-Steller ansteuern ,  0 oder 100%
- [STEUERN_SPRITZVERSTELLER](#job-steuern-spritzversteller) - ARF-Steller ansteuern ,  -12.5 Grad KW bis 51,25 Grad KW
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Loeschen des Fehlerspeichers
- [DIAGNOSE_ERHALTEN](#job-diagnose-erhalten) - Diagnose erhalten
- [ABGLEICH_LESEN_STARTMENGE](#job-abgleich-lesen-startmenge) - Startmengen-Abgleich lesen
- [ABGLEICH_VERSTELLEN_STARTMENGE](#job-abgleich-verstellen-startmenge) - Startmenge Abgleich verstellen
- [ABGLEICH_PROG_STARTMENGE](#job-abgleich-prog-startmenge) - Startmenge Abgleich programmieren
- [ABGLEICH_LESEN_BEGR_MENGE](#job-abgleich-lesen-begr-menge) - BEGR_MENGEn-Abgleich lesen
- [ABGLEICH_VERSTELLEN_BEGR_MENGE](#job-abgleich-verstellen-begr-menge) - BEGR_MENGE Abgleich verstellen
- [ABGLEICH_PROG_BEGR_MENGE](#job-abgleich-prog-begr-menge) - BEGR_MENGE Abgleich programmieren
- [ABGLEICH_LESEN_BEGR_MENGE_ROH](#job-abgleich-lesen-begr-menge-roh) - BEGR_MENGEn-Abgleich lesen (Rohwert)
- [ABGLEICH_VERSTELLEN_BEGR_MENGE_ROH](#job-abgleich-verstellen-begr-menge-roh) - BEGR_MENGE Abgleich verstellen (Rohwert)
- [ABGLEICH_LESEN_LL_REGELUNG](#job-abgleich-lesen-ll-regelung) - LL-Regelung-Abgleich lesen
- [ABGLEICH_VERSTELLEN_LL_REGELUNG](#job-abgleich-verstellen-ll-regelung) - LL_REGELUNG Abgleich verstellen
- [ABGLEICH_PROG_LL_REGELUNG](#job-abgleich-prog-ll-regelung) - LL_REGELUNG Abgleich programmieren
- [ABGLEICH_LESEN_AGR_RUECK](#job-abgleich-lesen-agr-rueck) - AGR_RUECKn-Abgleich lesen
- [ABGLEICH_VERSTELLEN_AGR_RUECK](#job-abgleich-verstellen-agr-rueck) - AGR_RUECK Abgleich verstellen
- [ABGLEICH_PROG_AGR_RUECK](#job-abgleich-prog-agr-rueck) - AGR_RUECK Abgleich programmieren
- [ABGLEICH_LESEN_LADEDRUCK](#job-abgleich-lesen-ladedruck) - LADEDRUCK-Abgleich lesen
- [ABGLEICH_VERSTELLEN_LADEDRUCK](#job-abgleich-verstellen-ladedruck) - LADEDRUCK Abgleich verstellen
- [ABGLEICH_PROG_LADEDRUCK](#job-abgleich-prog-ladedruck) - LADEDRUCK Abgleich programmieren
- [ABGLEICH_LESEN_ABGLEICHMENGE](#job-abgleich-lesen-abgleichmenge) - LADEDRUCK-Abgleich lesen
- [ABGLEICH_VERSTELLEN_ABGLEICHMENGE](#job-abgleich-verstellen-abgleichmenge) - LADEDRUCK Abgleich verstellen
- [ABGLEICH_PROG_ABGLEICHMENGE](#job-abgleich-prog-abgleichmenge) - LADEDRUCK Abgleich programmieren
- [ABGLEICHWERTE_LESEN](#job-abgleichwerte-lesen) - Lesen der Motorabgleichwerte
- [ABGLEICHWERTE_SCHREIBEN](#job-abgleichwerte-schreiben) - Beschreiben des internen Speichers mit den motorspezifischen Abgleichdaten
- [ABGLEICHFLAG_SCHREIBEN](#job-abgleichflag-schreiben) - Beschreiben des internen Speichers mit den motorspezifischen Abgleichdaten
- [ABGLEICHFLAG_LESEN](#job-abgleichflag-lesen) - Lesen des EEPROM-Speichers ab Adresse 0x0032
- [ABGLEICH_LESEN_FGR_VERBAUT](#job-abgleich-lesen-fgr-verbaut) - FGR-Abgleich lesen
- [ABGLEICH_VERSTELLEN_FGR_VERBAUT](#job-abgleich-verstellen-fgr-verbaut) - FGR-Funktion und Mainswitch konfigurieren
- [ABGLEICH_PROG_FGR](#job-abgleich-prog-fgr) - LADEDRUCK Abgleich programmieren
- [ABGLEICH_LESEN_KENNUNG_KLIMAANLAGE](#job-abgleich-lesen-kennung-klimaanlage) - Kennung Klimaanlage lesen: 1 = Kliamaanlage vorhanden,  0 = Klimaanlage nicht vorhanden 0xff = Fehler
- [ABGLEICH_VERSTELLEN_KENNUNG_KLIMAANLAGE](#job-abgleich-verstellen-kennung-klimaanlage) - Kennung Klimaanlage verstellen, 0 = nicht verbaut, 1 = verbaut
- [ABGLEICH_PROG_KENNUNG_KLIMAANLAGE](#job-abgleich-prog-kennung-klimaanlage) - Kennung Klimaanlage programmieren
- [ABGLEICH_LESEN_MENGENDRIFT](#job-abgleich-lesen-mengendrift) - Mengendrift-Abgleich lesen
- [ABGLEICH_VERSTELLEN_MENGENDRIFT](#job-abgleich-verstellen-mengendrift) - Mengendrift Abgleich verstellen
- [ABGLEICH_PROG_MENGENDRIFT](#job-abgleich-prog-mengendrift) - LADEDRUCK Abgleich programmieren
- [ABGLEICH_KIC_VERSTELLEN_PROGRAMMIEREN](#job-abgleich-kic-verstellen-programmieren) - FGR-Funktion und Mainswitch konfigurieren
- [ABGLEICH_TIMER_VERSTELLEN_PROGRAMMIEREN](#job-abgleich-timer-verstellen-programmieren) - FGR-Funktion und Mainswitch konfigurieren
- [ABGLEICH_LESEN_PUMPENABGLEICH_FLAG](#job-abgleich-lesen-pumpenabgleich-flag) - Kennung M_ABGLEICH_FLAG lesen
- [ABGLEICH_VERSTELLEN_PUMPENABGLEICH_FLAG](#job-abgleich-verstellen-pumpenabgleich-flag) - Kennung M_ABGLEICH_FLAG verstellen, 0 = nicht verbaut, 0xff = verbaut
- [ABGLEICH_PROG_PUMPENABGLEICH_FLAG](#job-abgleich-prog-pumpenabgleich-flag) - Kennung M_ABGLEICH_FLAG programmieren
- [STEUERN_SYNC_MODE](#job-steuern-sync-mode)
- [STATUS_SYNC_MODE](#job-status-sync-mode)
- [HOLE_EMA_FELD](#job-hole-ema-feld)
- [STATUS_PHI_SV_IST](#job-status-phi-sv-ist) - Spritzverstellerwinkel Pumpe
- [STATUS_TV_SV](#job-status-tv-sv) - Tastverhaeltnis Spritzversteller Pumpe
- [STATUS_T_MV_ON](#job-status-t-mv-on) - Einschaltzeitpunkt fuer Mengenmagnetventil
- [STATUS_T_MV_OFF](#job-status-t-mv-off) - Ausschaltzeitpunkt fuer Mengenmagnetventil
- [STATUS_SV_SOLL](#job-status-sv-soll) - Spritzversteller - Sollwinkel
- [STATUS_AE_IWZ](#job-status-ae-iwz) - Ansteuerende
- [STATUS_AB_IWZ](#job-status-ab-iwz) - Ansteuerbeginn
- [STATUS_ME_SOLL](#job-status-me-soll) - Sollmenge - Eingang aus MSG
- [STATUS_FB_SOLL](#job-status-fb-soll) - Foerderbeginn Nockenwellen-Sollwinkel
- [STATUS_D_AD_TK_N](#job-status-d-ad-tk-n) - Dyn. TKR-Kompensation
- [STATUS_D_AD_NW_N](#job-status-d-ad-nw-n) - Dyn. Ansteuerdauerkorrektur
- [STATUS_ATMOSPHAERENDRUCK](#job-status-atmosphaerendruck) - ADF Atmosphaerendruck ANMADF
- [STATUS_LADEDRUCK](#job-status-ladedruck) - LDF Lade- / Saugrohr-Druck ANMLDF
- [STATUS_LMM_MASSE](#job-status-lmm-masse) - LMM  Analogwert Luftmassenmesser HFM ANMLMM
- [STATUS_PWG_FAHRERWUNSCH_UNGEF](#job-status-pwg-fahrerwunsch-ungef) - PWG Pedalwertgeber  - Position (ungefiltert) ANMPWG
- [STATUS_PWG_WINKEL](#job-status-pwg-winkel)
- [STATUS_UBATT](#job-status-ubatt) - UBT Batteriespannung ANMUBATT
- [STATUS_UREF](#job-status-uref) - URF Referenzspannung ANMU_REF
- [STATUS_MOTORTEMPERATUR](#job-status-motortemperatur) - WTF Wassertemperatur ANMWTF
- [STATUS_PWG_FAHRERWUNSCH_V](#job-status-pwg-fahrerwunsch-v) - PWG Rohwert Pedalwertgeber ANOU_PWG
- [STATUS_LAST](#job-status-last) - M_L aktuelle Luftmasse ARMM_LIST
- [STATUS_ARF_SOLLWERT](#job-status-arf-sollwert) - M_L Sollwert fuer ARF-Regelung ARMM_LSOLL
- [STATUS_DIMDIGPREL_LOW](#job-status-dimdigprel-low) - Entprellte logische Zustaende d. digit. Eingaenge DIMDIGPREL_L
- [STATUS_DIMDIGPREL_HIGH](#job-status-dimdigprel-high) - Entprellte logische Zustaende d. digit. Eingaenge high DIMDIGPREL_H
- [STATUS_MOTORDREHZAHL](#job-status-motordrehzahl) - N Drehzahl (einfach gemittelt) DZMNMIT
- [STATUS_ABLUFTKLAPPE_TV](#job-status-abluftklappe-tv) - TV Ansteuerung Abluftlappensteuerung EHMFAKS
- [STATUS_ARF_STELLER_TV](#job-status-arf-steller-tv) - TV Ansteuerung ARF-Steller EHMFARS
- [STATUS_LADEDRUCKSTELLER_TV](#job-status-ladedrucksteller-tv) - TV Ansteuerung Ladedrucksteller EHMFLD_DK
- [STATUS_E_LUEFTER_TV](#job-status-e-luefter-tv) - TV Ansteuerung El.Motorluefter EHMFMLS
- [STATUS_V_ZU_N](#job-status-v-zu-n) - V/N aktuelles Verhaeltnis Geschwindigkeit/Drehzahl FGM_VZUN
- [STATUS_BESCHLEUNIGUNG](#job-status-beschleunigung) - Beschleunigung FGMBESCH
- [STATUS_GESCHWINDIGKEIT](#job-status-geschwindigkeit) - V aktuelle Geschwindigkeit FGMFGAKT
- [STATUS_MSR_EINGRIFF](#job-status-msr-eingriff) - M_E externer Momenteneingriff MSR MRMM_EXMSR
- [STATUS_EINSPRITZMENGE](#job-status-einspritzmenge) - M_E Aktuelle Einspritzmenge (ohne ARD) MRMM_EAKT
- [STATUS_BEGRENZUNGSMENGE](#job-status-begrenzungsmenge) - M_E resultierende Begrenzungsmenge MRMM_EBEGR
- [STATUS_WUNSCHMENGE_FGR](#job-status-wunschmenge-fgr) - M_E Wunschmenge aus FGR MRMM_EFGR
- [STATUS_EINSPRITZMENGE_LLR](#job-status-einspritzmenge-llr) - M_E Menge aus Leerlaufreglung MRMM_ELLR
- [STATUS_EINSPRITZMENGE_ARD](#job-status-einspritzmenge-ard) - M_E Einspritzmenge nach ARD MRMM_EMOT
- [STATUS_WUNSCHMENGE_PWG](#job-status-wunschmenge-pwg) - M_E Wunschmenge = f(PWG) aus Fahrverhaltenkennfeld MRMM_EPWG
- [STATUS_STARTMENGE_SOLLWERT](#job-status-startmenge-sollwert) - M_E resultierender Startmengen-Sollwert MRMM_ESTAR
- [STATUS_FAHRERWUNSCHMENGE_N_EX_EINGRIFF](#job-status-fahrerwunschmenge-n-ex-eingriff) - M_E Fahrerwunschmenge nach externem Mengeneingriff MRMM_EWUN
- [STATUS_FAHRERWUNSCHMENGE_PWG_FGR](#job-status-fahrerwunschmenge-pwg-fgr) - M_E Fahrerwunschmenge aus PWG oder FGR MRMM_EWUNF
- [STATUS_MOTORDREHZAHL_SOLL](#job-status-motordrehzahl-soll) - N Leerlaufsolldrehzahl MRMN_LLBAS
- [STATUS_PWG_FAHRERWUNSCH](#job-status-pwg-fahrerwunsch) - PWG gefilterte Pedalwertgeber-Position MRMPWGFI
- [STATUS_PWG_POTI_SPANNUNG](#job-status-pwg-poti-spannung)
- [STATUS_GESCHWINDIGKEIT_SOLLWERT](#job-status-geschwindigkeit-sollwert) - V Sollwert Fahrgeschwindigkeit fuer Diagnose MRMFG_SOLL
- [STATUS_MOTORDREHZAHL_SEK](#job-status-motordrehzahl-sek) - N Drehzahl aus Sekundaergeber DZMN_SEK
- [STATUS_LADEDRUCK_KORR](#job-status-ladedruck-korr) - P_L T_L-abhaengig korregierter Ladedruck ARMPKORR
- [STATUS_LADEDRUCK_SOLLWERT](#job-status-ladedruck-sollwert) - P_L Sollwert fuer Ladedruck LDMP_LSOLL
- [STATUS_SB_SOLLWERT](#job-status-sb-sollwert) - SB Spritzbeginn-Sollwert SBMPHISOLL
- [STATUS_SB_ISTWERT](#job-status-sb-istwert) - SB Spritzbeginn-Istwert SBMPHIIST
- [STATUS_WTF_SGR](#job-status-wtf-sgr) - T_W Wassertemperatur fuer SBR SBMWTF
- [STATUS_FB_KW_SW](#job-status-fb-kw-sw) - FB-KW-Sollwinkel FNMFBKWSW
- [STATUS_FB_NW_SW](#job-status-fb-nw-sw) - FB-NW-Sollwinkel FNMFBNWSW
- [STATUS_PI_REGLER](#job-status-pi-regler) - SBR: PI-Regler-Ausgangswert SBONAPI
- [STATUS_SIGNAL_NBF](#job-status-signal-nbf) - U_NBF Spannungssignal aus NBF ANMST_NBF
- [STATUS_STARTMENGEN_AGL](#job-status-startmengen-agl) - M_E Abgleichwert fuer Startmengenkorrektur MRMSTA_AGL
- [STATUS_BEGRENZUNGSMENGE_AGL_FAKTOR](#job-status-begrenzungsmenge-agl-faktor) - F_ME Abgleichfaktor fuer Begrenzungsmenge MRMBEG_AGL
- [STATUS_UMSCH_BEG_K](#job-status-umsch-beg-k) - Ext. Umschaltung auf Begrenzungs-Kl. MRMBM_EAKT
- [STATUS_PUMPENMENGE_UNKOR](#job-status-pumpenmenge-unkor) - Pumpenmenge unkorregiert MRMM_EFAHR
- [STATUS_DUESENMENGE_KOR](#job-status-duesenmenge-kor) - Duesenkorrekturmenge MRMM_EKORR
- [STATUS_SOLLMENGE_VOR_UEB](#job-status-sollmenge-vor-ueb) - M_E Soll-Menge vor Ueberwachung MRMM_EPUMP
- [STATUS_SOLLMENGE_AN_PSG](#job-status-sollmenge-an-psg) - M_E Soll-Menge an PSG MRMM_ESOLL
- [STATUS_ME_KOR_ABW](#job-status-me-kor-abw) - Mengenkorrekturkennfeld.Abweichung MRMMK_KL
- [STATUS_DREHZAHLANHEBUNG_KO](#job-status-drehzahlanhebung-ko) - Anhebung der Leerlaufdrehzahl bei Klimakompressor ein KLMN_LLKLM
- [STATUS_DREHZAHL_PSG](#job-status-drehzahl-psg) - Drehzahl NW-bezogen (PSG-Drehzahl) PKMDZNW
- [STATUS_TEMPERATUR_PUMPE](#job-status-temperatur-pumpe) - Pumpentemperatur PKMT_PUMP
- [STATUS_PSG_STATUSWORT](#job-status-psg-statuswort) - PSG Statuswort PKMPSGSTA
- [STATUS_PSG_SELBSTTEST](#job-status-psg-selbsttest) - PSG Selbsttestergebnis PKMPSG_ST
- [STATUS_ANSTEUERDAUER_MV](#job-status-ansteuerdauer-mv) - Ansteuerdauer MV-Endstufe PKMADAUER
- [STATUS_TIMEOUT_CAN](#job-status-timeout-can) - n-Timeoutzaehler fuer Senden CAN zeitsync. PKMTOCNT
- [STATUS_KD_ANT_1](#job-status-kd-ant-1) - Kundendienst-Antwort 1 PKMKDANT_1
- [STATUS_KD_ANT_2](#job-status-kd-ant-2) - Kundendienst-Antwort 2 PKMKDANT_2
- [STATUS_KD_ANT_3](#job-status-kd-ant-3) - Kundendienst-Antwort 3 PKMKDANT_3
- [STATUS_KD_ANT_4](#job-status-kd-ant-4) - Kundendienst-Antwort 4 PKMKDANT_4
- [STATUS_ANST_GLUEHREL_TV](#job-status-anst-gluehrel-tv) - TV Ansteuerung Gluehrelaissteller EHMFGRS
- [STATUS_ANST_VOR_PUMPE_TV](#job-status-anst-vor-pumpe-tv) - TV Ansteuerung - Vorfoerderpumpe EHMFVFP
- [STATUS_ANST_GLUEHANZ_TV](#job-status-anst-gluehanz-tv) - TV Anteuerung Gluehanzeige EHMFGAZ
- [STATUS_ANST_DIG_LAMPE_TV](#job-status-anst-dig-lampe-tv) - TV Ansteuerung Diagnoselampe EHMFDIA
- [STATUS_ANST_KO_TV](#job-status-anst-ko-tv) - TV Ansteuerung Klimakompressor EHMFSKOREL
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [STATUS_PWG_ANSCHLAG_MAX](#job-status-pwg-anschlag-max) - Auslesen des oberen Gaspedalanschlags
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [STATUS_REIBMENGE_N_KL_L_KOMP](#job-status-reibmenge-n-kl-l-komp) - Reibmenge nach Klimalastmomentkompensation MROM_ERBK
- [STEUERN_TESTPLATZ](#job-steuern-testplatz) - Freischaltung fuer SG-Befundung ansteuern
- [ECU_CONFIG](#job-ecu-config) - Ident-Daten fuer DME
- [STATUS_BETR_STUNDENZAEHLER](#job-status-betr-stundenzaehler) - UB akt. Betriebsstundenzaehler FBMBSTZ_UB
- [MWBLOCK_ROH](#job-mwblock-roh) - Messwerteblock roh ausgeben
- [MW_SELECT_LESEN](#job-mw-select-lesen) - Messwerteblock selectiv lesen
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Indentifikation, AIF, FS_Codes ShadowFS_Codes, ShadowFS_lang
- [MW_SELECT_LESEN_NORM](#job-mw-select-lesen-norm) - Messwerteblock selectiv lesen
- [STEUERN_ENDE_SELECTIV](#job-steuern-ende-selectiv) - Steller Steuern selektiv ausschalten
- [STATUS_DIMDIG_2](#job-status-dimdig-2) - MFL und CAN Digitaleingaenge DIMDIG_2
- [STATUS_MENGE_VE](#job-status-menge-ve) - Voreinspritzmenge MRMM_E_VE
- [STATUS_ANST_MOTORLAGER_TV](#job-status-anst-motorlager-tv) - TV Ansteuerung - Motorlager EHMFDSL
- [STATUS_ANST_KUEHLWASSERHEIZUNG_TV](#job-status-anst-kuehlwasserheizung-tv) - TV Ansteuerung Kuehlwasserheizung EHMFKWH
- [STATUS_KWH_AB](#job-status-kwh-ab) - Abbruchbedingungen Kuehlwasserheizung KHONOR_AB
- [STATUS_MRMM_EDELB](#job-status-mrmm-edelb) - M_E begrenzte Abgleichmenge MRMM_EDELB
- [STATUS_COMGTR_OPT](#job-status-comgtr-opt) - Identifikation Handschalter/Automatik COMGTR_OPT
- [MW_SELECT_LESEN_NORM_EINZEL](#job-mw-select-lesen-norm-einzel) - Messwerteblock selectiv lesen
- [STEUERN_MOTORLAGER](#job-steuern-motorlager) - MOTORLAGER ansteuern ,  0 oder 100%
- [STEUERN_KUEHLWASSERHEIZUNG](#job-steuern-kuehlwasserheizung) - KUEHLWASSERHEIZUNG ansteuern ,  5-95%

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

<a id="job-eeprom-lesen"></a>
### EEPROM_LESEN

Beliebige EPROM - Zellen auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EEPROM_LESEN_ADRESSE | long | Uebergabeparameter, Startadresse High-Middle-Low |
| EEPROM_LESEN_ANZAHL_BYTE | int | Uebergabeparameter, Anzahl der auszulesenden BYTES |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| EEPROM_LESEN_WERT | binary | nichts |
| EEPROM_LESEN_EINH | string | Einheit HEX |

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

<a id="job-codier-variante-lesen"></a>
### CODIER_VARIANTE_LESEN

Auslesen des Varianten - Steuerwort

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| CODIER_VARIANTE | string | Varianten - Steuerwort |

<a id="job-status-codier-checksumme"></a>
### STATUS_CODIER_CHECKSUMME

Codier - Checksumme abfragen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_CHECKSUMME_WERT | int | Ergebnis |

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
| F_ANZ_NR | int | Anzahl der gespeicherten Fehler |
| F_ORT_NR | int | Fehlercode des SG als Index |
| F_ORT_TEXT | string | Fehlercode des SG als Text |
| F_HFK | int | Haeufigkeit des einzelnen Fehlers |
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
| F_VORHANDEN | int | Statusbit Fehler vorhanden |
| F_ART_BYTE | int | Fehlerartbyte als Rohwert ausgeben |
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
| F_UW4_EINH | string | Umweltbedingung 4 Einheit |
| F_UW4_WERT | real | Umweltbedingung 4 Wert |
| F_UW5_NR | int | Umweltbedingung 5 Index |
| F_UW5_TEXT | string | Umweltbedingung 5 Text |
| F_UW5_EINH | string | Umweltbedingung 5 Einheit |
| F_UW5_WERT | real | Umweltbedingung 5 Wert |
| F_UW6_NR | int | Umweltbedingung 6 Index |
| F_UW6_TEXT | string | Umweltbedingung 6 Text |
| F_UW6_EINH | string | Umweltbedingung 6 Einheit |
| F_UW6_WERT | real | Umweltbedingung 6 Wert |
| F_CODEHEX | binary | 11 Fehlerbyte |
| F_HEX_CODE | binary | 11 Fehlerbyte |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

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
| F_UW4_EINH | string | Umweltbedingung 4 Einheit |
| F_UW4_WERT | real | Umweltbedingung 4 Wert |
| F_UW5_NR | int | Umweltbedingung 5 Index |
| F_UW5_TEXT | string | Umweltbedingung 5 Text |
| F_UW5_EINH | string | Umweltbedingung 5 Einheit |
| F_UW5_WERT | real | Umweltbedingung 5 Wert |
| F_UW6_NR | int | Umweltbedingung 6 Index |
| F_UW6_TEXT | string | Umweltbedingung 6 Text |
| F_UW6_EINH | string | Umweltbedingung 6 Einheit |
| F_UW6_WERT | real | Umweltbedingung 6 Wert |
| F_CODEHEX | binary | 11 Fehlerbyte |
| F_HEX_CODE | binary | 11 Fehlerbyte |

<a id="job-status-mw2"></a>
### STATUS_MW2

Messwerte (einzelne RAM - Zellen) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_MW2_WERT | real | MW  Wert |
| STATUS_MW2_EINH | string | Einheit |
| STATUS_MW2_TEXT | string | Text |

<a id="job-status-mw3"></a>
### STATUS_MW3

Messwerte (einzelne RAM - Zellen) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_MW3_WERT | real | MW  Wert |
| STATUS_MW3_EINH | string | Einheit |
| STATUS_MW3_TEXT | string | Text |

<a id="job-status-mw4"></a>
### STATUS_MW4

Messwerte (einzelne RAM - Zellen) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_MW4_WERT | real | MW  Wert |
| STATUS_MW4_EINH | string | Einheit |
| STATUS_MW4_TEXT | string | Text |

<a id="job-status-mw5"></a>
### STATUS_MW5

Messwerte (einzelne RAM - Zellen) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_MW5_WERT | real | MW  Wert |
| STATUS_MW5_EINH | string | Einheit |
| STATUS_MW5_TEXT | string | Text |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

Status Schalteingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_PN_FS_SCHALTER_EIN | int | Status Fahrstufe  bzw. Kupplungsschalter 0=Aus / 1=Ein |
| STAT_KUP_EIN | int | Status Fahrstufe  bzw. Kupplungsschalter 0=Aus / 1=Ein |
| STAT_BREMS_TEST_SCHALTER_EIN | int | Status Bremstestschalter 0=Aus / 1=Ein |
| STAT_BTS_EIN | int | Status Bremstestschalter 0=Aus / 1=Ein |
| STAT_BREMS_LICHT_SCHALTER_EIN | int | Status Bremslichtschalter 0=Aus / 1=Ein |
| STAT_BLS_EIN | int | Status Bremslichtschalter 0=Aus / 1=Ein |
| STAT_GLUEHZEIT_SG_EIN | int | Status Gluehzeitsteuergeraet 0=Aus / 1=Ein |
| STAT_PWG_EIN | int | Status PWG Schalter  0=Aus / 1=Ein |
| STAT_KO_EIN | int | Klima-Anforderung 0=Nein / 1=Ja |
| STAT_AC_EIN | int | Anforderung Klimabereitschaft 0=Nein / 1=Ja |
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

<a id="job-steuern-abluftklappe"></a>
### STEUERN_ABLUFTKLAPPE

Abluftklappe ansteuern ,  0 oder 100%

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | Verstellwert 0 oder 100 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-agr-steller"></a>
### STEUERN_AGR_STELLER

ARF - Steller  ansteuern ,  5-95%

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | Verstellwert 5 - 95 % |

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
| TASTVERHAELTNIS | int | Verstellwert 0 oder 100 % |

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

<a id="job-steuern-klimakompressor"></a>
### STEUERN_KLIMAKOMPRESSOR

ARF-Steller ansteuern ,  0 oder 100%

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | Verstellwert 0 - 100 % |

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
| TASTVERHAELTNIS | int | Verstellwert 0 oder 100 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-spritzversteller"></a>
### STEUERN_SPRITZVERSTELLER

ARF-Steller ansteuern ,  -12.5 Grad KW bis 51,25 Grad KW

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | real | Verstellwert   -12.5 Grad KW bis 51,25 Grad KW |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-diagnose-erhalten"></a>
### DIAGNOSE_ERHALTEN

Diagnose erhalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

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

BEGR_MENGEn-Abgleich lesen (Rohwert)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_LESEN_BEGR_MENGE_ROH_WERT | int | Aktuellen Abgleichwert |
| ABGLEICH_LESEN_BEGR_MENGE_ROH_STATUS | int | Rueckmeldebyte |

<a id="job-abgleich-verstellen-begr-menge-roh"></a>
### ABGLEICH_VERSTELLEN_BEGR_MENGE_ROH

BEGR_MENGE Abgleich verstellen (Rohwert)

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

<a id="job-abgleich-lesen-ladedruck"></a>
### ABGLEICH_LESEN_LADEDRUCK

LADEDRUCK-Abgleich lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_LESEN_LADEDRUCK_WERT | real | Aktuellen Abgleichwert |
| ABGLEICH_LESEN_LADEDRUCK_STATUS | int | Rueckmeldebyte |

<a id="job-abgleich-verstellen-ladedruck"></a>
### ABGLEICH_VERSTELLEN_LADEDRUCK

LADEDRUCK Abgleich verstellen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_VERSTELLEN_LADEDRUCK_WERT | real | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_VERSTELLEN_LADEDRUCK_STATUS | int | Status |

<a id="job-abgleich-prog-ladedruck"></a>
### ABGLEICH_PROG_LADEDRUCK

LADEDRUCK Abgleich programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_PROG_LADEDRUCK_STATUS | int | Status |

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
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_11 | real | Neuer Verstellwert 12 |
| ABGLEICH_VERSTELLEN_ABGLEICHMENGE_WERT_12 | real | Neuer Verstellwert |

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

<a id="job-abgleich-lesen-fgr-verbaut"></a>
### ABGLEICH_LESEN_FGR_VERBAUT

FGR-Abgleich lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_LESEN_FGR_VERBAUT_WERT | int | Aktueller Abgleichwert , 1= FGR vorhanden ,  0= FGR nicht vorhanden, 0xff = fehlerhafter Abgleich |
| ABGLEICH_LESEN_FGR_VERBAUT_STATUS | int | Rueckmeldebyte |

<a id="job-abgleich-verstellen-fgr-verbaut"></a>
### ABGLEICH_VERSTELLEN_FGR_VERBAUT

FGR-Funktion und Mainswitch konfigurieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_VERSTELLEN_FGR_VERBAUT_WERT | int | 1= FGR vorhanden ,  0= FGR nicht vorhanden, |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_VERSTELLEN_FGR_VERBAUT_STATUS | int | Status |

<a id="job-abgleich-prog-fgr"></a>
### ABGLEICH_PROG_FGR

LADEDRUCK Abgleich programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_PROG_FGR_STATUS | int | Status |

<a id="job-abgleich-lesen-kennung-klimaanlage"></a>
### ABGLEICH_LESEN_KENNUNG_KLIMAANLAGE

Kennung Klimaanlage lesen: 1 = Kliamaanlage vorhanden,  0 = Klimaanlage nicht vorhanden 0xff = Fehler

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_LESEN_KENNUNG_KLIMAANLAGE_WERT | int | Aktuellen Abgleichwert |
| ABGLEICH_LESEN_KENNUNG_KLIMAANLAGE_STATUS | int | Rueckmeldebyte |

<a id="job-abgleich-verstellen-kennung-klimaanlage"></a>
### ABGLEICH_VERSTELLEN_KENNUNG_KLIMAANLAGE

Kennung Klimaanlage verstellen, 0 = nicht verbaut, 1 = verbaut

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_VERSTELLEN_KENNUNG_KLIMAANLAGE_WERT | int | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_VERSTELLEN_KENNUNG_KLIMAANLAGE_STATUS | int | Status |

<a id="job-abgleich-prog-kennung-klimaanlage"></a>
### ABGLEICH_PROG_KENNUNG_KLIMAANLAGE

Kennung Klimaanlage programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_PROG_KENNUNG_KLIMAANLAGE_STATUS | int | Status |

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
| ABGLEICH_TIMER_VERSTELLEN_PROGRAMMIEREN_STATUS | int | Status |

<a id="job-abgleich-lesen-pumpenabgleich-flag"></a>
### ABGLEICH_LESEN_PUMPENABGLEICH_FLAG

Kennung M_ABGLEICH_FLAG lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_LESEN_PUMPENABGLEICH_FLAG_WERT | int | Aktuellen Abgleichwert |
| ABGLEICH_LESEN_PUMPENABGLEICH_FLAG_STATUS | int | Rueckmeldebyte |

<a id="job-abgleich-verstellen-pumpenabgleich-flag"></a>
### ABGLEICH_VERSTELLEN_PUMPENABGLEICH_FLAG

Kennung M_ABGLEICH_FLAG verstellen, 0 = nicht verbaut, 0xff = verbaut

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_VERSTELLEN_PUMPENABGLEICH_FLAG_WERT | int | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_VERSTELLEN_PUMPENABGLEICH_FLAG_STATUS | int | Status |

<a id="job-abgleich-prog-pumpenabgleich-flag"></a>
### ABGLEICH_PROG_PUMPENABGLEICH_FLAG

Kennung M_ABGLEICH_FLAG programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_PROG_PUMPENABGLEICH_FLAG_STATUS | int | Status |

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

<a id="job-status-sync-mode"></a>
### STATUS_SYNC_MODE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STATUS_SYNC_MODE_STATUS | int | Statusflag |
| STATUS_SYNC_MODE_TEXT | string | Statustext |

<a id="job-hole-ema-feld"></a>
### HOLE_EMA_FELD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| EMA_FAK1 | real | Faktor 1 |
| EMA_FAK2 | real | faktor 2 |
| EMA_WERT3 | real | Wert 3 |

<a id="job-status-phi-sv-ist"></a>
### STATUS_PHI_SV_IST

Spritzverstellerwinkel Pumpe

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| JOB_STAT_INT | int | "OKAY", wenn fehlerfrei |
| STAT_PHI_SV_IST_WERT | real | Ergebnis |
| STAT_PHI_SV_IST_EINH | string | Einheit |

<a id="job-status-tv-sv"></a>
### STATUS_TV_SV

Tastverhaeltnis Spritzversteller Pumpe

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_TV_SV_WERT | real | Ergebnis |
| STAT_TV_SV_EINH | string | Einheit |

<a id="job-status-t-mv-on"></a>
### STATUS_T_MV_ON

Einschaltzeitpunkt fuer Mengenmagnetventil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_T_MV_ON_WERT | real | Ergebnis |
| STAT_T_MV_ON_EINH | string | Einheit |

<a id="job-status-t-mv-off"></a>
### STATUS_T_MV_OFF

Ausschaltzeitpunkt fuer Mengenmagnetventil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_T_MV_OFF_WERT | real | Ergebnis |
| STAT_T_MV_OFF_EINH | string | Einheit |

<a id="job-status-sv-soll"></a>
### STATUS_SV_SOLL

Spritzversteller - Sollwinkel

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_SV_SOLL_WERT | real | Ergebnis |
| STAT_SV_SOLL_EINH | string | Einheit |

<a id="job-status-ae-iwz"></a>
### STATUS_AE_IWZ

Ansteuerende

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_AE_IWZ_WERT | real | Ergebnis |
| STAT_AE_IWZ_EINH | string | Einheit |

<a id="job-status-ab-iwz"></a>
### STATUS_AB_IWZ

Ansteuerbeginn

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_AB_IWZ_WERT | real | Ergebnis |
| STAT_AB_IWZ_EINH | string | Einheit |

<a id="job-status-me-soll"></a>
### STATUS_ME_SOLL

Sollmenge - Eingang aus MSG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_ME_SOLL_WERT | real | Ergebnis |
| STAT_ME_SOLL_EINH | string | Einheit |

<a id="job-status-fb-soll"></a>
### STATUS_FB_SOLL

Foerderbeginn Nockenwellen-Sollwinkel

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_FB_SOLL_WERT | real | Ergebnis |
| STAT_FB_SOLL_EINH | string | Einheit |

<a id="job-status-d-ad-tk-n"></a>
### STATUS_D_AD_TK_N

Dyn. TKR-Kompensation

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_D_AD_TK_N_WERT | real | Ergebnis |
| STAT_D_AD_TK_N_EINH | string | Einheit |

<a id="job-status-d-ad-nw-n"></a>
### STATUS_D_AD_NW_N

Dyn. Ansteuerdauerkorrektur

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_D_AD_NW_N_WERT | real | Ergebnis |
| STAT_D_AD_NW_N_EINH | string | Einheit |

<a id="job-status-atmosphaerendruck"></a>
### STATUS_ATMOSPHAERENDRUCK

ADF Atmosphaerendruck ANMADF

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ATMOSPHAERENDRUCK_WERT | real | Ergebnis |
| STAT_ATMOSPHAERENDRUCK_EINH | string | Einheit |

<a id="job-status-ladedruck"></a>
### STATUS_LADEDRUCK

LDF Lade- / Saugrohr-Druck ANMLDF

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LADEDRUCK_WERT | real | Ergebnis |
| STAT_LADEDRUCK_EINH | string | Einheit |

<a id="job-status-lmm-masse"></a>
### STATUS_LMM_MASSE

LMM  Analogwert Luftmassenmesser HFM ANMLMM

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LMM_MASSE_WERT | real | Ergebnis |
| STAT_LMM_MASSE_EINH | string | Einheit |

<a id="job-status-pwg-fahrerwunsch-ungef"></a>
### STATUS_PWG_FAHRERWUNSCH_UNGEF

PWG Pedalwertgeber  - Position (ungefiltert) ANMPWG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_PWG_FAHRERWUNSCH_UNGEF_WERT | real | Ergebnis |
| STAT_PWG_FAHRERWUNSCH_UNGEF_EINH | string | Einheit |

<a id="job-status-pwg-winkel"></a>
### STATUS_PWG_WINKEL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_PWG_WINKEL_WERT | real | Ergebnis |
| STAT_PWG_WINKEL_EINH | string | Einheit |

<a id="job-status-ubatt"></a>
### STATUS_UBATT

UBT Batteriespannung ANMUBATT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_UBATT_WERT | real | Ergebnis |
| STAT_UBATT_EINH | string | Einheit |

<a id="job-status-uref"></a>
### STATUS_UREF

URF Referenzspannung ANMU_REF

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_UREF_WERT | real | Ergebnis |
| STAT_UREF_EINH | string | Einheit |

<a id="job-status-motortemperatur"></a>
### STATUS_MOTORTEMPERATUR

WTF Wassertemperatur ANMWTF

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MOTORTEMPERATUR_WERT | real | Ergebnis |
| STAT_MOTORTEMPERATUR_EINH | string | Einheit |

<a id="job-status-pwg-fahrerwunsch-v"></a>
### STATUS_PWG_FAHRERWUNSCH_V

PWG Rohwert Pedalwertgeber ANOU_PWG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_PWG_FAHRERWUNSCH_V_WERT | real | Ergebnis |
| STAT_PWG_FAHRERWUNSCH_V_EINH | string | Einheit |

<a id="job-status-last"></a>
### STATUS_LAST

M_L aktuelle Luftmasse ARMM_LIST

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LAST_WERT | real | Ergebnis |
| STAT_LAST_EINH | string | Einheit |

<a id="job-status-arf-sollwert"></a>
### STATUS_ARF_SOLLWERT

M_L Sollwert fuer ARF-Regelung ARMM_LSOLL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ARF_SOLLWERT_WERT | real | Ergebnis |
| STAT_ARF_SOLLWERT_EINH | string | Einheit |

<a id="job-status-dimdigprel-low"></a>
### STATUS_DIMDIGPREL_LOW

Entprellte logische Zustaende d. digit. Eingaenge DIMDIGPREL_L

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DIMDIGPREL_LOW_WERT | real | Ergebnis |
| STAT_DIMDIGPREL_LOW_EINH | string | Einheit |

<a id="job-status-dimdigprel-high"></a>
### STATUS_DIMDIGPREL_HIGH

Entprellte logische Zustaende d. digit. Eingaenge high DIMDIGPREL_H

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DIMDIGPREL_HIGH_WERT | real | Ergebnis |
| STAT_DIMDIGPREL_HIGH_EINH | string | Einheit |

<a id="job-status-motordrehzahl"></a>
### STATUS_MOTORDREHZAHL

N Drehzahl (einfach gemittelt) DZMNMIT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MOTORDREHZAHL_WERT | real | Ergebnis |
| STAT_MOTORDREHZAHL_EINH | string | Einheit |

<a id="job-status-abluftklappe-tv"></a>
### STATUS_ABLUFTKLAPPE_TV

TV Ansteuerung Abluftlappensteuerung EHMFAKS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ABLUFTKLAPPE_TV_WERT | real | Ergebnis |
| STAT_ABLUFTKLAPPE_TV_EINH | string | Einheit |

<a id="job-status-arf-steller-tv"></a>
### STATUS_ARF_STELLER_TV

TV Ansteuerung ARF-Steller EHMFARS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ARF_STELLER_TV_WERT | real | Ergebnis |
| STAT_ARF_STELLER_TV_EINH | string | Einheit |

<a id="job-status-ladedrucksteller-tv"></a>
### STATUS_LADEDRUCKSTELLER_TV

TV Ansteuerung Ladedrucksteller EHMFLD_DK

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LADEDRUCKSTELLER_TV_WERT | real | Ergebnis |
| STAT_LADEDRUCKSTELLER_TV_EINH | string | Einheit |

<a id="job-status-e-luefter-tv"></a>
### STATUS_E_LUEFTER_TV

TV Ansteuerung El.Motorluefter EHMFMLS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_E_LUEFTER_TV_WERT | real | Ergebnis |
| STAT_E_LUEFTER_TV_EINH | string | Einheit |

<a id="job-status-v-zu-n"></a>
### STATUS_V_ZU_N

V/N aktuelles Verhaeltnis Geschwindigkeit/Drehzahl FGM_VZUN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_V_ZU_N_WERT | real | Ergebnis |
| STAT_V_ZU_N_EINH | string | Einheit |

<a id="job-status-beschleunigung"></a>
### STATUS_BESCHLEUNIGUNG

Beschleunigung FGMBESCH

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_BESCHLEUNIGUNG_WERT | real | Ergebnis |
| STAT_BESCHLEUNIGUNG_EINH | string | Einheit |

<a id="job-status-geschwindigkeit"></a>
### STATUS_GESCHWINDIGKEIT

V aktuelle Geschwindigkeit FGMFGAKT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_GESCHWINDIGKEIT_WERT | real | Ergebnis |
| STAT_GESCHWINDIGKEIT_EINH | string | Einheit |

<a id="job-status-msr-eingriff"></a>
### STATUS_MSR_EINGRIFF

M_E externer Momenteneingriff MSR MRMM_EXMSR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MSR_EINGRIFF_WERT | real | Ergebnis |
| STAT_MSR_EINGRIFF_EINH | string | Einheit |

<a id="job-status-einspritzmenge"></a>
### STATUS_EINSPRITZMENGE

M_E Aktuelle Einspritzmenge (ohne ARD) MRMM_EAKT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_EINSPRITZMENGE_WERT | real | Ergebnis |
| STAT_EINSPRITZMENGE_EINH | string | Einheit |

<a id="job-status-begrenzungsmenge"></a>
### STATUS_BEGRENZUNGSMENGE

M_E resultierende Begrenzungsmenge MRMM_EBEGR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_BEGRENZUNGSMENGE_WERT | real | Ergebnis |
| STAT_BEGRENZUNGSMENGE_EINH | string | Einheit |

<a id="job-status-wunschmenge-fgr"></a>
### STATUS_WUNSCHMENGE_FGR

M_E Wunschmenge aus FGR MRMM_EFGR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_WUNSCHMENGE_FGR_WERT | real | Ergebnis |
| STAT_WUNSCHMENGE_FGR_EINH | string | Einheit |

<a id="job-status-einspritzmenge-llr"></a>
### STATUS_EINSPRITZMENGE_LLR

M_E Menge aus Leerlaufreglung MRMM_ELLR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_EINSPRITZMENGE_LLR_WERT | real | Ergebnis |
| STAT_EINSPRITZMENGE_LLR_EINH | string | Einheit |

<a id="job-status-einspritzmenge-ard"></a>
### STATUS_EINSPRITZMENGE_ARD

M_E Einspritzmenge nach ARD MRMM_EMOT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_EINSPRITZMENGE_ARD_WERT | real | Ergebnis |
| STAT_EINSPRITZMENGE_ARD_EINH | string | Einheit |

<a id="job-status-wunschmenge-pwg"></a>
### STATUS_WUNSCHMENGE_PWG

M_E Wunschmenge = f(PWG) aus Fahrverhaltenkennfeld MRMM_EPWG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_WUNSCHMENGE_PWG_WERT | real | Ergebnis |
| STAT_WUNSCHMENGE_PWG_EINH | string | Einheit |

<a id="job-status-startmenge-sollwert"></a>
### STATUS_STARTMENGE_SOLLWERT

M_E resultierender Startmengen-Sollwert MRMM_ESTAR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_STARTMENGE_SOLLWERT_WERT | real | Ergebnis |
| STAT_STARTMENGE_SOLLWERT_EINH | string | Einheit |

<a id="job-status-fahrerwunschmenge-n-ex-eingriff"></a>
### STATUS_FAHRERWUNSCHMENGE_N_EX_EINGRIFF

M_E Fahrerwunschmenge nach externem Mengeneingriff MRMM_EWUN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_FAHRERWUNSCHMENGE_N_EX_EINGRIFF_WERT | real | Ergebnis |
| STAT_FAHRERWUNSCHMENGE_N_EX_EINGRIFF_EINH | string | Einheit |

<a id="job-status-fahrerwunschmenge-pwg-fgr"></a>
### STATUS_FAHRERWUNSCHMENGE_PWG_FGR

M_E Fahrerwunschmenge aus PWG oder FGR MRMM_EWUNF

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_FAHRERWUNSCHMENGE_PWG_FGR_WERT | real | Ergebnis |
| STAT_FAHRERWUNSCHMENGE_PWG_FGR_EINH | string | Einheit |

<a id="job-status-motordrehzahl-soll"></a>
### STATUS_MOTORDREHZAHL_SOLL

N Leerlaufsolldrehzahl MRMN_LLBAS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MOTORDREHZAHL_SOLL_WERT | real | Ergebnis |
| STAT_MOTORDREHZAHL_SOLL_EINH | string | Einheit |

<a id="job-status-pwg-fahrerwunsch"></a>
### STATUS_PWG_FAHRERWUNSCH

PWG gefilterte Pedalwertgeber-Position MRMPWGFI

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_PWG_FAHRERWUNSCH_WERT | real | Ergebnis |
| STAT_PWG_FAHRERWUNSCH_EINH | string | Einheit |

<a id="job-status-pwg-poti-spannung"></a>
### STATUS_PWG_POTI_SPANNUNG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_PWG_POTI_SPANNUNG_WERT | real | Ergebnis |
| STAT_PWG_POTI_SPANNUNG_1_WERT | real | Ergebnis |
| STAT_PWG_POTI_SPANNUNG_EINH | string | Einheit |
| STAT_ROHWERT1 | int | Ergebnis |
| STAT_ROHWERT2 | int | Ergebnis |

<a id="job-status-geschwindigkeit-sollwert"></a>
### STATUS_GESCHWINDIGKEIT_SOLLWERT

V Sollwert Fahrgeschwindigkeit fuer Diagnose MRMFG_SOLL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_GESCHWINDIGKEIT_SOLLWERT_WERT | real | Ergebnis |
| STAT_GESCHWINDIGKEIT_SOLLWERT_EINH | string | Einheit |

<a id="job-status-motordrehzahl-sek"></a>
### STATUS_MOTORDREHZAHL_SEK

N Drehzahl aus Sekundaergeber DZMN_SEK

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MOTORDREHZAHL_SEK_WERT | real | Ergebnis |
| STAT_MOTORDREHZAHL_SEK_EINH | string | Einheit |

<a id="job-status-ladedruck-korr"></a>
### STATUS_LADEDRUCK_KORR

P_L T_L-abhaengig korregierter Ladedruck ARMPKORR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LADEDRUCK_KORR_WERT | real | Ergebnis |
| STAT_LADEDRUCK_KORR_EINH | string | Einheit |

<a id="job-status-ladedruck-sollwert"></a>
### STATUS_LADEDRUCK_SOLLWERT

P_L Sollwert fuer Ladedruck LDMP_LSOLL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LADEDRUCK_SOLLWERT_WERT | real | Ergebnis |
| STAT_LADEDRUCK_SOLLWERT_EINH | string | Einheit |

<a id="job-status-sb-sollwert"></a>
### STATUS_SB_SOLLWERT

SB Spritzbeginn-Sollwert SBMPHISOLL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_SB_SOLLWERT_WERT | real | Ergebnis |
| STAT_SB_SOLLWERT_EINH | string | Einheit |

<a id="job-status-sb-istwert"></a>
### STATUS_SB_ISTWERT

SB Spritzbeginn-Istwert SBMPHIIST

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_SB_ISTWERT_WERT | real | Ergebnis |
| STAT_SB_ISTWERT_EINH | string | Einheit |

<a id="job-status-wtf-sgr"></a>
### STATUS_WTF_SGR

T_W Wassertemperatur fuer SBR SBMWTF

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_WTF_SGR_WERT | real | Ergebnis |
| STAT_WTF_SGR_EINH | string | Einheit |

<a id="job-status-fb-kw-sw"></a>
### STATUS_FB_KW_SW

FB-KW-Sollwinkel FNMFBKWSW

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_FB_KW_SW_WERT | real | Ergebnis |
| STAT_FB_KW_SW_EINH | string | Einheit |

<a id="job-status-fb-nw-sw"></a>
### STATUS_FB_NW_SW

FB-NW-Sollwinkel FNMFBNWSW

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_FB_NW_SW_WERT | real | Ergebnis |
| STAT_FB_NW_SW_EINH | string | Einheit |

<a id="job-status-pi-regler"></a>
### STATUS_PI_REGLER

SBR: PI-Regler-Ausgangswert SBONAPI

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_PI_REGLER_WERT | real | Ergebnis |
| STAT_PI_REGLER_EINH | string | Einheit |

<a id="job-status-signal-nbf"></a>
### STATUS_SIGNAL_NBF

U_NBF Spannungssignal aus NBF ANMST_NBF

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_SIGNAL_NBF_WERT | real | Ergebnis |
| STAT_SIGNAL_NBF_EINH | string | Einheit |

<a id="job-status-startmengen-agl"></a>
### STATUS_STARTMENGEN_AGL

M_E Abgleichwert fuer Startmengenkorrektur MRMSTA_AGL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_STARTMENGEN_AGL_WERT | real | Ergebnis |
| STAT_STARTMENGEN_AGL_EINH | string | Einheit |

<a id="job-status-begrenzungsmenge-agl-faktor"></a>
### STATUS_BEGRENZUNGSMENGE_AGL_FAKTOR

F_ME Abgleichfaktor fuer Begrenzungsmenge MRMBEG_AGL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_BEGRENZUNGSMENGE_AGL_FAKTOR_WERT | real | Ergebnis |
| STAT_BEGRENZUNGSMENGE_AGL_FAKTOR_EINH | string | Einheit |

<a id="job-status-umsch-beg-k"></a>
### STATUS_UMSCH_BEG_K

Ext. Umschaltung auf Begrenzungs-Kl. MRMBM_EAKT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_UMSCH_BEG_K_WERT | real | Ergebnis |
| STAT_UMSCH_BEG_K_EINH | string | Einheit |

<a id="job-status-pumpenmenge-unkor"></a>
### STATUS_PUMPENMENGE_UNKOR

Pumpenmenge unkorregiert MRMM_EFAHR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_PUMPENMENGE_UNKOR_WERT | real | Ergebnis |
| STAT_PUMPENMENGE_UNKOR_EINH | string | Einheit |

<a id="job-status-duesenmenge-kor"></a>
### STATUS_DUESENMENGE_KOR

Duesenkorrekturmenge MRMM_EKORR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DUESENMENGE_KOR_WERT | real | Ergebnis |
| STAT_DUESENMENGE_KOR_EINH | string | Einheit |

<a id="job-status-sollmenge-vor-ueb"></a>
### STATUS_SOLLMENGE_VOR_UEB

M_E Soll-Menge vor Ueberwachung MRMM_EPUMP

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_SOLLMENGE_VOR_UEB_WERT | real | Ergebnis |
| STAT_SOLLMENGE_VOR_UEB_EINH | string | Einheit |

<a id="job-status-sollmenge-an-psg"></a>
### STATUS_SOLLMENGE_AN_PSG

M_E Soll-Menge an PSG MRMM_ESOLL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_SOLLMENGE_AN_PSG_WERT | real | Ergebnis |
| STAT_SOLLMENGE_AN_PSG_EINH | string | Einheit |

<a id="job-status-me-kor-abw"></a>
### STATUS_ME_KOR_ABW

Mengenkorrekturkennfeld.Abweichung MRMMK_KL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ME_KOR_ABW_WERT | real | Ergebnis |
| STAT_ME_KOR_ABW_EINH | string | Einheit |

<a id="job-status-drehzahlanhebung-ko"></a>
### STATUS_DREHZAHLANHEBUNG_KO

Anhebung der Leerlaufdrehzahl bei Klimakompressor ein KLMN_LLKLM

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DREHZAHLANHEBUNG_KO_WERT | real | Ergebnis |
| STAT_DREHZAHLANHEBUNG_KO_EINH | string | Einheit |

<a id="job-status-drehzahl-psg"></a>
### STATUS_DREHZAHL_PSG

Drehzahl NW-bezogen (PSG-Drehzahl) PKMDZNW

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DREHZAHL_PSG_WERT | real | Ergebnis |
| STAT_DREHZAHL_PSG_EINH | string | Einheit |

<a id="job-status-temperatur-pumpe"></a>
### STATUS_TEMPERATUR_PUMPE

Pumpentemperatur PKMT_PUMP

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_TEMPERATUR_PUMPE_WERT | real | Ergebnis |
| STAT_TEMPERATUR_PUMPE_EINH | string | Einheit |

<a id="job-status-psg-statuswort"></a>
### STATUS_PSG_STATUSWORT

PSG Statuswort PKMPSGSTA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_PSG_STATUSWORT_WERT | real | Ergebnis |
| STAT_PSG_STATUSWORT_EINH | string | Einheit |

<a id="job-status-psg-selbsttest"></a>
### STATUS_PSG_SELBSTTEST

PSG Selbsttestergebnis PKMPSG_ST

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_PSG_SELBSTTEST_WERT | real | Ergebnis |
| STAT_PSG_SELBSTTEST_EINH | string | Einheit |

<a id="job-status-ansteuerdauer-mv"></a>
### STATUS_ANSTEUERDAUER_MV

Ansteuerdauer MV-Endstufe PKMADAUER

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANSTEUERDAUER_MV_WERT | real | Ergebnis |
| STAT_ANSTEUERDAUER_MV_EINH | string | Einheit |

<a id="job-status-timeout-can"></a>
### STATUS_TIMEOUT_CAN

n-Timeoutzaehler fuer Senden CAN zeitsync. PKMTOCNT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_TIMEOUT_CAN_WERT | real | Ergebnis |
| STAT_TIMEOUT_CAN_EINH | string | Einheit |

<a id="job-status-kd-ant-1"></a>
### STATUS_KD_ANT_1

Kundendienst-Antwort 1 PKMKDANT_1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_KD_ANT_1_WERT | real | Ergebnis |
| STAT_KD_ANT_1_EINH | string | Einheit |

<a id="job-status-kd-ant-2"></a>
### STATUS_KD_ANT_2

Kundendienst-Antwort 2 PKMKDANT_2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_KD_ANT_2_WERT | real | Ergebnis |
| STAT_KD_ANT_2_EINH | string | Einheit |

<a id="job-status-kd-ant-3"></a>
### STATUS_KD_ANT_3

Kundendienst-Antwort 3 PKMKDANT_3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_KD_ANT_3_WERT | real | Ergebnis |
| STAT_KD_ANT_3_EINH | string | Einheit |

<a id="job-status-kd-ant-4"></a>
### STATUS_KD_ANT_4

Kundendienst-Antwort 4 PKMKDANT_4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_KD_ANT_4_WERT | real | Ergebnis |
| STAT_KD_ANT_4_EINH | string | Einheit |

<a id="job-status-anst-gluehrel-tv"></a>
### STATUS_ANST_GLUEHREL_TV

TV Ansteuerung Gluehrelaissteller EHMFGRS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANST_GLUEHREL_TV_WERT | real | Ergebnis |
| STAT_ANST_GLUEHREL_TV_EINH | string | Einheit |

<a id="job-status-anst-vor-pumpe-tv"></a>
### STATUS_ANST_VOR_PUMPE_TV

TV Ansteuerung - Vorfoerderpumpe EHMFVFP

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANST_VOR_PUMPE_TV_WERT | real | Ergebnis |
| STAT_ANST_VOR_PUMPE_TV_EINH | string | Einheit |

<a id="job-status-anst-gluehanz-tv"></a>
### STATUS_ANST_GLUEHANZ_TV

TV Anteuerung Gluehanzeige EHMFGAZ

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANST_GLUEHANZ_TV_WERT | real | Ergebnis |
| STAT_ANST_GLUEHANZ_TV_EINH | string | Einheit |

<a id="job-status-anst-dig-lampe-tv"></a>
### STATUS_ANST_DIG_LAMPE_TV

TV Ansteuerung Diagnoselampe EHMFDIA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANST_DIG_LAMPE_TV_WERT | real | Ergebnis |
| STAT_ANST_DIG_LAMPE_TV_EINH | string | Einheit |

<a id="job-status-anst-ko-tv"></a>
### STATUS_ANST_KO_TV

TV Ansteuerung Klimakompressor EHMFSKOREL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANST_KO_TV_WERT | real | Ergebnis |
| STAT_ANST_KO_TV_EINH | string | Einheit |

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

<a id="job-status-pwg-anschlag-max"></a>
### STATUS_PWG_ANSCHLAG_MAX

Auslesen des oberen Gaspedalanschlags

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_PWG_ANSCHLAG_MAX_WERT | real | umgerechnet in Volt |
| STAT_PWG_ANSCHLAG_MAX_EINH | string | Einheit in Volt |

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

<a id="job-status-reibmenge-n-kl-l-komp"></a>
### STATUS_REIBMENGE_N_KL_L_KOMP

Reibmenge nach Klimalastmomentkompensation MROM_ERBK

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_REIBMENGE_N_KL_L_KOMP_WERT | real | Ergebnis |
| STAT_REIBMENGE_N_KL_L_KOMP_EINH | string | Einheit |

<a id="job-steuern-testplatz"></a>
### STEUERN_TESTPLATZ

Freischaltung fuer SG-Befundung ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-ecu-config"></a>
### ECU_CONFIG

Ident-Daten fuer DME

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| EGS_VORHANDEN | int | EGS vorhanden 1=ja ,  0=nein , 0xff=nicht unterstuetzt |

<a id="job-status-betr-stundenzaehler"></a>
### STATUS_BETR_STUNDENZAEHLER

UB akt. Betriebsstundenzaehler FBMBSTZ_UB

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_BETR_STUNDENZAEHLER_WERT | real | Ergebnis |
| STAT_BETR_STUNDENZAEHLER_EINH | string | Einheit |

<a id="job-mwblock-roh"></a>
### MWBLOCK_ROH

Messwerteblock roh ausgeben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| MWBLOCK_ROH_WERT | binary | MW  Wert |

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

<a id="job-pruefcode-lesen"></a>
### PRUEFCODE_LESEN

Indentifikation, AIF, FS_Codes ShadowFS_Codes, ShadowFS_lang

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| PRUEFCODE | binary | Indentifikation, AIF, FS_Codes ShadowFS_Codes, ShadowFS_lang |

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

<a id="job-steuern-ende-selectiv"></a>
### STEUERN_ENDE_SELECTIV

Steller Steuern selektiv ausschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STELLERMESSAGENR | binary |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-status-dimdig-2"></a>
### STATUS_DIMDIG_2

MFL und CAN Digitaleingaenge DIMDIG_2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DIMDIG_2_WERT | real | Ergebnis |
| STAT_DIMDIG_2_EINH | string | Einheit |

<a id="job-status-menge-ve"></a>
### STATUS_MENGE_VE

Voreinspritzmenge MRMM_E_VE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MENGE_VE_WERT | real | Ergebnis |
| STAT_MENGE_VE_EINH | string | Einheit |

<a id="job-status-anst-motorlager-tv"></a>
### STATUS_ANST_MOTORLAGER_TV

TV Ansteuerung - Motorlager EHMFDSL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANST_MOTORLAGER_TV_WERT | real | Ergebnis |
| STAT_ANST_MOTORLAGER_TV_EINH | string | Einheit |

<a id="job-status-anst-kuehlwasserheizung-tv"></a>
### STATUS_ANST_KUEHLWASSERHEIZUNG_TV

TV Ansteuerung Kuehlwasserheizung EHMFKWH

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANST_KUEHLWASSERHEIZUNG_TV_WERT | real | Ergebnis |
| STAT_ANST_KUEHLWASSERHEIZUNG_TV_EINH | string | Einheit |

<a id="job-status-kwh-ab"></a>
### STATUS_KWH_AB

Abbruchbedingungen Kuehlwasserheizung KHONOR_AB

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_KWH_AB_WERT | real | Ergebnis |
| STAT_KWH_AB_EINH | string | Einheit |

<a id="job-status-mrmm-edelb"></a>
### STATUS_MRMM_EDELB

M_E begrenzte Abgleichmenge MRMM_EDELB

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMM_EDELB_WERT | real | Ergebnis |
| STAT_MRMM_EDELB_EINH | string | Einheit |

<a id="job-status-comgtr-opt"></a>
### STATUS_COMGTR_OPT

Identifikation Handschalter/Automatik COMGTR_OPT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_COMGTR_OPT_WERT | real | Ergebnis |
| STAT_COMGTR_OPT_EINH | string | Einheit |

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

<a id="job-steuern-motorlager"></a>
### STEUERN_MOTORLAGER

MOTORLAGER ansteuern ,  0 oder 100%

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | Verstellwert 0 oder 100 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-kuehlwasserheizung"></a>
### STEUERN_KUEHLWASSERHEIZUNG

KUEHLWASSERHEIZUNG ansteuern ,  5-95%

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | Verstellwert 5 - 95 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

## Tables

### Index

- [BETRIEBSWTAB](#table-betriebswtab) (82 × 17)
- [BITS](#table-bits) (12 × 4)
- [FORTTEXTE](#table-forttexte) (48 × 4)
- [FARTMATRIX](#table-fartmatrix) (47 × 17)
- [FARTTEXTE](#table-farttexte) (97 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (11 × 5)
- [SHADOWFEHLER](#table-shadowfehler) (12 × 4)
- [BITSKHO](#table-bitskho) (9 × 9)
- [JOBRESULT](#table-jobresult) (39 × 2)

<a id="table-betriebswtab"></a>
### BETRIEBSWTAB

Dimensions: 82 rows × 17 columns

| NAME | TELEGRAM | POS_ADR | ADR | LEN_ADR | BYTE | DATA_TYPE | COMPU_TYPE | FACT_A | FACT_B | MASK | VALUE | ANZ | MEAS | RANGE | JOBNAME | LNAME |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| anmADF | 12070B100F63 | 04 | 0x0F63 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | hPa |   | ATMOSPHAERENDRUCK | ADF Atmosphaerendruck |
| anmLDF | 12070B100F62 | 04 | 0x0F62 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | hPa |   | LADEDRUCK | LDF Lade- / Saugrohr-Druck |
| anmLMM | 12070B100F61 | 04 | 0x0F61 | 0x00 | 05 | 5 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | % |   | LMM_MASSE | LMM  Analogwert Luftmassenmesser HFM |
| anmPWG | 12070B100F60 | 04 | 0x0F60 | 0x00 | 05 | 5 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | % |   | PWG_FAHRERWUNSCH_UNGEF | PWG Pedalwertgeber  - Position (ungefiltert) |
| anmUBATT | 12070B100F65 | 04 | 0x0F65 | 0x00 | 05 | 5 | -- | 0,02037243 | 0 | 0x00 | 0x00 | 6.2f | V |   | UBATT | UBT Batteriespannung |
| anmU_REF | 12070B100F93 | 04 | 0x0F93 | 0x00 | 05 | 5 | -- | 4,88759 | 0 | 0x00 | 0x00 | 6.2f | mV |   | UREF | URF Referenzspannung |
| anmWTF | 12070B100F00 | 04 | 0x0F00 | 0x00 | 05 | 5 | -- | 0,1 | -273,14 | 0x00 | 0x00 | 6.2f | Grad C |   | MOTORTEMPERATUR | WTF Wassertemperatur |
| anoU_PWG | 12070B100F67 | 04 | 0x0F67 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | mV |   | PWG_FAHRERWUNSCH_V | PWG Rohwert Pedalwertgeber |
| anoU_PWG1 | 12070B100F67 | 04 | 0x0F67 | 0x00 | 05 | 5 | -- | 0,001 | 0 | 0x00 | 0x00 | 6.2f | V |   | PWG_FAHRERWUNSCH_V | PWG Rohwert Pedalwertgeber |
| armM_List | 12070B100F30 | 04 | 0x0F30 | 0x00 | 05 | 5 | -- | 0,1 | 0 | 0x00 | 0x00 | 6.2f | mg/Hub Luft |   | LAST | M_L aktuelle Luftmasse |
| armM_Lsoll | 12070B100F32 | 04 | 0x0F32 | 0x00 | 05 | 5 | -- | 0,1 | 0 | 0x00 | 0x00 | 6.2f | mg/Hub Luft |   | ARF_SOLLWERT | M_L Sollwert fuer ARF-Regelung |
| dimDIGprel_l | 12070B100F70 | 04 | 0x0F70 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - |   | DIMDIGPREL_LOW | Entprellte logische Zustaende d. digit. Eingaenge |
| dimDIGprel_h | 12070B100F71 | 04 | 0x0F71 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - |   | DIMDIGPREL_HIGH | Entprellte logische Zustaende d. digit. Eingaenge high |
| dzmNmit | 12070B100F10 | 04 | 0x0F10 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min |   | MOTORDREHZAHL | N Drehzahl (einfach gemittelt) |
| ehmFAKS | 12070B100E9A | 04 | 0x0E9A | 0x00 | 05 | 5 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | % |   | ABLUFTKLAPPE_TV | TV Ansteuerung Abluftlappensteuerung |
| ehmFARS | 12070B100E80 | 04 | 0x0E80 | 0x00 | 05 | 5 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | % |   | ARF_STELLER_TV | TV Ansteuerung ARF-Steller |
| ehmFLD_DK | 12070B100E81 | 04 | 0x0E81 | 0x00 | 05 | 5 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | % |   | LADEDRUCKSTELLER_TV | TV Ansteuerung Ladedrucksteller |
| ehmFMLS | 12070B100E98 | 04 | 0x0E98 | 0x00 | 05 | 5 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | % |   | E_LUEFTER_TV | TV Ansteuerung El.Motorluefter |
| fgm_VzuN | 12070B100F0B | 04 | 0x0F0B | 0x00 | 05 | 5 | -- | 0,00004 | 0 | 0x00 | 0x00 | 6.2f | (km/h)/(1/min) |   | V_ZU_N | V/N aktuelles Verhaeltnis Geschwindigkeit/Drehzahl |
| fgmBESCH | 12070B100F0A | 04 | 0x0F0A | 0x00 | 05 | 7 | -- | 0,08477 | 0 | 0x00 | 0x00 | 6.2f | m/s^2 |   | BESCHLEUNIGUNG | Beschleunigung |
| fgmFGAKT | 12070B100F08 | 04 | 0x0F08 | 0x00 | 05 | 5 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | km/h |   | GESCHWINDIGKEIT | V aktuelle Geschwindigkeit |
| ldmADF | 12070B100F41 | 04 | 0x0F41 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | hPa |   | ATMOSPHAERENDRUCK_?? | P_ADF aktueller Atmosphaerendruck (aus ADF oder LDF) |
| ldmP_Llin | 12070B100F40 | 04 | 0x0F40 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | hPa |   | LADEDRUCK_?? | P_L aktueller Ladedruck (gefiltert) / Luftdruck |
| mrmM_EXMSR | 12070B100F89 | 04 | 0x0F89 | 0x00 | 05 | 7 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | mg/Hub |   | MSR_EINGRIFF | M_E externer Momenteneingriff MSR |
| mrmM_EAKT | 12070B100F80 | 04 | 0x0F80 | 0x00 | 05 | 7 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | mg/Hub |   | EINSPRITZMENGE | M_E Aktuelle Einspritzmenge (ohne ARD) |
| mrmM_EBEGR | 12070B100F8A | 04 | 0x0F8A | 0x00 | 05 | 7 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | mg/Hub |   | BEGRENZUNGSMENGE | M_E resultierende Begrenzungsmenge |
| mrmM_EFGR | 12070B100F85 | 04 | 0x0F85 | 0x00 | 05 | 7 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | mg/Hub |   | WUNSCHMENGE_FGR | M_E Wunschmenge aus FGR |
| mrmM_ELLR | 12070B100F8D | 04 | 0x0F8D | 0x00 | 05 | 7 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | mg/Hub |   | EINSPRITZMENGE_LLR | M_E Menge aus Leerlaufreglung |
| mrmM_EMOT | 12070B100F8C | 04 | 0x0F8C | 0x00 | 05 | 7 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | mg/Hub |   | EINSPRITZMENGE_ARD | M_E Einspritzmenge nach ARD |
| mrmM_EPWG | 12070B100F84 | 04 | 0x0F84 | 0x00 | 05 | 7 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | mg/Hub |   | WUNSCHMENGE_PWG | M_E Wunschmenge = f(PWG) aus Fahrverhaltenkennfeld |
| mrmM_ESTAR | 12070B100F82 | 04 | 0x0F82 | 0x00 | 05 | 7 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | mg/Hub |   | STARTMENGE_SOLLWERT | M_E resultierender Startmengen-Sollwert |
| mrmM_EWUN | 12070B100F8B | 04 | 0x0F8B | 0x00 | 05 | 7 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | mg/Hub |   | FAHRERWUNSCHMENGE_N_EX_EINGRIFF | M_E Fahrerwunschmenge nach externem Mengeneingriff |
| mrmM_EWUNF | 12070B100F86 | 04 | 0x0F86 | 0x00 | 05 | 7 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | mg/Hub |   | FAHRERWUNSCHMENGE_PWG_FGR | M_E Fahrerwunschmenge aus PWG oder FGR |
| mrmN_LLBAS | 12070B100E02 | 04 | 0x0E02 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min |   | MOTORDREHZAHL_SOLL | N Leerlaufsolldrehzahl |
| mrmPWGfi | 12070B100F83 | 04 | 0x0F83 | 0x00 | 05 | 5 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | % |   | PWG_FAHRERWUNSCH | PWG gefilterte Pedalwertgeber-Position |
| mrmFG_SOLL | 12070B100F09 | 04 | 0x0F09 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | km/h |   | GESCHWINDIGKEIT_SOLLWERT | V Sollwert Fahrgeschwindigkeit fuer Diagnose |
| dzmN_SEK | 12070B100F11 | 04 | 0x0F11 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min |   | MOTORDREHZAHL_SEK | N Drehzahl aus Sekundaergeber |
| armPkorr | 12070B100F33 | 04 | 0x0F33 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | hPa |   | LADEDRUCK_KORR | P_L T_L-abhaengig korregierter Ladedruck |
| ldmP_Lsoll | 12070B100F34 | 04 | 0x0F34 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | hPa |   | LADEDRUCK_SOLLWERT | P_L Sollwert fuer Ladedruck |
| sbmPHIsoll | 12070B100F52 | 04 | 0x0F52 | 0x00 | 05 | 7 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | Grad KW |   | SB_SOLLWERT | SB Spritzbeginn-Sollwert |
| sbmPHIist | 12070B100F53 | 04 | 0x0F53 | 0x00 | 05 | 7 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | Grad KW |   | SB_ISTWERT | SB Spritzbeginn-Istwert |
| sbmWTF | 12070B100F54 | 04 | 0x0F54 | 0x00 | 05 | 5 | -- | 0,1 | -273,14 | 0x00 | 0x00 | 6.2f | Grad C |   | WTF_SGR | T_W Wassertemperatur fuer SBR |
| fnmFBKWSW | 12070B100F55 | 04 | 0x0F55 | 0x00 | 05 | 5 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | Grad KW |   | FB_KW_SW | FB-KW-Sollwinkel |
| fnmFBNWSW | 12070B100F56 | 04 | 0x0F56 | 0x00 | 05 | 5 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | Grad NW |   | FB_NW_SW | FB-NW-Sollwinkel |
| sboNAPI | 12070B100F57 | 04 | 0x0F57 | 0x00 | 05 | 7 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | Grad KW |   | PI_REGLER | SBR: PI-Regler-Ausgangswert |
| anmST_NBF | 12070B100F66 | 04 | 0x0F66 | 0x00 | 05 | 5 | -- | 53,37248 | 0 | 0x00 | 0x00 | 6.2f | mV |   | SIGNAL_NBF | U_NBF Spannungssignal aus NBF |
| mrmSTA_AGL | 12070B100F94 | 04 | 0x0F94 | 0x00 | 05 | 7 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | mg/Hub |   | STARTMENGEN_AGL | M_E Abgleichwert fuer Startmengenkorrektur |
| mrmBEG_AGL | 12070B100F95 | 04 | 0x0F95 | 0x00 | 05 | 5 | -- | 0,0001 | 0 | 0x00 | 0x00 | 6.2f | - |   | BEGRENZUNGSMENGE_AGL_FAKTOR | F_ME Abgleichfaktor fuer Begrenzungsmenge |
| mrmBM_EAKT | 12070B100F96 | 04 | 0x0F96 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - |   | UMSCH_BEG_K | Ext. Umschaltung auf Begrenzungs-Kl. |
| mrmM_EFAHR | 12070B100F97 | 04 | 0x0F97 | 0x00 | 05 | 7 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | mg/Hub |   | PUMPENMENGE_UNKOR | Pumpenmenge unkorregiert |
| mrmM_EKORR | 12070B100F98 | 04 | 0x0F98 | 0x00 | 05 | 7 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | mg/Hub |   | DUESENMENGE_KOR | Duesenkorrekturmenge |
| mrmM_EPUMP | 12070B100F99 | 04 | 0x0F99 | 0x00 | 05 | 7 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | mg/Hub |   | SOLLMENGE_VOR_UEB | M_E Soll-Menge vor Ueberwachung |
| mrmM_ESOLL | 12070B100F9A | 04 | 0x0F9A | 0x00 | 05 | 7 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | mg/Hub |   | SOLLMENGE_AN_PSG | M_E Soll-Menge an PSG |
| mrmMK_KL | 12070B100F9B | 04 | 0x0F9B | 0x00 | 05 | 5 | -- | 0,00391 | 0 | 0x00 | 0x00 | 6.2f | - |   | ME_KOR_ABW | Mengenkorrekturkennfeld.Abweichung |
| klmN_LLKLM | 12070B100E05 | 04 | 0x0E05 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min |   | DREHZAHLANHEBUNG_KO | Anhebung der Leerlaufdrehzahl bei Klimakompressor ein |
| pkmDZNW | 12070B100E10 | 04 | 0x0E10 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min NW |   | DREHZAHL_PSG | Drehzahl NW-bezogen (PSG-Drehzahl) |
| pkmT_PUMP | 12070B100E11 | 04 | 0x0E10 | 0x00 | 05 | 5 | -- | 0,1 | -273,14 | 0x00 | 0x00 | 6.2f | Grad C |   | TEMPERATUR_PUMPE | Pumpentemperatur |
| pkmPSGSTA | 12070B100E12 | 04 | 0x0E12 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - |   | PSG_STATUSWORT | PSG Statuswort |
| pkmPSG_ST | 12070B100E13 | 04 | 0x0E13 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - |   | PSG_SELBSTTEST | PSG Selbsttestergebnis |
| pkmADAUER | 12070B100E14 | 04 | 0x0E14 | 0x00 | 05 | 5 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | Grad NW |   | ANSTEUERDAUER_MV | Ansteuerdauer MV-Endstufe |
| pkmTOCNT | 12070B100E15 | 04 | 0x0E16 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - |   | KD_ANT_1 | Kundendienst-Antwort 1 |
| pkmKDANT_2 | 12070B100E17 | 04 | 0x0E17 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - |   | KD_ANT_2 | Kundendienst-Antwort 2 |
| pkmKDANT_3 | 12070B100E18 | 04 | 0x0E18 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - |   | KD_ANT_3 | Kundendienst-Antwort 3 |
| pkmKDANT_4 | 12070B100E19 | 04 | 0x0E19 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - |   | KD_ANT_4 | Kundendienst-Antwort 4 |
| ehmFGRS | 12070B100E87 | 04 | 0x0E87 | 0x00 | 05 | 5 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | % |   | ANST_GLUEHREL_TV | TV Ansteuerung Gluehrelaissteller |
| ehmFVFP | 12070B100E91 | 04 | 0x0E91 | 0x00 | 05 | 5 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | % |   | ANST_VOR_PUMPE_TV | TV Ansteuerung - Vorfoerderpumpe |
| ehmFGAZ | 12070B100E94 | 04 | 0x0E94 | 0x00 | 05 | 5 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | % |   | ANST_GLUEHANZ_TV | TV Anteuerung Gluehanzeige |
| ehmFDIA | 12070B100E96 | 04 | 0x0E96 | 0x00 | 05 | 5 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | % |   | ANST_DIG_LAMPE_TV | TV Ansteuerung Diagnoselampe |
| ehmFSKOREL | 12070B100E99 | 04 | 0x0E99 | 0x00 | 05 | 5 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | % |   | ANST_KO_TV | TV Ansteuerung Klimakompressor |
| mroM_ERBK | 12070B100ECB | 04 | 0x0ECB | 0x00 | 05 | 7 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | mg/Hub |   | REIBMENGE_N_KL_L_KOMP | Reibmenge nach Klimalastmomentkompensation |
| fbmBSTZ_UB | 12070B10FFFE | 04 | 0xFFFE | 0x00 | 05 | 5 | -- | 0,1 | 0 | 0x00 | 0x00 | 6.2f | h |   | BETR_STUNDENZAEHLER | UB akt. Betriebsstundenzaehler |
| dimDIG_2 | 12070B100F72 | 04 | 0x0F72 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - |   | DIMDIG_2 | MFL und CAN Digitaleingaenge |
| mrmM_E_VE | 12070B100F9C | 04 | 0x0F9C | 0x00 | 05 | 7 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | mg/Hub |   | MENGE_VE | M_E Voreinspritzmenge |
| ehmFDSL | 12070B100E93 | 04 | 0x0E93 | 0x00 | 05 | 5 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | % |   | ANST_MOTORLAGER_TV | TV Ansteuerung - Motorlager |
| ehmFKWH | 12070B100E9B | 04 | 0x0E9B | 0x00 | 05 | 5 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | % |   | ANST_KUEHLWASSERHEIZUNG_TV | TV Ansteuerung - Kuehlwasserheizung |
| khoNOR_AB | 12070B100FB7 | 04 | 0x0FB7 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - |   | KWH_AB | Abbruchbedingungen Kuehlwasserheizung |
| mrmM_EDELB | 12070B101F8E | 04 | 0x1F8E | 0x00 | 05 | 7 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | mg/Hub |   | MRMM_EDELB | M_E begrenzte Abgleichmenge |
| comGTR_opt | 12070B101C00 | 04 | 0x1C00 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - |   | COMGTR_OPT | Identifikation Handschalter/Automatik |
| mroFGR_ABN | 12070B10DF08 | 04 | 0xDF08 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - |   | MROFGR_ABN | FGR Abschalt-Bedingungen |
| khoGENLAST | 12070B100ECC | 04 | 0x0ECC | 0x00 | 05 | 5 | -- | 0,01 | 0 | 0x00 | 0x00 | 6.2f | % |   | KHOGENLAST | Generatorlast |
| aroREG_2 | 12070B100EE0 | 04 | 0x0EE0 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - |   | AROREG_2 | AGR-Status  Regelung / Steuerung / Abschaltung |
| ldoRG_BER | 12070B100F45 | 04 | 0x0F45 | 0x00 | 05 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - |   | LDORG_BER | Status Ladedruckregelung |

<a id="table-bits"></a>
### BITS

Dimensions: 12 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| S_PWGL | 0 | 0x01 | 0x01 |
| S_BRL | 1 | 0x80 | 0x80 |
| S_BRT | 0 | 0x10 | 0x10 |
| S_PN | 1 | 0x40 | 0x40 |
| S_DIA | 0 | 0x40 | 0x40 |
| S_AC | 2 | 0x01 | 0x01 |
| S_KO | 2 | 0x02 | 0x02 |
| S_MFLAUS | 3 | 0x20 | 0x20 |
| S_MFLTGL | 3 | 0x80 | 0x80 |
| S_MFLEINP | 3 | 0x12 | 0x12 |
| S_MFLEINM | 3 | 0x40 | 0x40 |
| S_MFLWA | 3 | 0x09 | 0x09 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 48 rows × 4 columns

| ORT | ORTTEXT | UW_1 | UW_2 |
| --- | --- | --- | --- |
| 0x00 | -- | 0x00 | 0x00 |
| 0x01 | Mengensteller (wird z. Zt. nicht verwendet) | 0x01 | 0x02 |
| 0x03 | Elektrisches Abschaltventil ELAB (wird z. Zt. nicht verwendet) | 0x01 | 0x03 |
| 0x05 | Nadelbewegungsfuehler | 0x02 | 0x07 |
| 0x06 | Abgasrueckfuehr-Regelung | 0x02 | 0x07 |
| 0x08 | Gluehanlage | 0x02 | 0x07 |
| 0x0A | Regelung Spritzbeginn | 0x02 | 0x01 |
| 0x10 | Versorgungsspannung | 0x02 | 0x07 |
| 0x11 | Steuergeraet DDE (U_REF 2.5V) | 0x02 | 0x08 |
| 0x12 | Klemme 15 | 0x02 | 0x08 |
| 0x13 | DDE-Hauptrelais | 0x02 | 0x08 |
| 0x1A | Bremslicht / Bremstestschalter | 0x02 | 0x07 |
| 0x1B | Kuehlmittelheizung | 0x02 | 0x08 |
| 0x1C | Kupplungsschalter | 0x02 | 0x07 |
| 0x1D | Fahrgeschwindigkeitssignal | 0x02 | 0x07 |
| 0x20 | Bedienteil Fahrgeschwindigkeitsregelung | 0x02 | 0x07 |
| 0x23 | Fuehler Kraftstofftemperatur (in Einspritzpumpe verbaut) | 0x02 | 0x01 |
| 0x24 | Temperaturfuehler Motoroel (wird z. Zt. nicht verwendet) | 0x02 | 0x04 |
| 0x25 | Pedalwertgeber | 0x02 | 0x07 |
| 0x26 | Luftmassenmesser | 0x02 | 0x07 |
| 0x2D | Elektronische Wegfahrsperre (EWS) | 0x08 | 0x09 |
| 0x2E | Drehzahlgeber Einspritzpumpe (in Pumpe, nicht extra zu tauschen) | 0x02 | 0x06 |
| 0x2F | Drehzahlgeber Kurbelwelle | 0x03 | 0x07 |
| 0x34 | Fuehler Lufttemperatur (wird z. Zt. nicht verwendet) | 0x02 | 0x04 |
| 0x35 | Fuehler Motorkuehlmitteltemperatur | 0x02 | 0x06 |
| 0x36 | Ladedruckfuehler | 0x02 | 0x01 |
| 0x40 | Steuergeraet DDE (Microcontroller) | 0x02 | 0x07 |
| 0x41 | Einspritzpumpe Magnet-Abschalt-Ventil (MAB) | 0x02 | 0x06 |
| 0x42 | Steuergeraet DDE (EEPROM und Konfiguration) | 0x02 | 0x07 |
| 0x43 | Steuergeraet Einspritzpumpe | 0x02 | 0x06 |
| 0x44 | Magnetventil Einspritzmenge | 0x02 | 0x06 |
| 0x45 | Steuergeraet DDE (CAN-Controller) | 0x02 | 0x08 |
| 0x46 | Steuergeraet Einspritzpumpe (Kommunikation) | 0x02 | 0x06 |
| 0x47 | Synchronitaet der Drehzahlgeber | 0x02 | 0x06 |
| 0x48 | Spritzversteller-Regelung | 0x02 | 0x01 |
| 0x49 | Drehzahlgeber Einspritzpumpe (IWZ-System) | 0x02 | 0x06 |
| 0x50 | Motorlagersteuerung | 0x02 | 0x07 |
| 0x52 | Elektroluefter | 0x08 | 0x07 |
| 0x56 | Kuehlerjalousie | 0x08 | 0x07 |
| 0x65 | Lader-Regelung | 0x02 | 0x04 |
| 0x6B | Atmosphaerendruckfuehler (im Steuergeraet verbaut) | 0x02 | 0x05 |
| 0x72 | CAN-Bus | 0x02 | 0x08 |
| 0x73 | Kraftstoffvorfoerderpumpe | 0x07 | 0x08 |
| 0x74 | Relais Klimakompressor | 0x07 | 0x08 |
| 0x75 | Generatorlastsignal | 0x02 | 0x08 |
| 0x76 | Tankfuellstandsinfo | 0x02 | 0x08 |
| 0x77 | Umgebungstemperatur | 0x02 | 0x08 |
| 0xXY | unbekannter Fehlerort | 0x00 | 0x00 |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 47 rows × 17 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 | A6_0 | A6_1 | A7_0 | A7_1 | A8_0 | A8_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x01 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x03 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x05 | 0x00 | 0x00 | 0x00 | 0x76 | 0x00 | 0x75 | 0x00 | 0x89 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x06 | 0x00 | 0x85 | 0x00 | 0x00 | 0x00 | 0x86 | 0x00 | 0x27 | 0x00 | 0x28 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x08 | 0x00 | 0x83 | 0x00 | 0x00 | 0x00 | 0x84 | 0x00 | 0x32 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x0A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x81 | 0x00 | 0x82 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x10 | 0x00 | 0x00 | 0x00 | 0x74 | 0x00 | 0x73 | 0x00 | 0x14 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x11 | 0x00 | 0x00 | 0x00 | 0x79 | 0x00 | 0x80 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x12 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x48 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x13 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x37 | 0x00 | 0x00 | 0x00 | 0x38 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x1A | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x33 | 0x00 | 0x00 | 0x00 | 0x34 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x1B | 0x00 | 0x83 | 0x00 | 0x00 | 0x00 | 0x84 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x1C | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x70 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x1D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x69 | 0x00 | 0x25 | 0x00 | 0x94 | 0x00 | 0x26 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x20 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x78 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x23 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x57 | 0x00 | 0x58 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x24 | 0x00 | 0x00 | 0x00 | 0x02 | 0x00 | 0x01 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x25 | 0x00 | 0x02 | 0x00 | 0x01 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x19 | 0x00 | 0x20 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x26 | 0x00 | 0x00 | 0x00 | 0x02 | 0x00 | 0x01 | 0x00 | 0x23 | 0x00 | 0x12 | 0x00 | 0x13 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x2D | 0x00 | 0x64 | 0x00 | 0x65 | 0x00 | 0x66 | 0x00 | 0x67 | 0x00 | 0x68 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x2E | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x2F | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x00 | 0x17 | 0x00 | 0x18 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x34 | 0x00 | 0x00 | 0x00 | 0x02 | 0x00 | 0x01 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x35 | 0x00 | 0x00 | 0x00 | 0x76 | 0x00 | 0x75 | 0x00 | 0x21 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x36 | 0x00 | 0x00 | 0x00 | 0x02 | 0x00 | 0x01 | 0x00 | 0x22 | 0x00 | 0x12 | 0x00 | 0x13 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x40 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x95 | 0x00 | 0x24 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x41 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x29 | 0x00 | 0x30 | 0x00 | 0x96 | 0x00 | 0x31 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x42 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x90 | 0x00 | 0x35 | 0x00 | 0x77 | 0x00 | 0x36 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x43 | 0x00 | 0x39 | 0x00 | 0x40 | 0x00 | 0x41 | 0x00 | 0x42 | 0x00 | 0x43 | 0x00 | 0x44 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x44 | 0x00 | 0x00 | 0x00 | 0x47 | 0x00 | 0x00 | 0x00 | 0x46 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x45 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x49 | 0x00 | 0x00 | 0x00 | 0x50 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x46 | 0x00 | 0x00 | 0x00 | 0x51 | 0x00 | 0x00 | 0x00 | 0x52 | 0x00 | 0x00 | 0x00 | 0x53 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x47 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x54 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x48 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x55 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x49 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x56 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x50 | 0x00 | 0x83 | 0x00 | 0x00 | 0x00 | 0x84 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x52 | 0x00 | 0x83 | 0x00 | 0x00 | 0x00 | 0x84 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x56 | 0x00 | 0x83 | 0x00 | 0x00 | 0x00 | 0x84 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x65 | 0x00 | 0x85 | 0x00 | 0x00 | 0x00 | 0x86 | 0x00 | 0x87 | 0x00 | 0x88 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x6B | 0x00 | 0x00 | 0x00 | 0x02 | 0x00 | 0x01 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x72 | 0x00 | 0x59 | 0x00 | 0x60 | 0x00 | 0x61 | 0x00 | 0x62 | 0x00 | 0x63 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x73 | 0x00 | 0x83 | 0x00 | 0x84 | 0x00 | 0x84 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x74 | 0x00 | 0x83 | 0x00 | 0x84 | 0x00 | 0x84 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x75 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x92 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x76 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x93 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |
| 0x77 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x97 | 0x00 | 0x00 | 0x00 | 0x00 | 0x06 | 0x05 | 0x00 | 0x07 |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 97 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | Signal Kurzschluss nach B+ |
| 0x02 | Signal Unterbrechung oder KS nach B- |
| 0x03 | Unterbrechung |
| 0x04 | Zustand nicht plausibel |
| 0x05 | Fehler momentan vorhanden |
| 0x06 | Fehler momentan nicht vorhanden |
| 0x07 | Fehler sporadisch |
| 0x08 | Signal-Range-Check nach unten verletzt |
| 0x09 | Signal-Range-Check nach oben verletzt |
| 0x10 | Schleifer Signal-Range-Check nach unten verletzt |
| 0x11 | Schleifer Signal-Range-Check nach oben verletzt |
| 0x12 | Versorgungsspannung Kurzschluss nach B- |
| 0x13 | Versorgungsspannung Kurzschluss nach B+ |
| 0x14 | Versorgungsspannung Einspritzpumpe ueber- / unterschritten |
| 0x15 | Ueberdrehzahlerkennung |
| 0x16 | Plausibilitaet mit Ladedruck |
| 0x17 | Drehzahlaenderung unplausibel |
| 0x18 | Plausibilitaet mit Drehzahlgeber Einspritzpumpe |
| 0x19 | PWG Plausibilitaet mit Bremssignal (wegappliziert) |
| 0x20 | PWG Plausibilitaet mit Leergasschalter |
| 0x21 | Kuehlmitteltemperatur nicht erreicht (wegappliziert) |
| 0x22 | Plausibilitaet mit Atmosphaerendruckfuehler bei Leerlauf |
| 0x23 | Luftmasse zu gering |
| 0x24 | Microcontroller (Gate-Array) |
| 0x25 | Signal fehlerhaft |
| 0x26 | Plausibilitaet mit Einspritzmenge und Motordrehzahl |
| 0x27 | Positive Regelabweichung / Luftmasse zu niedrig |
| 0x28 | Negative Regelabweichung / Luftmasse zu hoch |
| 0x29 | Abschaltung defekt |
| 0x30 | dauernd freigeschaltet |
| 0x31 | dauernd gesperrt |
| 0x32 | Gluehkerzen bzw. Gluehrelais defekt |
| 0x33 | Plausibilitaet der Bremssignale nach Zuendung Ein |
| 0x34 | Plausibilitaet der Bremssignale im Fahrbetrieb |
| 0x35 | Allgemeine Abgleich Checksumme |
| 0x36 | Kommunikation mit EEPROM |
| 0x37 | Relais schaltet zu frueh ab |
| 0x38 | Relais schaltet zu spaet ab |
| 0x39 | Ansteuerdauer-Ueberwachung |
| 0x40 | Vergleich der Drehzahl Kurbelwelle zu Drehzahl Einspritzpumpe |
| 0x41 | Kein Pumpenkennfeld programmiert oder PSG-RAM defekt |
| 0x42 | Pumpensteuergeraet-EEPROM oder ADC defekt |
| 0x43 | Mengenendstufe fehlerhaft |
| 0x44 | CAN Botschaft - Pumpensteuergeraet Timeout |
| 0x46 | allgemeiner Fehler |
| 0x47 | dauernd bestromt |
| 0x48 | Zuendstellung 2 Plausibilitaet nach Steuergeraet-Initialisierung |
| 0x49 | CAN-Bus abgeschaltet |
| 0x50 | CAN-Bus Baustein defekt |
| 0x51 | CAN-Bus allgemeiner Fehler |
| 0x52 | CAN-Bus Empfangsfehler |
| 0x53 | CAN-Bus Sendefehler |
| 0x54 | Drehzahlgeber Kurbelwelle und Einspritzpumpe nicht synchron zueinander |
| 0x55 | Lageregelung um +/- 3 Grad KW falsch |
| 0x56 | Drehzahlgeber Einspritzpumpe defekt |
| 0x57 | Uebertemperatur im Pumpensteuergeraet erkannt |
| 0x58 | Signal-Range-Fehler |
| 0x59 | Empfangsfehler Elektronische Getriebesteuerung (EGS) |
| 0x60 | Empfangsfehler Antriebsschlupfregelung (ASR) |
| 0x61 | Empfangsfehler Motorschleppmomentregelung (MSR) |
| 0x62 | Empfangsfehler Combi-Instrument |
| 0x63 | Timeout Botschaft Antriebsschlupfregelung (ASR) |
| 0x64 | EWS -Signal plausibel, jedoch Wechselcode (WC) falsch |
| 0x65 | EWS -Signal nicht plausibel |
| 0x66 | kein EWS-Signal vorhanden |
| 0x67 | Urcode (UC) im EEPROM defekt |
| 0x68 | Wechselcode (WC) im EEPROM defekt |
| 0x69 | Geschwindigkeit zu gross |
| 0x70 | Plausibilitaet mit Fahrgeschwindigkeit |
| 0x71 | PWG Plausibilitaet mit Leergasschalter (wegappliziert) |
| 0x72 | PWG Plausibilitaet mit Poti (wegappliziert) |
| 0x73 | Versorgungsspannung DDE ueberschritten |
| 0x74 | Versorgungsspannung DDE unterschritten |
| 0x75 | Signal Unterbrechung oder KS nach B+ |
| 0x76 | Signal Kurzschluss nach B- |
| 0x77 | Mengenabgleich Checksumme |
| 0x78 | Signal von Multifunktions-Lenkrad fehlerhaft |
| 0x79 | Referenzspannung Unterbrechung oder KS nach B- |
| 0x80 | Referenzspannung Kurzschluss nach B+ |
| 0x81 | Positive Regelabweichung / Spritzbeginn ist um mehr als 2 Grad KW zu frueh |
| 0x82 | Negative Regelabweichung / Spritzbeginn ist um mehr als 2 Grad KW zu spaet |
| 0x83 | Ansteuerung Kurzschluss nach B+ |
| 0x84 | Ansteuerung Unterbrechung oder KS nach B- |
| 0x85 | Ansteuerung Magnetventil Kurzschluss nach B+ |
| 0x86 | Ansteuerung Magnetventil Unterbrechung oder KS nach B- |
| 0x87 | Positive Regelabweichung / Ladedruck zu niedrig |
| 0x88 | Negative Regelabweichung / Ladedruck zu hoch |
| 0x89 | Plausibilitaet mit Drehzahlgeber-Impulsen |
| 0x90 | Mengendriftkompensation(EEPROM Checksumme) |
| 0x92 | Generatorlast 0% |
| 0x93 | Tankfuellstandsinfo von CAN |
| 0x94 | Fahrgeschwindigkeit von CAN ungueltig |
| 0x95 | Redundante Schubueberwachung |
| 0x96 | Microcontroller - GateArray Abschaltung defekt |
| 0x97 | Fehlererkennung |
| 0xFF | unbekannte Fehlerart |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 11 rows × 5 columns

| UWNR | UWTEXT | UW_EINH | UWF_A | UWF_B |
| --- | --- | --- | --- | --- |
| 0x00 | ----   | ---- | 1 | 0 |
| 0x01 | Einspritzmenge | [mg/Hub] | 0.3922 | 0 |
| 0x02 | Motordrehzahl | [1/min] | 23.5 | 0 |
| 0x03 | Motordrehzahl Einspritzpumpe | [1/min] | 23.5 | 0 |
| 0x04 | Ladedruck | [mbar] | 13.725 | 0 |
| 0x05 | Lufttemperatur | [Grad C] | 1 | -40 |
| 0x06 | Kraftstofftemperatur Einspritzpumpe | [Grad C] | 1 | -40 |
| 0x07 | Kuehlmitteltemperatur | [Grad C] | 1 | -40 |
| 0x08 | Batteriespannung | [V] | 0.09986 | 0 |
| 0x09 | Anzahl fehlerhafte EWS-Uebertragungen | [1] | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | -- | 1 | 0 |

<a id="table-shadowfehler"></a>
### SHADOWFEHLER

Dimensions: 12 rows × 4 columns

| SH_FE | SH_0 | SH_1 | SH_2 |
| --- | --- | --- | --- |
| 0x20 | 0x04 | 0x00 | 0x00 |
| 0x13 | 0x08 | 0x20 | 0x00 |
| 0x41 | 0x04 | 0x08 | 0x00 |
| 0x2D | 0x04 | 0x00 | 0x00 |
| 0x08 | 0x08 | 0x00 | 0x00 |
| 0x73 | 0x01 | 0x04 | 0x00 |
| 0x44 | 0x02 | 0x00 | 0x00 |
| 0x74 | 0x01 | 0x04 | 0x00 |
| 0x42 | 0x04 | 0x10 | 0x00 |
| 0x12 | 0x08 | 0x20 | 0x00 |
| 0x43 | 0x02 | 0x08 | 0x10 |
| 0xXY | 0xFF | 0xFF | 0xFF |

<a id="table-bitskho"></a>
### BITSKHO

Dimensions: 9 rows × 9 columns

| TELNAME | TELEGRAMM | NAME | BYTE | MASK | VALUE | LNAME | TEXT_0 | TEXT_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| khoNOR_AB | 0FB7 | S_KWH_WTF | 6 | 0x01 | 0x01 | Abschaltbedingung Kuehlmittelheizung | io | Wassertemperatur ausreichend |
| khoNOR_AB | 0FB7 | S_KWH_GEN1 | 6 | 0x02 | 0x02 | Abschaltbedingung Kuehlmittelheizung | io | Generatorlastfehler |
| khoNOR_AB | 0FB7 | S_KWH_UBATT | 6 | 0x04 | 0x04 | Abschaltbedingung Kuehlmittelheizung | io | Batteriespannung zu niedrig |
| khoNOR_AB | 0FB7 | S_KWH_N | 6 | 0x08 | 0x08 | Abschaltbedingung Kuehlmittelheizung | io | Motordrehzahl zu niedrig |
| khoNOR_AB | 0FB7 | S_KWH_START | 6 | 0x10 | 0x10 | Abschaltbedingung Kuehlmittelheizung | io | Startverzoegerung aktiv |
| khoNOR_AB | 0FB7 | S_KWH_SENSDEF | 6 | 0x20 | 0x20 | Abschaltbedingung Kuehlmittelheizung | io | WTF, UTF oder Endstufe defekt |
| khoNOR_AB | 0FB7 | S_KWH_IKHA | 6 | 0x80 | 0x80 | Abschaltbedingung Kuehlmittelheizung | io | keine Heizleistungsanforderung von IHKA |
| khoNOR_AB | 0FB7 | S_KWH_GENSRC | 5 | 0x08 | 0x08 | Abschaltbedingung Kuehlmittelheizung | io | Generatorlast Null Prozent |
| khoNOR_AB | 0FB7 | S_KWH_APPL | 5 | 0x80 | 0x80 | Abschaltbedingung Kuehlmittelheizung | io | Wegappliziert |

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 39 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0x01 | AIF_NICHT_PROGRAMMIERT |
| 0x02 | ERROR_ANSTEUERARGUMENT_FEHLT |
| 0x03 | ERROR_ECU_ABGLEICHMENGE_PROGRAMMIEREN |
| 0x04 | ERROR_ECU_ABGLEICHMENGE_CHECKSUMME_VORGEBEN |
| 0x05 | ERROR_ECU_ABGLEICHMENGE_CHECKSUMME_PROGRAMMIEREN |
| 0x06 | ERROR_ANZAHL_OUT_OF_RANGE |
| 0x07 | ERROR_ARGUMENT_ANZAHL |
| 0x08 | ERROR_DATEN_WRONG_FORMAT |
| 0x09 | ERROR_DATEN_OUT_OF_RANGE |
| 0x0A | ERROR_PZ_IN_WRONG_FORMAT |
| 0x0B | ERROR_WRONG_PZ |
| 0x0C | ERROR_ARGUMENT_DATEN_LAENGE |
| 0x0D | ERROR_ARGUMENT_DATEN |
| 0x0F | ERROR_ECU_ABGLEICHMENGE_CHECKSUMME_VORGEBEN |
| 0x10 | ERROR_ECU_ABGLEICHMENGE_CHECKSUMME_PROGRAMMIEREN |
| 0x11 | ERROR_WRONG_ARGUMENT |
| 0x12 | ERROR_WRONG_VALUE |
| 0x13 | ERROR_NO_ARGUMENT |
| 0x14 | ERROR_PARAMETER_ABGLEICH_VERSTELLEN_FGR_VERBAUT |
| 0x15 | ERROR_PARAMETER_ABGLEICH_VERSTELLEN_KLIMAANLAGE_VERBAUT |
| 0x16 | ERROR_ECU_MENGENDRIFT_PROGRAMMIEREN |
| 0x17 | ERROR_ECU_MENGENDRIFT_CHECKSUMME_VORGEBEN |
| 0x18 | ERROR_ECU_MENGENDRIFT_CHECKSUMME_PROGRAMMIEREN |
| 0x19 | ERROR_PARAMETER_ABGLEICH_TIMER_VERSTELLEN_PROGRAMMIEREN_VERBAUT |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xB2 | ERROR_ECU_NUMBER |
| 0xFF | ERROR_ECU_NACK |
| 0x55 | ERROR_ECU_FUNCTION_EINZELNE_STELLGLIEDANSTEUERUNG_WIRD_AUFGEHOBEN |
| 0xAA | ERROR_ECU_FUNCTION_ALLE_STELLGLIEDANSTEUERUNGEN_WERDEN_AUFGEHOBEN |
| 0xF0 | ERROR_ECU_FUNCTION_UEBERGABEPARAMETER_UNGUELTIG |
| 0xF1 | ERROR_ECU_FUNCTION_MESSAGE_NR_UNGUELTIG |
| 0xF2 | ERROR_ECU_FUNCTION_ANSTEUERBEDINGUNG_NICHT_ERFUELLT |
| 0xF3 | ERROR_ECU_FUNCTION_ZU_VIELE_STELLGLIED_EINGRIFFE_AKTIV |
| 0xF4 | ERROR_ECU_FUNCTION_TASTVERHAELTNIS_UNGUELTIG |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |
