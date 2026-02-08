# TOENS_2.prg

- Jobs: [18](#jobs)
- Tables: [5](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Thermischer Oelniveau Sensor |
| ORIGIN | BMW TP-423 Drexel |
| REVISION | 1.00 |
| AUTHOR | BMW TP-423 Drexel |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [IDENT](#job-ident) - Identdaten fuer TOENS
- [IDENT_SCHREIBEN](#job-ident-schreiben) - Identdaten schreiben fuer TOENS
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen des internen Speichers
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des Speichers
- [CODIERUNG_LESEN](#job-codierung-lesen) - Auslesen der Codierdaten
- [CODIERUNG_SCHREIBEN](#job-codierung-schreiben) - Schreiben der Codierdaten
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode aufrechterhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [STATUS_IO](#job-status-io) - Status lesen
- [STATUS_SG](#job-status-sg) - SG-Status lesen
- [STEUERN_WARNLAMPE](#job-steuern-warnlampe) - Ansteuern der Warnlampe

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

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-ident"></a>
### IDENT

Identdaten fuer TOENS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| ID_BMW_NR | string | BMW Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Nummer |
| ID_SW_NR | int | Softwarenummer |

<a id="job-ident-schreiben"></a>
### IDENT_SCHREIBEN

Identdaten schreiben fuer TOENS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | Identdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

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
| F_HEX_CODE | binary |  |

<a id="job-is-lesen"></a>
### IS_LESEN

Infospeicher lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| F_ORT_NR | int | Index fuer Infoort |
| F_ORT_TEXT | string | Text zu Infoort |
| F_HFK | int | Fehlerhaeufigkeit |
| F_ART_ANZ | int | Anzahl der Infoarten |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen |
| F_HEX_CODE | binary |  |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Lesen des internen Speichers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int |  |
| ANZAHL | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-speicher-schreiben"></a>
### SPEICHER_SCHREIBEN

Beschreiben des Speichers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int |  |
| ANZAHL | int |  |
| DATEN | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Auslesen der Codierdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| CODEBLOCK_0 | binary |  |
| CODEBLOCK_1 | binary |  |
| CODEBLOCK_2 | binary |  |

<a id="job-codierung-schreiben"></a>
### CODIERUNG_SCHREIBEN

Schreiben der Codierdaten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODEBLOCK | binary | 1.Byte Blocknummer (0,1,2) danach Daten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | kann beliebig verwendet werden 0x00-0xFF |
| BYTE2 | int | kann beliebig verwendet werden 0x00-0xFF |
| BYTE3 | int | kann beliebig verwendet werden 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Diagnosemode aufrechterhalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-status-io"></a>
### STATUS_IO

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_KLEMME_30_EIN | int | Klemme 30 liegt an |
| STAT_KLEMME_15_EIN | int | Klemme 15 liegt an |
| STAT_WARNLAMPE_EIN | int | Kontrolleuchte angesteuert |
| STAT_WARNLAMPE_MONITOR_EIN | int | Kontrolleuchte Rueckmeldung |
| STAT_TOG_HIGH_WERT | real | gemessene TOENS-Signal-Highzeit |
| STAT_TOG_HIGH_EINH | string | ms |
| STAT_TOG_LOW_WERT | real | gemessene TOENS-Signal-Lowzeit |
| STAT_TOG_LOW_EINH | string | ms |
| STAT_DREHZAHL_WERT | int | gemessene Motordrehzahl |
| STAT_DREHZAHL_EINH | string | 1/min |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-status-sg"></a>
### STATUS_SG

SG-Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_TOG_LOW_WERT | real | gemessene TOENS-Signal-Lowzeit |
| STAT_TOG_LOW_EINH | string | ms |
| STAT_TOG_HIGH_WERT | real | gemessene TOENS-Signal-Highzeit |
| STAT_TOG_HIGH_EINH | string | ms |
| STAT_STATUS_FLAG_WERT | int | Status Flags |
| STAT_STATUS_FLAG_EINH | string | -- |
| STAT_DELAY_EIN | int | Startverzoegerung abgelaufen |
| STAT_OELKALT_EIN | int | kaltes Oel erkannt |
| STAT_OELWARM_EIN | int | warmes Oel erkannt |
| STAT_FKWREADY_EIN | int | orient. Messung abgelaufen |
| STAT_FIRSTAML_EIN | int | erster, vorgezogener Mittelwert |
| STAT_NEWAML_EIN | int | neuer Standardmittelwert |
| STAT_IGNOREMW_EIN | int | Messwertausblendung |
| STAT_FUNKTION_EIN | int | Funktionsanz. im TOENS-Takt |
| STAT_TOG_IMP_COUNTER_WERT | int | Messwertzaehler fuer Kurzzeit-Mittelwert |
| STAT_TOG_IMP_COUNTER_EINH | string | -- |
| STAT_MITTEL_LANG_COUNT_WERT | int | Messwertzaehler fuer Langzeit-Mittelwert |
| STAT_MITTEL_LANG_COUNT_EINH | string | -- |
| STAT_DREHZAHL_MITTEL_WERT | int | Mittelwert der Motordrehzahl |
| STAT_DREHZAHL_MITTEL_EINH | string | 1/min |
| STAT_TOG_HIGH_MITTEL_WERT | real | Kurzzeitmittelwert der TOENS-Heizzeit |
| STAT_TOG_HIGH_MITTEL_EINH | string | ms |
| STAT_TOG_NIVEAU_MITTEL_1_WERT | real | Kurzzeitmittelwert des Oelniveaus |
| STAT_TOG_NIVEAU_MITTEL_1_EINH | string | mm |
| STAT_TOG_NIVEAU_MITTEL_KORR_WERT | real | drehzahlkorregierter Kurzzeitmittelwert des Oelniveaus |
| STAT_TOG_NIVEAU_MITTEL_KORR_EINH | string | mm |
| STAT_TOG_NIVEAU_MITTEL_WERT | real | Langzeitmittelwert des Oelniveaus |
| STAT_TOG_NIVEAU_MITTEL_EINH | string | mm |
| STAT_TOGINFO_WERT | int | TOGINFO Flags |
| STAT_TOGINFO_EINH | string | -- |
| STAT_STATUS_WERT | int | TOGINFO Status |
| STAT_STATUS_EINH | string | -- |
| STAT_WARNUNGH_EIN | int | Warnung Oelverlust |
| STAT_WARNUNGL_EIN | int | Warnung Oelverbrauch |
| STAT_NOSIGNAL_EIN | int | Kein Togsignal (Pegel H) |
| STAT_SIG_TO_GND_EIN | int | Kein Togsignal (Pegel L) |
| STAT_NO_DREHZAHL_EIN | int | Kein Drehzahlsignal |
| STAT_NO_LED_EIN | int | Kein Lampenstrom |
| STAT_LED_TO_UB_EIN | int | Lampenkurzschluss |
| STAT_D_PLAUSENDE_EIN | int | Plausibilitaets-Pruefung abgeschlossen |
| STAT_D_KALTTEMP_EIN | int | Drehzahl-Kalttemp erkannt |
| STAT_D_STARTKONTROLLE_EIN | int | Drehzahl-Kontrolle gestartet |
| STAT_D_DTHETA_EIN | int | Delta Theta fuer Plausibilitaetspruefung erreicht |
| STAT_D_DREHZAHL_NULL_EIN | int | Drehzahl waehrend Plausibilitaetspruefung dauernd Null |
| STAT_D_AMHEIZ_EIN | int | Mittelwert Oeltemp. verfuegbar |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-steuern-warnlampe"></a>
### STEUERN_WARNLAMPE

Ansteuern der Warnlampe

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WARNLAMPE | string | 'EIN','AUS','1','0' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (8 × 2)
- [LIEFERANTEN](#table-lieferanten) (38 × 2)
- [FORTTEXTE](#table-forttexte) (5 × 2)
- [FARTTEXTE](#table-farttexte) (7 × 2)
- [IORTTEXTE](#table-iorttexte) (3 × 2)

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

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 38 rows × 2 columns

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
| 0x31 | DASA |
| 0x32 | Pioneer |
| 0x33 | Jatco |
| 0x34 | Fuba |
| 0x35 | UK-NSI |
| 0x36 | AABG |
| 0x37 | Dunlop |
| 0xFF | unbekannter Hersteller |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 5 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | TOENS-Signal |
| 0x02 | Drehzahlsignal |
| 0x03 | Warnlampe |
| 0x04 | Klemme 30 |
| 0xFF | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 7 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Fehler momentan nicht vorhanden |
| 0x01 | Fehler momentan vorhanden |
| 0x10 | Kurzschluss gegen U-Batt |
| 0x11 | Kurzschluss gegen Masse |
| 0x12 | Leitungsunterbrechung |
| 0x13 | unplausibler Wert |
| 0xFF | unbekannte Fehlerart |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 3 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Warnung: Oelverlust |
| 0x02 | Warnung: Oelverbrauch |
| 0xFF | unbekannter Fehlerort |
