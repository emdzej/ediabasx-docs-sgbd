# DDE41KL0.prg

- Jobs: [157](#jobs)
- Tables: [6](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | DDE 4.1 fuer M67 Slave |
| ORIGIN | BMW TI-433 Schiefer |
| REVISION | 1.00 |
| AUTHOR | BMW ZM-E-31 Lexmueller, BMW TI-433 Schiefer, BMW TI-433 Schaller |
| COMMENT | N/A |
| PACKAGE | 1.24 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [initialisierung](#job-initialisierung) - Default Init-Job
- [IDENT](#job-ident) - Ident-Daten fuer DME
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender-Info-Feldes
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [TEL_ROH](#job-tel-roh) - Rohtelegramm ohne Header lesen
- [SEED_KEY](#job-seed-key) - Schutzmechanismus SEED_KEY
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers
- [FS_SHADOW_LESEN](#job-fs-shadow-lesen) - Auslesen des Fehlerspeichers
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [FS_LESEN_STATUS](#job-fs-lesen-status) - Auslesen des Fehlerspeichers
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Kennung M_ABGLEICH_FLAG lesen
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Kennung M_ABGLEICH_FLAG lesen
- [MW_SELECT_LESEN](#job-mw-select-lesen) - Messwerteblock selectiv lesen
- [MW_SELECT_LESEN_NORM](#job-mw-select-lesen-norm) - Messwerteblock selectiv lesen
- [MW_SELECT_LESEN_NORM_EINZEL](#job-mw-select-lesen-norm-einzel) - Messwerteblock selectiv lesen
- [STATUS_SYNC_MODE](#job-status-sync-mode)
- [STEUERN_SYNC_MODE](#job-steuern-sync-mode)
- [ABGLEICH_LESEN_LL_REGELUNG](#job-abgleich-lesen-ll-regelung) - LL-Regelung-Abgleich lesen
- [ABGLEICH_VERSTELLEN_LL_REGELUNG](#job-abgleich-verstellen-ll-regelung) - LL_REGELUNG Abgleich verstellen
- [ABGLEICH_PROG_LL_REGELUNG](#job-abgleich-prog-ll-regelung) - LL_REGELUNG Abgleich programmieren
- [ABGLEICH_LESEN_VOLL_MENGE](#job-abgleich-lesen-voll-menge) - BEGR_MENGEn-Abgleich lesen
- [ABGLEICH_LESEN_VOLL_MENGE_ROH](#job-abgleich-lesen-voll-menge-roh) - Vollastmenge-Abgleich lesen
- [ABGLEICH_VERSTELLEN_VOLL_MENGE_ROH](#job-abgleich-verstellen-voll-menge-roh) - Vollastmenge-Abgleich verstellen
- [ABGLEICH_VERSTELLEN_VOLL_MENGE](#job-abgleich-verstellen-voll-menge) - BEGR_MENGE Abgleich verstellen
- [ABGLEICH_PROG_VOLL_MENGE](#job-abgleich-prog-voll-menge) - BEGR_MENGE Abgleich programmieren
- [ABGLEICH_LESEN_ABGLEICHMENGE](#job-abgleich-lesen-abgleichmenge) - LADEDRUCK-Abgleich lesen
- [ABGLEICH_VERSTELLEN_ABGLEICHMENGE](#job-abgleich-verstellen-abgleichmenge) - LADEDRUCK Abgleich verstellen
- [ABGLEICH_PROG_ABGLEICHMENGE](#job-abgleich-prog-abgleichmenge) - LADEDRUCK Abgleich programmieren
- [HOLE_EMA_FELD](#job-hole-ema-feld)
- [ABGLEICHWERTE_LESEN](#job-abgleichwerte-lesen) - Lesen der Motorabgleichwerte
- [ABGLEICHWERTE_SCHREIBEN](#job-abgleichwerte-schreiben) - Beschreiben des internen Speichers mit den motorspezifischen Abgleichdaten
- [ABGLEICH_LESEN_ABGLEICH_FLAG](#job-abgleich-lesen-abgleich-flag) - Kennung M_ABGLEICH_FLAG lesen
- [ABGLEICH_VERSTELLEN_ABGLEICH_FLAG](#job-abgleich-verstellen-abgleich-flag) - Kennung M_ABGLEICH_FLAG verstellen, 0 = nicht verbaut, 0xff = verbaut
- [ABGLEICH_PROG_ABGLEICH_FLAG](#job-abgleich-prog-abgleich-flag) - Kennung M_ABGLEICH_FLAG programmieren
- [ABGLEICHFLAG_LESEN](#job-abgleichflag-lesen) - Lesen des EEPROM-Speichers ab Adresse 0x0032
- [ABGLEICH_LESEN_MENGENDRIFT](#job-abgleich-lesen-mengendrift) - Mengendrift-Abgleich lesen
- [ABGLEICH_VERSTELLEN_MENGENDRIFT](#job-abgleich-verstellen-mengendrift) - Mengendrift Abgleich verstellen
- [ABGLEICH_PROG_MENGENDRIFT](#job-abgleich-prog-mengendrift) - LADEDRUCK Abgleich programmieren
- [ABGLEICH_KIC_VERSTELLEN_PROGRAMMIEREN](#job-abgleich-kic-verstellen-programmieren) - Uebertragung KIC Ein- oder Ausschalten
- [STEUERN_AGR_STELLER1](#job-steuern-agr-steller1) - ARF - Steller1  ansteuern ,  - - 10%%
- [STEUERN_AGR_STELLER2](#job-steuern-agr-steller2) - ARF - Steller2  ansteuern ,  - - 10%%
- [STEUERN_KS_HDPUMPE_ABSCHALTUNG](#job-steuern-ks-hdpumpe-abschaltung) - Elektrisches Abschaltventil ansteuern ,  0 oder 1
- [START_SYSTEMCHECK_ZYL_SEL_DREHZAHL](#job-start-systemcheck-zyl-sel-drehzahl) - Start zylinderselektive Drehzhahlen lesen
- [START_SYSTEMCHECK_ZYL_SEL_MENGENKOR](#job-start-systemcheck-zyl-sel-mengenkor) - Start zylinderselektive Mengenkorrekturen
- [STOP_SYSTEMCHECK](#job-stop-systemcheck) - Stop Systemtest
- [STATUS_LAUFUNRUHE_LLR_MENGE](#job-status-laufunruhe-llr-menge) - Auslesen selektive Mengenkorrektur
- [STATUS_LAUFUNRUHE_DREHZAHL](#job-status-laufunruhe-drehzahl) - Auslesen selektive Mengenkorrektur
- [ECU_CONFIG](#job-ecu-config) - Ident-Daten fuer DME
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Indentifikation, AIF, FS_Codes ShadowFS_Codes, ShadowFS_lang
- [STATUS_ANMUBT](#job-status-anmubt) - UBT Batteriespannung
- [STATUS_ANMVDF](#job-status-anmvdf) - VDF Vorfoerderdruck
- [STATUS_ANMWTF](#job-status-anmwtf) - WTF Wassertemperatur
- [STATUS_DZMNAKT](#job-status-dzmnakt) - N aktuelle Drehzahl aus letzter Periode
- [STATUS_EHMFARS1](#job-status-ehmfars1) - Tastverhaeltnis Ansteuerung Abgasrueckfuehrsteller 1
- [STATUS_EHMFARS2](#job-status-ehmfars2) - Tastverhaeltnis Ansteuerung Abgasrueckfuehrsteller 2
- [STATUS_EHMFKDR](#job-status-ehmfkdr) - Tastverhaeltnis Ansteuerung Raildruckregelventil
- [STATUS_ZUMP_RAIL](#job-status-zump-rail) - Raildruck fuer Mengenzumessung
- [STATUS_ZUMPQSOLL](#job-status-zumpqsoll) - Raildruck Sollwert
- [STATUS_ADMIDV](#job-status-admidv) - IDV Rohwert Istwert Stromregelung Druckregelventil
- [STATUS_ADMKDF](#job-status-admkdf) - KDF Rohwert Raildruck
- [STATUS_ADMLDF1](#job-status-admldf1) - LDF Rohwert Ladedruck
- [STATUS_ADMLMM1](#job-status-admlmm1) - LMM1 Rohwert Luftmasse 1
- [STATUS_ADMLTF1](#job-status-admltf1) - LTF1 Rohwert Lufttemperatur 1
- [STATUS_ADMUBT](#job-status-admubt) - UBT Rohwert Batteriespannung
- [STATUS_ADMUC1](#job-status-admuc1) - UC1 Rohwert Kondensatorspannung 1 fuer Zylinder 1 und 6
- [STATUS_ADMUC2](#job-status-admuc2) - UC2 Rohwert Kondensatorspannung 2 fuer Zylinder 4 und 7
- [STATUS_ADMUG1](#job-status-admug1) - UG1 Rohwert Speisespannung 1 fuer Luftmassenmesser 1, Ladedruckfuehler 1
- [STATUS_ADMUG2](#job-status-admug2) - UG2 Rohwert Speisespannung 2 fuer Raildrucksensor
- [STATUS_ANMIDV](#job-status-anmidv) - IDV Istwert Stromregelung Druckregelventil
- [STATUS_ANMKDF](#job-status-anmkdf) - KDF Raildruck
- [STATUS_ANMLDF1](#job-status-anmldf1) - LDF Ladedruck
- [STATUS_ANMLMM1](#job-status-anmlmm1) - LMM1 Luftmasse 1
- [STATUS_ANMLTF1](#job-status-anmltf1) - LTF1 Lufttemperatur 1
- [STATUS_ANMLTF2](#job-status-anmltf2) - LTF2 Lufttemperatur 2
- [STATUS_ANMUC1](#job-status-anmuc1) - UC1 Kondensatorspannung 1 fuer Zylinder 1 und 6
- [STATUS_ANMUC2](#job-status-anmuc2) - UC2 Kondensatorspannung 2 fuer Zylinder 4 und 7
- [STATUS_ANMUG1](#job-status-anmug1) - UG1 Speisespannung 1 fuer Luftmassenmesser 1, Ladedruckfuehler 1
- [STATUS_ANMUG2](#job-status-anmug2) - UG2 Speisespannung 2 fuer Raildrucksensor
- [STATUS_ANOU_IDV](#job-status-anou-idv) - IDV Spannung zur Strommessung Druckregelventil
- [STATUS_ANOU_KDF](#job-status-anou-kdf) - KDF Spannung Raildruckfuehler
- [STATUS_ANOU_KTF](#job-status-anou-ktf) - KTF Spannung Kraftstofftemperaturfuehler
- [STATUS_ANOU_LDF1](#job-status-anou-ldf1) - LDF1 Spannung Ladedruckfuehler
- [STATUS_ANOU_LMM1](#job-status-anou-lmm1) - LMM1 Spannung Luftmassenmesser 1
- [STATUS_ANOU_LTF1](#job-status-anou-ltf1) - LTF1 Spannung Lufttemperaturfuehler 1
- [STATUS_ANOU_UBT](#job-status-anou-ubt) - UBT Spannung Batteriespannung
- [STATUS_ANOU_UC1](#job-status-anou-uc1) - UC1 Spannung Kondensatorspannung 1 fuer Zylinder 1 und 6
- [STATUS_ANOU_UC2](#job-status-anou-uc2) - UC2 Spannung Kondensatorspannung 2 fuer Zylinder 4 und 7
- [STATUS_ANOU_UG1](#job-status-anou-ug1) - UG1 Spannung Speisespannung 1 fuer Luftmassenmesser 1, Ladedruckfuehler 1
- [STATUS_ANOU_UG2](#job-status-anou-ug2) - UG2 Spannung Speisespannung 2 fuer Raildrucksensor
- [STATUS_COMGTR_OPT](#job-status-comgtr-opt) - Identifikation Handschalter/Automatik
- [STATUS_DZMZMK1](#job-status-dzmzmk1) - Selektive Mengenkorrektur Zylinder 1
- [STATUS_DZMZMK2](#job-status-dzmzmk2) - Selektive Mengenkorrektur Zylinder 2
- [STATUS_DZMZMK3](#job-status-dzmzmk3) - Selektive Mengenkorrektur Zylinder 3
- [STATUS_DZMZMK4](#job-status-dzmzmk4) - Selektive Mengenkorrektur Zylinder 4
- [STATUS_DZMZMK5](#job-status-dzmzmk5) - Selektive Mengenkorrektur Zylinder 5
- [STATUS_DZMZMK6](#job-status-dzmzmk6) - Selektive Mengenkorrektur Zylinder 6
- [STATUS_DZMZMK7](#job-status-dzmzmk7) - Selektive Mengenkorrektur Zylinder 7
- [STATUS_DZMZMK8](#job-status-dzmzmk8) - Selektive Mengenkorrektur Zylinder 8
- [STATUS_DZMZN1](#job-status-dzmzn1) - Selektive Drehzahl Zylinder 1
- [STATUS_DZMZN2](#job-status-dzmzn2) - Selektive Drehzahl Zylinder 2
- [STATUS_DZMZN3](#job-status-dzmzn3) - Selektive Drehzahl Zylinder 3
- [STATUS_DZMZN4](#job-status-dzmzn4) - Selektive Drehzahl Zylinder 4
- [STATUS_DZMZN5](#job-status-dzmzn5) - Selektive Drehzahl Zylinder 5
- [STATUS_DZMZN6](#job-status-dzmzn6) - Selektive Drehzahl Zylinder 6
- [STATUS_DZMZN7](#job-status-dzmzn7) - Selektive Drehzahl Zylinder 7
- [STATUS_DZMZN8](#job-status-dzmzn8) - Selektive Drehzahl Zylinder 8
- [STATUS_EDMRSTCD](#job-status-edmrstcd) - Restart Code
- [STATUS_FBMBSTZ_UB](#job-status-fbmbstz-ub) - UB Betriebsstunden
- [STATUS_FBMSDIAL](#job-status-fbmsdial) - Anforderung Diagnoselampe aus Fehlerbehandlung (0:Aus,1:Ein,2:Blinken)
- [STATUS_FBOS_00](#job-status-fbos-00) - Defekte Pfade 1 bis 16
- [STATUS_FBOS_02](#job-status-fbos-02) - Defekte Pfade 17 bis 32
- [STATUS_FBOS_04](#job-status-fbos-04) - Defekte Pfade 33 bis 48
- [STATUS_FGMFGAKT](#job-status-fgmfgakt) - aktuelle Geschwindigkeit
- [STATUS_LDMADF](#job-status-ldmadf) - aktueller Atmosphaerendruck
- [STATUS_MRMCASE_A](#job-status-mrmcase-a) - ARD Zustand-Bits der aktiven Ruckeldaempfung
- [STATUS_MRMCASE_L](#job-status-mrmcase-l) - LLR Zustand-Bits der Leerlaufregelung
- [STATUS_MRMKM_AKT](#job-status-mrmkm-akt) - aktueller KM-Stand von Kombiinstrument
- [STATUS_MRMLLRIANT](#job-status-mrmllriant) - M_E Menge aus I-Anteil des PI-Leerlaufreglers
- [STATUS_MRMLLRPANT](#job-status-mrmllrpant) - M_E Menge aus P-Anteil des PI-Leerlaufreglers
- [STATUS_MRMM_EAKT](#job-status-mrmm-eakt) - M_E Aktuelle Einspritzmenge (ohne ARD)
- [STATUS_MRMM_EARD](#job-status-mrmm-eard) - M_E Menge ARD - Gesamt vor Begrenzung
- [STATUS_MRMM_EDELB](#job-status-mrmm-edelb) - M_E begrenzte Abgleichmenge
- [STATUS_MRMM_EFAHR](#job-status-mrmm-efahr) - M_E Fahrmenge nach Laufruheregler
- [STATUS_MRMM_EKORR](#job-status-mrmm-ekorr) - M_E Fahrmenge korrigiert mit Vollast- und Mengenabgleich
- [STATUS_MRMM_ELLR](#job-status-mrmm-ellr) - M_E Menge aus Leerlaufregelung
- [STATUS_MRMM_ELRR](#job-status-mrmm-elrr) - M_E Menge aus Laufruheregler
- [STATUS_MRMM_EMOT](#job-status-mrmm-emot) - M_E Einspritzmenge nach ARD
- [STATUS_MRMM_ESTAR](#job-status-mrmm-estar) - M_E resultierender Startmengen-Sollwert
- [STATUS_MRMM_EWUN](#job-status-mrmm-ewun) - M_E Fahrerwunschmenge nach externem Mengeneingriff
- [STATUS_MRMN_LLBAS](#job-status-mrmn-llbas) - N Leerlaufsolldrehzahl
- [STATUS_MRMN_LLDIA](#job-status-mrmn-lldia) - N Leerlaufsolldrehzahl fuer Diagnose
- [STATUS_MRMSTATUS](#job-status-mrmstatus) - Status Motorbetriebsphase
- [STATUS_MROLLRDANT](#job-status-mrollrdant) - M_E Menge aus Leerlaufregler-DT1-Vorsteuerung
- [STATUS_MROLRRREG](#job-status-mrolrrreg) - Nsegm Segmentdrehzahl-Regelabweichung fuer Laufruheregler
- [STATUS_MROM_ARDFF](#job-status-mrom-ardff) - M_E Menge ARD - Fuehrungsformer
- [STATUS_MROM_ARDSR](#job-status-mrom-ardsr) - M_E Menge ARD - Stoerregler
- [STATUS_ZHOSYNC_ST](#job-status-zhosync-st) - Synchronisationsstatus des Zumesshandlers
- [STATUS_ZUMAB_HE](#job-status-zumab-he) - Ansteuerbeginn Haupteinspritzung
- [STATUS_ZUMAB_NE](#job-status-zumab-ne) - Ansteuerbeginn Nacheinspritzung
- [STATUS_ZUMAD_NE](#job-status-zumad-ne) - Ansteuerdauer Nacheinspritzung Abgastrakt 1
- [STATUS_ZUOAB_VE1](#job-status-zuoab-ve1) - Ansteuerbeginn Voreinspritzung 1
- [STATUS_ZUOAD_HE](#job-status-zuoad-he) - Ansteuerdauer Haupteinspritzung
- [STATUS_ZUOAD_VE1](#job-status-zuoad-ve1) - Ansteuerdauer Voreinspritzung 1
- [STATUS_ZUOME_VE](#job-status-zuome-ve) - M_E Menge Voreinspritzung
- [STATUS_ZUOMEHE](#job-status-zuomehe) - M_E Menge Haupteinspritzung
- [STATUS_ZUOMEVGW](#job-status-zuomevgw) - GW-Kennfeld Menge Voreinspritzung
- [STATUS_ZUOVE_STAT](#job-status-zuove-stat) - Voreinspritzung - Schalter
- [STATUS_AN_LUFTTEMPERATUR2](#job-status-an-lufttemperatur2) - LTF2 Lufttemperatur 2
- [STATUS_LADEDRUCK](#job-status-ladedruck) - LDF Ladedruck
- [STATUS_MOTORDREHZAHL](#job-status-motordrehzahl) - N Drehzahl
- [STATUS_MOTORTEMPERATUR](#job-status-motortemperatur) - WTF Wassertemperatur
- [STATUS_RAILDRUCK](#job-status-raildruck) - KDF Raildruck
- [STATUS_UBATT](#job-status-ubatt) - UBT Batteriespannung
- [STATUS_VORFOERDERDRUCK](#job-status-vorfoerderdruck) - VDF Vorfoerderdruck
- [STATUS_LMM_MASSE](#job-status-lmm-masse) - LMM Luftmasse 2
- [STATUS_AN_LUFTTEMPERATUR](#job-status-an-lufttemperatur) - LTF2 Lufttemperatur 2

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

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

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

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-fs-lesen-status"></a>
### FS_LESEN_STATUS

Auslesen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_CODEHEX | binary | alle Fehlerbyte |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Kennung M_ABGLEICH_FLAG lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| PRUEFSTEMPEL_LESEN_WERT | long | "OKAY", wenn fehlerfrei |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Kennung M_ABGLEICH_FLAG lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WERT | long | Aktuellen Abgleichwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

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

<a id="job-status-sync-mode"></a>
### STATUS_SYNC_MODE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STATUS_SYNC_MODE_STATUS | int | Statusflag |
| STATUS_SYNC_MODE_TEXT | string | Statustext |

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

<a id="job-abgleich-lesen-voll-menge"></a>
### ABGLEICH_LESEN_VOLL_MENGE

BEGR_MENGEn-Abgleich lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_LESEN_VOLL_MENGE_ROH_WERT | int | Aktuellen Abgleichwert |
| ABGLEICH_LESEN_VOLL_MENGE_WERT | real | Aktuellen Abgleichwert |
| ABGLEICH_LESEN_VOLL_MENGE_STATUS | int | Rueckmeldebyte |

<a id="job-abgleich-lesen-voll-menge-roh"></a>
### ABGLEICH_LESEN_VOLL_MENGE_ROH

Vollastmenge-Abgleich lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_LESEN_VOLL_MENGE_ROH_WERT | int | Aktuellen Abgleichwert |
| ABGLEICH_LESEN_VOLL_MENGE_ROH_STATUS | int | Rueckmeldebyte |

<a id="job-abgleich-verstellen-voll-menge-roh"></a>
### ABGLEICH_VERSTELLEN_VOLL_MENGE_ROH

Vollastmenge-Abgleich verstellen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_VERSTELLEN_VOLL_MENGE_ROH_WERT | int | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_VERSTELLEN_VOLL_MENGE_ROH_STATUS | int | Status |

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

<a id="job-hole-ema-feld"></a>
### HOLE_EMA_FELD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| EMA_FAK1 | real | Faktor 1 |
| EMA_FAK2 | real | faktor 2 |
| EMA_WERT3 | real | Wert 3 |

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

<a id="job-abgleich-kic-verstellen-programmieren"></a>
### ABGLEICH_KIC_VERSTELLEN_PROGRAMMIEREN

Uebertragung KIC Ein- oder Ausschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_KIC_VERSTELLEN_PROGRAMMIEREN_WERT | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ABGLEICH_KIC_VERSTELLEN_PROGRAMMIEREN_STATUS | int | Status |

<a id="job-steuern-agr-steller1"></a>
### STEUERN_AGR_STELLER1

ARF - Steller1  ansteuern ,  - - 10%%

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | Verstellwert 5 - 95 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-agr-steller2"></a>
### STEUERN_AGR_STELLER2

ARF - Steller2  ansteuern ,  - - 10%%

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | Verstellwert 5 - 95 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ks-hdpumpe-abschaltung"></a>
### STEUERN_KS_HDPUMPE_ABSCHALTUNG

Elektrisches Abschaltventil ansteuern ,  0 oder 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | Verstellwert 0 oder 1 |

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

<a id="job-start-systemcheck-zyl-sel-mengenkor"></a>
### START_SYSTEMCHECK_ZYL_SEL_MENGENKOR

Start zylinderselektive Mengenkorrekturen

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
| STAT_LAUFUNRUHE_LLR_MENGE_ZYL7_WERT | real |  |
| STAT_LAUFUNRUHE_LLR_MENGE_ZYL8_WERT | real |  |
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
| STAT_LAUFUNRUHE_DREHZAHL_ZYL7_WERT | real |  |
| STAT_LAUFUNRUHE_DREHZAHL_ZYL8_WERT | real |  |
| STAT_LAUFUNRUHE_DREHZAHL_EINH | string |  |

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

<a id="job-status-ehmfars1"></a>
### STATUS_EHMFARS1

Tastverhaeltnis Ansteuerung Abgasrueckfuehrsteller 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_EHMFARS1_WERT | real | Ergebnis |
| STAT_EHMFARS1_EINH | string | Einheit |

<a id="job-status-ehmfars2"></a>
### STATUS_EHMFARS2

Tastverhaeltnis Ansteuerung Abgasrueckfuehrsteller 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_EHMFARS2_WERT | real | Ergebnis |
| STAT_EHMFARS2_EINH | string | Einheit |

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

<a id="job-status-admldf1"></a>
### STATUS_ADMLDF1

LDF Rohwert Ladedruck

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ADMLDF1_WERT | real | Ergebnis |
| STAT_ADMLDF1_EINH | string | Einheit |

<a id="job-status-admlmm1"></a>
### STATUS_ADMLMM1

LMM1 Rohwert Luftmasse 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ADMLMM1_WERT | real | Ergebnis |
| STAT_ADMLMM1_EINH | string | Einheit |

<a id="job-status-admltf1"></a>
### STATUS_ADMLTF1

LTF1 Rohwert Lufttemperatur 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ADMLTF1_WERT | real | Ergebnis |
| STAT_ADMLTF1_EINH | string | Einheit |

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

UC1 Rohwert Kondensatorspannung 1 fuer Zylinder 1 und 6

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ADMUC1_WERT | real | Ergebnis |
| STAT_ADMUC1_EINH | string | Einheit |

<a id="job-status-admuc2"></a>
### STATUS_ADMUC2

UC2 Rohwert Kondensatorspannung 2 fuer Zylinder 4 und 7

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ADMUC2_WERT | real | Ergebnis |
| STAT_ADMUC2_EINH | string | Einheit |

<a id="job-status-admug1"></a>
### STATUS_ADMUG1

UG1 Rohwert Speisespannung 1 fuer Luftmassenmesser 1, Ladedruckfuehler 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ADMUG1_WERT | real | Ergebnis |
| STAT_ADMUG1_EINH | string | Einheit |

<a id="job-status-admug2"></a>
### STATUS_ADMUG2

UG2 Rohwert Speisespannung 2 fuer Raildrucksensor

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ADMUG2_WERT | real | Ergebnis |
| STAT_ADMUG2_EINH | string | Einheit |

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

<a id="job-status-anmldf1"></a>
### STATUS_ANMLDF1

LDF Ladedruck

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANMLDF1_WERT | real | Ergebnis |
| STAT_ANMLDF1_EINH | string | Einheit |

<a id="job-status-anmlmm1"></a>
### STATUS_ANMLMM1

LMM1 Luftmasse 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANMLMM1_WERT | real | Ergebnis |
| STAT_ANMLMM1_EINH | string | Einheit |

<a id="job-status-anmltf1"></a>
### STATUS_ANMLTF1

LTF1 Lufttemperatur 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANMLTF1_WERT | real | Ergebnis |
| STAT_ANMLTF1_EINH | string | Einheit |

<a id="job-status-anmltf2"></a>
### STATUS_ANMLTF2

LTF2 Lufttemperatur 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANMLTF2_WERT | real | Ergebnis |
| STAT_ANMLTF2_EINH | string | Einheit |

<a id="job-status-anmuc1"></a>
### STATUS_ANMUC1

UC1 Kondensatorspannung 1 fuer Zylinder 1 und 6

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANMUC1_WERT | real | Ergebnis |
| STAT_ANMUC1_EINH | string | Einheit |

<a id="job-status-anmuc2"></a>
### STATUS_ANMUC2

UC2 Kondensatorspannung 2 fuer Zylinder 4 und 7

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANMUC2_WERT | real | Ergebnis |
| STAT_ANMUC2_EINH | string | Einheit |

<a id="job-status-anmug1"></a>
### STATUS_ANMUG1

UG1 Speisespannung 1 fuer Luftmassenmesser 1, Ladedruckfuehler 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANMUG1_WERT | real | Ergebnis |
| STAT_ANMUG1_EINH | string | Einheit |

<a id="job-status-anmug2"></a>
### STATUS_ANMUG2

UG2 Speisespannung 2 fuer Raildrucksensor

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANMUG2_WERT | real | Ergebnis |
| STAT_ANMUG2_EINH | string | Einheit |

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

<a id="job-status-anou-ktf"></a>
### STATUS_ANOU_KTF

KTF Spannung Kraftstofftemperaturfuehler

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANOU_KTF_WERT | real | Ergebnis |
| STAT_ANOU_KTF_EINH | string | Einheit |

<a id="job-status-anou-ldf1"></a>
### STATUS_ANOU_LDF1

LDF1 Spannung Ladedruckfuehler

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANOU_LDF1_WERT | real | Ergebnis |
| STAT_ANOU_LDF1_EINH | string | Einheit |

<a id="job-status-anou-lmm1"></a>
### STATUS_ANOU_LMM1

LMM1 Spannung Luftmassenmesser 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANOU_LMM1_WERT | real | Ergebnis |
| STAT_ANOU_LMM1_EINH | string | Einheit |

<a id="job-status-anou-ltf1"></a>
### STATUS_ANOU_LTF1

LTF1 Spannung Lufttemperaturfuehler 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANOU_LTF1_WERT | real | Ergebnis |
| STAT_ANOU_LTF1_EINH | string | Einheit |

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

UC1 Spannung Kondensatorspannung 1 fuer Zylinder 1 und 6

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANOU_UC1_WERT | real | Ergebnis |
| STAT_ANOU_UC1_EINH | string | Einheit |

<a id="job-status-anou-uc2"></a>
### STATUS_ANOU_UC2

UC2 Spannung Kondensatorspannung 2 fuer Zylinder 4 und 7

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANOU_UC2_WERT | real | Ergebnis |
| STAT_ANOU_UC2_EINH | string | Einheit |

<a id="job-status-anou-ug1"></a>
### STATUS_ANOU_UG1

UG1 Spannung Speisespannung 1 fuer Luftmassenmesser 1, Ladedruckfuehler 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANOU_UG1_WERT | real | Ergebnis |
| STAT_ANOU_UG1_EINH | string | Einheit |

<a id="job-status-anou-ug2"></a>
### STATUS_ANOU_UG2

UG2 Spannung Speisespannung 2 fuer Raildrucksensor

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ANOU_UG2_WERT | real | Ergebnis |
| STAT_ANOU_UG2_EINH | string | Einheit |

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

<a id="job-status-dzmzmk7"></a>
### STATUS_DZMZMK7

Selektive Mengenkorrektur Zylinder 7

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DZMZMK7_WERT | real | Ergebnis |
| STAT_DZMZMK7_EINH | string | Einheit |

<a id="job-status-dzmzmk8"></a>
### STATUS_DZMZMK8

Selektive Mengenkorrektur Zylinder 8

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DZMZMK8_WERT | real | Ergebnis |
| STAT_DZMZMK8_EINH | string | Einheit |

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

<a id="job-status-dzmzn7"></a>
### STATUS_DZMZN7

Selektive Drehzahl Zylinder 7

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DZMZN7_WERT | real | Ergebnis |
| STAT_DZMZN7_EINH | string | Einheit |

<a id="job-status-dzmzn8"></a>
### STATUS_DZMZN8

Selektive Drehzahl Zylinder 8

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DZMZN8_WERT | real | Ergebnis |
| STAT_DZMZN8_EINH | string | Einheit |

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

<a id="job-status-mrmkm-akt"></a>
### STATUS_MRMKM_AKT

aktueller KM-Stand von Kombiinstrument

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMKM_AKT_WERT | real | Ergebnis |
| STAT_MRMKM_AKT_EINH | string | Einheit |

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

<a id="job-status-mrmn-lldia"></a>
### STATUS_MRMN_LLDIA

N Leerlaufsolldrehzahl fuer Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MRMN_LLDIA_WERT | real | Ergebnis |
| STAT_MRMN_LLDIA_EINH | string | Einheit |

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

<a id="job-status-mrom-ardsr"></a>
### STATUS_MROM_ARDSR

M_E Menge ARD - Stoerregler

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MROM_ARDSR_WERT | real | Ergebnis |
| STAT_MROM_ARDSR_EINH | string | Einheit |

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

Ansteuerdauer Nacheinspritzung Abgastrakt 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ZUMAD_NE_WERT | real | Ergebnis |
| STAT_ZUMAD_NE_EINH | string | Einheit |

<a id="job-status-zuoab-ve1"></a>
### STATUS_ZUOAB_VE1

Ansteuerbeginn Voreinspritzung 1

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

Ansteuerdauer Voreinspritzung 1

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

<a id="job-status-an-lufttemperatur2"></a>
### STATUS_AN_LUFTTEMPERATUR2

LTF2 Lufttemperatur 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_AN_LUFTTEMPERATUR2_WERT | real | Ergebnis |
| STAT_AN_LUFTTEMPERATUR2_EINH | string | Einheit |

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

<a id="job-status-lmm-masse"></a>
### STATUS_LMM_MASSE

LMM Luftmasse 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LMM_MASSE_WERT | real | Ergebnis |
| STAT_LMM_MASSE_EINH | string | Einheit |

<a id="job-status-an-lufttemperatur"></a>
### STATUS_AN_LUFTTEMPERATUR

LTF2 Lufttemperatur 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_AN_LUFTTEMPERATUR_WERT | real | Ergebnis |
| STAT_AN_LUFTTEMPERATUR_EINH | string | Einheit |

## Tables

### Index

- [BETRIEBSWTAB](#table-betriebswtab) (107 × 17)
- [FORTTEXTE](#table-forttexte) (33 × 6)
- [FARTMATRIX](#table-fartmatrix) (32 × 33)
- [FARTTEXTE](#table-farttexte) (64 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (17 × 5)
- [JOBRESULT](#table-jobresult) (37 × 2)

<a id="table-betriebswtab"></a>
### BETRIEBSWTAB

Dimensions: 107 rows × 17 columns

| NAME | TELEGRAM | POS_ADR | LEN_ADR | ADR | BYTE | DATA_TYPE | COMPU_TYPE | FACT_A | FACT_B | MASK | VALUE | ANZ | MEAS | RANGE | JOBNAME | LNAME |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| anmUBT | B813F1042C100000 | 06 | 2 | 0x0F65 | 06 | 5 | -- | 0.0236197458 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anmUBT | UBT Batteriespannung |
| anmVDF | B813F1042C100000 | 06 | 2 | 0x1F06 | 06 | 5 | -- | 0.001 | 0 | 0x00 | 0x00 | 6.2f | bar | -- | anmVDF | VDF Vorfoerderdruck |
| anmWTF | B813F1042C100000 | 06 | 2 | 0x0F00 | 06 | 5 | -- | 0.1 | -273.14 | 0x00 | 0x00 | 6.2f | Grad C | -- | anmWTF | WTF Wassertemperatur |
| dzmNakt | B813F1042C100000 | 06 | 2 | 0x0F10 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min | -- | dzmNakt | N aktuelle Drehzahl aus letzter Periode |
| ehmFARS1 | B813F1042C100000 | 06 | 2 | 0x0E80 | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | % | -- | ehmFARS1 | Tastverhaeltnis Ansteuerung Abgasrueckfuehrsteller 1 |
| ehmFARS2 | B813F1042C100000 | 06 | 2 | 0x0E82 | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | % | -- | ehmFARS2 | Tastverhaeltnis Ansteuerung Abgasrueckfuehrsteller 2 |
| ehmFKDR | B813F1042C100000 | 06 | 2 | 0x0EA5 | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | % | -- | ehmFKDR | Tastverhaeltnis Ansteuerung Raildruckregelventil |
| zumP_RAIL | B813F1042C100000 | 06 | 2 | 0x1F5D | 06 | 5 | -- | 10.235414 | 0 | 0x00 | 0x00 | 6.2f | bar | -- | zumP_RAIL | Raildruck fuer Mengenzumessung |
| zumPQsoll | B813F1042C100000 | 06 | 2 | 0x1F5E | 06 | 5 | -- | 10.235414 | 0 | 0x00 | 0x00 | 6.2f | bar | -- | zumPQsoll | Raildruck Sollwert |
| admIDV | B813F1042C100000 | 06 | 2 | 0x2FFE | 06 | 5 | -- | 4.995005 | 0 | 0x00 | 0x00 | 6.2f | mA | -- | admIDV | IDV Rohwert Istwert Stromregelung Druckregelventil |
| admKDF | B813F1042C100000 | 06 | 2 | 0x2FFC | 06 | 5 | -- | 10.235414 | 0 | 0x00 | 0x00 | 6.2f | bar | -- | admKDF | KDF Rohwert Raildruck |
| admLDF1 | B813F1042C100000 | 06 | 2 | 0x2F26 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | mbar | -- | admLDF1 | LDF Rohwert Ladedruck |
| admLMM1 | B813F1042C100000 | 06 | 2 | 0x2F27 | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | % | -- | admLMM1 | LMM1 Rohwert Luftmasse 1 |
| admLTF1 | B813F1042C100000 | 06 | 2 | 0x2F28 | 06 | 5 | -- | 0.1 | -273.14 | 0x00 | 0x00 | 6.2f | Grad C | -- | admLTF1 | LTF1 Rohwert Lufttemperatur 1 |
| admUBT | B813F1042C100000 | 06 | 2 | 0x2065 | 06 | 5 | -- | 0.0236197458 | 0 | 0x00 | 0x00 | 6.2f | V | -- | admUBT | UBT Rohwert Batteriespannung |
| admUC1 | B813F1042C100000 | 06 | 2 | 0x2FF8 | 06 | 5 | -- | 0.0205718988 | 0 | 0x00 | 0x00 | 6.2f | V | -- | admUC1 | UC1 Rohwert Kondensatorspannung 1 fuer Zylinder 1 und 6 |
| admUC2 | B813F1042C100000 | 06 | 2 | 0x2FF9 | 06 | 5 | -- | 0.0205718988 | 0 | 0x00 | 0x00 | 6.2f | V | -- | admUC2 | UC2 Rohwert Kondensatorspannung 2 fuer Zylinder 4 und 7 |
| admUG1 | B813F1042C100000 | 06 | 2 | 0x2FF6 | 06 | 5 | -- | 0.01764418377 | 0 | 0x00 | 0x00 | 6.2f | V | -- | admUG1 | UG1 Rohwert Speisespannung 1 fuer Luftmassenmesser 1, Ladedruckfuehler 1 |
| admUG2 | B813F1042C100000 | 06 | 2 | 0x2FF7 | 06 | 5 | -- | 0.01764418377 | 0 | 0x00 | 0x00 | 6.2f | V | -- | admUG2 | UG2 Rohwert Speisespannung 2 fuer Raildrucksensor |
| anmIDV | B813F1042C100000 | 06 | 2 | 0x0FFE | 06 | 5 | -- | 4.995005 | 0 | 0x00 | 0x00 | 6.2f | mA | -- | anmIDV | IDV Istwert Stromregelung Druckregelventil |
| anmKDF | B813F1042C100000 | 06 | 2 | 0x0FFC | 06 | 5 | -- | 10.235414 | 0 | 0x00 | 0x00 | 6.2f | bar | -- | anmKDF | KDF Raildruck |
| anmLDF1 | B813F1042C100000 | 06 | 2 | 0x1F26 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | mbar | -- | anmLDF1 | LDF Ladedruck |
| anmLMM1 | B813F1042C100000 | 06 | 2 | 0x1F27 | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | % | -- | anmLMM1 | LMM1 Luftmasse 1 |
| anmLTF1 | B813F1042C100000 | 06 | 2 | 0x1F28 | 06 | 5 | -- | 0.1 | -273.14 | 0x00 | 0x00 | 6.2f | Grad C | -- | anmLTF1 | LTF1 Lufttemperatur 1 |
| anmLTF2 | B813F1042C100000 | 06 | 2 | 0x0F01 | 06 | 5 | -- | 0.1 | -273.14 | 0x00 | 0x00 | 6.2f | Grad C | -- | anmLTF2 | LTF2 Lufttemperatur 2 |
| anmUC1 | B813F1042C100000 | 06 | 2 | 0x0FF8 | 06 | 5 | -- | 0.0205718988 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anmUC1 | UC1 Kondensatorspannung 1 fuer Zylinder 1 und 6 |
| anmUC2 | B813F1042C100000 | 06 | 2 | 0x0FF9 | 06 | 5 | -- | 0.0205718988 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anmUC2 | UC2 Kondensatorspannung 2 fuer Zylinder 4 und 7 |
| anmUG1 | B813F1042C100000 | 06 | 2 | 0x0FF6 | 06 | 5 | -- | 0.01764418377 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anmUG1 | UG1 Speisespannung 1 fuer Luftmassenmesser 1, Ladedruckfuehler 1 |
| anmUG2 | B813F1042C100000 | 06 | 2 | 0x0FF7 | 06 | 5 | -- | 0.01764418377 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anmUG2 | UG2 Speisespannung 2 fuer Raildrucksensor |
| anoU_IDV | B813F1042C100000 | 06 | 2 | 0x300C | 06 | 5 | -- | 0.0048875855 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anoU_IDV | IDV Spannung zur Strommessung Druckregelventil |
| anoU_KDF | B813F1042C100000 | 06 | 2 | 0x300A | 06 | 5 | -- | 0.0048875855 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anoU_KDF | KDF Spannung Raildruckfuehler |
| anoU_KTF | B813F1042C100000 | 06 | 2 | 0x300B | 06 | 5 | -- | 0.0048875855 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anoU_KTF | KTF Spannung Kraftstofftemperaturfuehler |
| anoU_LDF1 | B813F1042C100000 | 06 | 2 | 0x3026 | 06 | 5 | -- | 0.0048875855 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anoU_LDF1 | LDF1 Spannung Ladedruckfuehler |
| anoU_LMM1 | B813F1042C100000 | 06 | 2 | 0x3027 | 06 | 5 | -- | 0.0048875855 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anoU_LMM1 | LMM1 Spannung Luftmassenmesser 1 |
| anoU_LTF1 | B813F1042C100000 | 06 | 2 | 0x3028 | 06 | 5 | -- | 0.0048875855 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anoU_LTF1 | LTF1 Spannung Lufttemperaturfuehler 1 |
| anoU_UBT | B813F1042C100000 | 06 | 2 | 0x3013 | 06 | 5 | -- | 0.0048875855 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anoU_UBT | UBT Spannung Batteriespannung |
| anoU_UC1 | B813F1042C100000 | 06 | 2 | 0x3008 | 06 | 5 | -- | 0.0048875855 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anoU_UC1 | UC1 Spannung Kondensatorspannung 1 fuer Zylinder 1 und 6 |
| anoU_UC2 | B813F1042C100000 | 06 | 2 | 0x3009 | 06 | 5 | -- | 0.0048875855 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anoU_UC2 | UC2 Spannung Kondensatorspannung 2 fuer Zylinder 4 und 7 |
| anoU_UG1 | B813F1042C100000 | 06 | 2 | 0x3016 | 06 | 5 | -- | 0.01764418377 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anoU_UG1 | UG1 Spannung Speisespannung 1 fuer Luftmassenmesser 1, Ladedruckfuehler 1 |
| anoU_UG2 | B813F1042C100000 | 06 | 2 | 0x3017 | 06 | 5 | -- | 0.01764418377 | 0 | 0x00 | 0x00 | 6.2f | V | -- | anoU_UG2 | UG2 Spannung Speisespannung 2 fuer Raildrucksensor |
| comGTR_opt | B813F1042C100000 | 06 | 2 | 0x1C00 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | comGTR_opt | Identifikation Handschalter/Automatik |
| dzmzMk1 | B813F1042C100000 | 06 | 2 | 0x0F19 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | dzmzMk1 | Selektive Mengenkorrektur Zylinder 1 |
| dzmzMk2 | B813F1042C100000 | 06 | 2 | 0x0F1A | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | dzmzMk2 | Selektive Mengenkorrektur Zylinder 2 |
| dzmzMk3 | B813F1042C100000 | 06 | 2 | 0x0F1B | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | dzmzMk3 | Selektive Mengenkorrektur Zylinder 3 |
| dzmzMk4 | B813F1042C100000 | 06 | 2 | 0x0F1C | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | dzmzMk4 | Selektive Mengenkorrektur Zylinder 4 |
| dzmzMk5 | B813F1042C100000 | 06 | 2 | 0x0F1D | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | dzmzMk5 | Selektive Mengenkorrektur Zylinder 5 |
| dzmzMk6 | B813F1042C100000 | 06 | 2 | 0x0F1E | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | dzmzMk6 | Selektive Mengenkorrektur Zylinder 6 |
| dzmzMk7 | B813F1042C100000 | 06 | 2 | 0x2F86 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | dzmzMk7 | Selektive Mengenkorrektur Zylinder 7 |
| dzmzMk8 | B813F1042C100000 | 06 | 2 | 0x2F87 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | dzmzMk8 | Selektive Mengenkorrektur Zylinder 8 |
| dzmzN1 | B813F1042C100000 | 06 | 2 | 0x0F13 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min | -- | dzmzN1 | Selektive Drehzahl Zylinder 1 |
| dzmzN2 | B813F1042C100000 | 06 | 2 | 0x0F14 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min | -- | dzmzN2 | Selektive Drehzahl Zylinder 2 |
| dzmzN3 | B813F1042C100000 | 06 | 2 | 0x0F15 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min | -- | dzmzN3 | Selektive Drehzahl Zylinder 3 |
| dzmzN4 | B813F1042C100000 | 06 | 2 | 0x0F16 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min | -- | dzmzN4 | Selektive Drehzahl Zylinder 4 |
| dzmzN5 | B813F1042C100000 | 06 | 2 | 0x0F17 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min | -- | dzmzN5 | Selektive Drehzahl Zylinder 5 |
| dzmzN6 | B813F1042C100000 | 06 | 2 | 0x0F18 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min | -- | dzmzN6 | Selektive Drehzahl Zylinder 6 |
| dzmzN7 | B813F1042C100000 | 06 | 2 | 0x2F80 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min | -- | dzmzN7 | Selektive Drehzahl Zylinder 7 |
| dzmzN8 | B813F1042C100000 | 06 | 2 | 0x2F81 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min | -- | dzmzN8 | Selektive Drehzahl Zylinder 8 |
| edmRSTCD | B813F1042C100000 | 06 | 2 | 0x0E00 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | edmRSTCD | Restart Code |
| fbmBSTZ_UB | B813F1042C100000 | 06 | 2 | 0x1300 | 06 | 5 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | h | -- | fbmBSTZ_UB | UB Betriebsstunden |
| fbmSDIAL | B813F1042C100000 | 06 | 2 | 0x1000 | 06 | 2 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | fbmSDIAL | Anforderung Diagnoselampe aus Fehlerbehandlung (0:Aus,1:Ein,2:Blinken) |
| fboS_00 | B813F1042C100000 | 06 | 2 | 0xDF70 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | fboS_00 | Defekte Pfade 1 bis 16 |
| fboS_02 | B813F1042C100000 | 06 | 2 | 0xDF72 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | fboS_02 | Defekte Pfade 17 bis 32 |
| fboS_04 | B813F1042C100000 | 06 | 2 | 0xDF74 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | fboS_04 | Defekte Pfade 33 bis 48 |
| fgmFGAKT | B813F1042C100000 | 06 | 2 | 0x0F08 | 06 | 5 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | km/h | -- | fgmFGAKT | aktuelle Geschwindigkeit |
| ldmADF | B813F1042C100000 | 06 | 2 | 0x0F41 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | mbar | -- | ldmADF | aktueller Atmosphaerendruck |
| mrmCASE_A | B813F1042C100000 | 06 | 2 | 0xDF21 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | mrmCASE_A | ARD Zustand-Bits der aktiven Ruckeldaempfung |
| mrmCASE_L | B813F1042C100000 | 06 | 2 | 0xDF20 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | mrmCASE_L | LLR Zustand-Bits der Leerlaufregelung |
| mrmKM_akt | B813F1042C100000 | 06 | 2 | 0x0FD0 | 06 | 5 | -- | 10 | 0 | 0x00 | 0x00 | 6.2f | km | -- | mrmKM_akt | aktueller KM-Stand von Kombiinstrument |
| mrmLLRIAnt | B813F1042C100000 | 06 | 2 | 0xDF13 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmLLRIAnt | M_E Menge aus I-Anteil des PI-Leerlaufreglers |
| mrmLLRPAnt | B813F1042C100000 | 06 | 2 | 0xDF14 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmLLRPAnt | M_E Menge aus P-Anteil des PI-Leerlaufreglers |
| mrmM_EAKT | B813F1042C100000 | 06 | 2 | 0x0F80 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmM_EAKT | M_E Aktuelle Einspritzmenge (ohne ARD) |
| mrmM_EARD | B813F1042C100000 | 06 | 2 | 0xDC88 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmM_EARD | M_E Menge ARD - Gesamt vor Begrenzung |
| mrmM_EDELB | B813F1042C100000 | 06 | 2 | 0x1F8E | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmM_EDELB | M_E begrenzte Abgleichmenge |
| mrmM_EFAHR | B813F1042C100000 | 06 | 2 | 0xDC86 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmM_EFAHR | M_E Fahrmenge nach Laufruheregler |
| mrmM_EKORR | B813F1042C100000 | 06 | 2 | 0x0F8E | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmM_EKORR | M_E Fahrmenge korrigiert mit Vollast- und Mengenabgleich |
| mrmM_ELLR | B813F1042C100000 | 06 | 2 | 0x0F8D | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmM_ELLR | M_E Menge aus Leerlaufregelung |
| mrmM_ELRR | B813F1042C100000 | 06 | 2 | 0xDC87 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmM_ELRR | M_E Menge aus Laufruheregler |
| mrmM_EMOT | B813F1042C100000 | 06 | 2 | 0x0F8C | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmM_EMOT | M_E Einspritzmenge nach ARD |
| mrmM_ESTAR | B813F1042C100000 | 06 | 2 | 0x0F82 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmM_ESTAR | M_E resultierender Startmengen-Sollwert |
| mrmM_EWUN | B813F1042C100000 | 06 | 2 | 0x0F8B | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mrmM_EWUN | M_E Fahrerwunschmenge nach externem Mengeneingriff |
| mrmN_LLBAS | B813F1042C100000 | 06 | 2 | 0x0E02 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min | -- | mrmN_LLBAS | N Leerlaufsolldrehzahl |
| mrmN_LLDIA | B813F1042C100000 | 06 | 2 | 0x0E08 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min | -- | mrmN_LLDIA | N Leerlaufsolldrehzahl fuer Diagnose |
| mrmSTATUS | B813F1042C100000 | 06 | 2 | 0x0F7F | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | mrmSTATUS | Status Motorbetriebsphase |
| mroLLRDAnt | B813F1042C100000 | 06 | 2 | 0xDF15 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mroLLRDAnt | M_E Menge aus Leerlaufregler-DT1-Vorsteuerung |
| mroLRRReg | B813F1042C100000 | 06 | 2 | 0xDC90 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min | -- | mroLRRReg | Nsegm Segmentdrehzahl-Regelabweichung fuer Laufruheregler |
| mroM_ARDFF | B813F1042C100000 | 06 | 2 | 0xDC89 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mroM_ARDFF | M_E Menge ARD - Fuehrungsformer |
| mroM_ARDSR | B813F1042C100000 | 06 | 2 | 0xDC8A | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | mroM_ARDSR | M_E Menge ARD - Stoerregler |
| zhmUM_ZA | B813F1042C100000 | 06 | 2 | 0x2F14 | 06 | 2 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | zhmUM_ZA | Umdrehungszaehler (1 Tick = 2 Umdrehungen) |
| zhoSYNC_ST | B813F1042C100000 | 06 | 2 | 0x1F50 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | zhoSYNC_ST | Synchronisationsstatus des Zumesshandlers |
| zumAB_HE | B813F1042C100000 | 06 | 2 | 0x1F5A | 06 | 7 | -- | 0.0234375 | 0 | 0x00 | 0x00 | 6.2f | Grad KW | -- | zumAB_HE | Ansteuerbeginn Haupteinspritzung |
| zumAB_NE | B813F1042C100000 | 06 | 2 | 0x1F60 | 06 | 7 | -- | 0.0234375 | 0 | 0x00 | 0x00 | 6.2f | Grad KW | -- | zumAB_NE | Ansteuerbeginn Nacheinspritzung |
| zumAD_NE | B813F1042C100000 | 06 | 2 | 0x1F61 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | us | -- | zumAD_NE | Ansteuerdauer Nacheinspritzung Abgastrakt 1 |
| zuoAB_VE1 | B813F1042C100000 | 06 | 2 | 0x1F51 | 06 | 7 | -- | 0.0234375 | 0 | 0x00 | 0x00 | 6.2f | Grad KW | -- | zuoAB_VE1 | Ansteuerbeginn Voreinspritzung 1 |
| zuoAD_HE | B813F1042C100000 | 06 | 2 | 0x1F5B | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | us | -- | zuoAD_HE | Ansteuerdauer Haupteinspritzung |
| zuoAD_VE1 | B813F1042C100000 | 06 | 2 | 0x1F52 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | us | -- | zuoAD_VE1 | Ansteuerdauer Voreinspritzung 1 |
| zuoME_VE | B813F1042C100000 | 06 | 2 | 0x1F53 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | zuoME_VE | M_E Menge Voreinspritzung |
| zuoMEHE | B813F1042C100000 | 06 | 2 | 0x1F5C | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | zuoMEHE | M_E Menge Haupteinspritzung |
| zuoMEVGW | B813F1042C100000 | 06 | 2 | 0x1F57 | 06 | 7 | -- | 0.01 | 0 | 0x00 | 0x00 | 6.2f | mm^3 | -- | zuoMEVGW | GW-Kennfeld Menge Voreinspritzung |
| zuoVE_STAT | B813F1042C100000 | 06 | 2 | 0x1F55 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | - | -- | zuoVE_STAT | Voreinspritzung - Schalter |
| anmLTF1 | B813F1042C100000 | 06 | 2 | 0x1F28 | 06 | 5 | -- | 0.1 | -273.14 | 0x00 | 0x00 | 6.2f | Grad C | -- | AN_LUFTTEMPERATUR1 | LTF1 Lufttemperatur 1 |
| anmLTF2 | B813F1042C100000 | 06 | 2 | 0x0F01 | 06 | 5 | -- | 0.1 | -273.14 | 0x00 | 0x00 | 6.2f | Grad C | -- | AN_LUFTTEMPERATUR2 | LTF2 Lufttemperatur 2 |
| anmLDF1 | B813F1042C100000 | 06 | 2 | 0x1F26 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | mbar | -- | LADEDRUCK | LDF Ladedruck |
| dzmNmit | B813F1042C100000 | 06 | 2 | 0x0F10 | 06 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min | -- | MOTORDREHZAHL | N Drehzahl |
| anmWTF | B813F1042C100000 | 06 | 2 | 0x0F00 | 06 | 5 | -- | 0.1 | -273.14 | 0x00 | 0x00 | 6.2f | Grad C | -- | MOTORTEMPERATUR | WTF Wassertemperatur |
| anmKDF | B813F1042C100000 | 06 | 2 | 0x2FFC | 06 | 5 | -- | 10.235414 | 0 | 0x00 | 0x00 | 6.2f | bar | -- | RAILDRUCK | KDF Raildruck |
| anmUBT | B813F1042C100000 | 06 | 2 | 0x0F65 | 06 | 5 | -- | 0.0236197458 | 0 | 0x00 | 0x00 | 6.2f | V | -- | UBATT | UBT Batteriespannung |
| anmVDF | B813F1042C100000 | 06 | 2 | 0x1F06 | 06 | 5 | -- | 0.001 | 0 | 0x00 | 0x00 | 6.2f | bar | -- | VORFOERDERDRUCK | VDF Vorfoerderdruck |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 33 rows × 6 columns

| ORT | ORTTEXT | UW_1 | UW_2 | UW_3 | UW_4 |
| --- | --- | --- | --- | --- | --- |
| 0x0101 | Luftmassenmesser 1 | 0x01 | 0x02 | 0x03 | 0x05 |
| 0x0111 | Lufttemperaturfuehler 1 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x0116 | Kuehlmitteltemperaturfuehler | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x0121 | Pedalwertgeber | 0x01 | 0x05 | 0x03 | 0x10 |
| 0x0191 | Raildrucksensor | 0x01 | 0x11 | 0x03 | 0x04 |
| 0x0208 | Injektor Zylinder 1 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x0209 | Injektor Zylinder 4 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x020A | Injektor Zylinder 6 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x020B | Injektor Zylinder 7 | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x0236 | Ladedruckfuehler | 0x01 | 0x02 | 0x03 | 0x05 |
| 0x0336 | Drehzahl Kurbelwelle | 0x01 | 0x02 | 0x03 | 0x05 |
| 0x0501 | Fahrgeschwindigkeitssignal | 0x01 | 0x02 | 0x06 | 0x03 |
| 0x0601 | CAN-Bus privat | 0x01 | 0x05 | 0x03 | 0x10 |
| 0x0606 | Steuergeraet DDE (Microcontroller) | 0x01 | 0x14 | 0x03 | 0x05 |
| 0x09F6 | Raildruckueberwachung im Start | 0x01 | 0x04 | 0x02 | 0x11 |
| 0x1191 | Raildruck-Regelung | 0x01 | 0x11 | 0x03 | 0x04 |
| 0x1196 | Raildruckregelventil | 0x01 | 0x11 | 0x05 | 0x04 |
| 0x1612 | Diagnoselampe | 0x01 | 0x11 | 0x03 | 0x04 |
| 0x1613 | Laufruheregler | 0x01 | 0x02 | 0x03 | 0x05 |
| 0x1641 | Steuergeraet DDE (EEPROM und Konfiguration) | 0x01 | 0x02 | 0x03 | 0x05 |
| 0x1DF1 | Redundanter Notstop | 0x01 | 0x02 | 0x03 | 0x04 |
| 0x1E26 | Ueberwachung Drehzahlgeber | 0x01 | 0x02 | 0x03 | 0x05 |
| 0x1E46 | Kondensatorspannung 1 fuer Zylinder 1 und 6 | 0x01 | 0x02 | 0x03 | 0x05 |
| 0x1E51 | Kondensatorspannung 2 fuer Zylinder 4 und 7 | 0x01 | 0x02 | 0x03 | 0x05 |
| 0x1E56 | Speisespannung 1 fuer HFM 1und LDF 1 | 0x01 | 0x02 | 0x05 | 0x03 |
| 0x1E61 | Speisespannung 2 fuer Raildrucksensor | 0x01 | 0x02 | 0x05 | 0x03 |
| 0x2801 | Versorgungsspannung | 0x01 | 0x02 | 0x03 | 0x15 |
| 0x3006 | Klemme 15           | 0x01 | 0x02 | 0x06 | 0x05 |
| 0x3511 | DDE-Hauptrelais | 0x01 | 0x02 | 0x05 | 0x04 |
| 0x3551 | Abgasrueckfuehrung (AGR) 2 | 0x01 | 0x02 | 0x03 | 0x05 |
| 0x3590 | Abgasrueckfuehrung (AGR) 1 | 0x01 | 0x02 | 0x03 | 0x05 |
| 0x3595 | Bremslicht- / Bremstestschalter | 0x01 | 0x05 | 0x03 | 0x10 |
| 0x0000 | unbekannter Fehlerort | 0x00 | 0x00 | 0x00 | 0x00 |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 32 rows × 33 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 | A6_0 | A6_1 | A7_0 | A7_1 | A8_0 | A8_1 | A9_0 | A9_1 | A10_0 | A10_1 | A11_0 | A11_1 | A12_0 | A12_1 | A13_0 | A13_1 | A14_0 | A14_1 | A15_0 | A15_1 | A16_0 | A16_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x0101 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x26 | 0x00 | 0x00 | 0x00 | 0x2C | 0x00 | 0x10 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x0111 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x11 | 0x00 | 0x2B | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x0116 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x11 | 0x00 | 0x2B | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x0121 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x10 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x0191 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x11 | 0x00 | 0x2B | 0x00 | 0x26 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x0208 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x28 | 0x00 | 0x00 | 0x00 | 0x27 | 0x00 | 0x12 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x22 | 0x00 | 0x00 |
| 0x0209 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x28 | 0x00 | 0x00 | 0x00 | 0x27 | 0x00 | 0x12 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x22 | 0x00 | 0x00 |
| 0x020A | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x28 | 0x00 | 0x00 | 0x00 | 0x27 | 0x00 | 0x12 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x22 | 0x00 | 0x00 |
| 0x020B | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x28 | 0x00 | 0x00 | 0x00 | 0x27 | 0x00 | 0x12 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x22 | 0x00 | 0x00 |
| 0x0236 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x2C | 0x00 | 0x10 | 0x00 | 0x26 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x0336 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x18 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x23 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x0501 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x2A |
| 0x0601 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x9 | 0x00 | 0x8 | 0x00 | 0x29 | 0x00 | 0x1A | 0x00 | 0x19 | 0x00 | 0xB | 0x00 | 0xA | 0x00 | 0x00 |
| 0x0606 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x16 | 0x00 | 0x00 |
| 0x09F6 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x32 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1191 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x14 | 0x00 | 0x17 | 0x00 | 0x00 | 0x00 | 0x1E | 0x00 | 0x13 | 0x00 | 0x1F | 0x00 | 0x00 | 0x00 | 0x30 |
| 0x1196 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x10 | 0x00 | 0x2C | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1612 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x31 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1613 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0xE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1641 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x5 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0xD | 0x00 | 0xC | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1DF1 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x1C |
| 0x1E26 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x1B | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x6 | 0x00 | 0xF | 0x00 | 0x7 | 0x00 | 0x00 |
| 0x1E46 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x24 | 0x00 | 0x25 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1E51 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x24 | 0x00 | 0x25 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1E56 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x11 | 0x00 | 0x10 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1E61 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x11 | 0x00 | 0x10 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x2801 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x2E | 0x00 | 0x2D | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x3006 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x2F |
| 0x3511 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x20 | 0x00 | 0x21 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x3551 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3 | 0x00 | 0x4 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x3590 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x1 | 0x00 | 0x2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x3595 | 0x00 | 0x00 | 0x00 | 0x00 | 0xEB | 0xEC | 0x00 | 0xEE | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xF6 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x1D |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 64 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x1 | AGR-Steller 1 Kurzschluss nach B+ |
| 0x2 | AGR-Steller 1 Unterbrechung oder Kurzschluss nach B- |
| 0x3 | AGR-Steller 2 Kurzschluss nach B+ |
| 0x4 | AGR-Steller 2 Unterbrechung oder Kurzschluss nach B- |
| 0x5 | Allgemeine Abgleiche Checksumme |
| 0x6 | Ausfall Drehzahlgebersignal Kurbelwelle |
| 0x7 | Ausfall Nockenwellengebersignal |
| 0x8 | Baustein defekt |
| 0x9 | Baustein offline |
| 0xA | Checksummenfehler |
| 0xB | GAD40 Quervergleich gestoert |
| 0xC | Injektorabgleich Checksumme |
| 0xD | Kommunikation mit EEPROM |
| 0xE | Korrekturmenge zu gross |
| 0xF | Kurbelwellengebersignal dynamisch unplausibel |
| 0x10 | Kurzschluss nach B+ |
| 0x11 | Kurzschluss nach B- |
| 0x12 | Lastabfall |
| 0x13 | Leckage |
| 0x14 | Maximaldruck ueberschritten |
| 0x15 | Mengendriftkompensation Checksumme |
| 0x16 | Microcontroller (Gate-Array Kommunikation) |
| 0x17 | Minimaldruck ueber Motordrehzahl zu klein |
| 0x18 | Motor hat ueberdreht |
| 0x19 | n-sync. Empfangsobjekt verzoegert |
| 0x1A | n-sync. Objekt nicht versendet |
| 0x1B | Nockenwellengebersignal Freqenz zu hoch |
| 0x1C | Plausibilitaet im Nachlauf |
| 0x1D | Plausibilitaet mit redundantem Kontakt |
| 0x1E | Raildruckregelventil klemmt |
| 0x1F | Regelabweichung ueber Motordrehzahl zu gross |
| 0x20 | Relais schaltet zu frueh ab |
| 0x21 | Relais schaltet zu spaet ab |
| 0x22 | Schnell-Loeschfehler |
| 0x23 | Signal dynamisch unplausibel |
| 0x24 | Spannung zu hoch |
| 0x25 | Spannung zu niedrig |
| 0x26 | Speisespannungsfehler |
| 0x27 | Strom an High Side zu gross |
| 0x28 | Strom an Low Side zu gross |
| 0x29 | t-sync. Empfangsobjekte verzoegert |
| 0x2A | Ueberwachung aus Master |
| 0x2B | Unterbrechung oder Kurzschluss nach B+ |
| 0x2C | Unterbrechung oder Kurzschluss nach B- |
| 0x2D | Versorgungsspannung DDE ueberschritten |
| 0x2E | Versorgungsspannung DDE unterschritten |
| 0x2F | Zuendstellung 2 Plausibilitaet nach Steuergeraet-Initialisierung |
| 0x30 | Raildruckueberhoehung |
| 0x31 | Ansteuerung wegen Fehler Raildruck-Regelung |
| 0x32 | Kein Raildruckaufbau |
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

Dimensions: 17 rows × 5 columns

| UWNR | UWTEXT | UW_EINH | UWF_A | UWF_B |
| --- | --- | --- | --- | --- |
| 0x00 | ---- | ---- | 1 | 0,0 |
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
| 0x16 | unbekannte Umweltbedingung | ---- | 1 | 0,0 |

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
