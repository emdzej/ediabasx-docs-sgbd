# ZKE3_SD2.prg

- Jobs: [12](#jobs)
- Tables: [4](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | ZKE III: Schiebehebedachmodul E39 ab 03/98 und E53 |
| ORIGIN | BMW TI-430 Gerd Huber |
| REVISION | 1.0 |
| AUTHOR | BMW TI-430 Gerd Huber |
| COMMENT | Ansteuern nur bei entsichertem Fahrzeug! |
| PACKAGE | 0.07 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Default init job
- [IDENT](#job-ident) - Ident-Daten fuer SHD
- [HERSTELLDATEN_LESEN](#job-herstelldaten-lesen) - Auslesen der Herstelldaten
- [STATUS_DIGITAL_SHD](#job-status-digital-shd) - Status der Digitalsignale des neuen SHD fuer E39 ab 03/98 (Ein-/Ausgaenge) Der Wertebereich ist bei allen Results: Bereich: 0, wenn FALSE / 1, wenn TRUE
- [STATUS_ANALOG_SHD](#job-status-analog-shd) - Status der Analogsignale des neuen SHD fuer E39 ab 03/98
- [STEUERN_DIGITAL_SHD](#job-steuern-digital-shd) - Ansteuern eines digitalen Ein- oder Ausgangs des neuen SHD fuer E39 ab 03/98
- [STATUS_BYTES_SHD](#job-status-bytes-shd) - Status aller Signale des Peripheriemoduls SHD Signalart: BYTE-weise, d.h. ohne Interpretation
- [STEUERN_START_AUTOINIT](#job-steuern-start-autoinit) - Autoinit starten (SHD E39 ab 03/98)
- [STEUERN_PRUEFMODUS_FREIGEBEN](#job-steuern-pruefmodus-freigeben) - Pruefmodus freigeben (SHD E39 ab 03/98)
- [SETZEN_E39_2_GLAS_FIXIERT](#job-setzen-e39-2-glas-fixiert) - fixiert die Codierung auf E39/2 Glas
- [SETZEN_SONDERFAHRZEUG_NICHT_FIXIERT](#job-setzen-sonderfahrzeug-nicht-fixiert) - setzt die Codierung auf Sonderfahrzeug loescht Fixierung

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
### INITIALISIERUNG

Default init job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 if done |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer SHD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Text table Lieferanten LIEF_TEXT |
| ID_SW_NR | int | Softwarenummer |
| _TEL_ANTWORT | binary |  |

<a id="job-herstelldaten-lesen"></a>
### HERSTELLDATEN_LESEN

Auslesen der Herstelldaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |
| BYTE4 | int | kann beliebig verwendet werden |
| _TEL_ANTWORT | binary |  |

<a id="job-status-digital-shd"></a>
### STATUS_DIGITAL_SHD

Status der Digitalsignale des neuen SHD fuer E39 ab 03/98 (Ein-/Ausgaenge) Der Wertebereich ist bei allen Results: Bereich: 0, wenn FALSE / 1, wenn TRUE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KEY_HEB | int | Taste Heben |
| STAT_KEY_AUF | int | Taste Oeffnen |
| STAT_KEY_ZU | int | Taste Schliessen |
| STAT_SHDK | int | GM-Signale 1: Komfortfunktion aktiv |
| STAT_SHDKS | int | GM-Signale 1: 0: Komfortoeffnen, 1: Komfortschliessen |
| STAT_SHDI | int | GM-Signale 2: SHD inaktiv |
| STAT_REV_GB | int | GM-Signale 2: 0: 1 Sekunde Reversieren, 1: bis Einklemmanfang |
| STAT_SHDTZI | int | GM-Signale 2: Tipp Zu inaktiv |
| STAT_SHDTAI | int | GM-Signale 2: Tipp Auf inaktiv |
| STAT_PANIK_MODE | int | Reserve ? |
| STAT_NORMIERT | int | Dach ist normiert |
| STAT_TIPP_HEB | int | Tippbetrieb Heben freigegeben |
| STAT_TIPP_AUS_HEB | int | Tippbetrieb Auf, Zu aus Hebebereich freigegeben |
| STAT_KO_HEB | int | Komfortoeffnen nach Heben |
| STAT_SAERO_MODE | int | Schliessen immer aus der gleichen Richtung |
| STAT_TAKT_ENA | int | Taktung freigegeben |
| STAT_SANFT_ENA | int | Sanftanlauf |
| STAT_MOTOR_EIN | int | Motor Einschalten |
| STAT_VOR | int | 0: Rueckwaertsfahrt, 1: Vorwaertsfahrt |
| STAT_QSHDZ | int | SHD-Signale: 0: SHD nicht geschlossen, 1: Dach geschlossen |
| STAT_THW_IDLE | int | Motor ist ausgekuehlt (von Thermowaechter) |
| STAT_SKB_FA | int | SKB ist aktiviert |
| STAT_KH_GOOD | int | Kennlinie Heben okay (ab 2. Abfrage aktuell) |
| STAT_KS_GOOD | int | Kennlinie Schieben okay (ab 2. Abfrage aktuell) |
| STAT_BUSAI_LOCK | int | Autoinit ueber Bus gesperrt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog-shd"></a>
### STATUS_ANALOG_SHD

Status der Analogsignale des neuen SHD fuer E39 ab 03/98

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_AKT_POS_WERT | real | aktuelle Dachposition Bereich: ? .. bis .. [.] |
| STAT_AKT_POS_EINH | string | Einheit: Milli-Meter ? |
| STAT_TAKT_VAL_WERT | real | PLM-Wert fuer Taktung Bereich: ? .. bis .. [.] |
| STAT_TAKT_VAL_EINH | string | Einheit: - |
| STAT_T_MOT_WERT | real | Motorankertemperatur Bereich: ? .. bis .. [.] |
| STAT_T_MOT_EINH | string | Einheit: Grad Celsius |
| STAT_U_IST_WERT | real | Spannung am Motor Bereich: ? .. bis .. [.] |
| STAT_U_IST_EINH | string | Einheit: Volt |
| STAT_U_BATT_WERT | real | Batteriespannung (Klemme 30) Bereich: ? .. bis .. [.] |
| STAT_U_BATT_EINH | string | Einheit: Volt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-digital-shd"></a>
### STEUERN_DIGITAL_SHD

Ansteuern eines digitalen Ein- oder Ausgangs des neuen SHD fuer E39 ab 03/98

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | gewuenschte Komponente table BITS_SHD NAME TEXT |
| EIN | int | '1', wenn einschalten / '0', wenn ausschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bytes-shd"></a>
### STATUS_BYTES_SHD

Status aller Signale des Peripheriemoduls SHD Signalart: BYTE-weise, d.h. ohne Interpretation

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_DATEN | binary | 10 Bytes |
| _TEL_ANTWORT | binary |  |

<a id="job-steuern-start-autoinit"></a>
### STEUERN_START_AUTOINIT

Autoinit starten (SHD E39 ab 03/98)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-steuern-pruefmodus-freigeben"></a>
### STEUERN_PRUEFMODUS_FREIGEBEN

Pruefmodus freigeben (SHD E39 ab 03/98)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-setzen-e39-2-glas-fixiert"></a>
### SETZEN_E39_2_GLAS_FIXIERT

fixiert die Codierung auf E39/2 Glas

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AUFTRAG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-setzen-sonderfahrzeug-nicht-fixiert"></a>
### SETZEN_SONDERFAHRZEUG_NICHT_FIXIERT

setzt die Codierung auf Sonderfahrzeug loescht Fixierung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AUFTRAG | binary |  |
| _TEL_ANTWORT | binary |  |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (62 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [BITS_SHD](#table-bits-shd) (5 × 5)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 13 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xB2 | ERROR_ECU_NUMBER |
| 0xFF | ERROR_ECU_NACK |
| ?10? | ERROR_ARGUMENT |
| ?20? | ERROR_FEHLERANZAHL |
| ?70? | ERROR_NUMBER_ARGUMENT |
| ?71? | ERROR_RANGE_ARGUMENT |
| ?72? | ERROR_VERIFY |
| 0x?? | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 62 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x01 | Reinshagen =&gt; Delphi |
| 0x02 | Kostal |
| 0x03 | Hella |
| 0x04 | Siemens |
| 0x05 | Eaton |
| 0x06 | UTA |
| 0x07 | Helbako |
| 0x08 | Bosch |
| 0x09 | Loewe =&gt; Lear |
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
| 0x28 | DODUCO =&gt; BERU |
| 0x29 | DENSO |
| 0x30 | NEC |
| 0x31 | DASA |
| 0x32 | Pioneer |
| 0x33 | Jatco |
| 0x34 | Fuba |
| 0x35 | UK-NSI |
| 0x36 | AABG |
| 0x37 | Dunlop |
| 0x38 | Sachs |
| 0x39 | ITT |
| 0x40 | FTE |
| 0x41 | Megamos |
| 0x42 | TRW |
| 0x43 | Wabco |
| 0x44 | ISAD Electronic Systems |
| 0x45 | HEC (Hella Electronics Corporation) |
| 0x46 | Gemel |
| 0x47 | ZF |
| 0x48 | GMPT |
| 0x49 | Harman Kardon |
| 0x50 | Remes |
| 0x51 | ZF Lenksysteme |
| 0x52 | Magneti Marelli |
| 0x53 | Borg Instruments |
| 0x54 | GETRAG |
| 0x55 | BHTC (Behr Hella Thermocontrol) |
| 0x56 | Siemens VDO Automotive |
| 0x57 | Visteon |
| 0x58 | Autoliv |
| 0x59 | Haberl |
| 0x60 | Magna Steyr |
| 0x61 | Marquardt |
| 0xFF | unbekannter Hersteller |

<a id="table-roverpartnumprefix"></a>
### ROVERPARTNUMPREFIX

Dimensions: 21 rows × 2 columns

| ROVER_NR | PREFIX |
| --- | --- |
| 0xA0 | AMR |
| 0xA1 | HHF |
| 0xA2 | JFC |
| 0xA3 | MKC |
| 0xA4 | SCB |
| 0xA5 | SRB |
| 0xA6 | XQC |
| 0xA7 | XQD |
| 0xA8 | XQE |
| 0xA9 | XVD |
| 0xAA | YAC |
| 0xAB | YDB |
| 0xAC | YFC |
| 0xAD | YUB |
| 0xAE | YWC |
| 0xAF | YWQ |
| 0xB0 | EGQ |
| 0xB1 | YIB |
| 0xB2 | YIC |
| 0xB3 | YIE |
| 0xXY | ??? |

<a id="table-bits-shd"></a>
### BITS_SHD

Dimensions: 5 rows × 5 columns

| NAME | BYTE | MASK | VALUE | TEXT |
| --- | --- | --- | --- | --- |
| KEY_HEB | 1 | 0x01 | 0x01 | Taste Heben |
| KEY_AUF | 1 | 0x02 | 0x02 | Taste Oeffnen |
| KEY_ZU | 1 | 0x04 | 0x04 | Taste Schliessen |
| SHDI | 2 | 0x04 | 0x04 | GM-Signale 2: SHD inaktiv |
| XY | XY | 0xXY | 0xXY | nicht definiertes Signal |
