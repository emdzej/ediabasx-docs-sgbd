# BAE.prg

- Jobs: [18](#jobs)
- Tables: [4](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Airbag ECE |
| ORIGIN | BMW TP-421 Winkler |
| REVISION | 1.08 |
| AUTHOR | BMW TP-421 Baumgartner, BMW TP-421 Winkler |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer AIRBAG E38
- [IDENT](#job-ident) - Ident-Daten fuer AIRBAG E38
- [STATUS_LESEN](#job-status-lesen) - Status des AIRBAG lesen
- [FS_QUICK_LESEN](#job-fs-quick-lesen) - Quicktest High-Konzept nach Lastenheft (mit Abwandlungen)
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [SG_LOGIN](#job-sg-login)
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [SPEICHER_LESEN](#job-speicher-lesen) - Speicher lesen BAE
- [TYP_LESEN](#job-typ-lesen) - Fahrzeugtyp lesen
- [DIAGNOSE_ERHALTEN](#job-diagnose-erhalten) - Diagnose aufrechterhalten
- [AUSSTATTUNG_SCHREIBEN](#job-ausstattung-schreiben) - Ausstattung schreiben
- [AUSSTATTUNG_LESEN](#job-ausstattung-lesen) - Ausstattung lesen BAE
- [PARAMETER_LESEN](#job-parameter-lesen) - Algorithmus- Parameter BAE auslesen
- [VERRIEGELUNG_LESEN](#job-verriegelung-lesen) - Auslesen des Pruefstempels
- [VERRIEGELUNG_SCHREIBEN](#job-verriegelung-schreiben) - Verriegelungsbytes setzen
- [HERSTELLDATUM_LESEN](#job-herstelldatum-lesen) - Herstelldatum des SG lesen

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

Init-Job fuer AIRBAG E38

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer AIRBAG E38

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

Status des AIRBAG lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| STAT_GURT_F_ANGESCHNALLT | int | 1 -&gt; angeschnallt |
| STAT_GURT_BF_ANGESCHNALLT | int | 1 -&gt; angeschnallt |
| STAT_SITZ_BF_BELEGT | int | 1 -&gt; Beifahrersitz belegt |
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
| STAT_SBE_SCHLUSS_IO | int | 0 -&gt; SBE defekt  Kurzschluss |
| STAT_SBE_HOCH_IO | int | 0 -&gt; SBE defekt  Hochohmig |
| STAT_SBE_KOMM_IO | int | 0 -&gt; SBE defekt  Kommunikationsstoerung |
| STAT_SBE_LOW_IO | int | 0 -&gt; ZP: Unterspannungsfehler |
| STAT_SENSOR_BF_IO | int | 0 -&gt; Drucksensor Beifahrer defekt |
| STAT_SENSOR_F_IO | int | 0 -&gt; Drucksensor Fahrer defekt |
| STAT_LAMPE_SCHLUSS_UBATT_IO | int | 0 -&gt; Fehlerlampe Schluss UBATT |
| STAT_LAMPE_SCHLUSS_MASSE_IO | int | 0 -&gt; Fehlerlampe Schluss/ Unterbr. Masse |
| STAT_GURTSCHL_BF_IO | int | 0 -&gt; Gurtschloss Beifahrer Unterbr./UBATT.Schluss |
| STAT_NA_BF_IO | int | 0 -&gt; Nicht auswertbarer Fehler, Gurtschloss Beifahrer |
| STAT_KAS_BF_IO | int | 0 -&gt; Kabelanliegeschluss Gurtschloss Beifahrer |
| STAT_GURTSCHL_F_IO | int | 0 -&gt; Gurtschloss Fahrer Unterbr./UBATT.Schluss |
| STAT_NA_F_IO | int | 0 -&gt; Nicht auswertbarer Fehler, Gurtschloss Fahrer |
| STAT_KAS_F_IO | int | 0 -&gt; Kabelanliegeschluss Gurtschloss Fahrer |

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
| F_ORT_TEXT | string | Fehlerort als Text |
| F_SPORADIK | int | Sporadikzaehler |
| BFU | long | Beginnfehleruhrzeit in Sec. |
| EFU | long | Endefehleruhrzeit in Sec. |
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
| F_ART_ANZ | int |  |
| F_HFK | int |  |
| F_UW_ANZ | int |  |

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

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| H_ADR | string | Login- Code High- Byte |
| L_ADR | string | Login- Code Low- Byte |

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

Speicher lesen BAE

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
| TEST | binary | Antwortdaten |

<a id="job-typ-lesen"></a>
### TYP_LESEN

Fahrzeugtyp lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| TYP | string | "E31","E32"... |

<a id="job-diagnose-erhalten"></a>
### DIAGNOSE_ERHALTEN

Diagnose aufrechterhalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-ausstattung-schreiben"></a>
### AUSSTATTUNG_SCHREIBEN

Ausstattung schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AB_F_VERB | string | 1 --&gt; verbaut |
| GS_F_VERB | string | 1 --&gt; verbaut |
| AB_BF_VERB | string | 1 --&gt; verbaut |
| GS_BF_VERB | string | 1 --&gt; verbaut |
| SCHLOSS_F_VERB | string | 1 --&gt; verbaut |
| SCHLOSS_BF_VERB | string | 1 --&gt; verbaut |
| SENSOR_F_VERB | string | 1 --&gt; verbaut |
| SENSOR_BF_VERB | string | 1 --&gt; verbaut |
| SITZ_ERKENNUNG_VERB | string | 1 --&gt; verbaut |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-ausstattung-lesen"></a>
### AUSSTATTUNG_LESEN

Ausstattung lesen BAE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| AB_F_VERBAUT | int | 1 --&gt; verbaut |
| GS_F_VERBAUT | int | 1 --&gt; verbaut |
| GS_BF_VERBAUT | int | 1 --&gt; verbaut |
| AB_BF_VERBAUT | int | 1 --&gt; verbaut |
| SCHLOSS_F_VERBAUT | int | 1 --&gt; verbaut |
| SCHLOSS_BF_VERBAUT | int | 1 --&gt; verbaut |
| SENSOR_F_VERBAUT | int | 1 --&gt; verbaut |
| SENSOR_BF_VERBAUT | int | 1 --&gt; verbaut |
| SITZ_ERKENNUNG_VERBAUT | int | 1 --&gt; verbaut |
| US_VERSION_VERBAUT | int | 1 --&gt; verbaut |

<a id="job-parameter-lesen"></a>
### PARAMETER_LESEN

Algorithmus- Parameter BAE auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", sonst Fehler |
| DATEN | binary | Codierdaten |

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

<a id="job-herstelldatum-lesen"></a>
### HERSTELLDATUM_LESEN

Herstelldatum des SG lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| HERSTELLDATUM | string | z.B: 21.4.93 ... |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (8 × 2)
- [FORTTEXTE](#table-forttexte) (48 × 2)
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

Dimensions: 48 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | AD- Wandler; Steuergeraetefehler |
| 0x02 | Widerstand ZK0 -&gt; Fahrer Airbag |
| 0x03 | Widerstand ZK1 -&gt; Fahrer Gurtstrammer |
| 0x04 | Widerstand ZK2 -&gt; Beifahrer Gurtstrammer |
| 0x05 | Widerstand ZK3 -&gt; Beifahrer Airbag |
| 0x06 | EEPROM |
| 0x07 | SPI- Kommunikation |
| 0x0C | Zuendspannung ZK0 -&gt; Fahrer Airbag |
| 0x0D | Zuendspannung ZK1 -&gt; Fahrer Gurtstrammer |
| 0x0E | Zuendspannung ZK2 -&gt; Beifahrer Gurtstrammer |
| 0x0F | Zuendspannung ZK3 -&gt; Beifahrer Airbag |
| 0x10 | Spannung Autarkiekondensator |
| 0x11 | Versorgungsspannung |
| 0x12 | TZ- Sperrleitung |
| 0x13 | Fehlerlampe |
| 0x14 | Sitzbelegungserkennung Beifahrer |
| 0x15 | Drucksensor Fahrer |
| 0x16 | Drucksensor Beifahrer |
| 0x17 | Temperatur; Steuergeraetefehler |
| 0x18 | Gurtschloss Fahrer |
| 0x19 | Gurtschloss Beifahrer |
| 0x30 | Steuergeraetefehler Autarkiefallmerker |
| 0x31 | Steuergeraetefehler Sicherheitsschalter / Ueberwachung |
| 0x32 | Steuergeraetefehler Airbag F LSH |
| 0x33 | Steuergeraetefehler Airbag F LSL |
| 0x34 | Steuergeraetefehler TZ- Sperrleitung |
| 0x35 | Steuergeraetefehler Zuendkontakt Fusspunkt |
| 0x36 | Steuergeraetefehler Gurtstr. F LSH |
| 0x37 | Steuergeraetefehler Gurtstr. F LSL |
| 0x38 | Steuergeraetefehler Einschwingpruefung |
| 0x39 | Steuergeraetefehler Gurtstr. BF LSH |
| 0x3A | Steuergeraetefehler Gurtstr. BF LSL |
| 0x3B | Steuergeraetefehler Stromquellenfehler |
| 0x3C | Steuergeraetefehler Airbag BF LSH |
| 0x3D | Steuergeraetefehler Airbag BF LSL |
| 0x3E | Steuergeraetefehler Reedspule |
| 0x3F | Steuergeraetefehler Mutiplexer |
| 0x41 | Steuergeraetefehler Autarkiekondensator |
| 0x43 | Steuergeraetefehler Zuendkondensator Airbag Fahrer |
| 0x44 | Steuergeraetefehler Zuendkondensator Gstr. Fahrer |
| 0x45 | Steuergeraetefehler Zuendkondensator Gstr. Beifahrer |
| 0x46 | Steuergeraetefehler Zuendkondensator Airbag Beifahrer |
| 0x47 | Steuergeraetefehler Signalpfad M1 |
| 0x48 | Steuergeraetefehler Signalpfad M2 |
| 0x49 | Kurzschluss zwischen den Zuendpillen |
| 0x4C | allg. Fehler des Airbag- Steuergeraetes |
| 0x4D | Fehler Crashtelegramm |
| 0xFF | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 10 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | Fehler nicht auswertbar |
| 0x02 | Fehler momentan vorhanden |
| 0x03 | Leitungsunterbrechung |
| 0x04 | Leckwiderstand oder Kurzschluss gegen Masse |
| 0x05 | Leckwiderstand oder Kurzschluss gegen U-Batt |
| 0x06 | Grenzwertunterschreitung |
| 0x07 | Grenzwertueberschreitung |
| 0x08 | sporadischer Fehler |
| 0xFF | nicht belegt |

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
