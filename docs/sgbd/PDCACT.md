# PDCACT.prg

- Jobs: [22](#jobs)
- Tables: [7](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | PDCACT |
| ORIGIN | BMW TI-430 Mueller |
| REVISION | 1.09 |
| AUTHOR | BMW TI-433 Spoljarec, BMW TI-431 Robert Kuessel, BMW TI-430 Marcus Mueller, BMW TI-431 Lothar Dennert |
| COMMENT | Park Distance Control E38 E39 E46 E53 R50 |
| PACKAGE | 1.02 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [IDENT](#job-ident) - Identdaten
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer PDC
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen bedingtes High-Konzept nach Lastenheft Codierung/Diagnose Die Fehlerspeichercodes sind willkuerlich vergeben Fehler stehen immer an der gleichen Stelle
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen des internen Speichers
- [COD_LESEN_VARIANTE](#job-cod-lesen-variante) - Auslesen der Codiervariante der PDC aktiv
- [COD_LESEN_SCHWELLE](#job-cod-lesen-schwelle) - Auslesen der codierten Schwellwerte der PDC aktiv
- [COD_LESEN_CHECKSUM](#job-cod-lesen-checksum) - Auslesen der Codierchecksummen
- [STATUS_IO_LESEN](#job-status-io-lesen) - Status der I/O Ports lesen
- [STEUERN_IO_STATUS](#job-steuern-io-status) - Ansteuern von den I/O Stati
- [STATUS_AUSSCHWINGZEIT_LESEN](#job-status-ausschwingzeit-lesen) - AUSSCHWINGZEIT lesen
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels
- [STATUS_WEG_V_MODE_LESEN](#job-status-weg-v-mode-lesen) - Status des Steuergeraets lesen
- [STATUS_MESSWERTE_LESEN](#job-status-messwerte-lesen) - Messwerte direkt und indirekt lesen
- [DIAGNOSE_WEITER](#job-diagnose-weiter) - Diagnose aufrechterhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [C_FG_LESEN](#job-c-fg-lesen) - Auslesen des Pruefstempels und Interpretation als FG-Nummer
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Beschreiben des Pruefstempels mit der FG-Nummer
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren

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

<a id="job-ident"></a>
### IDENT

Identdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Nummer |
| ID_SW_NR | int | Softwarenummer |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Init-Job fuer PDC

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen bedingtes High-Konzept nach Lastenheft Codierung/Diagnose Die Fehlerspeichercodes sind willkuerlich vergeben Fehler stehen immer an der gleichen Stelle

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
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
| F_ART5_NR | int | Index der 5. Fehlerart |
| F_ART5_TEXT | string | 5. Fehlerart als Text |
| F_ART6_NR | int | Index der 6. Fehlerart |
| F_ART6_TEXT | string | 6. Fehlerart als Text |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Lesen des internen Speichers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | long |  |
| SEGMENT | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-cod-lesen-variante"></a>
### COD_LESEN_VARIANTE

Auslesen der Codiervariante der PDC aktiv

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| COD_DATEN | string | 23 Codierbytes |
| COD_ANZAHL_WANDLER | int | 4 oder 8 |
| COD_TONGEBER_HINTEN | string | BC-GONG oder Lautsprecher |
| COD_TONGEBER_VORNE | string | BC-GONG oder Lautsprecher |
| COD_EIN_TONGEBER | int | 0 oder 1 |
| COD_PARKHILFESCHALTER | int | 0 oder 1 |
| COD_RUECKFAHRGONG | int | 0 oder 1 |
| COD_GETRIEBE | string | Schaltgetriebe oder Automatikgetriebe |
| COD_PDC_AKTIV_KL15 | int | 0 oder 1 |
| COD_DEAKTIVIERUNG | string | Rueckwaertsgang oder Weg/Geschwindigkeit |
| COD_EINSCHALTMELDUNG | string | keine / bei erstem aktivieren / bei jedem aktivieren |
| COD_ABSCHALTMELDUNG | int | 0 oder 1 |
| COD_TASTERMELDUNG | int | 0 oder 1 |
| COD_NOTFUNKTION | int | 0 oder 1 |
| COD_AKUSTIKKONZEPT | int | 0 oder 1 |
| COD_ABSTAND_WANDLER_HINTEN_ECKEN | int | 0 - 255 cm |
| COD_ABSTAND_WANDLER_HINTEN_MITTE | int | 0 - 255 cm |
| COD_ABSTAND_WANDLER_VORNE_ECKEN | int | 0 - 255 cm |
| COD_ABSTAND_WANDLER_VORNE_MITTE | int | 0 - 255 cm |
| COD_MESSBEREICH_HINTEN_ECKEN | int | 0 - 180 cm |
| COD_MESSBEREICH_HINTEN_MITTE | int | 0 - 180 cm |
| COD_MESSBEREICH_VORNE_ECKEN | int | 0 - 180 cm |
| COD_MESSBEREICH_VORNE_MITTE | int | 0 - 180 cm |
| COD_OFFSET_HINTEN_ECKEN | int | 0 - 60 cm |
| COD_OFFSET_HINTEN_MITTE | int | 0 - 60 cm |
| COD_OFFSET_VORNE_ECKEN | int | 0 - 60 cm |
| COD_OFFSET_VORNE_MITTE | int | 0 - 60 cm |
| COD_DAUERTONBEREICH_HINTEN | int | 0 - 255 cm |
| COD_DAUERTONBEREICH_VORNE | int | 0 - 255 cm |
| COD_LAUTSTAERKE_HINTEN | int | 0 - 7 |
| COD_LAUTSTAERKE_VORNE | int | 0 - 7 |
| COD_EINSCHALTGESCHWINDIGKEIT | int | 0 - 27 km/h |
| COD_ABSCHALTGESCHWINDIGKEIT | int | 3 - 30 km/h |
| COD_ABSCHALTWEG | int | 0 - 255 m |
| COD_WEGKENNZAHL | int | 0 - 8160 Imp/sek (Byte * 32) |
| COD_VERZOEGERUNG_RUECKFAHRGONG | real | 0 - 25,5 sek (Byte * 0,1) |

<a id="job-cod-lesen-schwelle"></a>
### COD_LESEN_SCHWELLE

Auslesen der codierten Schwellwerte der PDC aktiv

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODIERBLOCK | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| COD_DATEN | string | 13 Codierbytes |
| COD_SCHWELLE_15MS | int | Schwellenwert ab 1,5 ms |
| COD_SCHWELLE_20MS | int | Schwellenwert ab 2,0 ms |
| COD_SCHWELLE_25MS | int | Schwellenwert ab 2,5 ms |
| COD_SCHWELLE_30MS | int | Schwellenwert ab 3,0 ms |
| COD_SCHWELLE_35MS | int | Schwellenwert ab 3,5 ms |
| COD_SCHWELLE_40MS | int | Schwellenwert ab 4,0 ms |
| COD_SCHWELLE_45MS | int | Schwellenwert ab 4,5 ms |
| COD_SCHWELLE_50MS | int | Schwellenwert ab 5 ms |
| COD_SCHWELLE_60MS | int | Schwellenwert ab 6 ms |
| COD_SCHWELLE_70MS | int | Schwellenwert ab 7 ms |
| COD_SCHWELLE_80MS | int | Schwellenwert ab 8 ms |
| COD_SCHWELLE_90MS | int | Schwellenwert ab 9 ms |
| COD_FLAGS | int |  |

<a id="job-cod-lesen-checksum"></a>
### COD_LESEN_CHECKSUM

Auslesen der Codierchecksummen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| COD_CHKSUM_VARIANTE | int |  |
| COD_CHKSUM_H_ECKEN | int |  |
| COD_CHKSUM_H_MITTE | int |  |
| COD_CHKSUM_V_ECKEN | int |  |
| COD_CHKSUM_V_MITTE | int |  |

<a id="job-status-io-lesen"></a>
### STATUS_IO_LESEN

Status der I/O Ports lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_PORT_A | int | Byte des Ports A |
| STAT_PORT_B | int | Byte des Ports B |
| STAT_PORT_C | int | Byte des Ports C |
| STAT_PORT_E | int | Byte des Ports E |
| STAT_TASTER | int |  |
| STAT_ANHAENGER_JA | int | 1: Anhaenger vorhanden |
| STAT_RGANG_EIN | int | 1: Rueckwaertsgang eingelegt |
| STAT_DIAG_TON_HINTEN | int |  |
| STAT_SPG_WANDLER | int |  |
| STAT_DIAG_TON_VORNE | int |  |
| STAT_DIAG_FUNKTIONSANZEIGE | int |  |
| STAT_KLEMME_15 | int |  |

<a id="job-steuern-io-status"></a>
### STEUERN_IO_STATUS

Ansteuern von den I/O Stati

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | Diagnosemode, Tongeber, Kontrollsignal, System steuern siehe table IO_STATUS |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-status-ausschwingzeit-lesen"></a>
### STATUS_AUSSCHWINGZEIT_LESEN

AUSSCHWINGZEIT lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_AUSSCHWING_T_EINH | string | Einheit Ausschwingzeit usec |
| STAT_AUSSCHWING_T_HL_WERT | int | Ausschwingzeit hinten links |
| STAT_AUSSCHWING_T_HR_WERT | int | Ausschwingzeit hinten rechts |
| STAT_AUSSCHWING_T_HML_WERT | int | Ausschwingzeit hinten mitte links |
| STAT_AUSSCHWING_T_HMR_WERT | int | Ausschwingzeit hinten mitte rechts |
| STAT_AUSSCHWING_T_VL_WERT | int | Ausschwingzeit vorne links |
| STAT_AUSSCHWING_T_VR_WERT | int | Ausschwingzeit vorne rechts |
| STAT_AUSSCHWING_T_VML_WERT | int | Ausschwingzeit vorne mitte links |
| STAT_AUSSCHWING_T_VMR_WERT | int | Ausschwingzeit vorne mitte rechts |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |
| FG_ZIFFERN | string | die letzten vier Stellen der Fahrgestellnummer |
| _TEL_ANTWORT | binary |  |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-status-weg-v-mode-lesen"></a>
### STATUS_WEG_V_MODE_LESEN

Status des Steuergeraets lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_V_WERT | int | Geschwindigkeit des Fahrzeugs |
| STAT_V_EINH | string | Einheit km/h |
| STAT_WEG_HL_WERT | int | Abstand hinten links |
| STAT_WEG_HR_WERT | int | Abstand hinten rechts |
| STAT_WEG_HML_WERT | int | Abstand hinten in der Mitte links |
| STAT_WEG_HMR_WERT | int | Abstand hinten in der Mitte rechts |
| STAT_WEG_VL_WERT | int | Abstand vorne links |
| STAT_WEG_VR_WERT | int | Abstand vorne rechts |
| STAT_WEG_VML_WERT | int | Abstand vorne in der Mitte links |
| STAT_WEG_VMR_WERT | int | Abstand vorne in der Mitte rechts |
| STAT_WEG_EINH | string | Einheit cm fuer Abstaende |
| STAT_PARKHILFE_AKTIV | int | 1: Parkhilfe aktiv |
| STAT_4_WANDLER | int | 1: 4-Kanal PDC |
| STAT_4_BESTUECKUNG | int | 1: 4-Kanaele bestueckt |
| STAT_RUECKWAERTSGANG | int | 1: Rueckwaertsgang eingelegt |
| STAT_ANHAENGER | int | 1: Anhaengerbetrieb |
| STAT_SIGNAL_RUECKWAERTSGANG | string | BUS oder Pin 12 |
| STAT_SIGNAL_RUECKWAERTSGANG_NR | int | Rueckwaertsgangsignal  0 -&gt; Pin 12, 1: -&gt; BUS |
| STAT_SIGNAL_ANHAENGER | string | BUS oder Pin 5 |
| STAT_SIGNAL_ANHAENGER_NR | int | Anhaengersignal 0 -&gt; Pin 5, 1 -&gt; BUS |
| STAT_SIGNAL_WEGGEBER | string | BUS oder Pin 3 |
| STAT_SIGNAL_WEGGEBER_NR | int | BWeggebersignal 0 -&gt; Pin 3, 1 -&gt; BUS |
| STAT_PDC_AKTIV_KL15 | int | 0 oder 1 |
| STAT_DEAKTIVIERUNG | string | Rueckwaertsgang oder Weg/Geschwindigkeit |
| STAT_DEAKTIVIERUNG_NR | int | Deaktivierung ueber 0 -&gt; Weg/Geschwindigkeit, 1 -&gt; Rueckwaertsgang |
| STAT_EINSCHALTMELDUNG | string | keine / bei erstem aktivieren / bei jedem aktivieren |
| STAT_EINSCHALTMELDUNG_NR | int | 0 -&gt; keine / 1 -&gt; bei erstem aktivieren / 2 -&gt; bei jedem aktivieren |
| STAT_ABSCHALTMELDUNG | int | 0 oder 1 |
| STAT_TASTERMELDUNG | int | 0 oder 1 |

<a id="job-status-messwerte-lesen"></a>
### STATUS_MESSWERTE_LESEN

Messwerte direkt und indirekt lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_WEG_HL_WERT | int | Abstand hinten links |
| STAT_HL_HML_WERT | int | Abstand indirekt hinten links -&gt; hinten mitte links |
| STAT_HML_HL_WERT | int | Abstand indirekt hinten mitte links -&gt; hinten links |
| STAT_WEG_HML_WERT | int | Abstand hinten in der Mitte links |
| STAT_HML_HMR_WERT | int | Abstand indirekt hinten mitte links -&gt; hinten mitte rechts |
| STAT_HMR_HML_WERT | int | Abstand indirekt hinten mitte rechts -&gt; hinten mitte links |
| STAT_WEG_HMR_WERT | int | Abstand hinten in der Mitte rechts |
| STAT_HMR_HR_WERT | int | Abstand indirekt hinten mitte rechts -&gt; hinten rechts |
| STAT_HR_HMR_WERT | int | Abstand indirekt hinten rechts -&gt; hinten mitte rechts |
| STAT_WEG_HR_WERT | int | Abstand hinten rechts |
| STAT_WEG_VL_WERT | int | Abstand vorne links |
| STAT_VL_VML_WERT | int | Abstand indirekt vorne links -&gt; vorne mitte links |
| STAT_VML_VL_WERT | int | Abstand indirekt vorne mitte links -&gt; vorne links |
| STAT_WEG_VML_WERT | int | Abstand vorne in der Mitte links |
| STAT_VML_VMR_WERT | int | Abstand indirekt vorne mitte links -&gt; vorne mitte rechts |
| STAT_VMR_VML_WERT | int | Abstand indirekt vorne mitte rechts -&gt; vorne mitte links |
| STAT_WEG_VMR_WERT | int | Abstand vorne in der Mitte rechts |
| STAT_VMR_VR_WERT | int | Abstand indirekt vorne mitte rechts -&gt; vorne rechts |
| STAT_VR_VMR_WERT | int | Abstand indirekt vorne rechts -&gt; vorne mitte rechts |
| STAT_WEG_VR_WERT | int | Abstand vorne rechts |
| STAT_WEG_EINH | string | Einheit cm fuer Abstaende |

<a id="job-diagnose-weiter"></a>
### DIAGNOSE_WEITER

Diagnose aufrechterhalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Auslesen des Pruefstempels und Interpretation als FG-Nummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| FG_NR | string | Fahrgestellnummer |
| _TEL_ANTWORT | binary |  |

<a id="job-c-fg-auftrag"></a>
### C_FG_AUFTRAG

Beschreiben des Pruefstempels mit der FG-Nummer

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-c-c-lesen"></a>
### C_C_LESEN

Codierdaten lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-c-auftrag"></a>
### C_C_AUFTRAG

Codierdaten schreiben und verifizieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (76 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [FORTTEXTE](#table-forttexte) (19 × 2)
- [FARTTEXTE](#table-farttexte) (18 × 2)
- [FARTMATRIX](#table-fartmatrix) (18 × 13)
- [IO_STATUS](#table-io-status) (8 × 2)

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

Dimensions: 76 rows × 2 columns

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

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 19 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x10 | Wandler hinten links |
| 0x11 | Wandler hinten rechts |
| 0x12 | Wandler hinten Mitte links |
| 0x13 | Wandler hinten Mitte rechts |
| 0x14 | Wandler vorne links |
| 0x15 | Wandler vorne rechts |
| 0x16 | Wandler vorne Mitte links |
| 0x17 | Wandler vorne Mitte rechts |
| 0x18 | Spannung Wandler allgemein |
| 0x20 | Tongeber hinten aus |
| 0x21 | Tongeber hinten ein |
| 0x22 | Tongeber vorne aus |
| 0x23 | Tongeber vorne ein |
| 0x24 | Funktionsanzeige aus |
| 0x25 | Funktionsanzeige ein |
| 0x26 | Weggeber |
| 0x27 | Taste |
| 0x28 | Mikrocomputer |
| 0xXY | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 18 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | Kurzschluss Datenleitung gegen U-Batt |
| 0x02 | Kurzschluss Versorgungs-/Datenleitung gegen Masse |
| 0x03 | Leitungsunterbrechung |
| 0x04 | Ausschwingfehler |
| 0x05 | Fehler momentan vorhanden |
| 0x06 | sporadischer Fehler |
| 0x07 | Kurzschluss gegen U-Batt |
| 0x08 | Kurzschluss gegen Masse |
| 0x09 | Leitungsunterbrechung |
| 0x0A | Fehler momentan vorhanden |
| 0x0B | sporadischer Fehler |
| 0x0C | Fehler im RAM |
| 0x0D | Fehler Checksumme ROM |
| 0x0E | Fehler Checksumme EEPROM |
| 0x0F | Fehler momentan vorhanden |
| 0x10 | sporadischer Fehler |
| 0xFF | -- |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 18 rows × 13 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 | A6_0 | A6_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x10 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 |
| 0x11 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 |
| 0x12 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 |
| 0x13 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 |
| 0x14 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 |
| 0x15 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 |
| 0x16 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 |
| 0x17 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 |
| 0x18 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x09 | 0xFF | 0xFF | 0x00 | 0x0A | 0x00 | 0x0B |
| 0x20 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x09 | 0xFF | 0xFF | 0x00 | 0x0A | 0x00 | 0x0B |
| 0x21 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x09 | 0xFF | 0xFF | 0x00 | 0x0A | 0x00 | 0x0B |
| 0x22 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x09 | 0xFF | 0xFF | 0x00 | 0x0A | 0x00 | 0x0B |
| 0x23 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x09 | 0xFF | 0xFF | 0x00 | 0x0A | 0x00 | 0x0B |
| 0x24 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x09 | 0xFF | 0xFF | 0x00 | 0x0A | 0x00 | 0x0B |
| 0x25 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x09 | 0xFF | 0xFF | 0x00 | 0x0A | 0x00 | 0x0B |
| 0x26 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x09 | 0xFF | 0xFF | 0x00 | 0x0A | 0x00 | 0x0B |
| 0x27 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x09 | 0xFF | 0xFF | 0x00 | 0x0A | 0x00 | 0x0B |
| 0x28 | 0x00 | 0x0C | 0x00 | 0x0D | 0x00 | 0x0E | 0xFF | 0xFF | 0x00 | 0x0F | 0x00 | 0x10 |

<a id="table-io-status"></a>
### IO_STATUS

Dimensions: 8 rows × 2 columns

| SIGNAL | BYTE |
| --- | --- |
| DTAUS | 0x01 |
| DTVEIN | 0x02 |
| DTHEIN | 0x04 |
| DKSAUS | 0x08 |
| DKSEIN | 0x10 |
| DEIN | 0x20 |
| SAUS | 0x40 |
| SEIN | 0x80 |
