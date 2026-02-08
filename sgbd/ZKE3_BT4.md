# ZKE3_BT4.prg

- Jobs: [8](#jobs)
- Tables: [5](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | ZKE III: Beifahrertuermodul E53 |
| ORIGIN | BMW TI-430 Gerd Huber |
| REVISION | 1.00 |
| AUTHOR | BMW TI-433 Gerd Huber |
| COMMENT | Ansteuern nur bei entsichertem Fahrzeug! |
| PACKAGE | 1.00 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Default init job
- [IDENT](#job-ident) - Ident-Daten fuer GM III
- [HERSTELLDATEN_LESEN](#job-herstelldaten-lesen) - Auslesen der Herstelldaten
- [STATUS_DIGITAL_BT](#job-status-digital-bt) - Status der Digitalsignale der BT E53 (Ein-/Ausgaenge)
- [STATUS_ANALOG_BT](#job-status-analog-bt) - Status der Analogsignale der BT E53
- [STEUERN_DIGITAL_BT](#job-steuern-digital-bt) - Ansteuern eines digitalen Ein- oder Ausgangs der BT
- [STATUS_BYTES_BT](#job-status-bytes-bt) - Status aller Signale des Peripheriemoduls BT Signalart: BYTE-weise, d.h. ohne Interpretation

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

Ident-Daten fuer GM III

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

<a id="job-status-digital-bt"></a>
### STATUS_DIGITAL_BT

Status der Digitalsignale der BT E53 (Ein-/Ausgaenge)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_E_SSBA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_TKBT_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFFA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFFZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFFT_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFFHA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFFHZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFFHT_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFBA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFBZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFBT_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFBHA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFBHZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SFBHT_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SSPO_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SSPU_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SSPR_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SSPL_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SSBT_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SSPE_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_RFHBZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_RFHBA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_DAY_MODE_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_LED_ON_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_BREMS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MFSE_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MSFA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_SP_AB_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_SP_AUF_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_SP_RE_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_SP_LI_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_SP_HZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MER_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MVR_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MZS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_MSVR_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_BRKZS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_A_U2OFF_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| _TEL_ANTWORT | binary |  |

<a id="job-status-analog-bt"></a>
### STATUS_ANALOG_BT

Status der Analogsignale der BT E53

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_USPFH_WERT | real | Spannung am Spiegelpotentiometer BT horizontal Bereich: 0 bis 5 |
| STAT_USPFH_EINH | string | Einheit: 'Volt' |
| STAT_USPFV_WERT | real | Spannung am Spiegelpotentiometer BT vertikal Bereich: 0 bis 5 |
| STAT_USPFV_EINH | string | Einheit: 'Volt' |
| STAT_UEKSF_WERT | real | Spannung an der Einklemmschutzleiste BT Bereich: 0 bis 5 |
| STAT_UEKSF_EINH | string | Einheit: 'Volt' |
| STAT_IFHBT_WERT | real | momentaner Strom im FH-Antrieb BT Bereich: 0 bis 49,0 |
| STAT_IFHBT_EINH | string | Einheit: 'Ampere' |
| STAT_IBTMAX_WERT | real | maximaler Strom im FH-Antrieb BT Bereich: 0 bis 49,0 |
| STAT_IBTMAX_EINH | string | Einheit: 'Ampere' |
| STAT_U30_WERT | real | Spannung an Klemme 30 Bereich: 0 bis 28,5 |
| STAT_U30_EINH | string | Einheit: 'Volt' |
| STAT_UFHBTA_WERT | real | Spannung am Fensterheber BT AUF Bereich: 0 bis 55 |
| STAT_UFHBTA_EINH | string | Einheit: 'Volt' |
| STAT_UFHBTZ_WERT | real | Spannung am Fensterheber BT ZU Bereich: 0 bis 55 |
| STAT_UFHBTZ_EINH | string | Einheit: 'Volt' |
| STAT_LEDKISI_WERT | real | PWM-Signal LED Kindersicherung Bereich: 0 bis 98 |
| STAT_LEDKISI_EINH | string | Einheit: '%' |
| _TEL_ANTWORT | binary |  |

<a id="job-steuern-digital-bt"></a>
### STEUERN_DIGITAL_BT

Ansteuern eines digitalen Ein- oder Ausgangs der BT

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | gewuenschte Komponente table BITS_BT NAME ART TEXT |
| EIN | int | '1', wenn einschalten / '0', wenn ausschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-status-bytes-bt"></a>
### STATUS_BYTES_BT

Status aller Signale des Peripheriemoduls BT Signalart: BYTE-weise, d.h. ohne Interpretation

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_DATEN | binary | 30 Bytes |
| _TEL_ANTWORT | binary |  |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (69 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [BITS_BT](#table-bits-bt) (39 × 6)

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

Dimensions: 69 rows × 2 columns

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
| 0x62 | AB-Elektronik |
| 0x63 | Siemens VDO Borg |
| 0x64 | Hirschmann Electronics |
| 0x65 | Hoerbiger Electronics |
| 0x66 | Thyssen Krupp Automotive Mechatronics |
| 0x67 | Gentex GmbH |
| 0x68 | Atena GmbH |
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

<a id="table-digitalargument"></a>
### DIGITALARGUMENT

Dimensions: 16 rows × 2 columns

| TEXT | WERT |
| --- | --- |
| ein | 1 |
| aus | 0 |
| ja | 1 |
| nein | 0 |
| auf | 1 |
| ab | 0 |
| yes | 1 |
| no | 0 |
| on | 1 |
| off | 0 |
| up | 1 |
| down | 0 |
| true | 1 |
| false | 0 |
| 1 | 1 |
| 0 | 0 |

<a id="table-bits-bt"></a>
### BITS_BT

Dimensions: 39 rows × 6 columns

| NAME | BYTE | MASK | VALUE | ART | TEXT |
| --- | --- | --- | --- | --- | --- |
| SSBA | 1 | 0x02 | 0x02 | E | Schalter Spiegel Beifahrer in Fahr- oder Parkposition |
| TKBT | 1 | 0x04 | 0x04 | E | Tuerkontakt BT |
| SFFA | 4 | 0x01 | 0x01 | E | Schalter FH Fahrer auf |
| SFFZ | 4 | 0x02 | 0x02 | E | Schalter FH Fahrer zu |
| SFFT | 4 | 0x04 | 0x04 | E | Schalter FH Fahrer Tipp |
| SFFHA | 4 | 0x08 | 0x08 | E | Schalter FH Fahrer Hinten auf |
| SFFHZ | 4 | 0x10 | 0x10 | E | Schalter FH Fahrer Hinten zu |
| SFFHT | 4 | 0x20 | 0x20 | E | Schalter FH Fahrer Hinten Tipp |
| SFBA | 5 | 0x01 | 0x01 | E | Schalter FH Beifahrer auf |
| SFBZ | 5 | 0x02 | 0x02 | E | Schalter FH Beifahrer zu |
| SFBT | 5 | 0x04 | 0x04 | E | Schalter FH Beifahrer Tipp |
| SFBHA | 5 | 0x08 | 0x08 | E | Schalter FH Beifahrer Hinten auf |
| SFBHZ | 5 | 0x10 | 0x10 | E | Schalter FH Beifahrer Hinten zu |
| SFBHT | 5 | 0x20 | 0x20 | E | Schalter FH Beifahrer Hinten Tipp |
| SSPO | 6 | 0x01 | 0x01 | E | Schalter Spiegel oben |
| SSPU | 6 | 0x02 | 0x02 | E | Schalter Spiegel unten |
| SSPR | 6 | 0x04 | 0x04 | E | Schalter Spiegel rechts |
| SSPL | 6 | 0x08 | 0x08 | E | Schalter Spiegel links |
| SSBT | 6 | 0x10 | 0x10 | E | Schalter Spiegel Beifahrer Verstellen |
| SSPE | 6 | 0x20 | 0x20 | E | Schalter Spiegel Einklappen |
| RFHBZ | 7 | 0x01 | 0x01 | A | Relais Fensterheber Beifahrertuer zu |
| RFHBA | 7 | 0x02 | 0x02 | A | Relais Fensterheber Beifahrertuer auf |
| DAY_MODE | 7 | 0x10 | 0x10 | A | LED Mode (Tag oder Nacht) |
| LED_ON | 7 | 0x20 | 0x20 | A | LED ein |
| BREMS | 8 | 0x01 | 0x01 | A | Motoren Spiegel bremsen |
| MFSE | 8 | 0x02 | 0x02 | A | Motor Spiegel Ausklappen |
| MSFA | 8 | 0x04 | 0x04 | A | Motor Spiegel Einklappen |
| SP_AB | 8 | 0x08 | 0x08 | A | Spiegel abwaerts |
| SP_AUF | 8 | 0x10 | 0x10 | A | Spiegel aufwaerts |
| SP_RE | 8 | 0x20 | 0x20 | A | Spiegel rechts |
| SP_LI | 8 | 0x40 | 0x40 | A | Spiegel links |
| SP_HZ | 8 | 0x80 | 0x80 | A | Spiegel heizen |
| MER | 9 | 0x01 | 0x01 | A | Motor ZV entriegeln |
| MVR | 9 | 0x02 | 0x02 | A | Motor ZV verriegeln |
| MZS | 9 | 0x04 | 0x04 | A | Motor ZV sichern |
| MSVR | 9 | 0x08 | 0x08 | A | Motor ZV sichern in verriegelt |
| BRKZS | 9 | 0x10 | 0x10 | A | Bremsen ZV |
| U2OFF | 9 | 0x20 | 0x20 | A | Versorgungsspannung U2 |
| XY | XY | 0xXY | 0xXY | XY | nicht definiertes Signal |
