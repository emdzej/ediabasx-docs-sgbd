# CD53FLSH.prg

- Jobs: [36](#jobs)
- Tables: [8](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | CD53FLSH |
| ORIGIN | BMW EE-42 Wiesmeier |
| REVISION | 0.8 |
| AUTHOR | BMW TI-431 Krueger |
| COMMENT | CD53FLSH |
| PACKAGE | 0.05 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer das Radio
- [IDENT](#job-ident) - Identdaten
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [STATUS_LESEN](#job-status-lesen) - alle Stati des RADIO lesen
- [STEUERN_DEFAULT_SOUND](#job-steuern-default-sound) - Balance, Fader und Volume Defaulteinstellung
- [STEUERN_FADER_LV](#job-steuern-fader-lv) - Ansteuerung des Kanals links vorne
- [STEUERN_FADER_RV](#job-steuern-fader-rv) - Ansteuerung des Kanals rechts vorne
- [STEUERN_FADER_RH](#job-steuern-fader-rh) - Ansteuerung des Kanals rechts hinten
- [STEUERN_FADER_LH](#job-steuern-fader-lh) - Ansteuerung des Kanals links hinten
- [STEUERN_VOL_UP](#job-steuern-vol-up) - Lautstaerkeerhoehung um 11dB/s
- [STEUERN_VOL_DOWN](#job-steuern-vol-down) - Lautstaerkenabsenkung um 11dB/s
- [STEUERN_SEEK_UP](#job-steuern-seek-up) - Suchlauf aufwaerts
- [STEUERN_SEEK_DOWN](#job-steuern-seek-down) - Suchlauf abwaerts
- [STEUERN_AUDIO_KEY](#job-steuern-audio-key) - Audio-Taste betaetigen
- [STEUERN_GAL_DEK](#job-steuern-gal-dek) - GAL-WERT dekrementieren
- [STEUERN_GAL_INK](#job-steuern-gal-ink) - GAL-WERT inkrementieren
- [STEUERN_VF_DEK](#job-steuern-vf-dek) - VF-Mindestlautstaerke dekrementieren
- [STEUERN_VF_INK](#job-steuern-vf-ink) - VF-Mindestlautstaerke inkrementieren
- [STEUERN_FREQUENZ](#job-steuern-frequenz) - einstellen der Radiofrequenz
- [STEUERN_RADIO_POWER](#job-steuern-radio-power) - Ein-/Ausschalten des Radios
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [SERIALNUMBER](#job-serialnumber) - Herstelldaten lesen
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [FG_LESEN](#job-fg-lesen) - Auslesen des Pruefstempels und Interpretation als FG-Nummer
- [COD_LESEN](#job-cod-lesen) - Auslesen der Codierung Radio
- [SET_PROG_MODE](#job-set-prog-mode) - Setzen des Programmiermodus
- [STEUERN_SPEICHER_LOESCHEN](#job-steuern-speicher-loeschen) - Loescht den Speicher
- [STEUERN_SPEICHER_ADRESSE](#job-steuern-speicher-adresse) - Setzt Speicheradresse bei aktuellem Schritt
- [STEUERN_PROGRAMMIEREN_START](#job-steuern-programmieren-start) - Startet den Programmiervorgang
- [STEUERN_UEBERTRAGEN_PROGRAMM](#job-steuern-uebertragen-programm) - Uebertraegt Speicherdaten bei aktuellem Schritt
- [VERIFY_CHECKSUM](#job-verify-checksum) - Setzt Speicheradresse bei aktuellem Schritt
- [STEUERN_RESET](#job-steuern-reset) - Fuehrt einen Reset im Radio aus
- [FLASH_SCHREIBEN](#job-flash-schreiben) - Beliebige Flash Zellen beschreiben

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

Init-Job fuer das Radio

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

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
| ID_GERAETE_NAME | string | Entwicklungsbezeichnung des Radios ohne Unterstrich |
| ID_RADIO_NAME | string | Entwicklungsbezeichnung des Radios mit Unterstrich |
| ID_TASTE_DIAG | string | auslesen des Tastaturstatus moeglich |
| ID_SUCHSCHWELLE_DIAG | string | auslesen des Suchlaufschwellenstatus moeglich |
| ID_VF_DIAG | string | auslesen des VF-Status moeglich |
| ID_AN_AUS_DIAG | string | auslesen ob Radio ein aus moeglich |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose

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
| F_ART1_NR | int | Index der 1. Fehlerart (entweder 0 oder 32) |
| F_ART1_TEXT | string | 1. Fehlerart als Text |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-status-lesen"></a>
### STATUS_LESEN

alle Stati des RADIO lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| STAT_RADIO_TASTE_BETAETIGT | int | 0 -&gt; keine Taste betaetigt, 1 -&gt; bel. Taste betaetigt !! Achtung: bei Bordmonitorvarianten immer result=0 ! mit "Radio aus" nur Dummyergebnis ! |
| STAT_TELEFON_MUTE_AKTIV | int | 0 -&gt; Mute inaktiv, 1 -&gt; Mute aktiv ! mit "Radio aus" nur Dummyergebnis ! |
| STAT_GAL_KURVE | int | Gal-Kurve 1,2,3,4 eingestellt (auch mit "Radio aus" moeglich) |
| STAT_SEEK_SCHWELLE | int | Suchlaufschwelle 1:empfindlich oder 2:unempfindlich !! Achtung: bei nicht ECE-Varianten result immer=1 (auch mit "Radio aus" moeglich) |
| STAT_MIT_DSP | int | DSP verbaut oder nicht verbaut (auch mit Radio aus" moeglich) |
| STAT_VF_LAUT_WERT | int | Zahlenwert der VF-Lautstaerke (inkl. Vorzeichen) !! Achtung: bei nicht ECE-Varianten result = -0 ! mit "Radio aus" nur Dummyergebnis |
| STAT_GAL_GESCHW_WERT | int | Zahlenwert Geschw.-abhaengige Lautstaerkenregelung-Frequenz ! mit "Radio aus" nur Dummyergebnis ! Unterschiedliche Behandlung bei ZIS und BM-Varianten ! |
| STAT_GAL_GESCHW_EINH | string | Einheit der GAL-Geschwindigkeit (Km/h) |
| STAT_FELDSTAERKE_WERT | int | FELDSTAERKE des empf. Senders (relativ, 0-15) ! mit "Radio aus" nur Dummyergebnis |
| STAT_RADIO_EIN | int | 1: Radio ist eingeschaltet 0: Radio ist ausgeschaltet bei ausgeschaltetem Radio ist keine DSP-Diagnose moeglich |

<a id="job-steuern-default-sound"></a>
### STEUERN_DEFAULT_SOUND

Balance, Fader und Volume Defaulteinstellung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |

<a id="job-steuern-fader-lv"></a>
### STEUERN_FADER_LV

Ansteuerung des Kanals links vorne

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |

<a id="job-steuern-fader-rv"></a>
### STEUERN_FADER_RV

Ansteuerung des Kanals rechts vorne

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |

<a id="job-steuern-fader-rh"></a>
### STEUERN_FADER_RH

Ansteuerung des Kanals rechts hinten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |

<a id="job-steuern-fader-lh"></a>
### STEUERN_FADER_LH

Ansteuerung des Kanals links hinten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |

<a id="job-steuern-vol-up"></a>
### STEUERN_VOL_UP

Lautstaerkeerhoehung um 11dB/s

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INKREMENTE | int | Anzahl der Telegramme die geschickt werden (default 1) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |

<a id="job-steuern-vol-down"></a>
### STEUERN_VOL_DOWN

Lautstaerkenabsenkung um 11dB/s

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INKREMENTE | int | Anzahl der Telegramme die geschickt werden (default 1) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |

<a id="job-steuern-seek-up"></a>
### STEUERN_SEEK_UP

Suchlauf aufwaerts

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |

<a id="job-steuern-seek-down"></a>
### STEUERN_SEEK_DOWN

Suchlauf abwaerts

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |

<a id="job-steuern-audio-key"></a>
### STEUERN_AUDIO_KEY

Audio-Taste betaetigen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |

<a id="job-steuern-gal-dek"></a>
### STEUERN_GAL_DEK

GAL-WERT dekrementieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |

<a id="job-steuern-gal-ink"></a>
### STEUERN_GAL_INK

GAL-WERT inkrementieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |

<a id="job-steuern-vf-dek"></a>
### STEUERN_VF_DEK

VF-Mindestlautstaerke dekrementieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |

<a id="job-steuern-vf-ink"></a>
### STEUERN_VF_INK

VF-Mindestlautstaerke inkrementieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |

<a id="job-steuern-frequenz"></a>
### STEUERN_FREQUENZ

einstellen der Radiofrequenz

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FREQUENZ | string | Frequenz in KHz 0 - 999999 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-steuern-radio-power"></a>
### STEUERN_RADIO_POWER

Ein-/Ausschalten des Radios

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG1 | string | EIN/AUS,ON/OFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

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

<a id="job-serialnumber"></a>
### SERIALNUMBER

Herstelldaten lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| SERIEN_NR | string | Seriennummer vom Hersteller |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Ergebnis ist immer OKAY, da nur Dummy |

<a id="job-fg-lesen"></a>
### FG_LESEN

Auslesen des Pruefstempels und Interpretation als FG-Nummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| FG_NR | string | Fahrgestellnummer |
| _TEL_ANTWORT | binary |  |

<a id="job-cod-lesen"></a>
### COD_LESEN

Auslesen der Codierung Radio

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| COD_DATEN | string | die 4 Codierbytes |
| COD_LAENDERVARIANTE | string | Laendervariante des Radios table LandVar LAND_TEXT |

<a id="job-set-prog-mode"></a>
### SET_PROG_MODE

Setzen des Programmiermodus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |

<a id="job-steuern-speicher-loeschen"></a>
### STEUERN_SPEICHER_LOESCHEN

Loescht den Speicher

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |

<a id="job-steuern-speicher-adresse"></a>
### STEUERN_SPEICHER_ADRESSE

Setzt Speicheradresse bei aktuellem Schritt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Area Byte // Normalerweise 0x02 |
| BYTE2 | int | High address number |
| BYTE3 | int | Middle address number |
| BYTE4 | int | Low address number |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |

<a id="job-steuern-programmieren-start"></a>
### STEUERN_PROGRAMMIEREN_START

Startet den Programmiervorgang

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |

<a id="job-steuern-uebertragen-programm"></a>
### STEUERN_UEBERTRAGEN_PROGRAMM

Uebertraegt Speicherdaten bei aktuellem Schritt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Area Byte // Normalerweise 0x02 |
| BYTE2 | int | High address number |
| BYTE3 | int | Middle address number |
| BYTE4 | int | Low address number |
| BYTE5 | int | 0x00 bedeutet normale Programmierdaten 0x00 oder 0xFF bedeutet leerer ROM Bereich 0x01 oder 0x20 bedeutet Datenlänge |
| BYTE6 | int | Programmdaten maximal 32Byte |
| BYTE7 | int | Programmdaten |
| BYTE8 | int | Programmdaten |
| BYTE9 | int | Programmdaten |
| BYTE10 | int | Programmdaten |
| BYTE11 | int | Programmdaten |
| BYTE12 | int | Programmdaten |
| BYTE13 | int | Programmdaten |
| BYTE14 | int | Programmdaten |
| BYTE15 | int | Programmdaten |
| BYTE16 | int | Programmdaten |
| BYTE17 | int | Programmdaten |
| BYTE18 | int | Programmdaten |
| BYTE19 | int | Programmdaten |
| BYTE20 | int | Programmdaten |
| BYTE21 | int | Programmdaten |
| BYTE22 | int | Programmdaten |
| BYTE23 | int | Programmdaten |
| BYTE24 | int | Programmdaten |
| BYTE25 | int | Programmdaten |
| BYTE26 | int | Programmdaten |
| BYTE27 | int | Programmdaten |
| BYTE28 | int | Programmdaten |
| BYTE29 | int | Programmdaten |
| BYTE30 | int | Programmdaten |
| BYTE31 | int | Programmdaten |
| BYTE32 | int | Programmdaten |
| BYTE33 | int | Programmdaten |
| BYTE34 | int | Programmdaten |
| BYTE35 | int | Programmdaten |
| BYTE36 | int | Programmdaten |
| BYTE37 | int | Programmdaten |
| BYTE38 | int | Programmdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |

<a id="job-verify-checksum"></a>
### VERIFY_CHECKSUM

Setzt Speicheradresse bei aktuellem Schritt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | SumHi |
| BYTE2 | int | SumLo |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |

<a id="job-steuern-reset"></a>
### STEUERN_RESET

Fuehrt einen Reset im Radio aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |

<a id="job-flash-schreiben"></a>
### FLASH_SCHREIBEN

Beliebige Flash Zellen beschreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Programmierdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (56 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [FORTTEXTE](#table-forttexte) (4 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [DIAGINDEX](#table-diagindex) (68 × 7)
- [LANDVAR](#table-landvar) (6 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)

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

Dimensions: 56 rows × 2 columns

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
| 0x55 | BHTC |
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

Dimensions: 4 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | Energiesparmode aktiviert |
| 0x01 | Fehler an der CD-Wechsler-Schnittstelle |
| 0x02 | Fehler an der Antennenstromversorgung |
| 0xXY | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Fehler momentan nicht vorhanden |
| 0x20 | Fehler momentan vorhanden |
| 0xXY | unbekannte Fehlerart |

<a id="table-diagindex"></a>
### DIAGINDEX

Dimensions: 68 rows × 7 columns

| DIAG_NR | RADIO_NAME | RADIO_NAME_NEU | TASTE | SUCHSCHWELLE | VF | AN_AUS |
| --- | --- | --- | --- | --- | --- | --- |
| 0x00 | C23 MID ECE | C23_MID_ECE | 1 | 1 | 1 | 1 |
| 0x01 | C23 BM ECE | C23_BM_ECE | 0 | 1 | 1 | 1 |
| 0x02 | C23 MID US | C23_MID_US | 1 | 0 | 0 | 1 |
| 0x03 | C23 BM JPN | C23_BM_JPN | 0 | 0 | 0 | 1 |
| 0x04 | C33 JPN | C33_JPN | 1 | 0 | 0 | 0 |
| 0x05 | C23 BM OCN | C23_BM_OCN | 0 | 0 | 0 | 1 |
| 0x07 | CD23 | CD23 | 1 | 1 | 1 | 1 |
| 0x08 | C24 DIN | C24_DIN | 1 | 1 | 1 | 1 |
| 0x09 | C24 MID | C24_MID | 1 | 1 | 1 | 1 |
| 0x0A | C34 | C34 | 1 | 1 | 1 | 0 |
| 0x0B | C32 | C32 | 1 | 1 | 1 | 0 |
| 0x0C | CD33 | CD33 | 1 | 1 | 1 | 0 |
| 0x0D | C33 ECE | C33_ECE | 1 | 1 | 1 | 0 |
| 0x0E | C33 US | C33_US | 1 | 0 | 0 | 0 |
| 0x0F | C33 OCN | C33_OCN | 1 | 0 | 0 | 0 |
| 0x10 | C43 ECE | C43_ECE | 1 | 1 | 1 | 0 |
| 0x11 | CD43 | CD43 | 1 | 1 | 1 | 0 |
| 0x12 | C43 USA | C43_USA | 1 | 0 | 0 | 0 |
| 0x13 | C43 JPN | C43_JPN | 1 | 0 | 0 | 0 |
| 0x14 | C43 OCN | C43_OCN | 1 | 0 | 0 | 0 |
| 0x15 | C44 | C44 | 1 | 1 | 1 | 0 |
| 0x16 | C24 BM | C24_BM | 1 | 1 | 1 | 1 |
| 0x17 | C42 | C42 | 1 | 1 | 1 | 0 |
| 0x18 | C42R-RD1 Euro | C42R-RD1_Euro | 1 | 1 | 1 | 0 |
| 0x19 | RC42-Tempest US | RC42-Tempest_US | 1 | 1 | 0 | 0 |
| 0x1A | RD42-Tempest Ja | RD42-Tempest_Ja | 1 | 1 | 0 | 0 |
| 0x1B | RC43-RD1 Jap | RC43-RD1_Jap | 1 | 1 | 0 | 0 |
| 0x1C | RC43-RD1 Euro | RC43-RD1_Euro | 1 | 1 | 1 | 0 |
| 0x1D | RC43-Tempest US | RC43-Tempest_US | 1 | 1 | 0 | 0 |
| 0x1E | RC43-Tempest Ja | RC43-Tempest_Ja | 1 | 1 | 0 | 0 |
| 0x1F | RC43-Tempest Eu | RC43-Tempest_Eu | 1 | 1 | 1 | 0 |
| 0x20 | RC43-38a Euro | RC43-38a_Euro | 1 | 1 | 1 | 0 |
| 0x21 | RC43-38a US | RC43-38a_US | 1 | 1 | 0 | 0 |
| 0x22 | RC43-38a Jap | RC43-38a_Jap | 1 | 1 | 0 | 0 |
| 0x23 | C43 US E38 | C43_US_E38 | 1 | 1 | 0 | 0 |
| 0x24 | C43 US E39 | C43_US_E39 | 1 | 1 | 0 | 0 |
| 0x25 | C43 US BM | C43_US_BM | 1 | 1 | 0 | 0 |
| 0x26 | CD43 E39 | CD43_E39 | 1 | 1 | 1 | 0 |
| 0x27 | C42 R50 | C42_R50 | 1 | 1 | 1 | 1 |
| 0x28 | C53 MID L30 | C53_MID_L30 | 1 | 1 | 1 | 1 |
| 0x29 | CD53 L30 | CD53_L30 | 1 | 1 | 1 | 1 |
| 0x2A | MD53 L30 | MD53_L30 | 1 | 1 | 1 | 1 |
| 0x2B | CD54 L30 | CD54_L30 | 1 | 1 | 1 | 1 |
| 0x2C | CD54 E39 | CD54_E39 | 1 | 1 | 1 | 1 |
| 0x2D | CD54 E46 | CD54_E46 | 1 | 1 | 1 | 1 |
| 0x2E | C53 R50 | C53_R50 | 1 | 1 | 1 | 1 |
| 0x2F | CD53 R50 | CD53_R50 | 1 | 1 | 1 | 1 |
| 0x30 | MD53 R50 | MD53_R50 | 1 | 1 | 1 | 1 |
| 0x31 | C53 MID E39 | C53_MID_E39 | 1 | 1 | 1 | 1 |
| 0x32 | BM53 | BM53 | 1 | 1 | 1 | 1 |
| 0x33 | C53 E46 | C53_E46 | 1 | 1 | 1 | 1 |
| 0x34 | MD53 E46 | MD53_E46 | 1 | 1 | 1 | 1 |
| 0x35 | CD53 E46 | CD53_E46 | 1 | 1 | 1 | 1 |
| 0x36 | CD53 E39 | CD53_E39 | 1 | 1 | 1 | 1 |
| 0x37 | MD53 E39 | MD53_E39 | 1 | 1 | 1 | 1 |
| 0x39 | BM54 | BM54 | 1 | 1 | 1 | 1 |
| 0x3A | C53 MIR E46 | C53_MIR_E46 | 1 | 1 | 1 | 1 |
| 0x3B | MIR E52 | MIR_E52 | 1 | 1 | 1 | 1 |
| 0x3C | C33B E39 CKD | C33B_E39_CKD | 1 | 1 | 1 | 1 |
| 0x3D | C33B E46 CKD | C33B_E46_CKD | 1 | 1 | 1 | 1 |
| 0x3E | BM24 MMC | BM24_MMC | 1 | 1 | 1 | 1 |
| 0x3F | C52 E39 | C52_E39 | 1 | 1 | 1 | 1 |
| 0x40 | C52 E53 | C52_E53 | 1 | 1 | 1 | 1 |
| 0x41 | C53 E39 | C53_E39 | 1 | 1 | 1 | 1 |
| 0x42 | C53 E53 | C53_E53 | 1 | 1 | 1 | 1 |
| 0x43 | CD62 E85 | CD62_E85 | 1 | 1 | 1 | 1 |
| 0x44 | MD53 CID | MD53_CID | 1 | 1 | 1 | 1 |
| 0xFF | unbekannte Radioart | unbekannte Radioart | 0 | 0 | 0 | 0 |

<a id="table-landvar"></a>
### LANDVAR

Dimensions: 6 rows × 2 columns

| HEX | LAND_TEXT |
| --- | --- |
| 0x00 | ECE |
| 0x01 | US |
| 0x02 | JAPAN |
| 0x03 | OCEANIEN |
| 0x04 | KANADA |
| 0xXY | UNBEKANNT |

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
