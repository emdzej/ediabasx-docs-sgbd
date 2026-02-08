# SPM46BT.prg

- Jobs: [16](#jobs)
- Tables: [9](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Spiegel-Memory E46 Beifahrertuere |
| ORIGIN | BMW EI-61 King |
| REVISION | 1.00 |
| AUTHOR | BMW TI-433 Teepe, BMW TI-433 Drexel |
| COMMENT | N/A |
| PACKAGE | 1.01 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [IDENT](#job-ident) - Identdaten
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode aufrechterhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose
- [STATUS_LESEN](#job-status-lesen) - Auslesen der IO-Stati des Steuergeraetes Der Wertebereich fuer digitale Results: Bereich: 0, wenn FALSE / 1, wenn TRUE
- [STEUERN_DIGITAL](#job-steuern-digital) - Ansteuern von Funktionen des Steuergeraetes
- [CODIERUNG_LESEN](#job-codierung-lesen) - Auslesen der Codierung des Steuergeraetes Der Wertebereich fuer digitale Results: Bereich: 0, wenn FALSE / 1, wenn TRUE
- [SPEICHER_LESEN](#job-speicher-lesen) - Ansteuern von Funktionen des Steuergeraetes

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

Initialisierung und Kommunikationsparameter DS2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

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

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

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
| BYTE1 | int | 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | 0-255 bzw. 0x00-0xFF |
| FG_ZIFFERN | string | die letzten vier Stellen der Fahrgestellnummer |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_ARGUMENT, wenn Argumente nicht uebergeben oder ausser Bereich |

<a id="job-energiesparmode"></a>
### ENERGIESPARMODE

Einstellen des Energiesparmodes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PRODUKTIONSMODE | string | "ein" -&gt; Produktions Mode ein "aus" -&gt; Produktions Mode aus table DigitalArgument TEXT Default: "aus" |
| TRANSPORTMODE | string | "ein" -&gt; Transport Mode ein "aus" -&gt; Transport Mode aus table DigitalArgument TEXT Default: "aus" |
| WERKSTATTMODE | string | "ein" -&gt; Werkstatt Mode ein "aus" -&gt; Werkstatt Mode aus table DigitalArgument TEXT Default: "aus" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Sleep-Mode versetzen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEIT | real | a) Zeit nach der das Steuergerät einschläft Bereich   : 0.5 bis 20.0 [Sekunden] Auflösung : 0.5 [Sekunden] =&gt; zeitgesteuerter Power-Down (0x9B) wird aktiviert b) Default: (Es wird kein Argument übergeben!) =&gt; normaler Power-Down (0x9D) wird aktiviert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

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

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Text zu Fehlerort table FOrtTexte ORTTEXT |
| F_HFK | int | Fehlerhaeufigkeit |
| F_ART_ANZ | int | Anzahl der Fehlerarten immer 1 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen immer 0 |
| F_ART1_NR | int |  |
| F_ART1_TEXT | string | table FArtTexte ARTTEXT |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |

<a id="job-is-lesen"></a>
### IS_LESEN

Infospeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Text zu Fehlerort table IOrtTexte ORTTEXT |
| F_HFK | int | Fehlerhaeufigkeit |
| F_ART_ANZ | int | Anzahl der Fehlerarten immer 1 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen immer 0 |
| F_ART1_NR | int |  |
| F_ART1_TEXT | string | table IArtTexte ARTTEXT |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Auslesen der IO-Stati des Steuergeraetes Der Wertebereich fuer digitale Results: Bereich: 0, wenn FALSE / 1, wenn TRUE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TASTER_BEIKLAPPEN_AKTIV | int |  |
| STAT_WIPPE_AUF_AKTIV | int |  |
| STAT_WIPPE_AB_AKTIV | int |  |
| STAT_WIPPE_RECHTS_AKTIV | int |  |
| STAT_WIPPE_LINKS_AKTIV | int |  |
| STAT_WIPPE_NEUTRAL_AKTIV | int |  |
| STAT_POSITION_WIPPE | int | Position der Wippe fuer MK, da DIS keine Kombination aus den anderen Wippenresult bilden kann 0=neutral, 1=auf, 2=ab, 3=rechts, 4=links |
| STAT_SPANNUNG_SPIEGELVERSTELLSCHALTER_EINGANG_S_WERT | real |  |
| STAT_SPANNUNG_EINH | string | immer Volt |
| STAT_SPANNUNG_POTENTIOMETER_VERTIKAL_WERT | real |  |
| STAT_SPANNUNG_POTENTIOMETER_HORIZONTAL_WERT | real |  |
| STAT_SPANNUNG_VERSORGUNG_POTENTIOMETER_WERT | real |  |
| STAT_SPANNUNG_VERSORGUNG_SPIEGELVERSTELLSCHALTER_WERT | real |  |
| STAT_SPANNUNG_KLEMME_30_WERT | real |  |
| STAT_EINSCHALTDAUER_HEIZUNG_WERT | real |  |
| STAT_EINSCHALTDAUER_HEIZUNG_EINH | string | Prozent [%] |
| STAT_BEIKLAPP_RICHTUNG_AKTIV | int |  |
| STAT_WIEDERHOLSPERRE_BEIKLAPPEN_AKTIV | int |  |
| STAT_KLEMME_R_AKTIV | int |  |
| STAT_KLEMME_15_AKTIV | int |  |
| STAT_UNTERSPANNUNG_AKTIV | int |  |
| STAT_UEBERSPANNUNG_AKTIV | int |  |
| STAT_AUSGANGSSTATUS_HEIZUNG_AKTIV | int |  |
| STAT_WISCHER_1_AKTIV | int |  |
| STAT_AUSSENTEMPERATUR_WERT | int | Wert vom K-Bus |
| STAT_AUSSENTEMPERATUR_EINH | string | Grad C |
| STAT_SPIEGELHEIZUNGSNACHLAUF_AKTIV | int |  |
| STAT_STANDHEIZUNG_AKTIV | int |  |
| STAT_RUECKFAHRSIGNAL_AKTIV | int |  |
| STAT_BORDSTEINAUTOMATIK_AKTIV | int |  |
| STAT_ANHAENGERSIGNAL_AKTIV | int |  |
| STAT_BEIKLAPPUNG_AKTIV | int |  |
| STAT_R_L_SCHALTER_AKTIV | int |  |
| STAT_BLOCKERKENNUNG_SPIEGELVERSTELLUNG_AKTIV | int |  |
| STAT_DIAGNOSE_AKTIV | int |  |
| STAT_KLEMME_50_AKTIV | int |  |
| STAT_MOTOR_RECHTS_AKTIV | int |  |
| STAT_MOTOR_LINKS_AKTIV | int |  |
| STAT_MOTOR_AUF_AKTIV | int |  |
| STAT_MOTOR_AB_AKTIV | int |  |
| STAT_SPIEGELMOTOR_AKTIV | int |  |
| STAT_UNTERSPANNUNG_HEIZUNG_AKTIV | int |  |
| STAT_GL1_AKTIV | int |  |
| STAT_GH2_AKTIV | int |  |
| STAT_GH1_AKTIV | int |  |
| STAT_GL2_AKTIV | int |  |
| STAT_STATUS_FLAG_AKTIV | int |  |
| STAT_OVERLOAD_AKTIV | int |  |
| STAT_LS1_AKTIV | int |  |
| STAT_HS1_AKTIV | int |  |
| STAT_LS2_AKTIV | int |  |
| STAT_HS2_AKTIV | int |  |
| STAT_LS3_AKTIV | int |  |
| STAT_HS3_AKTIV | int |  |
| STAT_POWER_SUPPLY_FAIL_AKTIV | int |  |
| STAT_SPANNUNG_HEIZUNG_WERT | real |  |
| STAT_BLOCKSTROM_WERT | real |  |
| STAT_BLOCKSTROM_EINH | string | Ampere |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

Ansteuern von Funktionen des Steuergeraetes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT1 | string | moeglich sind folgende Argumente, Liste: 'SPIEGEL_AUS' = Spiegelverstellung aus 'SPIEGEL_RECHTS' = Spiegelverstellung rechts 'SPIEGEL_LINKS ' = Spiegelverstellung links 'SPIEGEL_AUF' = Spiegelverstellung aufwaerts 'SPIEGEL_AB' = Spiegelverstellung abwaerts 'AUSKLAPPEN' = Spiegel ausklappen 'EINKLAPPEN' = Spiegel einklappen 'MEM1_ANFAHREN' = Memoryposition 1 anfahren 'MEM2_ANFAHREN' = Memoryposition 2 anfahren 'MEM3_ANFAHREN' = Memoryposition 3 anfahren 'MEM1_SPEICHERN' = Memoryposition 1 speichern 'MEM2_SPEICHERN' = Memoryposition 2 speichern 'MEM3_SPEICHERN' = Memoryposition 3 speichern 'FUNKSCHLUESSEL' = Funkschluesselmeldung, Achtung Schluesselnummer erforderlich 'FAHRERTUER_AUF' = Fahrertuer ist offen 'FAHRERTUER_ZU' = Fahrertuer ist geschlossen 'KOMFORTSCHL'   = Komforschliessen ausloesen 'HEIZUNG_EIN'   = Spiegelheizung fuer 2 Sec ansteuern 'RFSI_EIN'      = Rueckfahrsignal ein 'RFSI_AUS'      = Rueckfahrsignal aus 'SELBSTTEST' = Selbsttest ausloesen: alle Mem-Positonen anfahren, Spiegel bei- und abklappen, Heizung fuer 1,5 sec aktivieren |
| ORT2 | int | 'FUNKSCHL_NR' = Nummer des Funkschluessel als zweites Argument bei Argument 1 = Funkschluessel |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Auslesen der Codierung des Steuergeraetes Der Wertebereich fuer digitale Results: Bereich: 0, wenn FALSE / 1, wenn TRUE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| COD_INDIVIDUALISIERUNG_AKTIV | int |  |
| COD_SPIEGEL_ABKLAPPEN_AKTIV | int |  |
| COD_SPIEGEL_BEIKLAPPEN_BEI_KS_AKTIV | int | invertiert! |
| COD_GESCHW_VERRIEGELUNG_BK_AKTIV | int |  |
| COD_DEFAULT_ABKLAPP_POSITION_AKTIV | int |  |
| COD_PERMANENTES_SPIEGELHEIZEN_BEI_KL15_AKTIV | int |  |
| COD_SITZ_MEMORY_VERBAUT_AKTIV | int |  |
| COD_LINKSLENKER_AKTIV | int | 1=LL, 0=RL |
| COD_GESCHWINDIGKEIT_VERRIEGELUNGSSPERRE_WERT | int | 0 bis 255 |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Ansteuern von Funktionen des Steuergeraetes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANZAHL_BYTES | int | Anzahl Bytes &gt;=1 und &lt;=32 |
| ADRESSE | long | Adresse High Bytes 0x0000 bis 0xFFFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATEN | binary | ausgelesene Daten |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (70 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [IARTTEXTE](#table-iarttexte) (3 × 2)
- [FORTTEXTE](#table-forttexte) (14 × 2)
- [IORTTEXTE](#table-iorttexte) (6 × 2)
- [STEUERN](#table-steuern) (22 × 3)

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

Dimensions: 70 rows × 2 columns

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
| 0x69 | Magna-Donelly |
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

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | sporadischer Fehler |
| 0x01 | statischer Fehler |
| 0x?? | unbekannte Fehlerart |

<a id="table-iarttexte"></a>
### IARTTEXTE

Dimensions: 3 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | sporadischer Fehler |
| 0x01 | statischer Fehler |
| 0x?? | unbekannte Fehlerart |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 14 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x001 | Timer Watchdog |
| 0x002 | EEPROM |
| 0x004 | Spiegelverstellschalter, Unterbrechung |
| 0x005 | Spiegelheizung Unterbrechung |
| 0x006 | Spiegelheizung Kurzschluss |
| 0x007 | Spiegelmotor, Potentiometer Vertikal |
| 0x008 | Spiegelmotor, Potentiometer Horizontal |
| 0x009 | Spiegelmotor Vertikal Unterbrechung |
| 0x00A | Spiegelmotor Vertikal Kurzschluss |
| 0x00B | Spiegelmotor Horizontal Unterbrechung |
| 0x00C | Spiegelmotor Horizontal Kurzschluss |
| 0x00D | Spiegelmotor Einklappen Unterbrechung |
| 0x00E | Spiegelmotor Einklappen Kurzschluss |
| 0x??? | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 6 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x000 | Unterspannung ( U &lt; 8,5 Volt ) |
| 0x001 | Ueberspannung ( U &gt; 16 Volt ) |
| 0x002 | Unterspannung Spiegelheizung |
| 0x003 | Wiederholsperre BK |
| 0x004 | Spiegelmotor, Potentiometer Plausibilitaet |
| 0x??? | unbekannter Fehlerort |

<a id="table-steuern"></a>
### STEUERN

Dimensions: 22 rows × 3 columns

| AUSGANG | BYTE | WERT |
| --- | --- | --- |
| SPIEGEL_AUS | 0x01 | 0x00 |
| SPIEGEL_RECHTS | 0x01 | 0x01 |
| SPIEGEL_LINKS | 0x01 | 0x02 |
| SPIEGEL_AUF | 0x01 | 0x03 |
| SPIEGEL_AB | 0x01 | 0x04 |
| AUSKLAPPEN | 0x01 | 0x05 |
| EINKLAPPEN | 0x01 | 0x06 |
| MEM1_ANFAHREN | 0x01 | 0x07 |
| MEM2_ANFAHREN | 0x01 | 0x08 |
| MEM3_ANFAHREN | 0x01 | 0x09 |
| MEM1_SPEICHERN | 0x01 | 0x0A |
| MEM2_SPEICHERN | 0x01 | 0x0B |
| MEM3_SPEICHERN | 0x01 | 0x0C |
| FUNKSCHLUESSEL | 0x01 | 0x0D |
| FAHRERTUER_AUF | 0x01 | 0x0E |
| FAHRERTUER_ZU | 0x01 | 0x0F |
| KOMFORTSCHL | 0x01 | 0x10 |
| HEIZUNG_EIN | 0x01 | 0x11 |
| RFSI_EIN | 0x01 | 0x12 |
| RFSI_AUS | 0x01 | 0x13 |
| SELBSTTEST | 0x01 | 0x1E |
| XYZ | 0x01 | 0xFF |
