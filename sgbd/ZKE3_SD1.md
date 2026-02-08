# ZKE3_SD1.prg

- Jobs: [11](#jobs)
- Tables: [5](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | ZKE III: Schiebehebedachmodul E38, E39 |
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
- [IDENT](#job-ident) - Ident-Daten fuer SHD
- [HERSTELLDATEN_LESEN](#job-herstelldaten-lesen) - Auslesen der Herstelldaten
- [STATUS_DIGITAL_SHD](#job-status-digital-shd) - Status der Digitalsignale des SHD (Ein-/Ausgaenge) Der Wertebereich ist bei allen Results: Bereich: 0, wenn FALSE / 1, wenn TRUE
- [STATUS_ANALOG_SHD](#job-status-analog-shd) - Status der Analogsignale des SHD
- [STEUERN_DIGITAL_SHD](#job-steuern-digital-shd) - Ansteuern eines digitalen Ein- oder Ausgangs des SHD
- [STATUS_BYTES_SHD](#job-status-bytes-shd) - Status aller Signale des Peripheriemoduls SHD Signalart: BYTE-weise, d.h. ohne Interpretation
- [STATUS_SHD](#job-status-shd) - Status der SHD-Signale
- [SCHREIBEN_SHD_AW](#job-schreiben-shd-aw) - ACHTUNG: nur fuer E39/2 mit SHD-Software-Stand &lt; 5  !!! Umcodieren des SHD E39/2 wegen Antiwummerstellung
- [TESTEN_SHD_AW](#job-testen-shd-aw) - ACHTUNG: nur fuer E39/2 mit SHD-Software-Stand &lt; 5  !!! Testen der Daten des SHD E39/2 bzgl. Antiwummerstellung

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

Status der Digitalsignale des SHD (Ein-/Ausgaenge) Der Wertebereich ist bei allen Results: Bereich: 0, wenn FALSE / 1, wenn TRUE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_IE_UBLOW_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_IE_DMSHDZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_IE_DMSHDA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SSHDH_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SSHDZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SSHDA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_IE_INKRA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_IE_INKRB_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_PS_COE39_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_IFN_NRM_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_IA_ENIC2_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_IA_MSHDA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_IA_MSHDZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_IA_INKRV_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog-shd"></a>
### STATUS_ANALOG_SHD

Status der Analogsignale des SHD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SHDPOS_WERT | real | SHD-Position Bereich: ? |
| STAT_SHDPOS_EINH | string | Einheit: 'Milli-Meter' |
| STAT_UMOT_WERT | real | Spannung am SHD-Motor Bereich: 0 bis 18,3 [Volt] |
| STAT_UMOT_EINH | string | Einheit: 'Milli-Volt' |
| STAT_DMOT_WERT | real | Drehmoment am SHD-Motor Bereich: 0 bis 255 [1] |
| STAT_DMOT_EINH | string | Einheit: '1' |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-digital-shd"></a>
### STEUERN_DIGITAL_SHD

Ansteuern eines digitalen Ein- oder Ausgangs des SHD

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | gewuenschte Komponente table BITS_SHD NAME ART TEXT |
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
| STAT_DATEN | binary | 9 Bytes |
| _TEL_ANTWORT | binary |  |

<a id="job-status-shd"></a>
### STATUS_SHD

Status der SHD-Signale

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_E_SSHDH_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SSHDZ_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_E_SSHDA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_DMOT_WERT | long | Drehmoment am SHD-Motor Bereich: 0 bis 255 |
| STAT_DMOT_EINH | string | Einheit: '1' |
| _TEL_ANTWORT | binary |  |

<a id="job-schreiben-shd-aw"></a>
### SCHREIBEN_SHD_AW

ACHTUNG: nur fuer E39/2 mit SHD-Software-Stand &lt; 5  !!! Umcodieren des SHD E39/2 wegen Antiwummerstellung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-testen-shd-aw"></a>
### TESTEN_SHD_AW

ACHTUNG: nur fuer E39/2 mit SHD-Software-Stand &lt; 5  !!! Testen der Daten des SHD E39/2 bzgl. Antiwummerstellung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| WERT_POS_AUF | int | Wert an der Speicherzelle bzgl. 'Position auf' (low Byte) |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (69 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [BITS_SHD](#table-bits-shd) (15 × 6)

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

<a id="table-bits-shd"></a>
### BITS_SHD

Dimensions: 15 rows × 6 columns

| NAME | BYTE | MASK | VALUE | ART | TEXT |
| --- | --- | --- | --- | --- | --- |
| UBLOW | 1 | 0x01 | 0x01 | IE | Unterspannung am PM SHD |
| DMSHDZ | 1 | 0x04 | 0x04 | IE | interne Diagnoserueckfuehrung Motor SHD ZU |
| DMSHDA | 1 | 0x08 | 0x08 | IE | interne Diagnoserueckfuehrung Motor SHD AUF |
| SSHDH | 1 | 0x20 | 0x20 | E | Schalter SHD HEBEN |
| SSHDZ | 1 | 0x40 | 0x40 | E | Schalter SHD ZU |
| SSHDA | 1 | 0x80 | 0x80 | E | Schalter SHD AUF |
| INKRA | 2 | 0x01 | 0x01 | IE | Inkrementalgeber A |
| INKRB | 2 | 0x02 | 0x02 | IE | Inkrementalgeber B |
| COE39 | 2 | 0x04 | 0x04 | PS | Kodierung E39 (ueber P-Bus) |
| NRM | 2 | 0x80 | 0x80 | IFN | SHD Normiert |
| ENIC2 | 3 | 0x04 | 0x04 | IA | Enable Eingangs-IC |
| MSHDA | 3 | 0x20 | 0x20 | IA | internes Relais SHD AUF |
| MSHDZ | 3 | 0x40 | 0x40 | IA | internes Relais SHD ZU |
| INKRV | 3 | 0x80 | 0x80 | IA | Inkrementalgeber Versorgung |
| XY | XY | 0xXY | 0xXY | XY | nicht definiertes Signal |
