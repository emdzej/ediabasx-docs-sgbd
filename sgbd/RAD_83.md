# RAD_83.PRG

- Jobs: [50](#jobs)
- Tables: [18](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Radio ZIS / BM / MIR  |
| ORIGIN | BMW EI-41 Siglow |
| REVISION | 1.004 |
| AUTHOR | BMW TI-431 Weber, Siemens EI-41 Niedermeier |
| COMMENT | Radio  |
| PACKAGE | 1.03 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
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
- [STEUERN_RADIO_POWER](#job-steuern-radio-power) - Switch radio ON/OFF
- [HERSTELLDATEN_LESEN](#job-herstelldaten-lesen) - Herstelldaten lesen
- [FG_LESEN](#job-fg-lesen) - Auslesen des Pruefstempels und Interpretation als FG-Nummer
- [COD_LESEN](#job-cod-lesen) - Auslesen der Codierung Radio
- [C_FG_LESEN](#job-c-fg-lesen) - Auslesen des Pruefstempels und Interpretation als FG-Nummer
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Beschreiben des Pruefstempels mit der FG-Nummer
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren
- [STEUERN_RADIO_SCHALTEN](#job-steuern-radio-schalten) - Ein-/Ausschalten des Radios KWP2000: $30 InputOutputControlByLocalIdentifier $0A inputOutputLocalIdentifier  - switch radio on or off $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default
- [STATUS_ANT_QFS](#job-status-ant-qfs) - Auslesen des Status Quality Fieldstrength KWP2000: $30 InputOutputControlByLocalIdentifier $12 inputOutputLocalIdentifier  - status QFS $01 inputOutputControlParameter - reportCurrentState Modus  : Default
- [SER_NR_DOM_LESEN](#job-ser-nr-dom-lesen) - Seriennummer 14-stellig lesen Neu für Entertainment-Komponenten ab 2003 Modus  : Default
- [STEUERN_RDS](#job-steuern-rds) - Einstellen der RDS Optionen
- [STEUERN_FOLDER_AND_TRACK_NUMBER](#job-steuern-folder-and-track-number) - Select folder and track of internal drive
- [STEUERN_TRACK_NUMBER](#job-steuern-track-number) - select track of internal drive
- [STATUS_CD_MD_CDC](#job-status-cd-md-cdc) - responds drive status
- [STATUS_IBOC](#job-status-iboc) - responds IBOC status
- [STATUS_RDS](#job-status-rds) - responds all RDS state of the radio
- [STATUS_NEXT_ENTSOURCE](#job-status-next-entsource) - responds current audio source
- [STEUERN_NEXT_ENTSOURCE](#job-steuern-next-entsource) - selection of audio source new for entertainment-devices from 2005 on Modus  : Default
- [STATUS_RADIO_SCHALTEN](#job-status-radio-schalten) - ON/OFF status of the radio
- [STATUS_FREQUENZ](#job-status-frequenz) - read frequency frequency in KHz 0 - 999999
- [STEUERN_VOLUMEAUDIO](#job-steuern-volumeaudio) - Volume setting as hex-value from 0x00 to 0x3F
- [STEUERN_AUDIOKANAELE](#job-steuern-audiokanaele) - selects the speaker
- [STATUS_ANT_DC](#job-status-ant-dc) - responds the status of antennea diversity
- [STEUERN_SINUSGENERATOR_EIN](#job-steuern-sinusgenerator-ein) - activates the sinus generator:
- [STEUERN_SINUSGENERATOR_AUS](#job-steuern-sinusgenerator-aus) - stopps the sinus generator

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

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

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
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_RADIO_TASTE_BETAETIGT | int | 0 -&gt; no buttom pressed, 1 -&gt; buttom pressed !! Attention: in case of BM-variants result=0 ! in case of "radio off" only a dummy result |
| STAT_TELEFON_MUTE_AKTIV | int | 0 -&gt; mute not active, 1 -&gt; mute active ! in case of "radio off" only a dummy result |
| STAT_GAL_KURVE | int | Gal-Kurve 1,2,3,4 eingestellt (also possible in state "radio off") |
| STAT_SEEK_SCHWELLE | int | Suchlaufschwelle 1:empfindlich oder 2:unempfindlich !! Attention: in case of non ECE-Varianten result =1 (also possible in state "radio off") |
| STAT_MIT_DSP | int | DSP available or not (also possible in state "radio off") |
| STAT_VF_LAUT_WERT | int | Zahlenwert der VF-Lautstaerke (inkl. Vorzeichen) !! Attention: in case of non ECE-variants result = -0 ! in case of "radio off" only a dummy result |
| STAT_GAL_GESCHW_WERT | int | Zahlenwert Geschw.-abhaengige Lautstaerkenregelung-Frequenz ! in case of "radio off" only a dummy result ! Different procedure for ZIS and BM-variants ! |
| STAT_GAL_GESCHW_EINH | string | Einheit der GAL-Geschwindigkeit (Km/h) |
| STAT_FELDSTAERKE_WERT | int | FELDSTAERKE des empf. Senders (relativ, 0-15) ! in case of "radio off" only a dummy result |
| STAT_RADIO_EIN | int | 1: radio on 0: radio off |
| STAT_AUXADAPTER | int | responds as integer, if aux adapter is present (doesn't work for BM53/BM54) 0: no Aux Adapter present 1: Aux Adapter INTERNALY present 2: Aux Adapter EXTERNALY present |
| STAT_AUXADAPTER_TEXT | string | responds as text, if aux adapter is present (doesn't work for BM53/BM54) kein Aux Adapter Aux Adapter INTERNALY present Aux Adapter EXTERNALY present |
| STAT_ANTENNENDIVERSITY | int | responds as integer, if antennea diversity is present 0: no antenna diversity present 1: antenna diversity present |
| STAT_ANTENNENDIVERSITY_TEXT | string | responds as text, if antennea diversity is present no antenna diversity present antenna diversity present |
| STAT_QUELLE | string | responds as text the active source   |
| STAT_RECEIVE_RDS | int | responds as integer, if RDS signal is recognized 0: no RDS signal recognized 1: RDS signal recognized |
| STAT_RECEIVE_TP | int | responds as integer, if TP broadcast station is recognized 0: no TP broadcast station recognized 1: TP broadcast station recognized |
| STAT_RECEIVE_TA | int | responds as integer, if TA is recognized 0: no TA recognized 1: TA recognized |
| STAT_RECEIVE_REG | int | responds as integer, if regional network is recognized 0: no regional network recognized 1: regional network recognized |
| STAT_RECEIVE_IBOC | int | responds as integer, if IBOC broadcast station is recognized 0: no IBOC broadcast station recognized 1: IBOC broadcast station recognized |
| STAT_RECEIVE_IBOC_HYBRID | int | responds as integer, if digital reception 0: radio reception analog 1: radio reception digital |
| STAT_CD_MD_CDC | int | Value of the digital CD playback quality (0-15) ! in case of source != CD/MD only a dummy result |
| STAT_DISC_IDENT | string | responds as text the disc identifier ! in case of source != CD/MD only a dummy result  |
| STAT_USER_RDS | int | responds as integer, if user-RDS switch 0: RDS switch off 1: RDS switch on |
| STAT_USER_TP | int | responds as integer, if user-TP switch 0: TP switch off 1: TP switch on |
| STAT_USER_PTY | int | responds as integer, if user-PTY switch 0: PTY switch off 1: PTY switch on |
| STAT_USER_REG | int | responds as integer, if user-REG switch 0: REG switch off 1: REG switch on |

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

Switch radio ON/OFF

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG1 | string | EIN/AUS,ON/OFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-herstelldaten-lesen"></a>
### HERSTELLDATEN_LESEN

Herstelldaten lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| SERIEN_NR | string | Seriennummer vom Hersteller |

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

<a id="job-steuern-radio-schalten"></a>
### STEUERN_RADIO_SCHALTEN

Ein-/Ausschalten des Radios KWP2000: $30 InputOutputControlByLocalIdentifier $0A inputOutputLocalIdentifier  - switch radio on or off $07 inputOutputControlParameter - ShortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SCHALTMODUS | string | Switch radio ON/OFF table TSchaltmodi NAME |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| MODUS | string | ON/OFF state |
| JOB_STATUS | string | OKAY, if successful table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ant-qfs"></a>
### STATUS_ANT_QFS

Auslesen des Status Quality Fieldstrength KWP2000: $30 InputOutputControlByLocalIdentifier $12 inputOutputLocalIdentifier  - status QFS $01 inputOutputControlParameter - reportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_QUALITY | int | Quality Bereich: 0..15 (der fuer die AF-Verfolgung massgebliche Wert, entspricht der Summe der gewichteten Einzelfaktoren, 15 = beste Qualitaet) 2-Tuner: Quality = 0 ! |
| STAT_FIELDSTRENGTH | int | Fieldstrength Bereich: 0..15 (4dB-Schritte von 0..60 dBµV) |
| STAT_ANT_PW | int | Antenna Power Supply Bereich: 0 = OFF, 1..15 = ON |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ser-nr-dom-lesen"></a>
### SER_NR_DOM_LESEN

Seriennummer 14-stellig lesen Neu für Entertainment-Komponenten ab 2003 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SER_NR_DOM | string | Seriennummer Gerät 14-stellig |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-rds"></a>
### STEUERN_RDS

Einstellen der RDS Optionen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | int | 0 = AF aus, TP aus 1 = AF aus, TP ein 2 = AF ein, TP aus 3 = AF ein, TP ein |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-folder-and-track-number"></a>
### STEUERN_FOLDER_AND_TRACK_NUMBER

Select folder and track of internal drive

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FOLDER | int | Folder number |
| TRACK | int | Track Number |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-track-number"></a>
### STEUERN_TRACK_NUMBER

select track of internal drive

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TRACK | int | Track Number |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-cd-md-cdc"></a>
### STATUS_CD_MD_CDC

responds drive status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY expected |
| STAT_DRIVE_TYPE | string | active drive CD/MD/CDC |
| STAT_DIGITAL_PLAYBACK_QUALITY | unsigned char | Value of the digital CD playback quality (0-15) ! bei Quelle != CD/MD nur Dummyergebnis |
| STAT_DISC_IDENT | string | responds as text the disc identifier ! bei Quelle != CD/MD nur Dummyergebnis |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-iboc"></a>
### STATUS_IBOC

responds IBOC status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY expected |
| STAT_IBOC_STATION_STATE | unsigned char | setting 0__1 |
| STAT_ANALOG_DIGITAL_STATE | unsigned char | setting 0 analog__1 digital |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rds"></a>
### STATUS_RDS

responds all RDS state of the radio

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY expected |
| STAT_RDS | string | AF/TP Status as string |
| STAT_RDS_VALUE | string | 0 = AF off, TP on 1 = AF off, TP on 2 = AF on, TP off 3 = AF on, TP off |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-next-entsource"></a>
### STATUS_NEXT_ENTSOURCE

responds current audio source

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY expected |
| STAT_ENTSOURCE | string | responds the hex-value of the current audio source  |
| STAT_ENTSOURCE_TEXT | string | responds as text the active source   |

<a id="job-steuern-next-entsource"></a>
### STEUERN_NEXT_ENTSOURCE

selection of audio source new for entertainment-devices from 2005 on Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| QUELLE | string | Quelle |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if successful table JobResult STATUS_TEXT |
| STAT_ENTSOURCE | string | responds the hex-value of the current audio source  |
| STAT_ENTSOURCE_TEXT | string | responds as text the active source  |

<a id="job-status-radio-schalten"></a>
### STATUS_RADIO_SCHALTEN

ON/OFF status of the radio

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if successful table JobResult STATUS_TEXT |
| STAT_RADIO_EIN | int | 1: Radio on 0: Radio off |

<a id="job-status-frequenz"></a>
### STATUS_FREQUENZ

read frequency frequency in KHz 0 - 999999

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-steuern-volumeaudio"></a>
### STEUERN_VOLUMEAUDIO

Volume setting as hex-value from 0x00 to 0x3F

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_LEVEL | string | setting of volume |
| ARG_AUDIO_SIGNAL | int | Default 0 (Entertainment) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-audiokanaele"></a>
### STEUERN_AUDIOKANAELE

selects the speaker

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_KANAL | int | speaker selection (0=all, 1=left front, 2=right front, 32=left back, 64=right back) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ant-dc"></a>
### STATUS_ANT_DC

responds the status of antennea diversity

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| STAT_ANT_DC | string | responds as text, if antennea diversity is present NOK: no antenna diversity present OK:  antenna diversity present |
| STAT_ANT_DC_VALUE | int | responds as integer, if antennea diversity is present 1: no antenna diversity present 0: antenna diversity present |

<a id="job-steuern-sinusgenerator-ein"></a>
### STEUERN_SINUSGENERATOR_EIN

activates the sinus generator:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_FREQUENZ | int | setting of frequency 40-20000 (CID) CD8x 20-17000 MIR, CD62, CD53 R50 0 = sinus generator off Default: 1000 |
| ARG_LEVEL | string | Volume setting as hex-value from 0x00 to 0x3F Default 0x10 |
| ARG_KANAL | int | speaker selection (0=all, 1=left front, 2=right front, 32=left back, 64=right back) Default: 0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-steuern-sinusgenerator-aus"></a>
### STEUERN_SINUSGENERATOR_AUS

stopps the sinus generator

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (93 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (3 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [FORTTEXTE](#table-forttexte) (7 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [DIAGINDEX](#table-diagindex) (83 × 7)
- [LANDVAR](#table-landvar) (6 × 2)
- [TSCHALTMODI](#table-tschaltmodi) (15 × 3)
- [TQUELLEN](#table-tquellen) (50 × 5)
- [TRDSSTATUS](#table-trdsstatus) (4 × 2)
- [TAUDIOVOLUME](#table-taudiovolume) (129 × 2)

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

Dimensions: 93 rows × 2 columns

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
| 0x72 | AISIN AW CO.LTD |
| 0x73 | Shorlock |
| 0x74 | Schrader |
| 0x75 | BERU Electronics GmbH |
| 0x76 | CEL |
| 0x77 | Audio Mobil |
| 0x78 | rd electronic |
| 0x79 | iSYS RTS GmbH |
| 0x80 | Westfalia Automotive GmbH |
| 0x81 | Tyco Electronics |
| 0x82 | Paragon AG |
| 0x83 | IEE S.A |
| 0x84 | TEMIC AUTOMOTIVE of NA |
| 0x85 | AKsys GmbH |
| 0x86 | META System |
| 0x87 | Hülsbeck & Fürst GmbH & Co KG |
| 0x88 | Mann & Hummel Automotive GmbH |
| 0x89 | Brose Fahrzeugteile GmbH & Co |
| 0x90 | Keihin |
| 0x91 | Vimercati S.p.A. |
| 0x92 | CRH |
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

Dimensions: 17 rows × 2 columns

| TEXT | WERT |
| --- | --- |
| ein | 1 |
| aus | 0 |
| ja | 1 |
| nein | 0 |
| auf | 1 |
| ab | 0 |
| an | 1 |
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

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 3 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | nein |
| SAE_CODE | nein |
| F_HLZ | nein |

<a id="table-hdetailstruktur"></a>
### HDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | nein |
| F_LZ | nein |
| F_UWB_ERW | nein |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | nein |
| F_LZ | nein |
| F_UWB_ERW | nein |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 7 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | energy saving mode active |
| 0x01 | error CD-changer interface |
| 0x02 | error power-supply for antenna |
| 0x03 | Internal CD-drive: high temparature |
| 0x04 | Internal CD-drive: hardware problem |
| 0x05 | Internal CD-drive: read-error |
| 0xXY | unbekannter Fehlerort |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

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

Dimensions: 83 rows × 7 columns

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
| 0x45 | CD53 E46 VDO | CD53_E46_VDO | 1 | 1 | 1 | 1 |
| 0x46 | CD53 E85 | CD53_E85 | 1 | 1 | 1 | 1 |
| 0x47 | MIR E85 | MIR_E85 | 1 | 1 | 1 | 1 |
| 0x48 | CD53 CID E85 | CD53_CID_E85 | 1 | 1 | 1 | 1 |
| 0x49 | MD53 CID E85 | MD53_CID_E85 | 1 | 1 | 1 | 1 |
| 0x4A | CD53 R50 VDO | CD53_R50_VDO | 1 | 1 | 1 | 1 |
| 0x50 | CD83 E85 VDO | CD83_E85_VDO | 1 | 1 | 1 | 1 |
| 0x51 | CD83 IBOC VDO | CD83_IBOC_VDO | 1 | 1 | 1 | 1 |
| 0x52 | CID-CD83 E85 VDO | CID-CD83_E85_VDO | 1 | 1 | 1 | 1 |
| 0x53 | CID-CD83 IBOC E85 VDO | CID-CD83_IBOC_E85_VDO | 1 | 1 | 1 | 1 |
| 0x54 | CID-MD83 E85 | CID-MD83_E85 | 1 | 1 | 1 | 1 |
| 0x55 | CID-CD84 E85 | CID-CD84_E85 | 1 | 1 | 1 | 1 |
| 0x56 | CD62 E85 | CD62_E85 | 1 | 1 | 1 | 1 |
| 0x57 | MIR E85 | MIR_E85 | 1 | 1 | 1 | 1 |
| 0x58 | CD53 R50 VDO | CD53_R50_VDO | 1 | 1 | 1 | 1 |
| 0xFF | unknown kind of radio | unknown kind of radio | 0 | 0 | 0 | 0 |

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

<a id="table-tschaltmodi"></a>
### TSCHALTMODI

Dimensions: 15 rows × 3 columns

| NAME | MASKE | TEXT |
| --- | --- | --- |
| aus | 0x0B | Radio aus |
| ein | 0x0C | Radio ein |
| Aus | 0x0B | Radio aus |
| Ein | 0x0C | Radio ein |
| AUS | 0x0B | Radio aus |
| EIN | 0x0C | Radio ein |
| off | 0x0B | Radio aus |
| on | 0x0C | Radio ein |
| Off | 0x0B | Radio aus |
| On | 0x0C | Radio ein |
| OFF | 0x0B | Radio aus |
| ON | 0x0C | Radio ein |
| 0 | 0x0B | Radio aus |
| 1 | 0x0C | Radio ein |
| Fehler | 0xXY | Nicht definiert |

<a id="table-tquellen"></a>
### TQUELLEN

Dimensions: 50 rows × 5 columns

| NUMMER | NAME_RAD | MASKE_RAD | NAME_SGBD | MASKE_SGBD |
| --- | --- | --- | --- | --- |
| 1 | NEXT | 0x00 | NEXT | 0x00 |
| 2 | NEXT | 0x00 | Next | 0x00 |
| 3 | NEXT | 0x00 | next | 0x00 |
| 4 | FM | 0x10 | FM | 0x01 |
| 5 | FM | 0x10 | Fm | 0x01 |
| 6 | FM | 0x10 | fm | 0x01 |
| 7 | WB | 0x11 | WB | 0x06 |
| 8 | WB | 0x11 | Wb | 0x06 |
| 9 | WB | 0x11 | wb | 0x06 |
| 10 | FM/IBOC | 0x14 | IBOC | 0x08 |
| 11 | FM/IBOC | 0x14 | Iboc | 0x08 |
| 12 | FM/IBOC | 0x14 | iboc | 0x08 |
| 13 | AM/MW | 0x20 | AM | 0x02 |
| 14 | AM/MW | 0x20 | Am | 0x02 |
| 15 | AM/MW | 0x20 | am | 0x02 |
| 16 | AM/LW | 0x21 | AM | 0x02 |
| 17 | AM/KW | 0x22 | AM | 0x02 |
| 18 | AM/IBOC | 0x24 | IBOC | 0x08 |
| 19 | CD intern | 0x30 | SCD | 0x03 |
| 20 | CD intern | 0x30 | SCd | 0x03 |
| 21 | CD intern | 0x30 | scd | 0x03 |
| 22 | CDC | 0x40 | CDC | 0x04 |
| 23 | CDC | 0x40 | Cdc | 0x04 |
| 24 | CDC | 0x40 | cdc | 0x04 |
| 25 | MD intern | 0x50 | MD | 0x05 |
| 26 | MD intern | 0x50 | Md | 0x05 |
| 27 | MD intern | 0x50 | md | 0x05 |
| 28 | SDARS | 0x74 | SDARS | 0x07 |
| 29 | SDARS | 0x74 | Sdars | 0x07 |
| 30 | SDARS | 0x74 | sdars | 0x07 |
| 31 | IBOC extern | 0x84 | IBOC | 0x08 |
| 32 | AUX | 0x90 | AUX | 0x09 |
| 33 | AUX | 0x90 | Aux | 0x09 |
| 34 | AUX | 0x90 | aux | 0x09 |
| 35 | DVD | 0xA0 | DVD | 0x0A |
| 36 | DVD | 0xA0 | Dvd | 0x0A |
| 37 | DVD | 0xA0 | dvd | 0x0A |
| 38 | TV | 0xB0 | TV | 0x0B |
| 39 | TV | 0xB0 | Tv | 0x0B |
| 40 | TV | 0xB0 | tv | 0x0B |
| 41 | AV-Aux | 0xC0 | AV-AUX | 0x0D |
| 42 | AV-Aux | 0xC0 | Av-Aux | 0x0D |
| 43 | AV-Aux | 0xC0 | av-aux | 0x0D |
| 44 | DAB | 0xD4 | DAB | 0x0E |
| 45 | DAB | 0xD4 | Dab | 0x0E |
| 46 | DAB | 0xD4 | dab | 0x0E |
| 47 | VIDEOTEXT | 0xFF | VIDEOTEXT | 0x0C |
| 48 | VIDEOTEXT | 0xFF | Videotext | 0x0C |
| 49 | VIDEOTEXT | 0xFF | videotext | 0x0C |
| 50 | NOT AVAILABLE | 0xFF | NOT AVAILABLE | 0xFF |

<a id="table-trdsstatus"></a>
### TRDSSTATUS

Dimensions: 4 rows × 2 columns

| RDS_VALUE | RDS_STRING |
| --- | --- |
| 0 | AF-aus / TP-aus |
| 1 | AF-aus / TP-ein |
| 2 | AF-ein / TP-aus |
| 3 | AF-ein / TP-ein |

<a id="table-taudiovolume"></a>
### TAUDIOVOLUME

Dimensions: 129 rows × 2 columns

| MASKE_LEVEL | MASKE_RAD |
| --- | --- |
| 0x00 | 0x00 |
| 0 | 0x00 |
| 0x01 | 0x01 |
| 1 | 0x01 |
| 0x02 | 0x02 |
| 2 | 0x02 |
| 0x03 | 0x03 |
| 3 | 0x03 |
| 0x04 | 0x04 |
| 4 | 0x04 |
| 0x05 | 0x05 |
| 5 | 0x05 |
| 0x06 | 0x06 |
| 6 | 0x06 |
| 0x07 | 0x07 |
| 7 | 0x07 |
| 0x08 | 0x08 |
| 8 | 0x08 |
| 0x09 | 0x09 |
| 9 | 0x09 |
| 0x0A | 0x10 |
| 10 | 0x10 |
| 0x0B | 0x11 |
| 11 | 0x11 |
| 0x0C | 0x12 |
| 12 | 0x12 |
| 0x0D | 0x13 |
| 13 | 0x13 |
| 0x0E | 0x14 |
| 14 | 0x14 |
| 0x0F | 0x15 |
| 15 | 0x15 |
| 0x10 | 0x16 |
| 16 | 0x16 |
| 0x11 | 0x17 |
| 17 | 0x17 |
| 0x12 | 0x18 |
| 18 | 0x18 |
| 0x13 | 0x19 |
| 19 | 0x19 |
| 0x14 | 0x20 |
| 20 | 0x20 |
| 0x15 | 0x21 |
| 21 | 0x21 |
| 0x16 | 0x22 |
| 22 | 0x22 |
| 0x17 | 0x23 |
| 23 | 0x23 |
| 0x18 | 0x24 |
| 24 | 0x24 |
| 0x19 | 0x25 |
| 25 | 0x25 |
| 0x1A | 0x26 |
| 26 | 0x26 |
| 0x1B | 0x27 |
| 27 | 0x27 |
| 0x1C | 0x28 |
| 28 | 0x28 |
| 0x1D | 0x29 |
| 29 | 0x29 |
| 0x1E | 0x30 |
| 30 | 0x30 |
| 0x1F | 0x31 |
| 31 | 0x31 |
| 0x20 | 0x32 |
| 32 | 0x32 |
| 0x21 | 0x33 |
| 33 | 0x33 |
| 0x22 | 0x34 |
| 34 | 0x34 |
| 0x23 | 0x35 |
| 35 | 0x35 |
| 0x24 | 0x36 |
| 36 | 0x36 |
| 0x25 | 0x37 |
| 37 | 0x37 |
| 0x26 | 0x38 |
| 38 | 0x38 |
| 0x27 | 0x39 |
| 39 | 0x39 |
| 0x28 | 0x40 |
| 40 | 0x40 |
| 0x29 | 0x41 |
| 41 | 0x41 |
| 0x2A | 0x42 |
| 42 | 0x42 |
| 0x2B | 0x43 |
| 43 | 0x43 |
| 0x2C | 0x44 |
| 44 | 0x44 |
| 0x2D | 0x45 |
| 45 | 0x45 |
| 0x2E | 0x46 |
| 46 | 0x46 |
| 0x2F | 0x47 |
| 47 | 0x47 |
| 0x30 | 0x48 |
| 48 | 0x48 |
| 0x31 | 0x49 |
| 49 | 0x49 |
| 0x32 | 0x50 |
| 50 | 0x50 |
| 0x33 | 0x51 |
| 51 | 0x51 |
| 0x34 | 0x52 |
| 52 | 0x52 |
| 0x35 | 0x53 |
| 53 | 0x53 |
| 0x36 | 0x54 |
| 54 | 0x54 |
| 0x37 | 0x55 |
| 55 | 0x55 |
| 0x38 | 0x56 |
| 56 | 0x56 |
| 0x39 | 0x57 |
| 57 | 0x57 |
| 0x3A | 0x58 |
| 58 | 0x58 |
| 0x3B | 0x59 |
| 59 | 0x59 |
| 0x3C | 0x60 |
| 60 | 0x60 |
| 0x3D | 0x61 |
| 61 | 0x61 |
| 0x3E | 0x62 |
| 62 | 0x62 |
| 0x3F | 0x63 |
| 63 | 0x63 |
| 0xFF | 0xFF |
