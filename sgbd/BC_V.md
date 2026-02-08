# BC_V.prg

- Jobs: [12](#jobs)
- Tables: [4](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Bordcomputer 5 E36 |
| ORIGIN | BMW TP-421 Spoljarec |
| REVISION | 1.05 |
| AUTHOR | BMW TP-421 Spoljarec |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer BCV
- [IDENT](#job-ident) - Auslesen der Identifikationsdaten
- [COD_LESEN](#job-cod-lesen) - Auslesen der BC-Codierung
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [DISPLAYTEST](#job-displaytest) - Ausloesen des Displaytests
- [STATUS_DIGITAL_LESEN](#job-status-digital-lesen) - alle digitalen Stati des BC 5 lesen
- [STATUS_TASTEN_LESEN](#job-status-tasten-lesen) - alle Tastatur Stati des BC 5 lesen
- [STATUS_ANALOG_LESEN](#job-status-analog-lesen) - alle analogen Stati des BC 5 lesen
- [STEUERN_IO_STATUS](#job-steuern-io-status) - Ansteuern von den I/O Stati
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode beenden

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

Init-Job fuer BCV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Auslesen der Identifikationsdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Ergebnis des Jobs |
| ID_GEN_NR | int | Generationsnummer |
| ID_HW_NR | int | Hardwarenummer |
| ID_SW_NR | int | Softwarenummer |
| ID_PP_NR | int | Pruefplannummer |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |

<a id="job-cod-lesen"></a>
### COD_LESEN

Auslesen der BC-Codierung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Ergebnis des Jobs |
| COD_DATEN | binary | 8 Byte Codierdaten nicht dekodiert |
| K_ZAHL | int | Wegeimpulse K-Zahl |
| EINSPRITZKENNZAHL | int | Steigung Einspitzkennlinie im BC |
| EINSPRITZSTEIGUNG | long | Einspritzsteigung s (Division durch Zylinderanzahl: -&gt; s') |
| SPRACHE | string | Sprachvariante |
| ZEITBASIS | string | 12h/24h-Stundenbasis |
| TEMPERATURBASIS | string | Temperatureinheit C/F |
| CCM_VERBAUT | string | BC mit/ohne CCM |
| HUPTON | string | 0: Hupe intermetierend/Dauerton |
| GESCHWINDIGKEITSBASIS | string | km/h oder MPH |
| ENTFERNUNGSBASIS | string | km oder Meilen |
| VERBRAUCHSBASIS | string | l/100km MPG km/l |
| MAX_TANKINHALT | long | maximaler Tankinhalt in Liter |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| F_ORT_NR | int | Fehlercode |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_HFK | int | Fehlerhaeufigkeit des jeweiligen Fehlers |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen |
| F_ART1_NR | int | Index der 1. Fehlerart |
| F_ART1_TEXT | string | 1. Fehlerart als Text |
| F_ART2_NR | int | Index der 2. Fehlerart |
| F_ART2_TEXT | string | 2. Fehlerart als Text |
| F_ART3_NR | int | Index der 3. Fehlerart |
| F_ART3_TEXT | string | 3. Fehlerart als Text |
| F_ART4_NR | int | Index der 4. Fehlerart |
| F_ART4_TEXT | string | 4. Fehlerart als Text |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-displaytest"></a>
### DISPLAYTEST

Ausloesen des Displaytests

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Ergebnis des Jobs |

<a id="job-status-digital-lesen"></a>
### STATUS_DIGITAL_LESEN

alle digitalen Stati des BC 5 lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| STAT_KL_R_EIN | int | 0 -&gt; KL. R aus, 1 -&gt; Kl. R ein (Radioklemme) |
| STAT_KL_15_EIN | int | 0 -&gt; KL. 15 aus, 1 -&gt; Kl. 15 ein (Signal Zuendung) |
| STAT_KL_50_EIN | int | 0 -&gt; KL. 50 aus, 1 -&gt; Kl. 50 ein (Startersignal) |
| STAT_KL_54_EIN | int | 0 -&gt; KL. 54 aus, 1 -&gt; Kl. 54 ein (Bremslichtschalter) |
| STAT_KL_54_TEST_EIN | int | 0 -&gt; KL. 54 Test aus, 1 -&gt; Kl. 54 Test ein (Bremslichttestschalter) |
| STAT_TIMER_EIN | int | 0 -&gt; Timer aus, 1 -&gt; Timer ein |
| STAT_HORN_EIN | int | 0 -&gt; Horn aus, 1 -&gt; Horn ein |
| STAT_CODE_EIN | int | 0 -&gt; Code aus, 1 -&gt; Code ein |
| STAT_GONG_T1_EIN | int | 0 -&gt; Gong T1 aus, 1 -&gt; Gong T1 ein |
| STAT_GONG_T2_EIN | int | 0 -&gt; Gong T2 aus, 1 -&gt; Gong T2 ein |
| STAT_BC_ZHL_EIN | int | 0 -&gt; Hinweisleuchte aus, 1 -&gt; ZHL ein |
| STAT_LED_CODE_EIN | int | 0 -&gt; LED Code aus, 1 -&gt; LED Code ein |
| STAT_LED_TIMER_EIN | int | 0 -&gt; LED Timer aus, 1 -&gt; LED Timer ein |
| STAT_LED_LIMIT_EIN | int | 0 -&gt; LED Limit aus, 1 -&gt; LED Limit ein |
| STAT_LCD_UHR_EIN | int | 0 -&gt; LCD Uhr aus, 1 -&gt; LCD Uhr ein (rechtes Display) |
| STAT_LCD_TEXT_EIN | int | 0 -&gt; LCD Text aus, 1 -&gt; LCD Text ein (linkes Display) |
| STAT_LSS_BETAETIGT | int | 0 -&gt; LSS nicht gedrueckt, 1 -&gt; LSS gedrueckt (Lenkstockschalter) |
| STAT_HAUBE_RADIO_KONTAKT_EIN | int | 0 -&gt; aus, 1 -&gt; ein |

<a id="job-status-tasten-lesen"></a>
### STATUS_TASTEN_LESEN

alle Tastatur Stati des BC 5 lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| STAT_TASTE_1000_EIN | int | 0 -&gt; Taste 1000 gedrueckt, 1 -&gt; Taste 1000 gedrueckt |
| STAT_TASTE_100_EIN | int | 0 -&gt; Taste 100 gedrueckt, 1 -&gt; Taste 100 gedrueckt |
| STAT_TASTE_10_EIN | int | 0 -&gt; Taste 10 gedrueckt, 1 -&gt; Taste 10 gedrueckt |
| STAT_TASTE_1_EIN | int | 0 -&gt; Taste 1 gedrueckt, 1 -&gt; Taste 1 gedrueckt |
| STAT_TASTE_VERBR_EIN | int | 0 -&gt; Taste VERBR gedrueckt, 1 -&gt; Taste VERBR gedrueckt |
| STAT_TASTE_A_TEMP_EIN | int | 0 -&gt; Taste A-TEMP gedrueckt, 1 -&gt; Taste A-TEMP gedrueckt |
| STAT_TASTE_GESCHW_EIN | int | 0 -&gt; Taste GESCHW gedrueckt, 1 -&gt; Taste GESCHW gedrueckt |
| STAT_TASTE_DISTANZ_EIN | int | 0 -&gt; Taste DISTANZ gedrueckt, 1 -&gt; Taste DISTANZ gedrueckt |
| STAT_TASTE_CHECK_EIN | int | 0 -&gt; Taste CHECK gedrueckt, 1 -&gt; Taste CHECK gedrueckt |
| STAT_TASTE_REICHW_EIN | int | 0 -&gt; Taste REICHW gedrueckt, 1 -&gt; Taste REICHW gedrueckt |
| STAT_TASTE_CODE_EIN | int | 0 -&gt; Taste CODE gedrueckt, 1 -&gt; Taste CODE gedrueckt |
| STAT_TASTE_LIMIT_EIN | int | 0 -&gt; Taste LIMIT gedrueckt, 1 -&gt; Taste LIMIT gedrueckt |
| STAT_TASTE_TIMER_EIN | int | 0 -&gt; Taste TIMER gedrueckt, 1 -&gt; Taste TIMER gedrueckt |
| STAT_TASTE_KM_MLS_EIN | int | 0 -&gt; Taste km/mls gedrueckt, 1 -&gt; Taste km/mls gedrueckt |
| STAT_TASTE_UHR_EIN | int | 0 -&gt; Taste UHR gedrueckt, 1 -&gt; Taste UHR gedrueckt |
| STAT_TASTE_DATUM_EIN | int | 0 -&gt; Taste DATUM gedrueckt, 1 -&gt; Taste DATUM gedrueckt |
| STAT_TASTE_MEMO_EIN | int | 0 -&gt; Taste MEMO gedrueckt, 1 -&gt; Taste MEMO gedrueckt |
| STAT_TASTE_SET_RES_EIN | int | 0 -&gt; Taste SET/RES gedrueckt, 1 -&gt; Taste SET/RES gedrueckt |

<a id="job-status-analog-lesen"></a>
### STATUS_ANALOG_LESEN

alle analogen Stati des BC 5 lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| STAT_DATUM_TAG | int | im BC gueltiger Tag 1..31 |
| STAT_DATUM_MONAT | int | im BC gueltiger Monat 1..12 |
| STAT_DATUM_JAHR | int | im BC gueltiges Jahr 1988..???? |
| STAT_UHRZEIT | string | aktuelle Uhrzeit im Format hh:mm:ss |
| STAT_STOPUHR | string | StopuhrZEIT IM Format hh:mm:ss |
| STAT_ZWISCHENZEIT | string | Stopuhr Zwischenzeit im Format hh:mm:ss |
| STAT_GESCHWINDIGKEIT | long | aktuelle Geschwindigkeit auf Zehntel km/h 0.0-250.0 |
| STAT_LIMIT | int | aktuell eingestelltes Limit 0-250 in km |
| STAT_REICHWEITE | int | Anzeigewert der Reichweite 0..???? in km |
| STAT_TANKINHALT | long | Tankgeberwert 0.0-99.9 in Liter |

<a id="job-steuern-io-status"></a>
### STEUERN_IO_STATUS

Ansteuern von den I/O Stati

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | siehe table IO_STATUS |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnosemode beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Ergebnis des Jobs |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (4 × 2)
- [SPRACH_TAB](#table-sprach-tab) (10 × 2)
- [FORTTEXTE](#table-forttexte) (22 × 2)
- [IO_STATUS](#table-io-status) (6 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 4 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x09 | OKAY |
| 0x0B | BUSY |
| 0x0A | ERROR_ECU_NACK |
| 0xXY | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-sprach-tab"></a>
### SPRACH_TAB

Dimensions: 10 rows × 2 columns

| SPB | SPRACHE_TEXT |
| --- | --- |
| 0x00 | Deutschland |
| 0x01 | engl. UK |
| 0x02 | engl. US |
| 0x03 | Italien |
| 0x04 | Spanien |
| 0x05 | engl. Japan |
| 0x06 | Frankreich |
| 0x07 | Kanada |
| 0x08 | Australien/Golf/ZA |
| 0xXY | unbekannte Sprache |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 22 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | BC ZHL - Check-Control-Lampe im Kombi |
| 0x02 | Gong T2 Ausgang |
| 0x03 | Gong T1 Ausgang |
| 0x04 | Code Ausgang - Wegfahrsicherung zur Motronic |
| 0x05 | Horn ausgang - Alarmhorn (Relaisbox/DWA) |
| 0x06 | Timer Ausgang |
| 0x07 | Temperatur Eingang - Aussentemperaturfuehler |
| 0x08 | BC CLC - Clock-Leitung zum Check-Modul |
| 0x09 | BC LAC - Latch-Signal zum Check-Modul |
| 0x0A | BC DATA - serielle Datenltg. zum Check.Modul |
| 0x0B | Klemme 15 ohne Klemme R |
| 0x0C | Klemme 50 ohne Klemme 15 |
| 0x0D | Haube/Radio - Ueberwachung Hauben-/Radio-Kontakt |
| 0x0E | Tacho A - Wegsignal vom Kombi |
| 0x0F | T KVA - Einspritzsignal von Motronic |
| 0x10 | kein Tanksignal vom Kombi |
| 0x11 | RxD - Diagnoseempfangsleitung Fehler |
| 0x12 | Kurzschluss TxD-Leitung nach UBatt |
| 0x13 | Lenkstockschalter |
| 0x14 | kein LCD-Dimmsignal vom Kombi |
| 0x15 | BLTS - Bremslichttestschalter |
| 0xXY | unbekannter Fehlerort |

<a id="table-io-status"></a>
### IO_STATUS

Dimensions: 6 rows × 2 columns

| SIGNAL | BYTE |
| --- | --- |
| TIMER | 0x02 |
| HORN | 0x04 |
| CODE | 0x08 |
| GONG1 | 0x10 |
| GONG2 | 0x20 |
| ZHL | 0x40 |
