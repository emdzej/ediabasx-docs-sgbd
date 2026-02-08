# IHKA31.prg

- Jobs: [11](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Integrierte Heiz- Klimaautomatik E31 |
| ORIGIN | BMW ET-421 Drexel |
| REVISION | 1.05 |
| AUTHOR | BMW ET-421 Drexel |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Kommunikationsparameter fuer IHKA
- [ENDE](#job-ende) - Dieser Job bricht die Kommunikation ab
- [IDENT](#job-ident) - Identifikation
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen
- [FS_LOESCHEN](#job-fs-loeschen) - Diese Funktion ist ein Dummy
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [STATUS_LESEN_ANALOG](#job-status-lesen-analog) - Status lesen
- [STATUS_LESEN_DIGITAL](#job-status-lesen-digital) - Status lesen
- [STATUS_BEDIENTEIL](#job-status-bedienteil) - Status lesen Bedienteileinstellungen
- [SPEICHER_LESEN](#job-speicher-lesen) - Speicher lesen

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

Kommunikationsparameter fuer IHKA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-ende"></a>
### ENDE

Dieser Job bricht die Kommunikation ab

_No arguments._

_No results._

<a id="job-ident"></a>
### IDENT

Identifikation

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| ID_VERSION_NR | int | Versionsnummer |
| ID_LENKER | string | Linkslenker oder Rechtslenker |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Text zu Fehlerort |
| F_HFK | int | Fehlerhaeufigkeit |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen |
| F_ART1_NR | int |  |
| F_ART1_TEXT | string |  |
| F_ART2_NR | int |  |
| F_ART2_TEXT | string |  |
| F_ART3_NR | int |  |
| F_ART3_TEXT | string |  |
| F_ART4_NR | int |  |
| F_ART4_TEXT | string |  |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Diese Funktion ist ein Dummy

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-status-lesen-analog"></a>
### STATUS_LESEN_ANALOG

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_INNENRAUMTEMP_WERT | real |  |
| STAT_AUSSENTEMP_WERT | real |  |
| STAT_VERDAMPFERTEMP_WERT | real |  |
| STAT_LI_TAUSCHERTEMP_WERT | real |  |
| STAT_RE_TAUSCHERTEMP_WERT | real |  |
| STAT_LI_INNENTEMP_KORR_SOLL_WERT | real |  |
| STAT_RE_INNENTEMP_KORR_SOLL_WERT | real |  |
| STAT_LI_INNENTEMP_SOLL_WERT | real |  |
| STAT_RE_INNENTEMP_SOLL_WERT | real |  |
| STAT_LUFTMENGENWAEHLRAD_WERT | real |  |
| STAT_SPANNUNG_KL15_WERT | real |  |
| STAT_GEBLAESESTEUERSPG_WERT | real |  |
| STAT_LI_FUEHRUNGSREGLER_WERT | real |  |
| STAT_RE_FUEHRUNGSREGLER_WERT | real |  |
| STAT_LI_TAKTVENTIL_TASTVERH_WERT | real |  |
| STAT_RE_TAKTVENTIL_TASTVERH_WERT | real |  |
| STAT_FAHRGESCHWINDIGKEIT_WERT | real |  |
| STAT_SCHICHTUNGSSTELLER_WERT | int |  |
| STAT_FRISCHLUFTKLAPPENPOS_WERT | int |  |
| STAT_UMLUFTKLAPPENPOS_WERT | int |  |
| STAT_LI_BELUEFTUNG_VORNE_WERT | int |  |
| STAT_RE_BELUEFTUNG_VORNE_WERT | int |  |
| STAT_LI_SCHICHTUNGSKLAPPE_WERT | int |  |
| STAT_RE_SCHICHTUNGSKLAPPE_WERT | int |  |
| STAT_FONDRAUMKLAPPE_WERT | int |  |
| STAT_LI_FUSSRAUMKLAPPE_WERT | int |  |
| STAT_RE_FUSSRAUMKLAPPE_WERT | int |  |
| STAT_ENTFROSTKLAPPE_WERT | int |  |
| STAT_HSH_STATUS | int |  |
| STAT_HSH_ZEITZAEHLER | int |  |
| STAT_HSH_MODULATION | int |  |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-status-lesen-digital"></a>
### STATUS_LESEN_DIGITAL

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_EICHFAHRT_EIN | int |  |
| STAT_KOMPRESSOR_EIN | int |  |
| STAT_ZUSATZWASSERPUMPE_EIN | int |  |
| STAT_VERDAMPFERREGELUNG_EIN | int |  |
| STAT_KALTSTARTVERR_EIN | int |  |
| STAT_EICHFAHRT_NOTWENDIG | int |  |
| STAT_LUFTMENGENWAEHLRAD_MAX | int |  |
| STAT_HECKSCHEIBENHEIZUNG_EIN | int |  |
| STAT_STANDLUEFTUNG_EIN | int |  |
| STAT_UMLUFT_SCHALTER_EIN | int |  |
| STAT_KLIMA_SCHALTER_EIN | int |  |
| STAT_LI_UNTEN_SCHALTER_EIN | int |  |
| STAT_LI_MAXIMAL_SCHALTER_EIN | int |  |
| STAT_LI_NORMAL_SCHALTER_EIN | int |  |
| STAT_DEFROST_SCHALTER_EIN | int |  |
| STAT_FONDRAUM_SCHALTER_EIN | int |  |
| STAT_RECHTSLENKER_EIN | int |  |
| STAT_RE_UNTEN_SCHALTER_EIN | int |  |
| STAT_RE_MAXIMAL_SCHALTER_EIN | int |  |
| STAT_RE_NORMAL_SCHALTER_EIN | int |  |
| STAT_STANDHEIZUNG_EIN | int |  |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-status-bedienteil"></a>
### STATUS_BEDIENTEIL

Status lesen Bedienteileinstellungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_LI_INNENTEMP_SOLL_WERT | real |  |
| STAT_RE_INNENTEMP_SOLL_WERT | real |  |
| STAT_LUFTMENGENWAEHLRAD_WERT | real |  |
| STAT_LUFTMENGENWAEHLRAD_MAX | int |  |
| STAT_HECKSCHEIBENHEIZUNG_EIN | int |  |
| STAT_UMLUFT_SCHALTER_EIN | int |  |
| STAT_KLIMA_SCHALTER_EIN | int |  |
| STAT_LI_UNTEN_SCHALTER_EIN | int |  |
| STAT_LI_MAXIMAL_SCHALTER_EIN | int |  |
| STAT_LI_NORMAL_SCHALTER_EIN | int |  |
| STAT_DEFROST_SCHALTER_EIN | int |  |
| STAT_RE_UNTEN_SCHALTER_EIN | int |  |
| STAT_RE_MAXIMAL_SCHALTER_EIN | int |  |
| STAT_RE_NORMAL_SCHALTER_EIN | int |  |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Speicher lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| DATEN | binary | Antworttelegramm |

## Tables

### Index

- [FARTMATRIX](#table-fartmatrix) (33 × 8)
- [FORTTEXTE](#table-forttexte) (33 × 3)
- [FARTTEXTE](#table-farttexte) (8 × 2)

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 33 rows × 8 columns

| CODE | A10 | A11 | A20 | A21 | A30 | A31 | A4MASK |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 0x00 | 0 | 0 | 0 | 3 | 0 | 2 | 0x00000001 |
| 0x01 | 0 | 0 | 0 | 3 | 0 | 2 | 0x00000002 |
| 0x02 | 0 | 0 | 0 | 3 | 0 | 2 | 0x00000004 |
| 0x03 | 0 | 0 | 0 | 3 | 0 | 2 | 0x00000008 |
| 0x04 | 0 | 0 | 0 | 3 | 0 | 2 | 0x00000010 |
| 0x05 | 0 | 4 | 0 | 0 | 0 | 1 | 0x00000020 |
| 0x06 | 0 | 0 | 0 | 0 | 0 | 0 | 0x00000000 |
| 0x07 | 0 | 0 | 0 | 4 | 0 | 1 | 0x00000080 |
| 0x08 | 0 | 0 | 0 | 3 | 0 | 2 | 0x00000100 |
| 0x09 | 0 | 0 | 0 | 3 | 0 | 2 | 0x00000200 |
| 0x0a | 0 | 0 | 0 | 3 | 0 | 2 | 0x00000400 |
| 0x0b | 0 | 0 | 0 | 3 | 0 | 2 | 0x00000800 |
| 0x0c | 0 | 0 | 0 | 4 | 0 | 1 | 0x00001000 |
| 0x0d | 0 | 0 | 0 | 4 | 0 | 1 | 0x00002000 |
| 0x0e | 0 | 0 | 0 | 4 | 0 | 1 | 0x00004000 |
| 0x0f | 0 | 0 | 0 | 4 | 0 | 1 | 0x00008000 |
| 0x10 | 0 | 0 | 0 | 0 | 0 | 0 | 0x00000000 |
| 0x11 | 0 | 0 | 0 | 4 | 0 | 1 | 0x00020000 |
| 0x12 | 0 | 0 | 0 | 0 | 0 | 0 | 0x00000000 |
| 0x13 | 0 | 0 | 0 | 0 | 0 | 0 | 0x00000000 |
| 0x14 | 0 | 0 | 0 | 0 | 0 | 0 | 0x00000000 |
| 0x15 | 0 | 0 | 0 | 0 | 0 | 0 | 0x00000000 |
| 0x16 | 0 | 5 | 0 | 0 | 0 | 1 | 0x00400000 |
| 0x17 | 0 | 5 | 0 | 0 | 0 | 1 | 0x00800000 |
| 0x18 | 0 | 5 | 0 | 0 | 0 | 1 | 0x01000000 |
| 0x19 | 0 | 5 | 0 | 0 | 0 | 1 | 0x02000000 |
| 0x1a | 0 | 5 | 0 | 0 | 0 | 1 | 0x04000000 |
| 0x1b | 0 | 5 | 0 | 0 | 0 | 1 | 0x08000000 |
| 0x1c | 0 | 5 | 0 | 0 | 0 | 1 | 0x10000000 |
| 0x1d | 0 | 5 | 0 | 0 | 0 | 1 | 0x20000000 |
| 0x1e | 0 | 5 | 0 | 0 | 0 | 1 | 0x40000000 |
| 0x1f | 0 | 5 | 0 | 0 | 0 | 1 | 0x80000000 |
| 0xFF | 0 | 0 | 0 | 0 | 0 | 0 | 0x00000000 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 33 rows × 3 columns

| CODE | ORT | ORTTEXT |
| --- | --- | --- |
| 0x00 | 0x01 | Sollwertsteller rechts |
| 0x01 | 0x04 | Waermetauscherfuehler rechts |
| 0x02 | 0x07 | Verdampferfuehler |
| 0x03 | 0x0a | Aussentemperaturfuehler |
| 0x04 | 0x0d | Innenraumtemperaturfuehler |
| 0x05 | 0x10 | Innenfuehlergeblaese |
| 0x06 | 0x13 | Relais Frontscheibenheizung |
| 0x07 | 0x16 | Relais Zusatzluefter |
| 0x08 | 0x19 | Sollwertsteller links |
| 0x09 | 0x1c | Waermetauscherfuehler links |
| 0x0a | 0x1f | Geblaesepotentiometer |
| 0x0b | 0x22 | Schichtungspotentiometer |
| 0x0c | 0x26 | Relais Zusatzwasserpumpe |
| 0x0d | 0x28 | Wasserventil links |
| 0x0e | 0x2c | Magnetkupplung Klimakompressor |
| 0x0f | 0x2e | Wasserventil rechts |
| 0x10 | 0x00 | unbekannter Fehlerort |
| 0x11 | 0x2f | Relais Heckscheibenheizung |
| 0x12 | 0x00 | unbekannter Fehlerort |
| 0x13 | 0x00 | unbekannter Fehlerort |
| 0x14 | 0x00 | unbekannter Fehlerort |
| 0x15 | 0x00 | unbekannter Fehlerort |
| 0x16 | 0x34 | Frischluftklappenmotor |
| 0x17 | 0x37 | Umluftklappenmotor |
| 0x18 | 0x3a | Belueftungsklappenmotor links |
| 0x19 | 0x3d | Schichtungsklappenmotor rechts |
| 0x1a | 0x40 | Schichtungsklappenmotor links |
| 0x1b | 0x43 | Fondraumklappenmotor |
| 0x1c | 0x46 | Fussraumklappenmotor links |
| 0x1d | 0x49 | Fussraumklappenmotor rechts |
| 0x1e | 0x4c | Entfrostungsklappenmotor |
| 0x1f | 0x4f | Belueftungsklappenmotor rechts |
| 0xFF | 0x00 | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 8 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0 | -- |
| 1 | Kurzschluss gegen U-Batt |
| 2 | Kurzschluss gegen U-Batt oder Leitungsunterbrechung |
| 3 | Kurzschluss gegen Masse |
| 4 | Kurzschluss gegen Masse oder Leitungsunterbrechung |
| 5 | Leitungsunterbrechung |
| 6 | Fehler momentan nicht vorhanden |
| 7 | Fehler momentan vorhanden |
