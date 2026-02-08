# EKM.prg

- Jobs: [21](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Elektronik Karosseriemodul EKM E31 |
| ORIGIN | BMW TI-433 Dennert |
| REVISION | 2.02 |
| AUTHOR | Softing Taubert, BMW ET-421 Drexel, BMW TI-433 Dennert |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung
- [IDENT](#job-ident) - Auslesen der Identifikationsdaten
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Beenden der Diagnose
- [GWSZ_RESET](#job-gwsz-reset) - Ruecksetzen des Gesamtwegstreckenzaehlers
- [SIA_RESET](#job-sia-reset) - Ruecksetzen der Service-Intervall-Anzeige
- [STATUS_MOTOR](#job-status-motor) - Pruefung ob Motor ein oder aus Wenn die Motordrehzahl groesser 360 U/min ist wird auf "Motor ist ein" erkannt
- [STATUS_DIAGNOSE_LESEN](#job-status-diagnose-lesen) - Abfrage der aktuellen Diagnose-Stati
- [STATUS_DIGITAL_GEFILTERT_LESEN](#job-status-digital-gefiltert-lesen) - Lesen der gefilterten Digitalwerte
- [STATUS_DIGITAL_UNGEFILTERT_LESEN](#job-status-digital-ungefiltert-lesen) - Lesen der ungefilterten Digitalwerte
- [CODIERDATEN_LESEN](#job-codierdaten-lesen) - Codierdaten lesen
- [SIA_DATEN_LESEN](#job-sia-daten-lesen) - SIA-Daten lesen und interpretieren
- [CODIERUNG_LESEN](#job-codierung-lesen) - Codier-Daten lesen und interpretieren
- [SPEICHER_LESEN](#job-speicher-lesen) - Speicher auslesen
- [SPEICHER_LESEN_IO_PROZ](#job-speicher-lesen-io-proz) - Speicher auslesen
- [STATUS_AUSGAENGE_LESEN](#job-status-ausgaenge-lesen) - Stati der Ausgaenge lesen
- [STATUS_ANALOG_GEFILTERT_LESEN](#job-status-analog-gefiltert-lesen) - gefilterte Analogwerte lesen
- [STATUS_ANALOG_UNGEFILTERT_LESEN](#job-status-analog-ungefiltert-lesen) - ungefilterte Analogwerte lesen
- [TACHO_A](#job-tacho-a) - liefert geschwindigkeitsproportionales Signal

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

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn i.O. |

<a id="job-ident"></a>
### IDENT

Auslesen der Identifikationsdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| ID_GEN_NR | string | Generationsnummer |
| ID_HW_NR | string | Hardwarenummer |
| ID_SW_NR | string | Softwarenummer |
| ID_PP_NR | string | Pruefplannummer |
| ID_DATUM_KW | string | Herstelldatum KW |
| ID_DATUM_JAHR | string | Herstelldatum Jahr |

<a id="job-fs-lesen"></a>
### FS_LESEN

Auslesen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| F_ORT_NR | int | Nr. des Fehlers |
| F_ORT_TEXT | string | Fehlertext |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen |
| F_HFK | int | Haeufigkeit eines Fehlers |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Beenden der Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-gwsz-reset"></a>
### GWSZ_RESET

Ruecksetzen des Gesamtwegstreckenzaehlers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-sia-reset"></a>
### SIA_RESET

Ruecksetzen der Service-Intervall-Anzeige

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG1 | string | Oel/Weg oder Zeit - Reset |
| ARG2 | string | Oel/Weg oder Zeit - Reset |
| ARG3 | string | Oel/Weg oder Zeit - Reset |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY, ERROR_NACK od. ERROR_PARAMETER |

<a id="job-status-motor"></a>
### STATUS_MOTOR

Pruefung ob Motor ein oder aus Wenn die Motordrehzahl groesser 360 U/min ist wird auf "Motor ist ein" erkannt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY, ERROR_NACK |
| STAT_MOTOR_EIN | int | wenn Motor ein, dann 1, sonst 0 |

<a id="job-status-diagnose-lesen"></a>
### STATUS_DIAGNOSE_LESEN

Abfrage der aktuellen Diagnose-Stati

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_GESCHW_SIM_AKTIV | int | Geschwindigkeits-Simulation ein |
| STAT_AD_ID_UNGUELTIG | int | AD- und ID-Werte voruebergehend ungueltig |
| STAT_SPANNUNG_INSTABIL | int | Klemmen oder Bordspannung &gt; 2sec instabil |
| STAT_AND_XOR_AUS | int | And- und Xor-Masken werden nicht verwendet |
| STAT_KL15_KL30_TEST_AKTIV | int | KL15 und KL30 PD im testmode |
| STAT_KL30_TEST_AKTIV | int | KL30 im Testmode |
| STAT_AD_SIM_AKTIV | int | AD-Werte werden simuliert |
| STAT_DIG_IN_SIM_AKTIV | int | digitale Eingaenge werden simuliert |
| STAT_DIG_OUT_SIM_AKTIV | int | digitale Ausgaenge werden simuliert |
| STAT_VERBR_SIM_AKTIV | int | Verbrauchs-Simulation ein |
| STAT_DREHZ_SIM_AKTIV | int | Drehzahl-Simulation ein |
| STAT_RELOAD_TIME_WERT | int | Reloadzeit fuer Diagnosemodes |
| STAT_RELOAD_TIME_EINH | string | Einheit fuer Realoadzeit |
| STAT_REST_DIA_ZEIT_WERT | int | restliche Diagnosezeit |
| STAT_REST_DIA_ZEIT_EINH | string | Einheit restliche Diagnosezeit |
| STAT_REST_TACHO_ZEIT_WERT | int | restliche Tachosimulationszeit |
| STAT_REST_TACHO_ZEIT_EINH | string | Einheit restliche Tachosimulationszeit |
| STAT_KL | string | Klemmenstatus (KL30, KLR, KL15, KL50) |

<a id="job-status-digital-gefiltert-lesen"></a>
### STATUS_DIGITAL_GEFILTERT_LESEN

Lesen der gefilterten Digitalwerte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_KLR_AKTIV | int | Klemme R aktiv |
| STAT_KL15_AKTIV | int | Klemme 15 aktiv |
| STAT_FAHRERTUER_ZU | int | Fahrertuer ist geschlossen |
| STAT_KOMBISCHNITTSTELLE | int | ?? |
| STAT_I_BUS | int | ?? |
| STAT_KL50_AKTIV | int | Klemme 50 aktiv |
| STAT_DWA_RADIO_EINGEBAUT | int | DWA-Kontakt meldet Radio ist eingebaut |
| STAT_GETRIEBEWAHLSCHALTER1_L1_AKTIV | int | Getriebewahlschalter1 (L1) ist geschlossen |
| STAT_GETRIEBEWAHLSCHALTER2_L2_AKTIV | int | Getriebewahlschalter (L2) ist geschlossen |
| STAT_GETRIEBEWAHLSCHALTER3_L3_AKTIV | int | Getriebewahlschalter (L3) ist geschlossen |
| STAT_GETRIEBEWAHLSCHALTER4_L4_AKTIV | int | Getriebewahlschalter (L4) ist geschlossen |
| STAT_GETRIEBEWAEHLHEBEL_POSITION | string | Getriebewaehlhebelposition (P,R,N,D,4,3,2,1,unbekannt) |
| STAT_PROGRAMMWAHLSCHALTER1_L6_OFFEN | int | Programmwahlschalter1 (L6) ist offen |
| STAT_PROGRAMMWAHLSCHALTER2_L7_OFFEN | int | Programmwahlschalter2 (L7) ist offen |
| STAT_SICHERHEITSGURT_GESTECKT | int | Sicherheitsgurt ist eingesteckt |
| STAT_SIA_RESET_HIGH | int | Sia-Reset ist high (kein Reset) |
| STAT_MOTOROELDRUCK_OK | int | Motoroeldruck hat korrekten Wert (i.O.) |
| STAT_WASCHWASSERSTAND_ZU_NIEDRIG | int | Wasserstand ist unter Minimum |
| STAT_LENKHILFE_OELSTAND_ZU_NIEDRIG | int | Oelstand ist unter Minimum |
| STAT_BREMSDRUCK_OK | int | Bremsdruck hat korrekten Wert (i.O.) |
| STAT_BREMSFLUESSIGKEITSSTAND_OK | int | Bremsfluessigkeitsstand hat korrekten Wert (i.O.) |
| STAT_KATALYSATOR_TEMP_OK | int | Katalysator-Temperatur ist ok |
| STAT_STARTBLOCK_AKTIV | int | Startblockierung ist aktiv (Zuendung ist unterbrochen) |
| STAT_MOTOROELSTAND_ZU_NIEDRIG | int | Motoroelstand ist unter Minimum |
| STAT_ZUENDSCHLUESSEL_ABGEZOGEN | int | der Zuendschluessel ist nicht im Zuendschloss |
| STAT_HECKKLAPPE_ZU | int | Heckklappe ist geschlossen |
| STAT_HANDBREMSE_GELOEST | int | Handbremse ist nicht angezogen |
| STAT_BREMSBELAG_VERSCHLISSEN | int | Bremsbelag ist verschlissen |
| STAT_EGS_DEFEKT | int | EGS ist defekt (nicht auswerten bei Schaltgetriebe!!!) |
| STAT_DWA_ALARM_OFF | int | DWA-Alarm ist nicht angesteuert |
| STAT_STANDLFTG_OFF | int | Standlueftung ist nicht angesteuert |
| STAT_STANDHZG_OFF | int | Standheizung ist nicht angesteuert |
| STAT_TACHO_A | int | ?? |
| STAT_AKUSTIK1_OFF | int | Akustik-Ausgang1 ist nicht aktiv |
| STAT_AKUSTIK2_OFF | int | Akustik-Ausgang2 ist nicht aktiv |
| STAT_AKUSTIK3_OFF | int | Akustik-Ausgang3 ist nicht aktiv |

<a id="job-status-digital-ungefiltert-lesen"></a>
### STATUS_DIGITAL_UNGEFILTERT_LESEN

Lesen der ungefilterten Digitalwerte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_KLR_AKTIV | int | Klemme R aktiv |
| STAT_KL15_AKTIV | int | Klemme 15 aktiv |
| STAT_FAHRERTUER_ZU | int | Fahrertuer ist geschlossen |
| STAT_KOMBISCHNITTSTELLE | int | ?? |
| STAT_I_BUS | int | ?? |
| STAT_KL50_AKTIV | int | Klemme 50 aktiv |
| STAT_DWA_RADIO_EINGEBAUT | int | DWA-Kontakt meldet Radio ist eingebaut |
| STAT_GETRIEBEWAHLSCHALTER1_L1_AKTIV | int | Getriebewahlschalter1 (L1) ist geschlossen |
| STAT_GETRIEBEWAHLSCHALTER2_L2_AKTIV | int | Getriebewahlschalter (L2) ist geschlossen |
| STAT_GETRIEBEWAHLSCHALTER3_L3_AKTIV | int | Getriebewahlschalter (L3) ist geschlossen |
| STAT_GETRIEBEWAHLSCHALTER4_L4_AKTIV | int | Getriebewahlschalter (L4) ist geschlossen |
| STAT_GETRIEBEWAEHLHEBEL_POSITION | string | Getriebewaehlhebelposition (P,R,N,D,4,3,2,1,unbekannt) |
| STAT_PROGRAMMWAHLSCHALTER1_L6_OFFEN | int | Programmwahlschalter1 (L6) ist offen |
| STAT_PROGRAMMWAHLSCHALTER2_L7_OFFEN | int | Programmwahlschalter2 (L7) ist offen |
| STAT_SICHERHEITSGURT_GESTECKT | int | Sicherheitsgurt ist eingesteckt |
| STAT_SIA_RESET_HIGH | int | Sia-Reset ist high (kein Reset) |
| STAT_MOTOROELDRUCK_OK | int | Motoroeldruck hat korrekten Wert (i.O.) |
| STAT_WASCHWASSERSTAND_ZU_NIEDRIG | int | Wasserstand ist unter Minimum |
| STAT_LENKHILFE_OELSTAND_ZU_NIEDRIG | int | Oelstand ist unter Minimum |
| STAT_BREMSDRUCK_OK | int | Bremsdruck hat korrekten Wert (i.O.) |
| STAT_BREMSFLUESSIGKEITSSTAND_OK | int | Bremsfluessigkeitsstand hat korrekten Wert (i.O.) |
| STAT_KATALYSATOR_TEMP_OK | int | Katalysator-Temperatur ist ok |
| STAT_STARTBLOCK_AKTIV | int | Startblockierung ist aktiv (Zuendung ist unterbrochen) |
| STAT_MOTOROELSTAND_ZU_NIEDRIG | int | Motoroelstand ist unter Minimum |
| STAT_ZUENDSCHLUESSEL_ABGEZOGEN | int | der Zuendschluessel ist nicht im Zuendschloss |
| STAT_HECKKLAPPE_ZU | int | Heckklappe ist geschlossen |
| STAT_HANDBREMSE_GELOEST | int | Handbremse ist nicht angezogen |
| STAT_BREMSBELAG_VERSCHLISSEN | int | Bremsbelag ist verschlissen |
| STAT_EGS_DEFEKT | int | EGS ist defekt (nicht auswerten bei Schaltgetriebe!!!) |
| STAT_DWA_ALARM_OFF | int | DWA-Alarm ist nicht angesteuert |
| STAT_STANDLFTG_OFF | int | Standlueftung ist nicht angesteuert |
| STAT_STANDHZG_OFF | int | Standheizung ist nicht angesteuert |
| STAT_TACHO_A | int | ?? |
| STAT_AKUSTIK1_OFF | int | Akustik-Ausgang1 ist nicht aktiv |
| STAT_AKUSTIK2_OFF | int | Akustik-Ausgang2 ist nicht aktiv |
| STAT_AKUSTIK3_OFF | int | Akustik-Ausgang3 ist nicht aktiv |

<a id="job-codierdaten-lesen"></a>
### CODIERDATEN_LESEN

Codierdaten lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int | Speicheradresse im I/O-Prozessor |
| ANZAHL | int | Anzahl der zu lesenden Bytes (1..10) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| COD_DATA | binary | Hexdump |

<a id="job-sia-daten-lesen"></a>
### SIA_DATEN_LESEN

SIA-Daten lesen und interpretieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| KM_STAND_GWSZ | real | Stand des Gesamtwegstreckenzaehler 0 bis 1048482 [km] |
| STAND_SIA_INSPEKTION | real | Stand des SIA-Zaehlers fuer Inspektion [SIA-km] |
| KM_STAND_SIA_EGS1 | real | Stand des 1. SIA-KM-Zaehlers fuer die EGS [SIA-km] |
| KM_STAND_SIA_EGS2 | real | Stand des 2. SIA-KM-Zaehlers fuer die EGS [SIA-km] |
| KM_STAND_SIA_EGS3 | real | Stand des 3. SIA-KM-Zaehlers fuer die EGS [SIA-km] |
| DAUER_DREHZAHLUEBERSCHREITUNG | real | Dauer der Drehzahlueberschreitung [s] |
| STAND_SIA_OELSERVICE1 | real | Stand des SIA-Zaehlers fuer Oelservice1 [SIA-km] |
| STAND_SIA_OELSERVICE2 | real | Stand des SIA-Zaehlers fuer Inspektion [SIA-km] |
| STAND_SIA_OELSERVICE3 | real | Stand des SIA-Zaehlers fuer Inspektion [SIA-km] |
| STAND_SIA_ZEITINSPEKTION1 | real | Stand des SIA-Zaehlers fuer Zeitinspektion [Tage] |
| STAND_SIA_ZEITINSPEKTION2 | real | Stand des SIA-Zaehlers fuer Inspektion [Tage] |
| STAND_SIA_ZEITINSPEKTION3 | real | Stand des SIA-Zaehlers fuer Inspektion [Tage] |
| STAND_SIA_ZEITINSPEKTION1_EGS | real | Stand des SIA-Zaehlers fuer Zeitinspektion Getriebe [Tage] |
| STAND_SIA_ZEITINSPEKTION2_EGS | real | Stand des SIA-Zaehlers fuer Inspektion Getriebe [Tage] |
| STAND_SIA_ZEITINSPEKTION3_EGS | real | Stand des SIA-Zaehlers fuer Inspektion Getriebe [Tage] |
| ANZAHL_OELRESET1_DURCHGEFUEHRT | int | Flag, wie oft 1. Oelservice schon zurueckgesetzt wurde |
| ANZAHL_OELRESET2_DURCHGEFUEHRT | int | Flag, wie oft 2. Oelservice schon zurueckgesetzt wurde |
| ANZAHL_OELRESET3_DURCHGEFUEHRT | int | Flag, wie oft 3. Oelservice schon zurueckgesetzt wurde |
| MOTORBETRIEBSZEIT | real | Motorbetriebszeit [h] |
| ANZAHL_MOTORSTARTS | real | Anzahl Motorstarts [Stueck] |
| _ANTWORT | binary | Antworttelegramm |

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Codier-Daten lesen und interpretieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| COD_BC_SPERRCODE | string | Sperrcode Motorstart |
| COD_DATUM_MM_TT | int | 0 = TT.MM, 1 =MM.TT |
| COD_ANKUNFTZEIT_12H | int | 0=24h, 1=12h |
| COD_SCHALTZEIT_12H | int | 0=24h, 1=12h |
| COD_BC_WEG_MILES | int | 0=km, 1=miles |
| COD_BC_VERBRAUCHS_EINHEIT | string | l/100km, mpg (US), mpg (UK), km/l |
| COD_BC_GESCHW_EINHEIT_MPH | int | 0=km/h, 1=mph |
| COD_DWA_DAUERTON | int | 0=Intervallton, 1=Dauerton |
| COD_DURCHSCHNITTSVERBRAUCHS_EINHEIT | string | l/100km, mpg (US), mpg (UK), km/l |
| COD_REICHWEITE_MILES | int | 0=km, 1=miles |
| COD_V_DURCHSCHNITT_MILES | int | 0=km/h, 1=mph |
| COD_RESTDISTANZ_MILES | int | 0=km, 1=miles |
| COD_TEMPERATUR_FAHRENHEIT | int | 0=Grad C, 1=Grad F |
| COD_LIMIT_MILES | int | 0=km/h, 1=mph |
| COD_UHRZEIT_12H | int | 0=24h, 1=12h |
| COD_STANDHEIZUNG_VERBAUT | int | 0=nein, 1=ja |
| COD_STANDLUEFTUNG_VERBAUT | int | 0=nein, 1=ja |
| COD_LAENDERVARIANTE_EINHEITEN | string | ECE,US,JAPAN,CDN/AUS/GOLF,UK |
| COD_LANDESSPRACHE | string | ECE,US,JAPAN,KANADA,F/B/L,E,I,AUS/GOLF,UK |
| COD_TANKABGLEICH_WERT | real | Korrekturfaktor Tankabgleich |
| COD_GELERNTES_GETRIEBE | string | 4-Gang,4-Gang-EGS,5-Gang-EGS,4-Gang-AGS,5-Gang-AGS |
| COD_LINKSLENKER | int | 0=nein, 1=ja |
| COD_BM_VERBAUT | int | 0=nein/MID, 1=ja |
| COD_CC_AUSFUEHRUNG | string | ECE,US,GOLF,JAPAN |
| COD_STEIGUNG_EINSPRITZKENNLINIE | real | wert in ul/ms |
| COD_K_ZAHL | int | Wegimpulszahl k |
| COD_K_ZAHL_INVERTIERT | int | invertierte K-Zahl, hier nochmal invertiert!! |
| COD_KM_OFFSET | int | Rueckstellwert Einfahrwegstrecke |
| COD_LIMIT | int | gesetzliches Limit (Golfstaaten) |
| COD_DREHZAHLGRENZE | int | Grenzdrehzahl M-Modelle |
| COD_SI_DREHZAHLSCHWELLE | int | Grenzdrehzahl SIA in 1/min |
| COD_SI_INSPEKTIONSGRENZE | int |  |
| COD_SI_AG_INSPEKTIONSGRENZE | real |  |
| COD_ZYLINDERZAHL | int |  |
| COD_SI_AG_ZEITGRENZE | int |  |
| COD_SIA_AUSFUEHRUNG_US | int | 0 = ECE, 1 = US |
| COD_SI_ZEITGRENZE | int |  |
| COD_SI_BEWERTUNGSFAKTOR_DREHZAHL | real |  |
| COD_SI_BEWERTUNGSFAKTOR_TEMPERATUR | real |  |
| COD_TACHOSKALEN_ENDWERT | int |  |
| COD_SCHWELLENWERT_STANDHEIZUNG_LUEFTUNG | int | Grad C |
| COD_KUEHLMITTELTEMP_UNTERGRENZE | int | Grad C |
| COD_KUEHLMITTELTEMP_OBERGRENZE | int | Grad C |
| COD_TANKRESERVE_MENGE | real | in Liter |
| COD_DIAG_ADRESSEN | binary | Diagnoseadressen |
| COD_AUSSENTEMP_KENNLINIE_ADC_WERTE | binary |  |
| COD_AUSSENTEMP_KENNLINIE_ADC_WERT1 | int | ADC-Stuetzwert 1 |
| COD_AUSSENTEMP_KENNLINIE_ADC_WERT2 | int | ADC-Stuetzwert 2 |
| COD_AUSSENTEMP_KENNLINIE_ADC_WERT3 | int | ADC-Stuetzwert 3 |
| COD_AUSSENTEMP_KENNLINIE_ADC_WERT4 | int | ADC-Stuetzwert 4 |
| COD_AUSSENTEMP_KENNLINIE_ADC_WERT5 | int | ADC-Stuetzwert 5 |
| COD_AUSSENTEMP_KENNLINIE_ADC_WERT6 | int | ADC-Stuetzwert 6 |
| COD_AUSSENTEMP_KENNLINIE_ADC_WERT7 | int | ADC-Stuetzwert 7 |
| COD_AUSSENTEMP_KENNLINIE_ADC_WERT8 | int | ADC-Stuetzwert 8 |
| COD_AUSSENTEMP_KENNLINIE_TEMP_WERTE | binary |  |
| COD_AUSSENTEMP_KENNLINIE_TEMP_WERT1 | int | Temp-Stuetzwert 1 |
| COD_AUSSENTEMP_KENNLINIE_TEMP_WERT2 | int | Temp-Stuetzwert 2 |
| COD_AUSSENTEMP_KENNLINIE_TEMP_WERT3 | int | Temp-Stuetzwert 3 |
| COD_AUSSENTEMP_KENNLINIE_TEMP_WERT4 | int | Temp-Stuetzwert 4 |
| COD_AUSSENTEMP_KENNLINIE_TEMP_WERT5 | int | Temp-Stuetzwert 5 |
| COD_AUSSENTEMP_KENNLINIE_TEMP_WERT6 | int | Temp-Stuetzwert 6 |
| COD_AUSSENTEMP_KENNLINIE_TEMP_WERT7 | int | Temp-Stuetzwert 7 |
| COD_AUSSENTEMP_KENNLINIE_TEMP_WERT8 | int | Temp-Stuetzwert 8 |
| COD_KUEHLMITTELTEMP_KENNLINIE_ADC_WERTE | binary |  |
| COD_KUEHLMITTELTEMP_KENNLINIE_ADC_WERT1 | int | ADC-Stuetzwert 1 |
| COD_KUEHLMITTELTEMP_KENNLINIE_ADC_WERT2 | int | ADC-Stuetzwert 2 |
| COD_KUEHLMITTELTEMP_KENNLINIE_ADC_WERT3 | int | ADC-Stuetzwert 3 |
| COD_KUEHLMITTELTEMP_KENNLINIE_ADC_WERT4 | int | ADC-Stuetzwert 4 |
| COD_KUEHLMITTELTEMP_KENNLINIE_ADC_WERT5 | int | ADC-Stuetzwert 5 |
| COD_KUEHLMITTELTEMP_KENNLINIE_ADC_WERT6 | int | ADC-Stuetzwert 6 |
| COD_KUEHLMITTELTEMP_KENNLINIE_ADC_WERT7 | int | ADC-Stuetzwert 7 |
| COD_KUEHLMITTELTEMP_KENNLINIE_ADC_WERT8 | int | ADC-Stuetzwert 8 |
| COD_KUEHLMITTELTEMP_KENNLINIE_TEMP_WERTE | binary |  |
| COD_KUEHLMITTELTEMP_KENNLINIE_TEMP_WERT1 | int | Temp-Stuetzwert 1 |
| COD_KUEHLMITTELTEMP_KENNLINIE_TEMP_WERT2 | int | Temp-Stuetzwert 2 |
| COD_KUEHLMITTELTEMP_KENNLINIE_TEMP_WERT3 | int | Temp-Stuetzwert 3 |
| COD_KUEHLMITTELTEMP_KENNLINIE_TEMP_WERT4 | int | Temp-Stuetzwert 4 |
| COD_KUEHLMITTELTEMP_KENNLINIE_TEMP_WERT5 | int | Temp-Stuetzwert 5 |
| COD_KUEHLMITTELTEMP_KENNLINIE_TEMP_WERT6 | int | Temp-Stuetzwert 6 |
| COD_KUEHLMITTELTEMP_KENNLINIE_TEMP_WERT7 | int | Temp-Stuetzwert 7 |
| COD_KUEHLMITTELTEMP_KENNLINIE_TEMP_WERT8 | int | Temp-Stuetzwert 8 |
| COD_KUEHLMITTELTEMP_ANZEIGEWINKEL | binary |  |
| COD_KUEHLMITTELTEMP_ANZEIGEWINKEL_WERT1 | int | Anzeigewinkel-Stuetzwert 1 |
| COD_KUEHLMITTELTEMP_ANZEIGEWINKEL_WERT2 | int | Anzeigewinkel-Stuetzwert 2 |
| COD_KUEHLMITTELTEMP_ANZEIGEWINKEL_WERT3 | int | Anzeigewinkel-Stuetzwert 3 |
| COD_KUEHLMITTELTEMP_ANZEIGEWINKEL_WERT4 | int | Anzeigewinkel-Stuetzwert 4 |
| COD_KUEHLMITTELTEMP_ANZEIGEWINKEL_WERT5 | int | Anzeigewinkel-Stuetzwert 5 |
| COD_KUEHLMITTELTEMP_ANZEIGEWINKEL_WERT6 | int | Anzeigewinkel-Stuetzwert 6 |
| COD_KUEHLMITTELTEMP_ANZEIGEWINKEL_WERT7 | int | Anzeigewinkel-Stuetzwert 7 |
| COD_KUEHLMITTELTEMP_ANZEIGEWINKEL_WERT8 | int | Anzeigewinkel-Stuetzwert 8 |
| COD_TANKKENNLINIE_ADC_WERTE | binary |  |
| COD_TANKKENNLINIE_ADC_WERT1 | int | ADC-Wert 1 |
| COD_TANKKENNLINIE_ADC_WERT2 | int | ADC-Wert 2 |
| COD_TANKKENNLINIE_ADC_WERT3 | int | ADC-Wert 3 |
| COD_TANKKENNLINIE_ADC_WERT4 | int | ADC-Wert 4 |
| COD_TANKKENNLINIE_ADC_WERT5 | int | ADC-Wert 5 |
| COD_TANKKENNLINIE_ADC_WERT6 | int | ADC-Wert 6 |
| COD_TANKKENNLINIE_ADC_WERT7 | int | ADC-Wert 7 |
| COD_TANKKENNLINIE_ADC_WERT8 | int | ADC-Wert 8 |
| COD_TANKKENNLINIE_LITER_WERTE | binary |  |
| COD_TANKKENNLINIE_LITER_WERT1 | int | Liter-Stuetzwert 1 |
| COD_TANKKENNLINIE_LITER_WERT2 | int | Liter-Stuetzwert 2 |
| COD_TANKKENNLINIE_LITER_WERT3 | int | Liter-Stuetzwert 3 |
| COD_TANKKENNLINIE_LITER_WERT4 | int | Liter-Stuetzwert 4 |
| COD_TANKKENNLINIE_LITER_WERT5 | int | Liter-Stuetzwert 5 |
| COD_TANKKENNLINIE_LITER_WERT6 | int | Liter-Stuetzwert 6 |
| COD_TANKKENNLINIE_LITER_WERT7 | int | Liter-Stuetzwert 7 |
| COD_TANKKENNLINIE_LITER_WERT8 | int | Liter-Stuetzwert 8 |
| COD_TANKINHALT_ANZEIGEWINKEL | binary |  |
| COD_TANKINHALT_ANZEIGEWINKEL_WERT1 | int | Anzeigewinkel zum Stuetzwert 1 |
| COD_TANKINHALT_ANZEIGEWINKEL_WERT2 | int | Anzeigewinkel zum Stuetzwert 2 |
| COD_TANKINHALT_ANZEIGEWINKEL_WERT3 | int | Anzeigewinkel zum Stuetzwert 3 |
| COD_TANKINHALT_ANZEIGEWINKEL_WERT4 | int | Anzeigewinkel zum Stuetzwert 4 |
| COD_TANKINHALT_ANZEIGEWINKEL_WERT5 | int | Anzeigewinkel zum Stuetzwert 5 |
| COD_TANKINHALT_ANZEIGEWINKEL_WERT6 | int | Anzeigewinkel zum Stuetzwert 6 |
| COD_TANKINHALT_ANZEIGEWINKEL_WERT7 | int | Anzeigewinkel zum Stuetzwert 7 |
| COD_TANKINHALT_ANZEIGEWINKEL_WERT8 | int | Anzeigewinkel zum Stuetzwert 8 |
| COD_CODE_NR_FAHRZEUGDATEN | long |  |
| COD_WEGSTRECKENZAEHLER_KM | int | 1=km, 0=miles |
| COD_GANGANZEIGE_AUSGEBLENDET | int | 1=augeblendet |
| COD_PROGRAMMANZEIGE_AUSGEBLENDET | int | 1=ausgeblendet |
| COD_GETRIEBE | string | EGS/AGS, 5-Gang, 6-Gang |
| COD_ZUENDIMPULSE_PRO_KW_UMDREHUNG | int |  |
| COD_ECE_MOTOR | int | 1=ECE, 0=US |
| COD_OTTO_MOTOR | int | 0=Diesel, 1=Otto |
| COD_MOTOR_VARIANTE | string | eta, normal, M-Modell |
| COD_ORIGINAL_EKM_KOMBI | int | 1=ja, 0=Austauschpunkt gesetzt |
| COD_RESERVEMENGE_REICHWEITE | real | Sicherheitsreservemenge fuer Reichweiteberechnung |
| COD_KNICKPUNKT_RESERVEMENGE_REICHWEITE | real | Sicherheitsreservemenge fuer Reichweiteberechnung |
| COD_KOMBI_MIT_DREHZAHLMESSER | int | 1=ja, 0 = nein |
| COD_KOMBI_MIT_TANKANZEIGE | int | 1=ja, 0 = nein |
| COD_KOMBI_MIT_KUEHLMITTELTEMP_ANZEIGE | int | 1=ja, 0 = nein |
| COD_KOMBI_MIT_MOTOROELTEMP_ANZEIGE | int | 1=ja, 0 = nein |
| COD_KOMBI_MIT_VERBRAUCHSANZEIGE | int | 1=ja, 0 = nein |
| COD_ENERGIE_CONTROL_30L_PRO_100_KM | int | 1=ja, 0 = 100l/100km |
| COD_ENERGIE_CONTROL_ANZEIGE_EINHEIT | string | l/100km, km/l, mpg(US), mgp(UK) |
| COD_WINKEL_TACHO_ENDAUSSCHLAG | real | 0 bis 360 Grad |
| COD_TACHO_SKALENOFFSET | real |  |
| COD_WINKEL_DZM_ENDAUSSCHLAG | real | 0 bis 360 Grad |
| COD_DZM_SKALENENDWERT | int |  |
| COD_WINKEL_KVA_ENDAUSSCHLAG | real | 0 bis 360 Grad |
| COD_KVA_SKALENOFFSET | real |  |
| COD_WINKEL_K_TEMP_ENDAUSSCHLAG | real | 0 bis 360 Grad |
| COD_K_TEMP_SKALENOFFSET | real |  |
| COD_WINKEL_TANK_ENDAUSSCHLAG | real | 0 bis 360 Grad |
| COD_TANK_SKALENOFFSET | real |  |
| COD_FG_NUMMER | string | codierte Fahrgestellnummer (7-stellig) |
| COD_FG_NUMMER_INVERTIERT | string | invertierte/invertierte Fahrgestellnummer (7-stellig) wird wie die nicht invertierte FG-NR ausgegeben! |
| COD_KORREKTURFAKTOR_UHR | int | eincodiert vom Hersteller |
| COD_BMW_TEILENUMMER | int | codierte BMW-Teilenummer (1-stellig) |
| COD_PRODUKTIONSDATUM_KW | string | codiertes Produktionsdatum |
| COD_PRODUKTIONSDATUM_JAHR | string | codiertes Produktionsdatum |
| COD_HW_STAND | int | codierter Hardwarestand |
| COD_PP_NR | int | codierte Pruefplannummer |
| COD_GEBRAUCHTBIT_EKM1 | int | Gebrauchtbit 1 EKM |
| COD_GEBRAUCHTBIT_EKM2 | int | Gebrauchtbit 2 EKM |
| COD_GEBRAUCHTBIT_KOMBI1 | int | Gebrauchtbit 1 Kombi |
| COD_GEBRAUCHTBIT_KOMBI2 | int | Gebrauchtbit 2 Kombi |
| _ANTWORT | binary | Antworttelegramm |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Speicher auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | long | Speicheradresse 24Bit |
| ANZAHL | int | Anzahl der zu lesenden Bytes (1..249) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| SPEICH_DATA | binary | Hexdump |

<a id="job-speicher-lesen-io-proz"></a>
### SPEICHER_LESEN_IO_PROZ

Speicher auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int | Speicheradresse im I/O-Prozessor 16Bit |
| ANZAHL | int | Anzahl der zu lesenden Bytes (1..1024) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| SPEICH_DATA | binary | Hexdump |

<a id="job-status-ausgaenge-lesen"></a>
### STATUS_AUSGAENGE_LESEN

Stati der Ausgaenge lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_AKT_STARTBLOCK_AKTIV | int | aktueller Wert Startblockierung |
| STAT_AKT_AKUSTIK1_AUS | int | aktueller Wert Akustik1 |
| STAT_AKT_AKUSTIK2_AUS | int | aktueller Wert Akustik2 |
| STAT_AKT_AKUSTIK3_AUS | int | aktueller Wert Akustik3 |
| STAT_AKT_STANDHZG_AUS | int | aktueller Wert Standheizung |
| STAT_AKT_STANDLFTG_AUS | int | aktueller Wert Standlueftung |
| STAT_AKT_DWA_ALARM_AUS | int | aktueller Wert Standlueftung |
| STAT_NORM_STARTBLOCK_AKTIV | int | normaler Wert Startblockierung |
| STAT_NORM_AKUSTIK1_AUS | int | normaler Wert Akustik1 |
| STAT_NORM_AKUSTIK2_AUS | int | normaler Wert Akustik2 |
| STAT_NORM_AKUSTIK3_AUS | int | normaler Wert Akustik3 |
| STAT_NORM_STANDHZG_AUS | int | normaler Wert Standheizung |
| STAT_NORM_STANDLFTG_AUS | int | normaler Wert Standlueftung |
| STAT_NORM_DWA_ALARM_AUS | int | normaler Wert Standlueftung |

<a id="job-status-analog-gefiltert-lesen"></a>
### STATUS_ANALOG_GEFILTERT_LESEN

gefilterte Analogwerte lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_KURZSCHLUSS_WERT | int | Analogwert - Kurzschlussueberwachung |
| STAT_KURZSCHLUSS_EINH | string | Einheit Kurzschlussueberwachung ?? |
| STAT_SPANNUNGSREFERENZ_2V_WERT | int | Analogwert Spannungsreferenz (2Volt) |
| STAT_SPANNUNGSREFERENZ_2V_EINH | string | Einheit Spannungsreferenz ?? |
| STAT_KUEHLMITTELTEMP_WERT | int | Analogwert Kuehlmitteltemperatur |
| STAT_KUEHLMITTELTEMP_EINH | string | Einheit Kuehlmitteltemperatur ?? |
| STAT_AUSSENTEMP_WERT | int | Analogwert Aussentemperatur |
| STAT_AUSSENTEMP_EINH | string | Einheit Aussentemperatur ?? |
| STAT_KRAFTSTOFF_WERT | int | Analogwert Kraftstoffvorratsgeber |
| STAT_KRAFTSTOFF_EINH | string | Einheit Kraftstoffvorratsgeber ?? |
| STAT_OELSTAND_WERT | int | Analogwert Oelstand dynamisch |
| STAT_OELSTAND_EINH | string | Einheit Oelstand dynamisch ?? |
| STAT_LEHNENVERR_LINKS_WERT | int | Analogwert Lehnenverriegelung links |
| STAT_LEHNENVERR_LINKS_EINH | string | Einheit Lehnenverriegelung links ?? |
| STAT_LEHNENVERR_RECHTS_WERT | int | Analogwert Lehnenverriegelung rechts |
| STAT_LEHNENVERR_RECHTS_EINH | string | Einheit Lehnenverriegelung rechts ?? |

<a id="job-status-analog-ungefiltert-lesen"></a>
### STATUS_ANALOG_UNGEFILTERT_LESEN

ungefilterte Analogwerte lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_KURZSCHLUSS_WERT | int | Analogwert - Kurzschlussueberwachung |
| STAT_KURZSCHLUSS_EINH | string | Einheit Kurzschlussueberwachung ?? |
| STAT_SPANNUNGSREFERENZ_2V_WERT | int | Analogwert Spannungsreferenz (2Volt) |
| STAT_SPANNUNGSREFERENZ_2V_EINH | string | Einheit Spannungsreferenz ?? |
| STAT_KUEHLMITTELTEMP_WERT | int | Analogwert Kuehlmitteltemperatur |
| STAT_KUEHLMITTELTEMP_EINH | string | Einheit Kuehlmitteltemperatur ?? |
| STAT_AUSSENTEMP_WERT | int | Analogwert Aussentemperatur |
| STAT_AUSSENTEMP_EINH | string | Einheit Aussentemperatur ?? |
| STAT_KRAFTSTOFF_WERT | int | Analogwert Kraftstoffvorratsgeber |
| STAT_KRAFTSTOFF_EINH | string | Einheit Kraftstoffvorratsgeber ?? |
| STAT_OELSTAND_WERT | int | Analogwert Oelstand dynamisch |
| STAT_OELSTAND_EINH | string | Einheit Oelstand dynamisch ?? |
| STAT_LEHNENVERR_LINKS_WERT | int | Analogwert Lehnenverriegelung links |
| STAT_LEHNENVERR_LINKS_EINH | string | Einheit Lehnenverriegelung links ?? |
| STAT_LEHNENVERR_RECHTS_WERT | int | Analogwert Lehnenverriegelung rechts |
| STAT_LEHNENVERR_RECHTS_EINH | string | Einheit Lehnenverriegelung rechts ?? |

<a id="job-tacho-a"></a>
### TACHO_A

liefert geschwindigkeitsproportionales Signal

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GESCHWINDIGKEIT | int | Vorgabegeschwindigkeit in km/h, (4-250 km/h) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (61 × 2)
- [SIARESET](#table-siareset) (3 × 2)
- [STATDIAKL](#table-statdiakl) (5 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 61 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | unbekannter Fehlerort |
| 0x01 | Klemme 15, Klemme R und (Td+Ti) |
| 0x02 | Klemme 50, ohne Klemme 15 |
| 0x03 | Klemme 50, mehr als 60 sec aktiv |
| 0x04 | Alarmausgang, Kurzschluss gegen U-Batt |
| 0x05 | Alarmausgang, Leitungsunterbrechung oder Kurzschluss gegen Masse |
| 0x06 | Akustik 1, Kurzschluss gegen U-Batt |
| 0x07 | Akustik 1, Leitungsunterbrechung oder Kurzschluss gegen Masse |
| 0x08 | Akustik 2, Kurzschluss gegen U-Batt |
| 0x09 | Akustik 2, Leitungsunterbrechung oder Kurzschluss gegen Masse |
| 0x0a | Akustik 3, Kurzschluss gegen U-Batt |
| 0x0b | Akustik 3, Leitungsunterbrechung oder Kurzschluss gegen Masse |
| 0x0c | Ti 1, Leitungsunterbrechung oder Kurzschluss gegen U-Batt |
| 0x0d | Ti 1, Kurzschluss gegen Masse |
| 0x0e | Ti 1, Signal gestoert |
| 0x0f | Ti 2, Leitungsunterbrechung oder Kurzschluss gegen U-Batt |
| 0x10 | Ti 2, Kurzschluss gegen Masse |
| 0x11 | Ti 2, Signal gestoert |
| 0x12 | Klemme 15 ohne Klemme R |
| 0x13 | Td, Leitungsunterbrechung oder Kurzschluss gegen U-Batt |
| 0x14 | Td, Kurzschluss gegen Masse |
| 0x15 | Td, Signal gestoert |
| 0x16 | Wegsignal, Leitungsunterbrechung |
| 0x17 | Wegsignal, Signal gestoert |
| 0x18 | Standheizung Kurzschluss gegen U-Batt |
| 0x19 | Standheizung Kurzschluss gegen Masse |
| 0x1a | Standlueftung Kurzschluss gegen U-Batt |
| 0x1b | Standlueftung Kurzschluss gegen Masse |
| 0x1c | Startblockierung Kurzschluss gegen U-Batt |
| 0x1d | Startblockierung Kurzschluss gegen Masse |
| 0x1e | Tacho A, Kurzschluss gegen U-Batt |
| 0x1f | Tacho A, Kurzschluss gegen Masse |
| 0x20 | Masse Tacho und Kraftstoffvorratsgeber |
| 0x21 | Kraftstoffvorratsgeber Kurzschluss gegen U-Batt |
| 0x22 | Kraftstoffvorratsgeber Kurzschluss gegen Masse |
| 0x23 | Kuehlermitteltemperatur, Leitungsunterbrechung oder Kurzschluss gegen U-Batt |
| 0x24 | Kuehlermitteltemperatur, Kurzschluss gegen Masse |
| 0x25 | Aussentemperatur Kurzschluss gegen U-Batt |
| 0x26 | Aussentemperatur Kurzschluss gegen Masse |
| 0x27 | Masse Aussentemperatur und Kuehlermitteltemperatur |
| 0x28 | Datenuebertragung zum Kombi gestoert |
| 0x29 | Datenuebertragung zum Kombi Kurzschluss gegen U-Batt |
| 0x2a | Datenuebertragung zum Kombi Kurzschluss gegen Masse |
| 0x2b | Datenuebertragung zum MID/BM gestoert |
| 0x2c | Datenuebertragung zum ZKE/GM2 gestoert |
| 0x2d | Datenuebertragung zum LKM gestoert |
| 0x2e | Datenuebertragung zur BM-Tastatur gestoert |
| 0x2f | Datenuebertragung zum Audiomodul gestoert |
| 0x30 | Datenuebertragung zur AHK gestoert |
| 0x31 | Datenuebertragung zum Navigationssystem gestoert |
| 0x32 | Datenuebertragung zur Verdecksteuerung gestoert |
| 0x33 | Datenuebertragung zum TV-Tuner gestoert |
| 0x34 | Datenuebertragung zur RDC gestoert |
| 0x35 | I-Bus, Kurzschluss gegen U-Batt |
| 0x36 | I-Bus, Kurzschluss gegen Masse |
| 0x37 | I-Bus, Datenuebertragung gestoert |
| 0x38 | EKM-Speicher fehlerhaft |
| 0x39 | Wegfahrsicherung, Code |
| 0x3a | EKM-Code fehlerhaft |
| 0x3b | Interner Fehler |
| 0xFF | unbekannter Fehlerort |

<a id="table-siareset"></a>
### SIARESET

Dimensions: 3 rows × 2 columns

| SELECTOR | RESET |
| --- | --- |
| OEL_RESET | 0x01 |
| WEG_RESET | 0x04 |
| ZEIT_RESET | 0x08 |

<a id="table-statdiakl"></a>
### STATDIAKL

Dimensions: 5 rows × 2 columns

| KS | KLEMME |
| --- | --- |
| 0x01 | KL30 |
| 0x02 | KLR |
| 0x03 | KL15 |
| 0x04 | KL50 |
| 0xFF | ERROR_UNBEKANNTER_KLEMMENSTATUS |
