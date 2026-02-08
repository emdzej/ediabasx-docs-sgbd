# BMSS501.prg

- Jobs: [130](#jobs)
- Tables: [11](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | MSS50 fuer S50B32 |
| ORIGIN | BMW TI-433 Dennert |
| REVISION | 1.12 |
| AUTHOR | BMW TP-421 Weber, BMW EE-32 Schaffert, BMW TI-433 Dennert |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [EDIC_RESET](#job-edic-reset) - EDIC-Reset
- [initialisierung](#job-initialisierung) - Default Init-Job
- [INFO](#job-info) - Information SGBD
- [FS_LESEN_TEXT](#job-fs-lesen-text) - Auslesen des Fehlerspeichers (nur die F.-Namen)
- [ISN_LESEN](#job-isn-lesen) - liefert fertig formatierte ISN fuer MSS50
- [RAM_LESEN](#job-ram-lesen) - Beliebige RAM - Zellen auslesen
- [ROM_LESEN](#job-rom-lesen) - Beliebige FLASH - Zellen auslesen
- [EEPROM_LESEN](#job-eeprom-lesen) - Beliebige EEPROM - Zellen auslesen
- [IDENT](#job-ident) - Ident-Daten fuer DME
- [ADAPT_LOESCHEN](#job-adapt-loeschen) - alle Adaptionen gleichzeitig loeschen
- [ADAPT_SELEKTIV_LOESCHEN](#job-adapt-selektiv-loeschen) - Adaptionen bitweise loeschen und Zustaende bitweise setzen
- [STEUERN_LAMBDAREGLER_SPERREN](#job-steuern-lambdaregler-sperren) - LA-Regler ueber Adaptionstelegramm loeschen
- [STEUERN_LLS_TESTDREHZAHL](#job-steuern-lls-testdrehzahl) - feste Leerlaufanhebung fuer VANOS-Test
- [ABGAS_VARIANTE_LESEN](#job-abgas-variante-lesen) - Auslesen der Abgasvariante
- [STATUS_CODIER_CHECKSUMME](#job-status-codier-checksumme) - Codier - Checksumme abfragen
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender-Info-Feldes
- [FS_QUICK_LESEN](#job-fs-quick-lesen) - Auslesen des QUICK Fehlerspeichers
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [FS_SHADOW_LESEN](#job-fs-shadow-lesen) - Auslesen des Fehlerspeichers
- [STATUS_MOTORDREHZAHL](#job-status-motordrehzahl) - Motordrehzahl auslesen
- [STATUS_MOTORTEMPERATUR](#job-status-motortemperatur) - Motortemperatur auslesen
- [STATUS_AN_LUFTTEMPERATUR](#job-status-an-lufttemperatur) - Ansauglufttemperatur auslesen
- [STATUS_GESCHWINDIGKEIT](#job-status-geschwindigkeit) - Fahrzeuggeschwindigkeit
- [STATUS_ZUENDWINKEL](#job-status-zuendwinkel) - Wert Zuendwinkel  auslesen
- [STATUS_DK_POTI](#job-status-dk-poti) - Drosselklappenstellung  auslesen
- [STATUS_EVANOS_IST](#job-status-evanos-ist) - Wert Nockenwellenistposition Einlass auslesen
- [STATUS_AVANOS_IST](#job-status-avanos-ist) - Wert Nockenwellenistposition Auslass auslesen
- [STATUS_EVANOS_SOLL](#job-status-evanos-soll) - Wert Nockenwellensollposition Einlass auslesen
- [STATUS_AVANOS_SOLL](#job-status-avanos-soll) - Wert Nockenwellensollposition Auslass auslesen
- [STATUS_T_EINSPRITZ1](#job-status-t-einspritz1) - Wert Einspritzzeit (ohne Ub-Korrektur!) Bank1/Zyl1
- [STATUS_T_EINSPRITZ2](#job-status-t-einspritz2) - Wert Einspritzzeit (ohne Ub-Korrektur!) Bank2/Zyl4
- [STATUS_LA_REGLER1](#job-status-la-regler1) - Lambdaregler-Faktor Bank 1 auslesen
- [STATUS_LA_REGLER2](#job-status-la-regler2) - Lambdaregler-Faktor Bank 2 auslesen
- [STATUS_INT](#job-status-int) - INT-Signal
- [STATUS_INT_2](#job-status-int-2) - INT-Signal Bank 2
- [STATUS_ADD](#job-status-add) - ADD-Signal
- [STATUS_ADD_2](#job-status-add-2) - ADD-Signal Bank 2
- [STATUS_MUL](#job-status-mul) - MUL-Signal
- [STATUS_MUL_2](#job-status-mul-2) - MUL-Signal Bank 2
- [STATUS_KLOPF1](#job-status-klopf1) - Klopfsignal Zylinder 1
- [STATUS_KLOPF2](#job-status-klopf2) - Klopfsignal Zylinder 2
- [STATUS_KLOPF3](#job-status-klopf3) - Klopfsignal Zylinder 3
- [STATUS_KLOPF4](#job-status-klopf4) - Klopfsignal Zylinder 4
- [STATUS_KLOPF5](#job-status-klopf5) - Klopfsignal Zylinder 5
- [STATUS_KLOPF6](#job-status-klopf6) - Klopfsignal Zylinder 6
- [STATUS_UBATT](#job-status-ubatt) - Batteriespannung
- [STATUS_LMM](#job-status-lmm) - Luftmasse
- [STATUS_LL_LUFTBEDARF](#job-status-ll-luftbedarf) - Luftmasse
- [STATUS_UB](#job-status-ub) - Batteriespannung
- [STATUS_LUFTMASSE](#job-status-luftmasse) - Luftmasse
- [STATUS_TL](#job-status-tl) - Lastsignal
- [STATUS_OEL_TEMPERATUR](#job-status-oel-temperatur) - Motoroeltemperatur
- [STATUS_TVTE](#job-status-tvte) - Tankenlueftungsventil Highzeit
- [STATUS_AUSBLEND](#job-status-ausblend) - Anzahl ausgeblendeter Zylinder
- [STATUS_ADC_INTOUT1](#job-status-adc-intout1) - Integrator Klopfsensor 1/2 (MUX)
- [STATUS_ADC_INTOUT2](#job-status-adc-intout2) - Integrator Klopfsensor 1/2 (MUX)
- [STATUS_ADC_VPP](#job-status-adc-vpp) - Programmierspannung
- [STATUS_ADC_UBHR](#job-status-adc-ubhr) - Spannung Hauptrelaiskontakt
- [STATUS_ADC_TSG](#job-status-adc-tsg) - Steuergeraetetemperatur
- [STATUS_ADC_VEXT](#job-status-adc-vext) - Ausgang externe 5V-Versorgung
- [STATUS_ADC_UBINT](#job-status-adc-ubint) - interne 5V-Versorgung
- [STATUS_ADC_ULS1](#job-status-adc-uls1) - Lambdasondendifferenzspannung 1
- [STATUS_ADC_ULS2](#job-status-adc-uls2) - Lambdasondendifferenzspannung 2
- [STATUS_L_SONDE](#job-status-l-sonde) - Lambdasondendifferenzspannung 1
- [STATUS_L_SONDE_2](#job-status-l-sonde-2) - Lambdasondendifferenzspannung 2
- [STATUS_ADC_TANS](#job-status-adc-tans) - Fuehler Ansauglufttemperatur
- [STATUS_ADC_TMOT](#job-status-adc-tmot) - Ausgang externe 5V-Versorgung
- [STATUS_ADC_UHFM](#job-status-adc-uhfm) - Spannung Luftmassenmesser
- [STATUS_DKP_VOLT](#job-status-dkp-volt) - Schleifenspannung DK-Poti
- [STATUS_DIGITAL](#job-status-digital) - Status Schalteingaenge
- [STEUERN_EV_1](#job-steuern-ev-1) - EV  1 ansteuern
- [STEUERN_EV_2](#job-steuern-ev-2) - EV  2 ansteuern
- [STEUERN_EV_3](#job-steuern-ev-3) - EV 3 ansteuern
- [STEUERN_EV_4](#job-steuern-ev-4) - EV 4 ansteuern
- [STEUERN_EV_5](#job-steuern-ev-5) - EV  5 ansteuern
- [STEUERN_EV_6](#job-steuern-ev-6) - EV  6 ansteuern
- [STEUERN_Z_1](#job-steuern-z-1) - Z1 ansteuern
- [STEUERN_Z_2](#job-steuern-z-2) - Z2 ansteuern
- [STEUERN_Z_3](#job-steuern-z-3) - Z3 ansteuern
- [STEUERN_Z_4](#job-steuern-z-4) - Z4 ansteuern
- [STEUERN_Z_5](#job-steuern-z-5) - Z5 ansteuern
- [STEUERN_Z_6](#job-steuern-z-6) - Z6 ansteuern
- [STEUERN_SLP](#job-steuern-slp) - Sekundaerluftpumpe ansteuern
- [STEUERN_LSH](#job-steuern-lsh) - Lambdasondenheizung ansteuern
- [STEUERN_TEV](#job-steuern-tev) - Tankentlueftungsventil  ansteuern
- [STEUERN_ELUEFTER](#job-steuern-eluefter) - E-Luefterventil  ansteuern
- [STEUERN_FL](#job-steuern-fl) - Fehlerlampe NICHT UEBER DS2 - nur Pre-Drive-Check
- [STEUERN_LOEL](#job-steuern-loel) - Oelwarnlampe NICHT UEBER DS2 - Test nur ueber Pre-Drive-Check
- [STEUERN_AVANOS](#job-steuern-avanos) - EVANOS ansteuern
- [STEUERN_EVANOS](#job-steuern-evanos) - EVANOS ansteuern
- [STEUERN_EVANOS_VERSTELLZEIT](#job-steuern-evanos-verstellzeit) - Verstellzeitmessung EVANOS anstossen
- [STEUERN_AVANOS_VERSTELLZEIT](#job-steuern-avanos-verstellzeit) - Verstellzeitmessung AVANOS anstossen
- [STEUERN_EVANOS_DICHTHEIT](#job-steuern-evanos-dichtheit) - Dichtheitmessung EVANOS anstossen
- [STEUERN_AVANOS_DICHTHEIT](#job-steuern-avanos-dichtheit) - Dichtheitmessung EVANOS anstossen
- [STEUERN_EVANOS_FRUEHANSCHLAG](#job-steuern-evanos-fruehanschlag) - Fruehanschlag EVANOS anfahren
- [STEUERN_EVANOS_SPAETANSCHLAG](#job-steuern-evanos-spaetanschlag) - Spaetanschlag EVANOS anfahren
- [STEUERN_AVANOS_FRUEHANSCHLAG](#job-steuern-avanos-fruehanschlag) - Fruehanschlag AVANOS anfahren
- [STEUERN_AVANOS_SPAETANSCHLAG](#job-steuern-avanos-spaetanschlag) - Spaetanschlag AVANOS anfahren
- [STEUERN_LL_STELLER](#job-steuern-ll-steller) - Leerlaufsteller ansteuern (nur Stellglied)
- [STEUERN_EKP](#job-steuern-ekp) - EKP-Relais abschalten moeglich (ca.30s bis Motor aus)
- [STEUERN_KO](#job-steuern-ko) - Klimakompressorrelais ansteuern (5x 2s EIN/2s AUS)
- [UPROG_EIN](#job-uprog-ein) - Programmierspannung einschalten nach Info aus SG
- [UPROG_AUS](#job-uprog-aus) - Programmierspannung ausschalten
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
- [STATUS_TEV](#job-status-tev) - MUL-Signal TEV-Bank1
- [STATUS_TEV_2](#job-status-tev-2) - MUL-Signal TEV-Bank2
- [FS_EEPROM_LOESCHEN](#job-fs-eeprom-loeschen) - Loeschen des EEPROM-Fehlerspeichers
- [SPEICHER_SCHREIBEN_BINAER](#job-speicher-schreiben-binaer) - Schreibe binaere Bytes ueber direkte Adressierung Maximallaenge ist begrenzt

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

_No arguments._

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

<a id="job-abgas-variante-lesen"></a>
### ABGAS_VARIANTE_LESEN

Auslesen der Abgasvariante

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| ABGAS_VARIANTE_WERT | int | Abgasvariante 0=KAT-V , 1= KAT |

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
| F_STRING | binary | 10 Fehlerbyte |

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

<a id="job-status-motordrehzahl"></a>
### STATUS_MOTORDREHZAHL

Motordrehzahl auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_MOTORDREHZAHL_WERT | real | Ergebnis Motordrehzahl |
| STATUS_MOTORDREHZAHL_EINH | string | Einheit Motordrehzahl |

<a id="job-status-motortemperatur"></a>
### STATUS_MOTORTEMPERATUR

Motortemperatur auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_MOTORTEMPERATUR_WERT | real | Ergebnis Motortemperatur |
| STATUS_MOTORTEMPERATUR_EINH | string | Einheit Motortemperatur |

<a id="job-status-an-lufttemperatur"></a>
### STATUS_AN_LUFTTEMPERATUR

Ansauglufttemperatur auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_AN_LUFTTEMPERATUR_WERT | real | Ergebnis Ansauglufttemperatur |
| STATUS_AN_LUFTTEMPERATUR_EINH | string | Einheit Ansauglufttemperatur |

<a id="job-status-geschwindigkeit"></a>
### STATUS_GESCHWINDIGKEIT

Fahrzeuggeschwindigkeit

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_GESCHWINDIGKEIT_WERT | real | Motortemperatur Wert |
| STATUS_GESCHWINDIGKEIT_EINH | string | Einheit kmh |

<a id="job-status-zuendwinkel"></a>
### STATUS_ZUENDWINKEL

Wert Zuendwinkel  auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_ZUENDWINKEL_WERT | real | Ergebnis Zuendwinkel |
| STATUS_ZUENDWINKEL_EINH | string | Einheit Zuendwinkel |

<a id="job-status-dk-poti"></a>
### STATUS_DK_POTI

Drosselklappenstellung  auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_DK_POTI_WERT | real | Ergebnis Drosselklappenpoti |
| STATUS_DK_POTI_EINH | string | Einheit Drosselklappenpoti in % |

<a id="job-status-evanos-ist"></a>
### STATUS_EVANOS_IST

Wert Nockenwellenistposition Einlass auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_EVANOS_IST_WERT | real | Ergebnis Nockenwellenistposition Einlass |
| STATUS_EVANOS_IST_EINH | string | Einheit Nockenwellenposition |

<a id="job-status-avanos-ist"></a>
### STATUS_AVANOS_IST

Wert Nockenwellenistposition Auslass auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_AVANOS_IST_WERT | real | Ergebnis Nockenwellenistposition Auslass |
| STATUS_AVANOS_IST_EINH | string | Einheit Nockenwellenposition |

<a id="job-status-evanos-soll"></a>
### STATUS_EVANOS_SOLL

Wert Nockenwellensollposition Einlass auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_EVANOS_SOLL_WERT | real | Ergebnis Nockenwellensollposition Einlass |
| STATUS_EVANOS_SOLL_EINH | string | Einheit Nockenwellenposition |

<a id="job-status-avanos-soll"></a>
### STATUS_AVANOS_SOLL

Wert Nockenwellensollposition Auslass auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_AVANOS_SOLL_WERT | real | Ergebnis Nockenwellensollposition Auslass |
| STATUS_AVANOS_SOLL_EINH | string | Einheit Nockenwellenposition |

<a id="job-status-t-einspritz1"></a>
### STATUS_T_EINSPRITZ1

Wert Einspritzzeit (ohne Ub-Korrektur!) Bank1/Zyl1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_T_EINSPRITZ1_WERT | real | Ergebnis Einspritzzeit Bank1 |
| STATUS_T_EINSPRITZ1_EINH | string | Einheit Einspritzzeit |

<a id="job-status-t-einspritz2"></a>
### STATUS_T_EINSPRITZ2

Wert Einspritzzeit (ohne Ub-Korrektur!) Bank2/Zyl4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_T_EINSPRITZ2_WERT | real | Ergebnis Einspritzzeit Bank2 |
| STATUS_T_EINSPRITZ2_EINH | string | Einheit Einspritzzeit |

<a id="job-status-la-regler1"></a>
### STATUS_LA_REGLER1

Lambdaregler-Faktor Bank 1 auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_LA_REGLER1_WERT | real | Ergebnis Lambdaregler Bank 1 |
| STATUS_LA_REGLER1_EINH | string | Einheit Lambdaregler |

<a id="job-status-la-regler2"></a>
### STATUS_LA_REGLER2

Lambdaregler-Faktor Bank 2 auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_LA_REGLER2_WERT | real | Ergebnis Lambdaregler Bank 2 |
| STATUS_LA_REGLER2_EINH | string | Einheit Lambdaregler |

<a id="job-status-int"></a>
### STATUS_INT

INT-Signal

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_INT_WERT | real | INT-Signal Wert |
| STATUS_INT_EINH | string | Einheit |

<a id="job-status-int-2"></a>
### STATUS_INT_2

INT-Signal Bank 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_INT_2_WERT | real | INT-Signal Wert |
| STATUS_INT_2_EINH | string | Einheit |

<a id="job-status-add"></a>
### STATUS_ADD

ADD-Signal

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_ADD_WERT | real | ADD-Signal Wert |
| STATUS_ADD_EINH | string | Einheit |

<a id="job-status-add-2"></a>
### STATUS_ADD_2

ADD-Signal Bank 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_ADD_2_WERT | real | ADD-Signal Wert |
| STATUS_ADD_2_EINH | string | Einheit |

<a id="job-status-mul"></a>
### STATUS_MUL

MUL-Signal

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_MUL_WERT | real | MUL-Signal Wert |
| STATUS_MUL_EINH | string | Einheit [1] |

<a id="job-status-mul-2"></a>
### STATUS_MUL_2

MUL-Signal Bank 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_MUL_2_WERT | real | MUL-Signal Wert Bank 2 |
| STATUS_MUL_2_EINH | string | Einheit [1] |

<a id="job-status-klopf1"></a>
### STATUS_KLOPF1

Klopfsignal Zylinder 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_KLOPF1_WERT | real | Ergebnis Klopfsignal Zylinder 1 |
| STATUS_KLOPF1_EINH | string | Einheit Klofsignal |

<a id="job-status-klopf2"></a>
### STATUS_KLOPF2

Klopfsignal Zylinder 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_KLOPF2_WERT | real | Ergebnis Klopfsignal Zylinder 2 |
| STATUS_KLOPF2_EINH | string | Einheit Klofsignal |

<a id="job-status-klopf3"></a>
### STATUS_KLOPF3

Klopfsignal Zylinder 3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_KLOPF3_WERT | real | Ergebnis Klopfsignal Zylinder 3 |
| STATUS_KLOPF3_EINH | string | Einheit Klofsignal |

<a id="job-status-klopf4"></a>
### STATUS_KLOPF4

Klopfsignal Zylinder 4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_KLOPF4_WERT | real | Ergebnis Klopfsignal Zylinder 4 |
| STATUS_KLOPF4_EINH | string | Einheit Klofsignal |

<a id="job-status-klopf5"></a>
### STATUS_KLOPF5

Klopfsignal Zylinder 5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_KLOPF5_WERT | real | Ergebnis Klopfsignal Zylinder 5 |
| STATUS_KLOPF5_EINH | string | Einheit Klofsignal |

<a id="job-status-klopf6"></a>
### STATUS_KLOPF6

Klopfsignal Zylinder 6

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_KLOPF6_WERT | real | Ergebnis Klopfsignal Zylinder 6 |
| STATUS_KLOPF6_EINH | string | Einheit Klofsignal |

<a id="job-status-ubatt"></a>
### STATUS_UBATT

Batteriespannung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_UBATT_WERT | real | Ergebnis Batteriespannung |
| STATUS_UBATT_EINH | string | Einheit Spannung |

<a id="job-status-lmm"></a>
### STATUS_LMM

Luftmasse

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_LMM_WERT | real | Ergebnis Luftmasse |
| STATUS_LMM_EINH | string | Einheit Luftmasse |

<a id="job-status-ll-luftbedarf"></a>
### STATUS_LL_LUFTBEDARF

Luftmasse

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_LL_LUFTBEDARF_WERT | real | Ergebnis Luftmasse |
| STATUS_LL_LUFTBEDARF_EINH | string | Einheit Luftmasse |

<a id="job-status-ub"></a>
### STATUS_UB

Batteriespannung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_UB_WERT | real | Ergebnis Batteriespannung |
| STATUS_UB_EINH | string | Einheit Spannung |

<a id="job-status-luftmasse"></a>
### STATUS_LUFTMASSE

Luftmasse

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_LUFTMASSE_WERT | real | Ergebnis Luftmasse |
| STATUS_LUFTMASSE_EINH | string | Einheit Luftmasse |

<a id="job-status-tl"></a>
### STATUS_TL

Lastsignal

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_TL_WERT | real | Ergebnis Lastsignal |
| STATUS_TL_EINH | string | Einheit Lastsignal |

<a id="job-status-oel-temperatur"></a>
### STATUS_OEL_TEMPERATUR

Motoroeltemperatur

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_OEL_TEMPERATUR_WERT | real | Ergebnis Motoroeltemperatur |
| STATUS_OEL_TEMPERATUR_EINH | string | Einheit Motoroeltemperatur |

<a id="job-status-tvte"></a>
### STATUS_TVTE

Tankenlueftungsventil Highzeit

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_TVTE_WERT | real | Ergebnis Tankentlueftungsventil Highzeit |
| STATUS_TVTE_EINH | string | Einheit Zeit |

<a id="job-status-ausblend"></a>
### STATUS_AUSBLEND

Anzahl ausgeblendeter Zylinder

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_AUSBLEND_WERT | int | Ergebnis Anzahl ausgeblendeter Zylinder |
| STATUS_AUSBLEND_EINH | string | Einheit Anzahl |

<a id="job-status-adc-intout1"></a>
### STATUS_ADC_INTOUT1

Integrator Klopfsensor 1/2 (MUX)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_ADC_INTOUT1_WERT | real | Integrator Klopfsensor 1/2 |
| STATUS_ADC_INTOUT1_EINH | string | Einheit V |

<a id="job-status-adc-intout2"></a>
### STATUS_ADC_INTOUT2

Integrator Klopfsensor 1/2 (MUX)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_ADC_INTOUT2_WERT | real | Integrator Klopfsensor 3/- |
| STATUS_ADC_INTOUT2_EINH | string | Einheit V |

<a id="job-status-adc-vpp"></a>
### STATUS_ADC_VPP

Programmierspannung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_ADC_VPP_WERT | real | Programmierspannung |
| STATUS_ADC_VPP_EINH | string | Einheit V |

<a id="job-status-adc-ubhr"></a>
### STATUS_ADC_UBHR

Spannung Hauptrelaiskontakt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_ADC_UBHR_WERT | real |  |
| STATUS_ADC_UBHR_EINH | string | Einheit V |

<a id="job-status-adc-tsg"></a>
### STATUS_ADC_TSG

Steuergeraetetemperatur

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_ADC_TSG_WERT | real | Steuergeraetetemperatur |
| STATUS_ADC_TSG_EINH | string | Einheit V |

<a id="job-status-adc-vext"></a>
### STATUS_ADC_VEXT

Ausgang externe 5V-Versorgung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_ADC_VEXT_WERT | real |  |
| STATUS_ADC_VEXT_EINH | string | Einheit V |

<a id="job-status-adc-ubint"></a>
### STATUS_ADC_UBINT

interne 5V-Versorgung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_ADC_UBINT_WERT | real |  |
| STATUS_ADC_UBINT_EINH | string | Einheit V |

<a id="job-status-adc-uls1"></a>
### STATUS_ADC_ULS1

Lambdasondendifferenzspannung 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_ADC_ULS1_WERT | real |  |
| STATUS_ADC_ULS1_EINH | string | Einheit V |

<a id="job-status-adc-uls2"></a>
### STATUS_ADC_ULS2

Lambdasondendifferenzspannung 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_ADC_ULS2_WERT | real |  |
| STATUS_ADC_ULS2_EINH | string | Einheit V |

<a id="job-status-l-sonde"></a>
### STATUS_L_SONDE

Lambdasondendifferenzspannung 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_L_SONDE_WERT | real |  |
| STATUS_L_SONDE_EINH | string | Einheit V |

<a id="job-status-l-sonde-2"></a>
### STATUS_L_SONDE_2

Lambdasondendifferenzspannung 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_L_SONDE_2_WERT | real |  |
| STATUS_L_SONDE_2_EINH | string | Einheit V |

<a id="job-status-adc-tans"></a>
### STATUS_ADC_TANS

Fuehler Ansauglufttemperatur

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_ADC_TANS_WERT | real |  |
| STATUS_ADC_TANS_EINH | string | Einheit V |

<a id="job-status-adc-tmot"></a>
### STATUS_ADC_TMOT

Ausgang externe 5V-Versorgung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_ADC_TMOT_WERT | real |  |
| STATUS_ADC_TMOT_EINH | string | Einheit V |

<a id="job-status-adc-uhfm"></a>
### STATUS_ADC_UHFM

Spannung Luftmassenmesser

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_ADC_UHFM_WERT | real |  |
| STATUS_ADC_UHFM_EINH | string | Einheit V |

<a id="job-status-dkp-volt"></a>
### STATUS_DKP_VOLT

Schleifenspannung DK-Poti

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_DKP_VOLT_WERT | real |  |
| STATUS_DKP_VOLT_EINH | string | Einheit V |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

Status Schalteingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| BA_AKTIV | int | Status Beschleunigungsanreicherung |
| SA_AKTIV | int | Status Schubabschaltung |
| LSH_AKTIV | int | Status Lambdasondenheizung |
| ZUENDUNG1_AKTIV | int | Status Zuendung 1 |
| ZUENDUNG2_AKTIV | int | Status Zuendung 2 |
| ZUENDUNG3_AKTIV | int | Status Zuendung 3 |
| ZUENDUNG4_AKTIV | int | Status Zuendung 4 |
| ZUENDUNG5_AKTIV | int | Status Zuendung 5 |
| ZUENDUNG6_AKTIV | int | Status Zuendung 6 |
| SLP_AKTIV | int | Status Sekundaerluftpumpe |
| NOISE_AKTIV | int | Status Geraeuschminderung |
| SCHUTZ_AKTIV | int | Status Klopfschutzbetrieb |
| KLOPFREGELUNG_AKTIV | int | Status Klopfregelung |
| STATUS_AC_EIN | int | Status Klimabereitschaft |
| S_GANG_EIN | int | Status Gang |
| S_FPR_EIN | int | Status Fahrprogramm |
| STATUS_KO_EIN | int | Status Klimakompressor |
| S_FST_EIN | int | Status Tankreserve |
| S_KL15_EIN | int | Status Zuendung |
| S_KL50_EIN | int | Status Anlasser |
| MOTOR_STEHT | int | Status Motorstillstand |
| MOTOR_START | int | Status Start |
| STATUS_LL_EIN | int | Status Leerlauf |
| STATUS_VL_EIN | int | Status Teillast |
| MOTOR_TEILLAST | int | Status Vollast |
| MOTOR_ZUENDUNG_AUS | int | Status Zuendung |
| MOTOR_NACHLAUF | int | Status Nachlauf |

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

<a id="job-steuern-z-1"></a>
### STEUERN_Z_1

Z1 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-z-2"></a>
### STEUERN_Z_2

Z2 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-z-3"></a>
### STEUERN_Z_3

Z3 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-z-4"></a>
### STEUERN_Z_4

Z4 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-z-5"></a>
### STEUERN_Z_5

Z5 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-z-6"></a>
### STEUERN_Z_6

Z6 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-slp"></a>
### STEUERN_SLP

Sekundaerluftpumpe ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-lsh"></a>
### STEUERN_LSH

Lambdasondenheizung ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-tev"></a>
### STEUERN_TEV

Tankentlueftungsventil  ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-eluefter"></a>
### STEUERN_ELUEFTER

E-Luefterventil  ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-fl"></a>
### STEUERN_FL

Fehlerlampe NICHT UEBER DS2 - nur Pre-Drive-Check

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-loel"></a>
### STEUERN_LOEL

Oelwarnlampe NICHT UEBER DS2 - Test nur ueber Pre-Drive-Check

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-avanos"></a>
### STEUERN_AVANOS

EVANOS ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-evanos"></a>
### STEUERN_EVANOS

EVANOS ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-evanos-verstellzeit"></a>
### STEUERN_EVANOS_VERSTELLZEIT

Verstellzeitmessung EVANOS anstossen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| EVAN_VERSTELLZEIT_FRUEH | int |  |
| EVAN_VERSTELLZEIT_FRUEH_EINH | string |  |
| EVAN_VERSTELLZEIT_SPAET | int |  |
| EVAN_VERSTELLZEIT_SPAET_EINH | string |  |

<a id="job-steuern-avanos-verstellzeit"></a>
### STEUERN_AVANOS_VERSTELLZEIT

Verstellzeitmessung AVANOS anstossen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| AVAN_VERSTELLZEIT_FRUEH | int |  |
| AVAN_VERSTELLZEIT_FRUEH_EINH | string |  |
| AVAN_VERSTELLZEIT_SPAET | int |  |
| AVAN_VERSTELLZEIT_SPAET_EINH | string |  |

<a id="job-steuern-evanos-dichtheit"></a>
### STEUERN_EVANOS_DICHTHEIT

Dichtheitmessung EVANOS anstossen

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

<a id="job-steuern-avanos-dichtheit"></a>
### STEUERN_AVANOS_DICHTHEIT

Dichtheitmessung EVANOS anstossen

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

<a id="job-steuern-evanos-fruehanschlag"></a>
### STEUERN_EVANOS_FRUEHANSCHLAG

Fruehanschlag EVANOS anfahren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| EVAN_ISTWERT | int |  |
| EVAN_ISTWERT_EINH | string |  |
| EVAN_SOLLWERT | int |  |
| EVAN_SOLLWERT_EINH | string |  |

<a id="job-steuern-evanos-spaetanschlag"></a>
### STEUERN_EVANOS_SPAETANSCHLAG

Spaetanschlag EVANOS anfahren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| EVAN_ISTWERT | int |  |
| EVAN_ISTWERT_EINH | string |  |
| EVAN_SOLLWERT | int |  |
| EVAN_SOLLWERT_EINH | string |  |

<a id="job-steuern-avanos-fruehanschlag"></a>
### STEUERN_AVANOS_FRUEHANSCHLAG

Fruehanschlag AVANOS anfahren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| AVAN_ISTWERT | int |  |
| AVAN_ISTWERT_EINH | string |  |
| AVAN_SOLLWERT | int |  |
| AVAN_SOLLWERT_EINH | string |  |

<a id="job-steuern-avanos-spaetanschlag"></a>
### STEUERN_AVANOS_SPAETANSCHLAG

Spaetanschlag AVANOS anfahren

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

<a id="job-steuern-ekp"></a>
### STEUERN_EKP

EKP-Relais abschalten moeglich (ca.30s bis Motor aus)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ko"></a>
### STEUERN_KO

Klimakompressorrelais ansteuern (5x 2s EIN/2s AUS)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-uprog-ein"></a>
### UPROG_EIN

Programmierspannung einschalten nach Info aus SG

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

<a id="job-status-tev"></a>
### STATUS_TEV

MUL-Signal TEV-Bank1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_TEV_WERT | real | MUL-Signal Wert |
| STATUS_TEV_EINH | string | Einheit [1] |

<a id="job-status-tev-2"></a>
### STATUS_TEV_2

MUL-Signal TEV-Bank2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_TEV_2_WERT | real | MUL-Signal Wert Bank 2 |
| STATUS_TEV_2_EINH | string | Einheit [1] |

<a id="job-fs-eeprom-loeschen"></a>
### FS_EEPROM_LOESCHEN

Loeschen des EEPROM-Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

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

## Tables

### Index

- [BETRIEBSWMATRIX](#table-betriebswmatrix) (26 × 8)
- [BITS](#table-bits) (27 × 4)
- [FORTTEXTE](#table-forttexte) (69 × 6)
- [FARTMATRIX](#table-fartmatrix) (69 × 17)
- [FARTTEXTE](#table-farttexte) (42 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (42 × 5)
- [NULLEINSTEXTE](#table-nulleinstexte) (4 × 3)
- [JOBRESULT](#table-jobresult) (8 × 2)
- [PROGRESULT](#table-progresult) (16 × 2)
- [IORESULT](#table-ioresult) (6 × 2)
- [CODIER_CS](#table-codier-cs) (8 × 2)

<a id="table-betriebswmatrix"></a>
### BETRIEBSWMATRIX

Dimensions: 26 rows × 8 columns

| NAME | QUELLE | ZELLE | ORD | TYP | FAKT_A | FAKT_B | EINH |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Motordrehzahl | LINRAM | 0x600AA0 | HL | 1 | 0 | 1 | 1/min |
| Motortemperatur | LINRAM | 0xE004E4 | -- | 1 | -48 | 1 | Grad C |
| Ansauglufttemp | LINRAM | 0xE004DE | -- | 1 | -48 | 1 | Grad C |
| DK-Poti adaptiert | LINRAM | 0xE0068A | -- | 1 | 0 | 0.3922 | % |
| Geschwindigkeit | LINRAM | 0x600AB6 | HL | 1 | 0 | 1 | km/h |
| Luftmasse | LINRAM | 0xE00552 | HL | 1 | 0 | 0.25 | kg/h |
| Zuendwinkel_Zyl1 | LINRAM | 0x60046E | HL | 1 | 0 | 0.1 | Grad KW |
| Einspritzzeit_Bank1 | LINRAM | 0xE0044E | HL | 1 | 0 | 0.001 | ms |
| Einspritzzeit_Bank2 | LINRAM | 0xE00454 | HL | 1 | 0 | 0.001 | ms |
| EVANOS_Ist | LINRAM | 0xE00604 | HL | 1 | 0 | 0.1 | Grad KW |
| AVANOS_Ist | LINRAM | 0xE00634 | HL | 1 | 0 | 0.1 | Grad KW |
| Lambdaregler_Bank1 | LINRAM | 0xE0059A | HL | 1 | 0 | 0.0000305 | [1] |
| Lambdaregler_Bank2 | LINRAM | 0xE005AC | HL | 1 | 0 | 0.0000305 | [1] |
| Tastverh_TEV | LINRAM | 0xE00A0C | HL | 1 | 0 | 0.016 | ms |
| n_Ausblend_Zyl | LINRAM | 0xE004CE | -- | 1 | 0 | 1 | [1] |
| KMW1 | LINRAM | 0x60053C | -- | 1 | 0 | 0.0196 | Volt |
| KMW2 | LINRAM | 0x60053D | -- | 1 | 0 | 0.0196 | Volt |
| KMW3 | LINRAM | 0x60053E | -- | 1 | 0 | 0.0196 | Volt |
| KMW4 | LINRAM | 0x60053F | -- | 1 | 0 | 0.0196 | Volt |
| KMW5 | LINRAM | 0x600540 | -- | 1 | 0 | 0.0196 | Volt |
| KMW6 | LINRAM | 0x600541 | -- | 1 | 0 | 0.0196 | Volt |
| Ubatt | LINRAM | 0x600A80 | -- | 1 | 0 | 0.1 | Volt |
| EVANOS_Soll | LINRAM | 0xE00614 | -- | 1 | 0 | 1 | Grad KW |
| AVANOS_Soll | LINRAM | 0xE0064A | -- | 1 | 0 | 1 | Grad KW |
| Motoroeltemp. | LINRAM | 0xE00A53 | -- | 1 | -48 | 1 | Grad C |
| Lastsignal | LINRAM | 0xE0055A | HL | 1 | 0 | 0.001 | ms |

<a id="table-bits"></a>
### BITS

Dimensions: 27 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| BA | 0 | 0x01 | 0x01 |
| SA | 1 | 0x02 | 0x02 |
| LSH | 2 | 0x02 | 0x02 |
| TZ1 | 4 | 0x01 | 0x01 |
| TZ2 | 4 | 0x02 | 0x02 |
| TZ3 | 4 | 0x04 | 0x04 |
| TZ4 | 4 | 0x08 | 0x08 |
| TZ5 | 4 | 0x10 | 0x10 |
| TZ6 | 4 | 0x20 | 0x20 |
| SLP | 6 | 0x02 | 0x02 |
| NOISE | 8 | 0x80 | 0x80 |
| KLOPF | 10 | 0x02 | 0x02 |
| SCHUTZ | 10 | 0x01 | 0x01 |
| S_AC | 11 | 0x01 | 0x01 |
| S_GANG | 11 | 0x02 | 0x00 |
| S_FPR | 11 | 0x04 | 0x00 |
| S_KL50 | 11 | 0x08 | 0x00 |
| S_KO | 11 | 0x20 | 0x00 |
| S_FST | 11 | 0x40 | 0x40 |
| S_KL15 | 11 | 0x80 | 0x80 |
| M_SS | 12 | 0x01 | 0x01 |
| M_STRT | 12 | 0x02 | 0x02 |
| M_LL | 12 | 0x04 | 0x04 |
| M_TL | 12 | 0x08 | 0x08 |
| M_VL | 12 | 0x10 | 0x10 |
| M_ZA | 12 | 0x20 | 0x20 |
| M_NL | 12 | 0x40 | 0x40 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 69 rows × 6 columns

| ORT | ORTTEXT | UW_1 | UW_2 | UW_3 | UW_4 |
| --- | --- | --- | --- | --- | --- |
| 0x24 | Tankentlueftungsventil | 0x00 | 0x01 | 0x03 | 0x0C |
| 0x36 | Bordnetzspannung | 0x00 | 0x01 | 0x04 | 0x05 |
| 0x19 | Zuendendstufe 1 | 0x00 | 0x01 | 0x05 | 0x0D |
| 0x17 | Zuendendstufe 2 | 0x00 | 0x01 | 0x05 | 0x0D |
| 0x18 | Zuendendstufe 3 | 0x00 | 0x01 | 0x05 | 0x0D |
| 0x32 | Zuendendstufe 4 | 0x00 | 0x01 | 0x05 | 0x0D |
| 0x34 | Zuendendstufe 5 | 0x00 | 0x01 | 0x05 | 0x0D |
| 0x33 | Zuendendstufe 6 | 0x00 | 0x01 | 0x05 | 0x0D |
| 0x25 | Relais Lambdasondenheizung | 0x00 | 0x01 | 0x04 | 0x05 |
| 0x02 | Leerlaufsteller schliessende Spule | 0x00 | 0x01 | 0x04 | 0x0E |
| 0x1D | Leerlaufsteller oeffnende Spule | 0x00 | 0x01 | 0x04 | 0x0E |
| 0x9B | intern: Fehlerspeicher Master | 0x00 | 0x08 | 0x1A | 0x05 |
| 0x96 | intern: Speichertest Master | 0x00 | 0x08 | 0x1A | 0x05 |
| 0x0F | Zuendstrom Bank 1 | 0x00 | 0x01 | 0x04 | 0x05 |
| 0x09 | Zuendstrom Bank 2 | 0x00 | 0x01 | 0x04 | 0x05 |
| 0x46 | Klopfsensor 1 | 0x00 | 0x01 | 0x04 | 0x05 |
| 0x45 | Klopfsensor 2 | 0x00 | 0x01 | 0x04 | 0x05 |
| 0x44 | Klopfsensor 3 | 0x00 | 0x01 | 0x04 | 0x05 |
| 0x2A | Geschwindigkeitssensor | 0x00 | 0x01 | 0x04 | 0x11 |
| 0x97 | intern: Treiberdiagnose | 0x00 | 0x1A | 0x07 | 0x12 |
| 0x98 | intern: Kommunikation Master | 0x00 | 0x1A | 0x07 | 0x12 |
| 0x56 | CAN-Bus Off | 0x00 | 0x01 | 0x1A | 0x05 |
| 0x88 | Fehler Leerlaufregler | 0x00 | 0x01 | 0x04 | 0x0E |
| 0x50 | Schalter Gang | 0x00 | 0x01 | 0x11 | 0x05 |
| 0x89 | CAN-Protokollfehler | 0x00 | 0x01 | 0x1A | 0x05 |
| 0x8A | CAN-Timeout Botschaft 1 | 0x00 | 0x01 | 0x1A | 0x05 |
| 0x8B | CAN-Timeout Botschaft 2 | 0x00 | 0x01 | 0x1A | 0x05 |
| 0x8C | CAN-Timeout Botschaft 3 | 0x00 | 0x01 | 0x1A | 0x05 |
| 0x9F | intern: Klopfbaustein 1 | 0x00 | 0x01 | 0x04 | 0x05 |
| 0xA0 | intern: Klopfbaustein 2 | 0x00 | 0x01 | 0x04 | 0x05 |
| 0xA1 | intern: Klopfbaustein 3 | 0x00 | 0x01 | 0x04 | 0x05 |
| 0xA2 | Synchronisation NW-Geber | 0x00 | 0x01 | 0x04 | 0x05 |
| 0x52 | Anlasserschalter KL50 | 0x00 | 0x01 | 0x1A | 0x23 |
| 0xA3 | intern: SG-Reset | 0x00 | 0x1A | 0x06 | 0x1B |
| 0x35 | Relais Elektroluefter | 0x00 | 0x01 | 0x04 | 0x05 |
| 0x82 | EWS-Signalmanipulation | 0x25 | 0x26 | 0x1A | 0x05 |
| 0x10 | Fehler KW-Geber | 0x00 | 0x01 | 0x04 | 0x0F |
| 0x9C | intern: Fehlerspeicher Slave | 0x00 | 0x01 | 0x1A | 0x05 |
| 0x9D | intern: Speichertest Slave | 0x00 | 0x01 | 0x1A | 0x05 |
| 0x40 | Klimaschalter AC/KO | 0x23 | 0x24 | 0x04 | 0x05 |
| 0x01 | Relais Kraftstoffpumpe | 0x00 | 0x01 | 0x04 | 0x05 |
| 0x13 | Relais Sekundaerluftpumpe | 0x00 | 0x01 | 0x04 | 0x05 |
| 0x4E | Kuehlwassertemperaturfuehler | 0x00 | 0x01 | 0x04 | 0x05 |
| 0x4D | Ansauglufttemperaturfuehler | 0x00 | 0x01 | 0x08 | 0x05 |
| 0x0D | Lambdasonde 1 | 0x00 | 0x01 | 0x09 | 0x05 |
| 0x0C | Lambdasonde 2 | 0x00 | 0x01 | 0x0A | 0x05 |
| 0x29 | Luftmassenmesser | 0x00 | 0x02 | 0x0B | 0x13 |
| 0x49 | Drosselklappenpotentiometer | 0x00 | 0x01 | 0x04 | 0x0B |
| 0x90 | Lambdaregler 1 | 0x00 | 0x01 | 0x04 | 0x13 |
| 0x91 | Lambdaregler 2 | 0x00 | 0x01 | 0x04 | 0x27 |
| 0x30 | Relais Klimakompressor | 0x00 | 0x01 | 0x04 | 0x05 |
| 0x07 | Einlassnockenwellengeber | 0x00 | 0x01 | 0x02 | 0x14 |
| 0x0A | Auslassnockenwellengeber | 0x00 | 0x01 | 0x02 | 0x15 |
| 0x43 | Einlass-VANOS-Fruehventil | 0x00 | 0x01 | 0x04 | 0x16 |
| 0x48 | Einlass-VANOS-Spaetventil | 0x00 | 0x01 | 0x04 | 0x17 |
| 0x16 | Auslass-VANOS-Fruehventil | 0x00 | 0x01 | 0x04 | 0x18 |
| 0x15 | Auslass-VANOS-Spaetventil | 0x00 | 0x01 | 0x04 | 0x19 |
| 0x2C | aktiver Oelniveaugeber | 0x00 | 0x01 | 0x04 | 0x1C |
| 0x2E | Verbrauchssignal | 0x00 | 0x01 | 0x1A | 0x05 |
| 0x2F | Drehzahlsignal | 0x00 | 0x01 | 0x1A | 0x05 |
| 0x42 | EWS-Schnittstelle | 0x00 | 0x08 | 0x04 | 0x05 |
| 0x03 | Einspritzventil 1 | 0x00 | 0x01 | 0x05 | 0x1D |
| 0x05 | Einspritzventil 2 | 0x00 | 0x01 | 0x05 | 0x1E |
| 0x04 | Einspritzventil 3 | 0x00 | 0x01 | 0x05 | 0x1F |
| 0x21 | Einspritzventil 4 | 0x00 | 0x01 | 0x05 | 0x20 |
| 0x1F | Einspritzventil 5 | 0x00 | 0x01 | 0x05 | 0x21 |
| 0x20 | Einspritzventil 6 | 0x00 | 0x01 | 0x05 | 0x22 |
| 0x9E | intern: Kommunikation Slave | 0x00 | 0x01 | 0x07 | 0x12 |
| 0xXY | unbekannter Fehlercode | 0xFF | 0xFF | 0xFF | 0xFF |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 69 rows × 17 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 | A6_0 | A6_1 | A7_0 | A7_1 | A8_0 | A8_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x24 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x0D | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x36 | 0x00 | 0x06 | 0x00 | 0x13 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x19 | 0x00 | 0x0E | 0x00 | 0x0F | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x17 | 0x00 | 0x0E | 0x00 | 0x0F | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x18 | 0x00 | 0x0E | 0x00 | 0x0F | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x32 | 0x00 | 0x0E | 0x00 | 0x0F | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x34 | 0x00 | 0x0E | 0x00 | 0x0F | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x33 | 0x00 | 0x0E | 0x00 | 0x0F | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x25 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x0D | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x02 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x0D | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x1D | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x0D | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x9B | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x28 | 0x00 | 0x1A | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x96 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x1F | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x0F | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x0B | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x09 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x0B | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x46 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x45 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x44 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x2A | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x97 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x1B | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x98 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x1B | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x56 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x16 | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x88 | 0x00 | 0x23 | 0x00 | 0x24 | 0x00 | 0x25 | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x50 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x0B | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x89 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x1B | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x8A | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x16 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x8B | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x16 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x8C | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x16 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x9F | 0x00 | 0x1D | 0x00 | 0x1E | 0x00 | 0x1B | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xA0 | 0x00 | 0x1D | 0x00 | 0x1E | 0x00 | 0x1B | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xA1 | 0x00 | 0x1D | 0x00 | 0x1E | 0x00 | 0x1B | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xA2 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x52 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x0B | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xA3 | 0x00 | 0x26 | 0x00 | 0x27 | 0x00 | 0x08 | 0x00 | 0x1C | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x35 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x0D | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x82 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x15 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x10 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x16 | 0x00 | 0x0C | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x9C | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x28 | 0x00 | 0x1A | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x9D | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x1F | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x40 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x01 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x0D | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x13 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x0D | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x4E | 0x00 | 0x12 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x4D | 0x00 | 0x12 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x0D | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x0B | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x0C | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x0B | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x29 | 0x00 | 0x06 | 0x00 | 0x13 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x49 | 0x00 | 0x12 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x90 | 0x00 | 0x20 | 0x00 | 0x21 | 0x00 | 0x08 | 0x00 | 0x22 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x91 | 0x00 | 0x20 | 0x00 | 0x21 | 0x00 | 0x08 | 0x00 | 0x22 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x30 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x0D | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x07 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x16 | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x0A | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x16 | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x43 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x0D | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x48 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x0D | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x16 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x0D | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x15 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x0D | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x2C | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x0B | 0x00 | 0x09 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x2E | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x0D | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x2F | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x0D | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x42 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x16 | 0x00 | 0x17 | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x03 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x0D | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x0D | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x04 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x0D | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x21 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x0D | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x1F | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x0D | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x20 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x0D | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x9E | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x1B | 0x00 | 0x0a | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xXY | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 42 rows × 2 columns

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
| 0x09 | Unplausibler Zustand / Wert unplausibel |
| 0x0A | Abgasrelevanter Fehler |
| 0x0B | Leitungsbruch / Abriss |
| 0x0C | Stoerung |
| 0x0D | Treiber Uebertemperatur |
| 0x0E | Primaerkreisfehler |
| 0x0F | Sekundaerkreisfehler |
| 0x10 | Sensorwiderstand abgefallen |
| 0x11 | Kommunikationsfehler SPI |
| 0x12 | Kurzschluss nach UBatt / Wert zu gross / Abriss |
| 0x13 | Kurzschluss nach Masse / Wert zu klein / Abriss |
| 0x14 | Signal fehlt |
| 0x15 | Signal manipuliert / unerwartet |
| 0x16 | Signal fehlt / Timeout / Leitungsbruch |
| 0x17 | Paritaetsfehler |
| 0x18 | Spule Primaerkreisfehler |
| 0x19 | Spule Sekundaerkreisfehler |
| 0x1A | Initialisierung / Abspeicherung gestoert |
| 0x1B | Kommunikation gestoert |
| 0x1C | unzulaessige Resets / FLASH defekt / DS2-SG-Reset |
| 0x1D | Integratorschwelle ueberschritten |
| 0x1E | Integratorschwelle unterschritten |
| 0x1F | Test unplausibel |
| 0x20 | Regler laeuft gegen Maximalwert |
| 0x21 | Regler laeuft gegen Minimalwert |
| 0x22 | Regelung unplausibel |
| 0x23 | Steller klemmt offen |
| 0x24 | Steller klemmt geschlossen |
| 0x25 | Leckluft |
| 0x26 | Reset Master |
| 0x27 | Reset Slave |
| 0x28 | Pruefsumme falsch / Manipulation |
| 0xXY | unbekannte Fehlerart |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 42 rows × 5 columns

| UWNR | UWTEXT | UW_EINH | UWF_B | UWF_A |
| --- | --- | --- | --- | --- |
| 0x00 | Motordrehzahl | 1/min | 0 | 40 |
| 0x01 | Lastsignal | ms | 0 | 0.032 |
| 0x02 | DK-Poti adaptiert | % | 0 | 0.3922 |
| 0x03 | Tastverh. Tankentl. | ms | 0 | 0.512 |
| 0x04 | Motortemperatur | Grad C | -48 | 1 |
| 0x05 | Batteriespannung HR | V | 0 | 0.1 |
| 0x06 | Resetzaehler Master | - | 0 | 1 |
| 0x07 | SPI-Fehlercode | - | 0 | 1 |
| 0x08 | Ansauglufttemperatur | Grad C | -48 | 1 |
| 0x09 | Lambdasondenspannung 1 | V | 0 | 0.032 |
| 0x0a | Lambdasondenspannung 2 | V | 0 | 0.032 |
| 0x0b | Spg. Luftmassenmesser | V | 0 | 0.032 |
| 0x0c | Statusmaske Tankentl. | - | 0 | 1 |
| 0x0d | Schliesszeit | ms | 0 | 0.128 |
| 0x0e | Tastverh. LL-Steller | ms | 0 | 64 |
| 0x0f | Status TPU_PMMX_IRQ | - | 0 | 1 |
| 0x10 | Reset-Register CPU | - | 0 | 1 |
| 0x11 | Geschwindigkeit | km/h | 0 | 2 |
| 0x12 | IPK-Fehlercode | - | 0 | 1 |
| 0x13 | Adaptionsfaktor ti1 | - | 0 | 0.0078125 |
| 0x14 | EVANOS-Ist-Winkel | Grad KW | 0 | 0.8 |
| 0x15 | AVANOS-Ist-Winkel | Grad KW | 0 | 0.8 |
| 0x16 | Pulsz. EVANOS-Fruehv. | ms | 0 | 2.048 |
| 0x17 | Pulsz. EVANOS-Spaetv. | ms | 0 | 2.048 |
| 0x18 | Pulsz. AVANOS-Fruehv. | ms | 0 | 2.048 |
| 0x19 | Pulsz. AVANOS-Spaetv. | ms | 0 | 2.048 |
| 0x1A | Steuergeraetetemp. | Grad C | -48 | 1 |
| 0x1B | Resetzaehler Slave | - | 0 | 1 |
| 0x1C | Motoroeltemperatur | Grad C | 0 | 1 |
| 0x1D | Einspritzzeit 1 | ms | 0 | 0.256 |
| 0x1E | Einspritzzeit 2 | ms | 0 | 0.256 |
| 0x1F | Einspritzzeit 3 | ms | 0 | 0.256 |
| 0x20 | Einspritzzeit 4 | ms | 0 | 0.256 |
| 0x21 | Einspritzzeit 5 | ms | 0 | 0.256 |
| 0x22 | Einspritzzeit 6 | ms | 0 | 0.256 |
| 0x23 | Zust.-Maske Schalter | - | 0 | 1 |
| 0x24 | Zust.-Maske Klima | - | 0 | 1 |
| 0x25 | ISN-high $0x.. | - | 0 | 1 |
| 0x26 | ISN-low  $..xx | - | 0 | 1 |
| 0x27 | Adaptionsfaktor ti2 | - | 0 | 0.0078125 |
| 0xFF | unbekannte Umweltbed. | - | 0 | 1 |
| 0xXY | ---- | ---- | 0 | 1 |

<a id="table-nulleinstexte"></a>
### NULLEINSTEXTE

Dimensions: 4 rows × 3 columns

| SELECTOR | 0 | 1 |
| --- | --- | --- |
| AE | AUS | EIN |
| OZ | OFFEN | ZU |
| AA | AUS | AKTIV |
| XY | --?-- | --?-- |

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 8 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xB2 | ERROR_ECU_NUMBER |
| 0xFF | ERROR_ECU_NACK |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |

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
| 0x06 | Programmierspannung zu niedrig |
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

<a id="table-ioresult"></a>
### IORESULT

Dimensions: 6 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | Stellglied wird angesteuert |
| 0x01 | Ansteuerung nicht fuer diese Pin-Nummer |
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
