# SM_RD.prg

- Jobs: [13](#jobs)
- Tables: [5](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | SM_RD E31 / E32 / E34 |
| ORIGIN | BMW TP-422 Teepe |
| REVISION | 1.44 |
| AUTHOR | BMW TP-422 Teepe |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Default init job
- [IDENT](#job-ident) - Default ident job
- [FS_LESEN](#job-fs-lesen) - Default fs_lesen job
- [STATUS_ANALOG_LESEN](#job-status-analog-lesen) - Default position_lesen job
- [FS_LOESCHEN](#job-fs-loeschen) - Default FS_LOESCHEN job
- [STEUERN_DIGITAL](#job-steuern-digital) - Ansteuern eines digitalen Ein- oder Ausgangs
- [STATUS_DIGITAL_LESEN](#job-status-digital-lesen) - Default STATUS_DIGITAL_LESEN job
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Default diagnose_ende job
- [RAM_LESEN](#job-ram-lesen) - Auslesen des Speicherinhaltes
- [RAM_SCHREIBEN](#job-ram-schreiben) - Schreiben des Speicherinhaltes
- [EEPROM_LESEN](#job-eeprom-lesen) - Auslesen des Speicherinhaltes
- [EEPROM_SCHREIBEN](#job-eeprom-schreiben) - Schreiben des Speicherinhaltes

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

Default init job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 if done |

<a id="job-ident"></a>
### IDENT

Default ident job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | Hardwarenummer |
| ID_COD_INDEX | int | Codierindex |
| ID_DIAG_INDEX | int | Diagnoseindex |
| ID_BUS_INDEX | int | Busindex |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferantennummer |
| ID_LIEF_TEXT | string | Lieferantenname |
| ID_SW_NR | int | Softwarenummer |

<a id="job-fs-lesen"></a>
### FS_LESEN

Default fs_lesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ORT_NR | int | Nr des Fehlers |
| F_ORT_TEXT | string | Fehlertext |
| F_HFK | int | Haeufigkeit des Fehlers (hier immer 1) |
| F_ART_ANZ | int | Anzahl der Fehlerarten (hier immer 0) |
| F_UW_ANZ | int | Anzahl der Umweltarten (hier immer 0) |

<a id="job-status-analog-lesen"></a>
### STATUS_ANALOG_LESEN

Default position_lesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_KOPFSTUETZE_WERT | int | Position der Kopfstuetze |
| STAT_SITZHOEHE_WERT | int | Position der Sitzhoehe |
| STAT_LEHNE_WERT | int | Position der Sitzlehne |
| STAT_OBERSCHENKEL_WERT | int | Position der Oberschenkelauflage |
| STAT_SITZNEIGUNG_WERT | int | Position der Sitzneigung |
| STAT_SITZSCHLITTEN_WERT | int | Position des Sitzschlittens |
| STAT_BF_SPIEGEL_HOR_WERT | int | Position Beifahrerspiegel horizontal |
| STAT_BF_SPIEGEL_VER_WERT | int | Position Beifahrerspiegel vertikal |
| STAT_F_SPIEGEL_HOR_WERT | int | Position Fahrerspiegel horizontal |
| STAT_F_SPIEGEL_VER_WERT | int | Position der Fahrerspiegel vertikal |
| STAT_KOPFSTUETZE_EINH | string | Position der Kopfstuetze |
| STAT_SITZHOEHE_EINH | string | Position der Sitzhoehe |
| STAT_LEHNE_EINH | string | Position der Sitzlehne |
| STAT_OBERSCHENKEL_EINH | string | Position der Oberschenkelauflage |
| STAT_SITZNEIGUNG_EINH | string | Position der Sitzneigung |
| STAT_SITZSCHLITTEN_EINH | string | Position des Sitzschlittens |
| STAT_BF_SPIEGEL_HOR_EINH | string | Position Beifahrerspiegel horizontal |
| STAT_BF_SPIEGEL_VER_EINH | string | Position Beifahrerspiegel vertikal |
| STAT_F_SPIEGEL_HOR_EINH | string | Position Fahrerspiegel horizontal |
| STAT_F_SPIEGEL_VER_EINH | string | Position der Fahrerspiegel vertikal |
| STAT_U_BATT_WERT | int | Messwert Batteriespannung 0 bis 18 Volt |
| STAT_U_BATT_EINH | string | Messwert Batteriespannung |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Default FS_LOESCHEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

Ansteuern eines digitalen Ein- oder Ausgangs

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | gewuenschte Komponente und Richtung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-status-digital-lesen"></a>
### STATUS_DIGITAL_LESEN

Default STATUS_DIGITAL_LESEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_SCHALTER_OBERSCHENKELAUFLAGE_VOR_EIN | int | aktiv low! |
| STAT_SCHALTER_OBERSCHENKELAUFLAGE_ZURUECK_EIN | int | aktiv low! |
| STAT_SCHALTER_HOEHE_AUF_EIN | int | aktiv low! |
| STAT_SCHALTER_KOPFSTUETZE_AB_EIN | int | aktiv low! |
| STAT_SCHALTER_KOPFSTUETZE_AUF_EIN | int | aktiv low! |
| STAT_SCHALTER_LEHNE_ZURUECK_EIN | int | aktiv low! |
| STAT_SCHALTER_LEHNE_VOR_EIN | int | aktiv low! |
| STAT_SCHALTER_SCHLITTEN_ZURUECK_EIN | int | aktiv low! |
| STAT_TUERKONTAKT_EIN | int | aktiv low! |
| STAT_SICHERHEITSSCHALTER_EIN | int | aktiv low! |
| STAT_SCHALTER_SCHLITTEN_VOR_EIN | int | aktiv low! |
| STAT_SCHALTER_NEIGUNG_AB_EIN | int | aktiv low! |
| STAT_SCHALTER_NEIGUNG_AUF_EIN | int | aktiv low! |
| STAT_SCHALTER_HOEHE_AB_EIN | int | aktiv low! |
| STAT_RELAIS_1_UEBERWACHUNG_KONTAKT_EIN | int | aktiv low! |
| STAT_RELAIS_2_UEBERWACHUNG_KONTAKT_EIN | int | aktiv low! |
| STAT_RELAIS_3_UEBERWACHUNG_KONTAKT_EIN | int | aktiv low! |
| STAT_RELAIS_4_UEBERWACHUNG_KONTAKT_EIN | int | aktiv low! |
| STAT_RELAIS_5_UEBERWACHUNG_KONTAKT_EIN | int | aktiv low! |
| STAT_RELAIS_6_UEBERWACHUNG_KONTAKT_EIN | int | aktiv low! |
| STAT_RELAIS_7_UEBERWACHUNG_KONTAKT_EIN | int | aktiv low! |
| STAT_RELAIS_8_UEBERWACHUNG_KONTAKT_EIN | int | aktiv low! |
| STAT_RELAIS_1_UEBERWACHUNG_ANSTEUERUNG_EIN | int |  |
| STAT_RELAIS_2_UEBERWACHUNG_ANSTEUERUNG_EIN | int |  |
| STAT_RELAIS_3_UEBERWACHUNG_ANSTEUERUNG_EIN | int |  |
| STAT_RELAIS_4_UEBERWACHUNG_ANSTEUERUNG_EIN | int |  |
| STAT_RELAIS_5_UEBERWACHUNG_ANSTEUERUNG_EIN | int |  |
| STAT_RELAIS_6_UEBERWACHUNG_ANSTEUERUNG_EIN | int |  |
| STAT_RELAIS_7_UEBERWACHUNG_ANSTEUERUNG_EIN | int |  |
| STAT_RELAIS_8_UEBERWACHUNG_ANSTEUERUNG_EIN | int |  |
| STAT_SPEICHERTASTE_EIN | int | aktiv low |
| STAT_TASTE_1_EIN | int | aktiv low |
| STAT_TASTE_2_EIN | int | aktiv low |
| STAT_TASTE_3_EIN | int | aktiv low |
| STAT_ANZEIGE_SPEICHERBEREITSCHAFT_EIN | int |  |
| STAT_SPIEGELSCHALTER_RECHTS_EIN | int | aktiv low |
| STAT_SPIEGELSCHALTER_LINKS_EIN | int | aktiv low |
| STAT_SPIEGELSCHALTER_AUF_EIN | int | aktiv low |
| STAT_SPIEGELSCHALTER_AB_EIN | int | aktiv low |
| STAT_SPIEGELWAHLSCHALTER | string | Fahrer (low), Beifahrer (high) |
| STAT_SPIEGELTREIBER_UEBERSTROM_EIN | int | aktiv low |
| STAT_VERSORGUNGSSPANNUNG_SPIEGEL_EIN | int | aktiv low |
| STAT_SPIEGELTREIBER_MBH_EIN | int | aktiv high |
| STAT_SPIEGELTREIBER_MBH_MBV_EIN | int | aktiv high |
| STAT_SPIEGELTREIBER_MBV_EIN | int | aktiv high |
| STAT_SPIEGELTREIBER_MFH_EIN | int | aktiv high |
| STAT_SPIEGELTREIBER_MFH_MFV_EIN | int | aktiv high |
| STAT_SPIEGELTREIBER_MFV_EIN | int | aktiv high |
| STAT_SPIEGELMOTOR_STROMRUECKFUEHRUNG_EIN | int | aktiv low |
| STAT_EINGANG_KLEMME_r_EIN | int | aktiv high |
| STAT_EINGANG_KLEMME_15_EIN | int | aktiv high |
| STAT_RUECKWAERTSGANG_EIN | int | aktiv high |
| STAT_RELAIS_1_ANSTEUERUNG_EIN | int | aktiv low |
| STAT_RELAIS_2_ANSTEUERUNG_EIN | int | aktiv low |
| STAT_RELAIS_3_ANSTEUERUNG_EIN | int | aktiv low |
| STAT_RELAIS_4_ANSTEUERUNG_EIN | int | aktiv low |
| STAT_RELAIS_5_ANSTEUERUNG_EIN | int | aktiv low |
| STAT_RELAIS_6_ANSTEUERUNG_EIN | int | aktiv low |
| STAT_RELAIS_7_ANSTEUERUNG_EIN | int | aktiv low |
| STAT_RELAIS_8_ANSTEUERUNG_EIN | int | aktiv low |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Default diagnose_ende job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-ram-lesen"></a>
### RAM_LESEN

Auslesen des Speicherinhaltes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LOW | int | gewuenschte Startadresse low als Hexwert! |
| ANZAHL | int | gewuenschte Anzahl als Hexwert! |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| DATEN | binary | angeforderter Datenblock (max 12 Bytes!) |

<a id="job-ram-schreiben"></a>
### RAM_SCHREIBEN

Schreiben des Speicherinhaltes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE_LOW | int | gewuenschte Adresse low als Hexwert! |
| ANZAHL | int | gewuenschte Anzahl Bytes (maximal 7!) |
| BYTE1 | int | gewuenschter Wert fuer Byte1 als Hexwert! |
| BYTE2 | int | gewuenschter Wert fuer Byte2 als Hexwert! |
| BYTE3 | int | gewuenschter Wert fuer Byte3 als Hexwert! |
| BYTE4 | int | gewuenschter Wert fuer Byte4 als Hexwert! |
| BYTE5 | int | gewuenschter Wert fuer Byte5 als Hexwert! |
| BYTE6 | int | gewuenschter Wert fuer Byte6 als Hexwert! |
| BYTE7 | int | gewuenschter Wert fuer Byte7 als Hexwert! |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| DATEN | binary | geaenderte Bytes |

<a id="job-eeprom-lesen"></a>
### EEPROM_LESEN

Auslesen des Speicherinhaltes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LOW | int | gewuenschte Startadresse low als Hexwert! |
| ANZAHL | int | gewuenschte Anzahl (max. 12) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| DATEN | binary | angeforderter Datenblock (max 12 Bytes!) |

<a id="job-eeprom-schreiben"></a>
### EEPROM_SCHREIBEN

Schreiben des Speicherinhaltes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE_LOW | int | gewuenschte Adresse low als Hexwert! |
| ANZAHL | int | gewuenschte Anzahl Bytes (maximal 7!) |
| BYTE1 | int | gewuenschter Wert fuer Byte1 als Hexwert! |
| BYTE2 | int | gewuenschter Wert fuer Byte2 als Hexwert! |
| BYTE3 | int | gewuenschter Wert fuer Byte3 als Hexwert! |
| BYTE4 | int | gewuenschter Wert fuer Byte4 als Hexwert! |
| BYTE5 | int | gewuenschter Wert fuer Byte5 als Hexwert! |
| BYTE6 | int | gewuenschter Wert fuer Byte6 als Hexwert! |
| BYTE7 | int | gewuenschter Wert fuer Byte7 als Hexwert! |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| DATEN | binary | angeforderte Datenbytes |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (48 × 2)
- [LIEFERANTEN](#table-lieferanten) (27 × 2)
- [STEUERN](#table-steuern) (21 × 4)
- [BYTES](#table-bytes) (11 × 9)
- [JOBRESULT](#table-jobresult) (8 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 48 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Potentiometerfehler Kopfstuetze |
| 0x02 | Potentiometerfehler Sitzhoehe |
| 0x03 | Potentiometerfehler Lehnenneigung |
| 0x04 | Potentiometerfehler Oberschenkelauflage |
| 0x05 | Potentiometerfehler Sitzneigung |
| 0x06 | Potentiometerfehler Sitzlaengsverstellung |
| 0x07 | nicht verwendet 07 |
| 0x08 | nicht verwendet 08 |
| 0x09 | intern 09 |
| 0x0A | intern 0A |
| 0x0B | Potentiometer Beifahrerspiegel horizontal |
| 0x0C | Potentiometer Beifahrerspiegel vertikal |
| 0x0D | Potentiometer Fahrerspiegel horizontal |
| 0x0E | Potentiometer Fahrerspiegel vertikal |
| 0x0F | intern 0F |
| 0x10 | intern 10 |
| 0x11 | Antrieb Kopfstuetze |
| 0x12 | Antrieb Sitzhoehe |
| 0x13 | Antrieb Sitzlehne |
| 0x14 | Antrieb Oberschenkelauflage |
| 0x15 | Antrieb Sitzneigung |
| 0x16 | Antrieb Sitzschlitten |
| 0x17 | Relaisueberwachung Langzeitfehler |
| 0x18 | Relaisueberwachung Kurzzeitfehler |
| 0x19 | intern 19 |
| 0x1A | intern 1A |
| 0x1B | Antrieb BF-Spiegel horizontal |
| 0x1C | Antrieb BF-Spiegel vertikal |
| 0x1D | Antrieb F-Spiegel horizontal |
| 0x1E | Antrieb F-Spiegel vertikal |
| 0x1F | intern 1F |
| 0x20 | intern 20 |
| 0x21 | Laufrichtung Kopfstuetze |
| 0x22 | Laufrichtung Sitzhoehe |
| 0x23 | Laufrichtung Lehnenneigung |
| 0x24 | Laufrichtung Oberschenkelauflage |
| 0x25 | Laufrichtung Sitzneigung |
| 0x26 | Laufrichtung Sitzschlitten |
| 0x27 | intern 27 |
| 0x28 | intern 28 |
| 0x29 | intern 29 |
| 0x2A | intern 2A |
| 0x2B | Laufrichtung BF-Spiegel horizontal |
| 0x2C | Laufrichtung BF-Spiegel vertikal |
| 0x2D | Laufrichtung F-Spiegel horizontal |
| 0x2E | Laufrichtung F-Spiegel vertikal |
| 0x2F | intern 2F |
| 0x30 | intern 30 |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 27 rows × 2 columns

| LIEF_NR | LIEF_NAME |
| --- | --- |
| 0x01 | Reinshagen |
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
| 0xFF | unbekannter Hersteller |

<a id="table-steuern"></a>
### STEUERN

Dimensions: 21 rows × 4 columns

| ORT | BYTE1 | BYTE2 | BYTE3 |
| --- | --- | --- | --- |
| SOZ | 0xFD | 0xFF | 0xFF |
| SOV | 0xFB | 0xFF | 0xFF |
| SHA | 0xF7 | 0xFF | 0xFF |
| SKB | 0xEF | 0xFF | 0xFF |
| SKA | 0xDF | 0xFF | 0xFF |
| SLZ | 0xBF | 0xFF | 0xFF |
| SLV | 0x7F | 0xFF | 0xFF |
| SSZ | 0xFF | 0xF7 | 0xFF |
| SSV | 0xFF | 0xEF | 0xFF |
| SNB | 0xFF | 0xDF | 0xFF |
| SNA | 0xFF | 0xBF | 0xFF |
| SHB | 0xFF | 0x7F | 0xFF |
| SPFA | 0xFF | 0xFF | 0x07 |
| SPFB | 0xFF | 0xFF | 0x0B |
| SPFL | 0xFF | 0xFF | 0x0D |
| SPFR | 0xFF | 0xFF | 0x0E |
| SPBA | 0xFF | 0xFF | 0x17 |
| SPBB | 0xFF | 0xFF | 0x1B |
| SPBL | 0xFF | 0xFF | 0x1D |
| SPBR | 0xFF | 0xFF | 0x1E |
| default | 0xFF | 0xFF | 0xFF |

<a id="table-bytes"></a>
### BYTES

Dimensions: 11 rows × 9 columns

| NAME | BYTE | MIN | MAX | MINDEF | MAXDEF | A | B | DIV |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| POKO | 0x03 | 0x08 | 0xF8 | -1 | -2 | -20 | 5000 | 1000 |
| POSH | 0x04 | 0x08 | 0xF8 | -1 | -2 | -20 | 5000 | 1000 |
| POLN | 0x05 | 0x08 | 0xF8 | -1 | -2 | -20 | 5000 | 1000 |
| POOA | 0x06 | 0x08 | 0xF8 | -1 | -2 | -20 | 5000 | 1000 |
| POSN | 0x07 | 0x08 | 0xF8 | -1 | -2 | -20 | 5000 | 1000 |
| POSS | 0x08 | 0x08 | 0xF8 | -1 | -2 | -20 | 5000 | 1000 |
| POBH | 0x09 | 0x08 | 0xF8 | -1 | -2 | -20 | 5000 | 1000 |
| POBV | 0x0A | 0x08 | 0xF8 | -1 | -2 | -20 | 5000 | 1000 |
| POFH | 0x0B | 0x08 | 0xF8 | -1 | -2 | -20 | 5000 | 1000 |
| POFV | 0x0C | 0x08 | 0xF8 | -1 | -2 | -20 | 5000 | 1000 |
| UBAT | 0x0E | 0x00 | 0xFF |   |   | 718 | 0 | 10 |

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
