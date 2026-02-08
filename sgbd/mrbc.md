# mrbc.prg

- Jobs: [25](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Boardcomputer BC-DS2 |
| ORIGIN | I+ME Actia GmbH, Keck |
| REVISION | 1.021 |
| AUTHOR | I+ME Actia GmbH, Keck und BMW Motorrad, Kufer |
| COMMENT | N/A |
| PACKAGE | 1.52 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [GP_TESTCOM](#job-gp-testcom) - Kommunikation mit dem Steuergerät prüfen
- [IDENT](#job-ident) - Modus  : Default
- [GP_TEILENUMMER](#job-gp-teilenummer) - Lesen der BMW Teile-Nummer Byte 3-6
- [GP_HARDWARENUMMER](#job-gp-hardwarenummer) - Lesen der Hardware Nummer Byte 7
- [GP_CODIERINDEX](#job-gp-codierindex) - Codier Index lesen Byte 8
- [GP_DIAGNOSEINDEX](#job-gp-diagnoseindex) - Diagnose Index lesen Byte 9
- [GP_HERSTELLERDATUM_KW](#job-gp-herstellerdatum-kw) - Kalenderwoche Herstelldatum lesen Byte 10
- [GP_HERSTELLERDATUM_JAHR](#job-gp-herstellerdatum-jahr) - Herstelldatum Jahr lesen Byte 11
- [GP_LIEFERANTENNUMMER](#job-gp-lieferantennummer) - Lieferanten Nummer lesen Byte 12
- [GET_AUSSENTEMPERATUR](#job-get-aussentemperatur) - Außentemperatur lesen in Grad Celsius
- [GET_AUSSENTEMPERATUR_F](#job-get-aussentemperatur-f) - Außentemperatur lesen in Grad Fahrenheit
- [GET_RESET_TASTER](#job-get-reset-taster) - Status Reset Taster
- [GET_MODE_TASTER](#job-get-mode-taster) - Status Mode Taster
- [GET_FERNBEDIENUNGS_TASTER](#job-get-fernbedienungs-taster) - Status Mode Taster
- [SL_TANKINHALT](#job-sl-tankinhalt) - Tankinhalt aus dem Speicher lesen Wert in Milli Liter
- [SL_TANKINHALT_USGAL](#job-sl-tankinhalt-usgal) - Tankinhalt aus dem Speicher lesen Wert in US Galonen
- [SL_TANKINHALT_GBGAL](#job-sl-tankinhalt-gbgal) - Tankinhalt aus dem Speicher lesen Wert in GB Galonen
- [SL_KZAHL](#job-sl-kzahl) - Wert K Zahl lesen k_bc wert, Eeeprom Adresse 0x10000
- [SL_EINSPRITZZEIT](#job-sl-einspritzzeit) - Einspritzzeit lesen s_bc wert, Eeeprom Adresse 0x10002
- [SP_SEGMENTE_ZUSTAND](#job-sp-segmente-zustand) - Ansteuerung Segmente
- [SP_HELLIGKEIT_WERT](#job-sp-helligkeit-wert) - Ansteuerung Helligkeit
- [SP_RESET](#job-sp-reset) - Reset Steuergerät
- [SP_DIAGNOSE_ENDE](#job-sp-diagnose-ende) - Diagnose beenden

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

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn OK 0 wenn nicht OK |

<a id="job-gp-testcom"></a>
### GP_TESTCOM

Kommunikation mit dem Steuergerät prüfen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| TESTCOM | int | 1 - Kommunikation funktioniert 0 - Kommunikation funktioniert nicht |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-ident"></a>
### IDENT

Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| VARIANTE_IND | string | Name der SGBD, immer MRBC |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-gp-teilenummer"></a>
### GP_TEILENUMMER

Lesen der BMW Teile-Nummer Byte 3-6

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| TEILENUMMER_WERT | unsigned long | BMW Teile-Nummer |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-gp-hardwarenummer"></a>
### GP_HARDWARENUMMER

Lesen der Hardware Nummer Byte 7

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| HARDWARENUMMER_WERT | int | Hardware Nummer |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-gp-codierindex"></a>
### GP_CODIERINDEX

Codier Index lesen Byte 8

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| CODIERINDEX_WERT | int | Codier Index |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-gp-diagnoseindex"></a>
### GP_DIAGNOSEINDEX

Diagnose Index lesen Byte 9

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| DIAGNOSEINDEX_WERT | int | Diagnose Index |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-gp-herstellerdatum-kw"></a>
### GP_HERSTELLERDATUM_KW

Kalenderwoche Herstelldatum lesen Byte 10

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| HERSTELLERDATUM_KW_WERT | int | Herstelldatum Kalenderwoche |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-gp-herstellerdatum-jahr"></a>
### GP_HERSTELLERDATUM_JAHR

Herstelldatum Jahr lesen Byte 11

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| HERSTELLERDATUM_JAHR_WERT | int | Herstelldatum Jahr |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-gp-lieferantennummer"></a>
### GP_LIEFERANTENNUMMER

Lieferanten Nummer lesen Byte 12

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| LIEFERANTENNUMMER_WERT | int | Lieferanten-Nummer |
| STAT_WERT_TEXT | string | Text Zulieferer |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-get-aussentemperatur"></a>
### GET_AUSSENTEMPERATUR

Außentemperatur lesen in Grad Celsius

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| AUSSENTEMPERATUR_WERT | real | Aussentemperatur |
| AUSSENTEMPERATUR_EINH | string | Einheit °C |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-get-aussentemperatur-f"></a>
### GET_AUSSENTEMPERATUR_F

Außentemperatur lesen in Grad Fahrenheit

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| AUSSENTEMPERATUR_WERT | real | Aussentemperatur |
| AUSSENTEMPERATUR_EINH | string | Einheit °F |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-get-reset-taster"></a>
### GET_RESET_TASTER

Status Reset Taster

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STATUS_WERT | int | Werte: 0 - ein, 1 - aus |
| STATUS_TASTER_TEXT | string | Werte: Ein, Aus |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-get-mode-taster"></a>
### GET_MODE_TASTER

Status Mode Taster

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STATUS_WERT | int | Werte: 0 - ein, 1 - aus |
| STATUS_TASTER_TEXT | string | Werte: Ein, Aus |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-get-fernbedienungs-taster"></a>
### GET_FERNBEDIENUNGS_TASTER

Status Mode Taster

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STATUS_WERT | int | Werte: 0 - ein, 1 - aus |
| STATUS_TASTER_TEXT | string | Werte: Ein, Aus |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-sl-tankinhalt"></a>
### SL_TANKINHALT

Tankinhalt aus dem Speicher lesen Wert in Milli Liter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| TANKINHALT_WERT | real | Tankinhalt |
| TANKINHALT_EINH | string | Einheit in Milli Liter |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-sl-tankinhalt-usgal"></a>
### SL_TANKINHALT_USGAL

Tankinhalt aus dem Speicher lesen Wert in US Galonen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| TANKINHALT_WERT | real | Tankinhalt |
| TANKINHALT_EINH | string | Einheit in US Galonen |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-sl-tankinhalt-gbgal"></a>
### SL_TANKINHALT_GBGAL

Tankinhalt aus dem Speicher lesen Wert in GB Galonen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| TANKINHALT_WERT | real | Tankinhalt |
| TANKINHALT_EINH | string | Einheit in GB Galonen |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-sl-kzahl"></a>
### SL_KZAHL

Wert K Zahl lesen k_bc wert, Eeeprom Adresse 0x10000

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| KZAHL_SL | int | k-Zahl |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-sl-einspritzzeit"></a>
### SL_EINSPRITZZEIT

Einspritzzeit lesen s_bc wert, Eeeprom Adresse 0x10002

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| EINSPRITZZEIT_WERT | int | Einspritzzeit |
| EINSPRITZZEIT_EINH | string | Einheit Milli Sekunden |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-sp-segmente-zustand"></a>
### SP_SEGMENTE_ZUSTAND

Ansteuerung Segmente

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ONOFF | int | 1 - alle Segmente ein 0 - alle Segmente aus 2 - Reset |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-sp-helligkeit-wert"></a>
### SP_HELLIGKEIT_WERT

Ansteuerung Helligkeit

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VALUE | int | Wertebereich Value 10..190 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-sp-reset"></a>
### SP_RESET

Reset Steuergerät

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-sp-diagnose-ende"></a>
### SP_DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (81 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (3 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 13 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0x11 | AIF_NICHT_PROGRAMMIERT |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xB2 | ERROR_ECU_NUMBER |
| 0xFF | ERROR_ECU_NACK |
| 0x01 | ERROR_ECU_FUNCTION_ANSTEUERBEDINGUNG_NICHT_ERFUELLT |
| 0x02 | ERROR_ECU_FUNCTION_UEBERGABEPARAMETER_UNGUELTIG |
| 0x05 | ERROR_ECU_FUNCTION NOCH NICHT GESTARTET |
| 0x06 | FUNCTION BEENDET; DATEN GUELTIG |
| 0x55 | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 81 rows × 2 columns

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
| 0x18 | Continental Teves |
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
| 0x69 | Magna-Donelly |
| 0x70 | Koyo Steering Europe |
| 0x71 | NSI B.V |
| 0x72 | ASIN AWCO.LTD |
| 0x73 | Shorlock |
| 0x74 | Schrader |
| 0x75 | BERU Electronics GmbH |
| 0x76 | CEL |
| 0x77 | Audio Mobil |
| 0x78 | rd electronic |
| 0x79 | iSYS RTS GmbH |
| 0x80 | Westfalia Automotive GmbH |
| 0xFF | unbekannter Hersteller |

<a id="table-digitalargument"></a>
### DIGITALARGUMENT

Dimensions: 3 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | AUS |
| 0x01 | EIN |
| 0xFF | UNBEKANNT |
