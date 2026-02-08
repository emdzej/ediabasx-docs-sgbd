# ZAE2.prg

- Jobs: [16](#jobs)
- Tables: [4](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | AIRBAG 2 |
| ORIGIN | BMW TP-421 Winkler H.-J. |
| REVISION | 1.09 |
| AUTHOR | BMW TP-421 Baumgartner, BMW TP-421 Winkler |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer AIRBAG ZAE II
- [IDENT](#job-ident) - Ident-Daten fuer AIRBAG ZAE II
- [STATUS_LESEN](#job-status-lesen) - Status des AIRBAG II lesen
- [FS_QUICK_LESEN](#job-fs-quick-lesen) - Quicktest High-Konzept nach Lastenheft (mit Abwandlungen)
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [SG_LOGIN](#job-sg-login)
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [SPEICHER_LESEN](#job-speicher-lesen) - Speicher lesen ZAE
- [DIAGNOSE_ERHALTEN](#job-diagnose-erhalten) - Diagnose aufrechterhalten
- [AUSSTATTUNG_LESEN](#job-ausstattung-lesen) - Ausstattung lesen ZAE2
- [VERRIEGELUNG_LESEN](#job-verriegelung-lesen) - Auslesen des Pruefstempels
- [VERRIEGELUNG_SCHREIBEN](#job-verriegelung-schreiben) - Verriegelungsbytes setzen
- [HERSTELLERDATEN_LESEN](#job-herstellerdaten-lesen) - Herstellerdaten des SG lesen
- [TYP_LESEN](#job-typ-lesen) - Typ des Fzg. lesen

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

Init-Job fuer AIRBAG ZAE II

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer AIRBAG ZAE II

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferant |
| ID_SW_NR | int | Softwarenummer |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Status des AIRBAG II lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| STAT_GURT_F_ANGESCHNALLT | int | 1 -&gt; angeschnallt |
| STAT_GURT_BF_ANGESCHNALLT | int | 1 -&gt; angeschnallt |
| STAT_SITZ_BF_BELEGT | int | 1 -&gt; Beifahrersitz belegt |
| STAT_KINDERSITZ_BELEGT | int | 1 -&gt; Beifahrersitz belegt |
| STAT_ZK0_LECK_UBATT_IO | int | 0 -&gt; ZK0 Leckwiderstand gegen UBATT |
| STAT_ZK0_LECK_MASSE_IO | int | 0 -&gt; ZK0 Leckwiderstand gegen Masse |
| STAT_ZK0_WID_SMALL_IO | int | 0 -&gt; ZK0 Widerstand zu klein |
| STAT_ZK0_WID_BIG_IO | int | 0 -&gt; ZK0 Widerstand zu gross |
| STAT_ZK1_LECK_UBATT_IO | int | 0 -&gt; ZK1 Leckwiderstand gegen UBATT |
| STAT_ZK1_LECK_MASSE_IO | int | 0 -&gt; ZK1 Leckwiderstand gegen Masse |
| STAT_ZK1_WID_SMALL_IO | int | 0 -&gt; ZK1 Widerstand zu klein |
| STAT_ZK1_WID_BIG_IO | int | 0 -&gt; ZK1 Widerstand zu gross |
| STAT_ZK2_LECK_UBATT_IO | int | 0 -&gt; ZK2 Leckwiderstand gegen UBATT |
| STAT_ZK2_LECK_MASSE_IO | int | 0 -&gt; ZK2 Leckwiderstand gegen Masse |
| STAT_ZK2_WID_SMALL_IO | int | 0 -&gt; ZK2 Widerstand zu klein |
| STAT_ZK2_WID_BIG_IO | int | 0 -&gt; ZK2 Widerstand zu gross |
| STAT_ZK3_LECK_UBATT_IO | int | 0 -&gt; ZK3 Leckwiderstand gegen UBATT |
| STAT_ZK3_LECK_MASSE_IO | int | 0 -&gt; ZK3 Leckwiderstand gegen Masse |
| STAT_ZK3_WID_SMALL_IO | int | 0 -&gt; ZK3 Widerstand zu klein |
| STAT_ZK3_WID_BIG_IO | int | 0 -&gt; ZK3 Widerstand zu gross |
| STAT_ZK4_LECK_UBATT_IO | int | 0 -&gt; ZK4 Leckwiderstand gegen UBATT |
| STAT_ZK4_LECK_MASSE_IO | int | 0 -&gt; ZK4 Leckwiderstand gegen Masse |
| STAT_ZK4_WID_SMALL_IO | int | 0 -&gt; ZK4 Widerstand zu klein |
| STAT_ZK4_WID_BIG_IO | int | 0 -&gt; ZK4 Widerstand zu gross |
| STAT_ZK5_LECK_UBATT_IO | int | 0 -&gt; ZK5 Leckwiderstand gegen UBATT |
| STAT_ZK5_LECK_MASSE_IO | int | 0 -&gt; ZK5 Leckwiderstand gegen Masse |
| STAT_ZK5_WID_SMALL_IO | int | 0 -&gt; ZK5 Widerstand zu klein |
| STAT_ZK5_WID_BIG_IO | int | 0 -&gt; ZK5 Widerstand zu gross |
| STAT_GURTSCHL_BF_PLAUSI_IO | int | 0 -&gt; Plausibilitaet BF NIO |
| STAT_KAS_BF_MASSE_IO | int | 0 -&gt; Kabelanliegeschluss Gurtschloss Beifahrer gegen Masse |
| STAT_KAS_BF_UBATT_IO | int | 0 -&gt; Kabelanliegeschluss Gurtschloss Beifahrer gegen UBATT |
| STAT_NA_BF_IO | int | 0 -&gt; Nicht auswertbarer Fehler, Gurtschloss Beifahrer |
| STAT_GURTSCHL_F_PLAUSI_IO | int | 0 -&gt; Plausibilitaet F NIO |
| STAT_KAS_F_MASSE_IO | int | 0 -&gt; Kabelanliegeschluss Gurtschloss Fahrer gegen Masse |
| STAT_KAS_F_UBATT_IO | int | 0 -&gt; Kabelanliegeschluss Gurtschloss Fahrer gegen UBATT |
| STAT_NA_F_IO | int | 0 -&gt; Nicht auswertbarer Fehler, Gurtschloss Fahrer |
| STAT_SBE_PLAUSI | int | 0 -&gt; SBE Plausibilitaet |
| STAT_SBE_ANALOG_SCHLUSS_IO | int | 0 -&gt; SBE ANALOG Leitungsunterbrechung / Kurzschluss |
| STAT_SBE_DIGITAL_SCHLUSS_IO | int | 0 -&gt; SBE DIGITAL Leitungsunterbrechung / Kurzschluss |
| STAT_SBE_HOCH_IO | int | 0 -&gt; SBE defekt  Hochohmig |
| STAT_SBE_KOMM_IO | int | 0 -&gt; SBE defekt  Kommunikationsstoerung |
| STAT_SBE_ANALOG_LECK_IO | int | 0 -&gt; SBE Analog Leitungsleck- bzw. Anliegeschluss |
| STAT_SBE_DIGITAL_PLUS | int | 0 -&gt; SBE Digital Leitung Plus |
| STAT_SBE_DIGITAL_MASSE | int | 0 -&gt; SBE Digital Leitung Masse |
| STAT_LAMPE_SCHLUSS_UBATT_IO | int | 0 -&gt; Fehlerlampe Schluss UBATT |
| STAT_LAMPE_SCHLUSS_MASSE_IO | int | 0 -&gt; Fehlerlampe Schluss/ Unterbr. Masse |
| STAT_UNTERSPANNUNG_IO | int | 0 -&gt; Unterspannungsfehler |
| STAT_KSE_ANALOG_UBATT_IO | int | 0 -&gt; KSE Analog Unterbr./UBATT- Schluss |
| STAT_KSE_ANALOG_WID_IO | int | 0 -&gt; KSE Analog Widerstand IO |
| STAT_KSE_ANALOG_MASSE_IO | int | 0 -&gt; KSE Analog  Anliegeschluss Masse |
| STAT_KSE_PLAUSI_IO | int | 0 -&gt; KSE Plausibilitaet Analog + Digital NIO |
| STAT_KSE_DIGITAL_UBATT | int | 0 -&gt; KSE Leitung Plus |
| STAT_KSE_DIGITAL_MASSE | int | 0 -&gt; KSE Leitung Masse |
| STAT_KSE_DIGITAL_KOMM_IO | int | 0 -&gt; KSE Kommunikationsstoerung |
| STAT_KSE_DIGITAL_FEHLER | int | 0 -&gt; KSE Digital Fehler |
| STAT_MRSA_R_FEHLER_IO | int | 0 -&gt; MRSA_R sendet Fehler |
| STAT_MRSA_L_FEHLER_IO | int | 0 -&gt; MRSA_L sendet Fehler |
| STAT_MRSA_R_KOMM | int | 0 -&gt; MRSA_R Kommunikationsfehler |
| STAT_MRSA_L_KOMM | int | 0 -&gt; MRSA_L Kommunikationsfehler |

<a id="job-fs-quick-lesen"></a>
### FS_QUICK_LESEN

Quicktest High-Konzept nach Lastenheft (mit Abwandlungen)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| F_ANZ | int | Anzahl Fehler |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| F_ORT_NR | int | momentan identisch Fehlerbytemaske |
| F_HFK | int | Haeufigkeitszaehler |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_ART1_NR | int | Index der 1. Fehlerart |
| F_ART1_TEXT | string | 1. Fehlerart als Text |
| F_ART2_NR | int | Index der 2. Fehlerart |
| F_ART2_TEXT | string | 2. Fehlerart als Text |
| F_ART3_NR | int | Index der 3. Fehlerart |
| F_ART3_TEXT | string | 3. Fehlerart als Text |
| F_ART4_NR | int | Index der 4. Fehlerart |
| F_ART4_TEXT | string | 4. Fehlerart als Text |
| F_ART5_NR | int | Index der 5. Fehlerart |
| F_ART5_TEXT | string | 5. Fehlerart als Text |
| F_ART6_NR | int | Index der 6. Fehlerart |
| F_ART6_TEXT | string | 6. Fehlerart als Text |
| F_ART7_NR | int | Index der 7. Fehlerart |
| F_ART7_TEXT | string | 7. Fehlerart als Text |
| F_ART8_NR | int | Index der 8. Fehlerart |
| F_ART8_TEXT | string | 8. Fehlerart als Text |
| F_ART_ANZ | int | immer 8 |
| F_SPORADIK | int | Sporadikzaehler (identisch Haeufigkeitszaehler) |
| BFU | long | Beginnfehleruhrzeit in Sec. |
| EFU | long | Endefehleruhrzeit in Sec. |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-sg-login"></a>
### SG_LOGIN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY, wenn fehlerfrei" |
| TELEGRAMM | binary | antworttelegramm |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Speicher lesen ZAE

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| H_ADR | string | Startadresse High- Byte |
| L_ADR | string | Startadresse Low- Byte |
| ANZ_BYTE | string | Anzahl der zu lesenden Bytes |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| DATEN | binary | Codierdaten |

<a id="job-diagnose-erhalten"></a>
### DIAGNOSE_ERHALTEN

Diagnose aufrechterhalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-ausstattung-lesen"></a>
### AUSSTATTUNG_LESEN

Ausstattung lesen ZAE2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| AB_F_VERBAUT | int | 1 --&gt; verbaut |
| GS_F_VERBAUT | int | 1 --&gt; verbaut |
| AB_BF_VERBAUT | int | 1 --&gt; verbaut |
| GS_BF_VERBAUT | int | 1 --&gt; verbaut |
| SCHLOSS_F_VERBAUT | int | 1 --&gt; verbaut |
| SCHLOSS_BF_VERBAUT | int | 1 --&gt; verbaut |
| SENSOR_VERBAUT | int | 1 --&gt; verbaut |
| SITZ_ERKENNUNG_VERBAUT | int | 1 --&gt; verbaut |
| KINDERSITZ_ERKENNUNG_VERBAUT | int | 1 --&gt; verbaut |
| US_VERSION | int | 1 --&gt; US Version |
| SIDEBAG_L_AKTIV | int | 1 --&gt; ZK 4 aktiv |
| SIDEBAG_R_AKTIV | int | 1 --&gt; ZK 5 aktiv |
| TRIGGERSCHALTER_VERBAUT | int | 1 --&gt; Triggerschalter verbaut |
| ABLAUF_STG | int | 1 --&gt; Ablaufsteuerung |
| GURTSCHLOSS_DIGITAL | int | 1 --&gt; Gurtschloss digital |
| SITZBELEGUNG_DIGITAL | int | 1 --&gt; Sitzbelegung digital |
| KINDERSITZBELEGUNG_DIGITAL | int | 1 --&gt; Kindersitzbelegung digital |

<a id="job-verriegelung-lesen"></a>
### VERRIEGELUNG_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |

<a id="job-verriegelung-schreiben"></a>
### VERRIEGELUNG_SCHREIBEN

Verriegelungsbytes setzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| ERROR_CODE | string | OKAY, FEHLER |

<a id="job-herstellerdaten-lesen"></a>
### HERSTELLERDATEN_LESEN

Herstellerdaten des SG lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| TYP | string | z.B: E31 / 03h , E34 / 01h ... |
| CODIERDATUM | string | z.B: 21.4.93 ... |
| WERKSKENNUNG | string | z.B: |
| HAENDLERKENNUNG | string | z.B: |

<a id="job-typ-lesen"></a>
### TYP_LESEN

Typ des Fzg. lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| TYP | string | z.B: E31 / 03h , E34 / 01h ... |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (8 × 2)
- [FORTTEXTE](#table-forttexte) (27 × 2)
- [FARTTEXTE](#table-farttexte) (10 × 2)
- [LIEFERANTEN](#table-lieferanten) (31 × 2)

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

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 27 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | interner Steuergeraetefehler |
| 0x02 | Fehlerlampe |
| 0x03 | Versorgungsspannung |
| 0x04 | Zuendkreis 0 -&gt; Fahrer Airbag |
| 0x05 | Zuendkreis 1 -&gt; Fahrer Gurtstrammer |
| 0x06 | Zuendkreis 2 -&gt; Beifahrer Gurtstrammer |
| 0x07 | Zuendkreis 3 -&gt; Beifahrer Airbag |
| 0x08 | Zuendkreis 4 -&gt; Seitenairbag links |
| 0x09 | Zuendkreis 5 -&gt; Seitenairbag rechts |
| 0x0A | Zuendkreis 6 -&gt; Airbag Kopf links |
| 0x0B | Zuendkreis 7 -&gt; Airbag Kopf rechts |
| 0x10 | Analoge Gurtschlossabfrage Fahrer |
| 0x11 | Analoge Gurtschlossabfrage Beifahrer |
| 0x12 | MRSA_LINKS Leitungsfehler |
| 0x13 | MRSA_LINKS falsche Algo- Parameter |
| 0x14 | MRSA_LINKS MRSA sendet Fehler |
| 0x15 | MRSA_RECHTS Leitungsfehler |
| 0x16 | MRSA_RECHTS falsche Algo- Parameter |
| 0x17 | MRSA_RECHTS MRSA sendet Fehler |
| 0x18 | Digitale Sitzbelegungserkennung |
| 0x1A | Plausibilitaet der Sitzbelegungserkennung |
| 0x1B | Digitale KSE |
| 0x1D | Plausibilitaet der KSE |
| 0x1F | Digitale KSE |
| 0x20 | MRSA_LINKS Kommunikationsfehler |
| 0x21 | MRSA_RECHTS Kommunikationsfehler |
| 0xFF | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 10 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | -- |
| 0x02 | -- |
| 0x03 | Leitungsunterbrechung oder Kurzschluss gegen Masse |
| 0x04 | Leckwiderstand oder Kurzschluss gegen Masse |
| 0x05 | Leckwiderstand oder Kurzschluss gegen U-Batt |
| 0x06 | Grenzwertunterschreitung |
| 0x07 | Grenzwertueberschreitung |
| 0x08 | -- |
| 0xFF | unbekannte Fehlerart |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 31 rows × 2 columns

| LIEF_NR | LIEF_NAME |
| --- | --- |
| 0x01 | Reinshagen / Delphi |
| 0x02 | Kostal |
| 0x03 | Hella |
| 0x04 | Siemens |
| 0x05 | Eaton |
| 0x06 | UTA |
| 0x07 | Helbako |
| 0x08 | Bosch |
| 0x09 | Loewe |
| 0x10 | VDO |
| 0x11 | Valeo |
| 0x12 | MBB |
| 0x13 | Kammerer |
| 0x14 | SWF |
| 0x15 | Blaupunkt |
| 0x16 | Philips |
| 0x17 | Alpine |
| 0x18 | Teves |
| 0x19 | Elektromatik Suedafrika |
| 0x20 | Becker |
| 0x21 | Preh |
| 0x22 | Alps |
| 0x23 | Motorola |
| 0x24 | Temic |
| 0x25 | Webasto |
| 0x26 | MotoMeter |
| 0x27 | Delphi PHI |
| 0x28 | DODUCO |
| 0x29 | DENSO |
| 0x30 | NEC |
| 0xFF | unbekannter Hersteller |
