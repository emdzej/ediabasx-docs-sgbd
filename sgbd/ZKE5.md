# ZKE5.prg

- Jobs: [30](#jobs)
- Tables: [9](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Zentrale Karosserie-Elektronik V  fuer E46 |
| ORIGIN | BMW TI-430 Gerd Huber |
| REVISION | 1.28 |
| AUTHOR | BMW TI-430 Gerd Huber, BMW MK-4 St. Frank, BMW TI-431 Lothar Dennert,EE-51 Alex Franckenstein |
| COMMENT | Ansteuern nur bei entsichertem Fahrzeug! |
| PACKAGE | 0.12 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [C_CI_LESEN](#job-c-ci-lesen) - Codierindex lesen Standard Codierjob
- [C_FG_LESEN](#job-c-fg-lesen) - Fahrgestellnummer lesen Standard Codierjob
- [C_FG_SCHREIBEN](#job-c-fg-schreiben) - Fahrgestellnummer schreiben Standard Codierjob
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Fahrgestellnummer schreiben und ruecklesen Standard Codierjob
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung / Kommunikationsparameter fuer Grundmodul V automatischer Aufruf beim ersten Zugriff auf die SGBD
- [IDENT](#job-ident) - Ident-Daten fuer Grundmodul V
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose Sonderfall: Loeschdatum (KW/Jahr) integriert !
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen Sonderfall: Loeschdatum (KW/Jahr) integriert !
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [HERSTELLDATEN_LESEN](#job-herstelldaten-lesen) - Auslesen der Herstelldaten
- [STATUS_DIGITAL](#job-status-digital) - Status der Digitalsignale des GM V (Ein-/Ausgaenge) Der Wertebereich ist bei fast allen Results: Bereich: 0, wenn FALSE / 1, wenn TRUE Andernfalls ist der Bereich gezielt spezifiziert.
- [STATUS_EKS](#job-status-eks) - Status bzgl. Einklemmschutz bei Grundmodul V
- [STATUS_ANALOG](#job-status-analog) - Status der Analogsignale des GM V
- [STEUERN_DIGITAL](#job-steuern-digital) - Ansteuern eines digitalen Ein- oder Ausgangs v. GM5 ! erlaubte Namen des Arguments 'ORT' ueber Tool XTRACT.exe ! Aufruf 'XTRACT [-F] ZKE5.prg'
- [COD_LESEN](#job-cod-lesen) - Auslesen der Codierdaten des GM V (Block 0) (Block 1 mit Parameter '1')
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen Info-Speicher ist im Aufbau analog zum Fehlerspeicher Low-Konzept nach Lastenheft Codierung/Diagnose
- [IS_LESEN_ZV](#job-is-lesen-zv) - Infospeicher lesen / Sonderfall: ZV-Ringspeicher Analog zu FS_LESEN gibt es mehrere (15+1) Ergebnis-Saetze Im Satz  1 steht die Information zum letzten ZV-Befehl. Im Satz 15 steht die aelteste Information. Im Satz 16 steht das Ergebnis JOB_STATUS.
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen des internen Speichers der ZKE V Als Argumente werden die Anzahl und die Adresse der Datenbytes uebergeben.
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Speicherinhalt lesen
- [STATUS_KEY_MEMORY](#job-status-key-memory) - Auslesen der Nummer des Funkschluessels, mit dem zuletzt entriegelt wurde
- [STATUS_FUNKSCHLUESSEL](#job-status-funkschluessel) - !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!! !!!        A C H T U N G         !!! !!! Dieser Job ist abhaengig von !!! !!! der Softwarenummer des SG's. !!! !!! Es liegen derzeit nur Daten  !!! !!! fuer folgende SW-Nr. vor :   !!! !!! 1.1, 1.2, 1.4, 1.5, 1.6, 2.0 !!! !!! 3.0, 3.1, 3.3                     !!! !!! bzw. für folgende Diag.Index !!! !!! 41, 51, 42, 52               !!! !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!! Auslesen der Funkschluesseldaten aus dem internen Speicher der ZKE V
- [STEUERN_IB_AUS](#job-steuern-ib-aus) - dauerhaftes Ausschalten der Innenbeleuchtung Das Innenlicht kann nur manuell durch Druecken des Tasters wieder aktiviert werden.
- [FS_LESEN_DWA](#job-fs-lesen-dwa) - Fehlerspeicher lesen (nur DWA-Fehler) Sonderjob für Hr. Mühlbauer, TR-443
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

<a id="job-c-ci-lesen"></a>
### C_CI_LESEN

Codierindex lesen Standard Codierjob

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_COD_INDEX | int | Codier-Index |
| _TELEGRAMM | binary | Antworttelegramm |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Fahrgestellnummer lesen Standard Codierjob

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FG_NR | string | die letzten vier Stellen der Fahrgestellnummer |
| _TELEGRAMM | binary | Antworttelegramm |

<a id="job-c-fg-schreiben"></a>
### C_FG_SCHREIBEN

Fahrgestellnummer schreiben Standard Codierjob

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TELEGRAMM | binary | Antworttelegramm |

<a id="job-c-fg-auftrag"></a>
### C_FG_AUFTRAG

Fahrgestellnummer schreiben und ruecklesen Standard Codierjob

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TELEGRAMM | binary | Antworttelegramm |

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung / Kommunikationsparameter fuer Grundmodul V automatischer Aufruf beim ersten Zugriff auf die SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer Grundmodul V

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
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
| ID_VARIANTE | string | Variante des Grundmoduls: ZKE5_LOW, ZKE5_HIGH, ZKE5_LOW_LIN, ZKE5_HIGH_LIN, ZKE? |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose Sonderfall: Loeschdatum (KW/Jahr) integriert !

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | int | Index fuer Fehlerort momentan identisch Fehlerbyte |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_HFK | int | Fehlerhaeufigkeit Bereich: 0 - 31 |
| F_ART_ANZ | int | Anzahl der Fehlerarten Bereich: immer 1 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Bereich: immer 0 |
| F_ART1_NR | int | 1. (einzige) Fehlerart Bereich: 0, 1 |
| F_ART1_TEXT | string | 1. (einzige) Fehlerart als Text table FArtTexte ARTTEXT |
| F_LOESCHDATUM_KW | int | Loeschdatum des Fehlerspeichers (KW) |
| F_LOESCHDATUM_JAHR | int | Loeschdatum des Fehlerspeichers (Jahr) |
| _TEL_ANTWORT0 | binary | 0. Hex-Antwort von SG |
| _TEL_ANTWORT1 | binary | 1. Hex-Antwort von SG |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen Sonderfall: Loeschdatum (KW/Jahr) integriert !

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LOESCHDATUM_KW | int | aktuelle Kalenderwoche beim Loeschen des Fehlerspeichers |
| LOESCHDATUM_JAHR | int | aktuelles Kalenderjahr beim Loeschen des Fehlerspeichers |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| FG_ZIFFERN | string | die letzten vier Stellen der Fahrgestellnummer |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-herstelldaten-lesen"></a>
### HERSTELLDATEN_LESEN

Auslesen der Herstelldaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE4 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE5 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE6 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE7 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE8 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE9 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE10 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

Status der Digitalsignale des GM V (Ein-/Ausgaenge) Der Wertebereich ist bei fast allen Results: Bereich: 0, wenn FALSE / 1, wenn TRUE Andernfalls ist der Bereich gezielt spezifiziert.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SIB | int | Eingang: Schalter Innenbeleuchtung |
| STAT_TOEHK | int | Eingang: Taster Entriegeln Heckklappe |
| STAT_TZV | int | Eingang: Taster Centerlock |
| STAT_TOEHS | int | Eingang: Taster Entriegeln Heckscheibe |
| STAT_TOEHKI | int | Eingang: Taster Entriegeln Heckklappe innen |
| STAT_HKK | int | Eingang: Heckklappen-Kontakt |
| STAT_ERHK | int | Eingang: Entriegeln Heckklappe |
| STAT_RSK | int | Eingang: Rueckstellkontakt Wischer |
| STAT_SFFA | int | Eingang: Schalter Fensterheber Fahrer auf |
| STAT_SFFZ | int | Eingang: Schalter Fensterheber Fahrer zu |
| STAT_SFBA | int | Eingang: Schalter Fensterheber Beifahrer auf |
| STAT_SFBZ | int | Eingang: Schalter Fensterheber Beifahrer zu |
| STAT_SW2 | int | Eingang: Wischerschalter 2 |
| STAT_KISI | int | Eingang: Kindersicherung Fensterheber hinten |
| STAT_MHK | int | Eingang: Motorhauben-Kontakt |
| STAT_HFK | int | Eingang: Handschuhfach-Kontakt |
| STAT_HSK | int | Eingang: Heckscheiben-Kontakt |
| STAT_INRS | int | Eingang: Innenraumschutz |
| STAT_NG | int | Eingang: Neigungsgeber |
| STAT_INRS2 | int | Eingang: Innenraumschutz 2 |
| STAT_KL_R_HW | int | Eingang: Klemme R (Hardware) |
| STAT_REE1 | int | Eingang: Reserve 1 |
| STAT_REE3 | int | Eingang: Reserve 3 |
| STAT_CS | int | Eingang: Crash-Sensor |
| STAT_KL30BTS | int | Eingang: Versorgung fuer IB, WP, MERHK und VA |
| STAT_KL30ZV | int | Eingang: Versorgung fuer Zentralverriegelung |
| STAT_KL30FHV | int | Eingang: Versorgung fuer Klemme 30 Fensterheber vorne |
| STAT_SFFHA | int | Eingang: Schalter Fensterheber Fahrer hinten auf |
| STAT_SFFHZ | int | Eingang: Schalter Fensterheber Fahrer hinten zu |
| STAT_SFBHA | int | Eingang: Schalter Fensterheber Beifahrer hinten auf |
| STAT_SFBHZ | int | Eingang: Schalter Fensterheber Beifahrer hinten zu |
| STAT_SFFHA2 | int | Eingang: Schalter 2 Fensterheber Fahrer hinten auf |
| STAT_SFFHZ2 | int | Eingang: Schalter 2 Fensterheber Fahrer hinten zu |
| STAT_SFBHA2 | int | Eingang: Schalter 2 Fensterheber Beifahrer hinten auf |
| STAT_SFBHZ2 | int | Eingang: Schalter 2 Fensterheber Beifahrer hinten zu |
| STAT_REE2 | int | Eingang: Reserve 2 |
| STAT_VRHK | int | Eingang: Verriegeln Heckklappe |
| STAT_SWA | int | Eingang: Schalter Waschen |
| STAT_SW1 | int | Eingang: Schalter Wischerstufe 1 |
| STAT_DMVR | int | Eingang: Diagnose Verriegeln |
| STAT_DMER | int | Eingang: Diagnose Entriegeln |
| STAT_DMZS | int | Eingang: Diagnose Sichern |
| STAT_DMVRFT | int | Eingang: Diagnose Verriegeln Fahrertuer |
| STAT_TKFT | int | Eingang: Tuerkontakt Fahrertuer |
| STAT_TKBT | int | Eingang: Tuerkontakt Beifahrertuer |
| STAT_TKFH | int | Eingang: Tuerkontakt Fahrertuer hinten |
| STAT_TKBH | int | Eingang: Tuerkontakt Beifahrertuer hinten |
| STAT_VRFT | int | Eingang: Verriegeln Fahrertuer |
| STAT_ERFT | int | Eingang: Entriegeln Fahrertuer |
| STAT_VRBT | int | Eingang: Verriegeln Beifahrertuer |
| STAT_ERBT | int | Eingang: Entriegeln Beifahrertuer |
| STAT_DSTDWA | int | Eingang: Diagnose Status DWA |
| STAT_FZV | int | Eingang: Funkfernbedienung Zentralverriegelung |
| STAT_DERHK | int | Eingang: Diagnose Entriegeln Heckklappe |
| STAT_DWP | int | Eingang: Diagnose Waschpumpe |
| STAT_DVA | int | Eingang: Diagnose Verbraucherabschaltung |
| STAT_DIB | int | Eingang: Diagnose Innenbeleuchtung |
| STAT_SFF | int | Schalter Fensterheber Fahrer moegliche Werte: 0=AUS, 1=AUF, 2=ZU, 3=AUTOMATIK |
| STAT_SFF_TEXT | string | Schalter Fensterheber Fahrer moegliche Texte: AUS, AUF, ZU, AUTOMATIK |
| STAT_SFB | int | Schalter Fensterheber Beifahrer moegliche Werte: 0=AUS, 1=AUF, 2=ZU, 3=AUTOMATIK |
| STAT_SFB_TEXT | string | Schalter Fensterheber Beifahrer moegliche Texte: AUS, AUF, ZU, AUTOMATIK |
| STAT_SFFH | int | Schalter Fensterheber Fahrer hinten moegliche Werte: 0=AUS, 1=AUF, 2=ZU, 3=AUTOMATIK |
| STAT_SFFH_TEXT | string | Schalter Fensterheber Fahrer hinten moegliche Texte: AUS, AUF, ZU, AUTOMATIK |
| STAT_SFBH | int | Schalter Fensterheber Beifahrer hinten moegliche Werte: 0=AUS, 1=AUF, 2=ZU, 3=AUTOMATIK |
| STAT_SFBH_TEXT | string | Schalter Fensterheber Beifahrer hinten moegliche Texte: AUS, AUF, ZU, AUTOMATIK |
| STAT_SFFH2 | int | Schalter 2 Fensterheber Fahrer hinten moegliche Werte: 0=AUS, 1=AUF, 2=ZU, 3=AUTOMATIK |
| STAT_SFFH2_TEXT | string | Schalter 2 Fensterheber Fahrer hinten moegliche Texte: AUS, AUF, ZU, AUTOMATIK |
| STAT_SFBH2 | int | Schalter 2 Fensterheber Beifahrer hinten moegliche Werte: 0=AUS, 1=AUF, 2=ZU, 3=AUTOMATIK |
| STAT_SFBH2_TEXT | string | Schalter 2 Fensterheber Beifahrer hinten moegliche Texte: AUS, AUF, ZU, AUTOMATIK |
| STAT_SW | int | Schalter Wischer moegliche Werte: 0=AUS, 1=INTERVALL, 2=STUFE1, 3=STUFE2 |
| STAT_SW_TEXT | string | Schalter Wischer moegliche Texte: AUS, INTERVALL, STUFE1, STUFE2 |
| STAT_VERFT | int | Verriegeln / Entriegeln Fahrertuer moegliche Werte: 0=RUHE, 1=VERRIEGELN, 2=ENTRIEGELN, 3=FEHLER |
| STAT_VERFT_TEXT | string | Verriegeln / Entriegeln Fahrertuer moegliche Texte: RUHE, ENTRIEGELN, VERRIEGELN, FEHLER |
| STAT_VERBT | int | Verriegeln / Entriegeln Beifahrertuer moegliche Werte: 0=RUHE, 1=VERRIEGELN, 2=ENTRIEGELN, 3=FEHLER |
| STAT_VERBT_TEXT | string | Verriegeln / Entriegeln Beifahrertuer moegliche Texte: RUHE, ENTRIEGELN, VERRIEGELN, FEHLER |
| STAT_MFFHA | int | Ausgang: Motor Fensterheber Fahrer hinten auf |
| STAT_MFFHZ | int | Ausgang: Motor Fensterheber Fahrer hinten zu |
| STAT_MFBHZ | int | Ausgang: Motor Fensterheber Beifahrer hinten zu |
| STAT_MFBHA | int | Ausgang: Motor Fensterheber Beifahrer hinten auf |
| STAT_MER | int | Ausgang: Motor Entriegeln |
| STAT_MZS | int | Ausgang: Motor Sichern |
| STAT_MVRFT | int | Ausgang: Motor Verriegeln Fahrertuer |
| STAT_REA3 | int | Ausgang: Reserve 3 |
| STAT_WI1 | int | Ausgang: Wischerrelais Stufe 1 |
| STAT_WI2 | int | Ausgang: Wischerrelais Stufe 2 |
| STAT_SRA | int | Ausgang: Relais Scheinwerferreinigung |
| STAT_RERHS | int | Ausgang: Relais Entriegeln Heckscheibe |
| STAT_SIRENE | int | Ausgang: Sirene bzw. Alarmhorn |
| STAT_DWAL | int | Ausgang: DWA-LED |
| STAT_MVR | int | Ausgang: Motor Verriegeln |
| STAT_MFFA | int | Ausgang: Motor Fensterheber Fahrer auf |
| STAT_MFFZ | int | Ausgang: Motor Fensterheber Fahrer zu |
| STAT_MFBA | int | Ausgang: Motor Fensterheber Beifahrer auf |
| STAT_MFBZ | int | Ausgang: Motor Fensterheber Beifahrer zu |
| STAT_STDWA | int | Ausgang: Status Diebstahlwarnanlage |
| STAT_ENEKS | int | Ausgang: Einklemmschutz-Versorgung aktiv |
| STAT_ENPU | int | Ausgang: Enable Pull Up |
| STAT_REA1 | int | Ausgang: Reserve 1 |
| STAT_REA2 | int | Ausgang: Reserve 2 |
| STAT_ENANGR1 | int | Ausgang: Enable Analogsignale Gruppe 1 |
| STAT_VA2 | int | Ausgang: Verbraucherabschaltung 2 EIN |
| STAT_IB | int | Ausgang: Innenbeleuchtung |
| STAT_VA | int | Ausgang: Verbraucherabschaltung EIN |
| STAT_WP | int | Ausgang: Waschpumpe |
| STAT_MERHK | int | Ausgang: Motor Entriegeln Heckklappe |
| STAT_CVM_FA | int | K-Bus: Anforderung von CVM: Fenster auf |
| STAT_CVM_FZ | int | K-Bus: Anforderung von CVM: Fenster zu |
| STAT_CVM_VKA | int | K-Bus: Anforderung von CVM: Verdeckklappe Auffahren |
| STAT_CVM_VKZ | int | K-Bus: Anforderung von CVM: Verdeckklappe Zufahren |
| STAT_KL_R | int | K-Bus: Klemme R |
| STAT_KL15 | int | K-Bus: Klemme 15 |
| STAT_KL58 | int | K-Bus: Klemme 58 |
| STAT_EWS_FREE | int | K-Bus: EWS freigeschaltet |
| STAT_EWS_KEY | int | K-Bus: gueltiger Schluessel steckt |
| STAT_RDC | int | K-Bus: Reifenstechen aktiv |
| STAT_CSMODE | int | K-Bus: System im Crash-Mode |
| STAT_DIAGMOD | int | K-Bus: System im Diagnosemode |
| STAT_ZV | int | K-Bus: ZV ist verriegelt |
| STAT_ZS | int | K-Bus: ZV ist gesichert |
| STAT_SER | int | K-Bus: Selektiv entriegelt |
| STAT_WB | int | K-Bus: Crash-Warnblinken, DWA-Quittierung |
| STAT_OA | int | K-Bus: Optischer Alarm |
| STAT_ES | int | K-Bus: ZV ist entsichert |
| STAT_QFFZ | int | K-Bus: Quittierung Fensterheber Fahrer ist zu |
| STAT_QFBZ | int | K-Bus: Quittierung Fensterheber Beifahrer ist zu |
| STAT_QFFHZ | int | K-Bus: Quittierung Fensterheber Fahrer hinten ist zu |
| STAT_QFBHZ | int | K-Bus: Quittierung Fensterheber Beifahrer hinten ist zu |
| STAT_SOFTON | int | K-Bus: IB-Lampe ist an oder Ansteuerung laeuft |
| STAT_KB_FSHD | int | K-Bus: Schiebe-Hebedach-Handbedienung |
| STAT_KB_KOE | int | K-Bus: Komfortfunktion Oeffnen |
| STAT_KB_KS | int | K-Bus: Komfortfunktion Schliessen |
| STAT_FB_BAT | int | K-Bus: Fernbedien-Sender Batterie schwach |
| STAT_FB_NR | int | K-Bus: Gueltige FB-Nr. liegt vor (Personalisierung) |
| STAT_FB_SEND_L | int | K-Bus: Sender-Nr. Low-Bit, bei dem zuletzt ER-Taste gedrueckt |
| STAT_FB_SEND_H | int | K-Bus: Sender-Nr. High-Bit, bei dem zuletzt ER-Taste gedrueckt |
| STAT_FB_VR | int | K-Bus: VR-Taste gedrueckt |
| STAT_FB_ER | int | K-Bus: ER-Taste gedrueckt |
| STAT_FB_HK | int | K-Bus: HK-Taste gedrueckt |
| STAT_KB_VKER | int | K-Bus: Status Verdeckklappe entriegelt |
| STAT_SEND_L | int | Eingang Funk: Sender-Nummer (Low-Bit) |
| STAT_SEND_H | int | Eingang Funk: Sender-Nummer (High-Bit) |
| STAT_FZVSIG | int | Eingang Funk: Funksignal empfangen |
| STAT_FZVKEY | int | Eingang Funk: Funkschluesselsignale empfangen |
| STAT_TASTE1 | int | Eingang Funk: Fernbedienung Taste 1 betaetigt |
| STAT_TASTE2 | int | Eingang Funk: Fernbedienung Taste 2 betaetigt |
| STAT_TASTE3 | int | Eingang Funk: Fernbedienung Taste 3 betaetigt |
| STAT_FUINIT | int | Eingang Funk: Initialisierung Funkschluessel moeglich |
| STAT_LOBAT1 | int | Eingang Funk: Schluessel Sender 1 Batterie schwach |
| STAT_LOBAT2 | int | Eingang Funk: Schluessel Sender 2 Batterie schwach |
| STAT_LOBAT3 | int | Eingang Funk: Schluessel Sender 3 Batterie schwach |
| STAT_LOBAT4 | int | Eingang Funk: Schluessel Sender 4 Batterie schwach |
| STAT_FSIB | int | Eingang Funk: FS IB-Befehl |
| STAT_FSAHK | int | Eingang Funk: Heckklappentaste Entriegeln Heckklappe |
| STAT_ZV1FS | int | Eingang Funk: ZV-Befehl entriegeln |
| STAT_ZV0FS | int | Eingang Funk: ZV-Befehl verriegeln |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-eks"></a>
### STATUS_EKS

Status bzgl. Einklemmschutz bei Grundmodul V

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_EKSFT | int | Einklemmschutz Fahrertuer moegliche Werte: 0=GEDRUECKT, 1=NICHT_GEDRUECKT, 2=UNTERBRECHUNG |
| STAT_EKSFT_TEXT | string | Einklemmschutz Fahrertuer moegliche Texte: GEDRUECKT, NICHT_GEDRUECKT, UNTERBRECHUNG |
| STAT_EKSBT | int | Einklemmschutz Beifahrertuer moegliche Werte: 0=GEDRUECKT, 1=NICHT_GEDRUECKT, 2=UNTERBRECHUNG |
| STAT_EKSBT_TEXT | string | Einklemmschutz Beifahrertuer moegliche Texte: GEDRUECKT, NICHT_GEDRUECKT, UNTERBRECHUNG |
| STAT_EKSFH | int | Einklemmschutz Fahrertuer hinten moegliche Werte: 0=GEDRUECKT, 1=NICHT_GEDRUECKT, 2=UNTERBRECHUNG |
| STAT_EKSFH_TEXT | string | Einklemmschutz Fahrertuer hinten moegliche Texte: GEDRUECKT, NICHT_GEDRUECKT, UNTERBRECHUNG |
| STAT_EKSBH | int | Einklemmschutz Beifahrertuer hinten moegliche Werte: 0=GEDRUECKT, 1=NICHT_GEDRUECKT, 2=UNTERBRECHUNG |
| STAT_EKSBH_TEXT | string | Einklemmschutz Beifahrertuer hinten moegliche Texte: GEDRUECKT, NICHT_GEDRUECKT, UNTERBRECHUNG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog"></a>
### STATUS_ANALOG

Status der Analogsignale des GM V

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_V30E_WERT | real | Spannung KL30E Bereich: 0 bis 25,5 [V] |
| STAT_V30P_WERT | real | Spannung KL30PULL Bereich: 0 bis 25,5 [V] |
| STAT_IFFH_WERT | real | Strom Fensterheber Fahrer hinten Bereich: 0 bis 61,2 [A] |
| STAT_IFBH_WERT | real | Strom Fensterheber Beifahrer hinten Bereich: 0 bis 61,2 [A] |
| STAT_IFFHMAX_WERT | real | Anlaufstrom Fensterheber Fahrer hinten Bereich: 0 bis 61,2 [A] |
| STAT_IFBHMAX_WERT | real | Anlaufstrom Fensterheber Beifahrer hinten Bereich: 0 bis 61,2 [A] |
| STAT_IFHF_WERT | real | Strom Fensterheber Fahrer Bereich: 0 bis 61,2 [A] |
| STAT_IFHB_WERT | real | Strom Fensterheber Beifahrer Bereich: 0 bis 61,2 [A] |
| STAT_IFHFMAX_WERT | real | Anlaufstrom Fensterheber Fahrer Bereich: 0 bis 61,2 [A] |
| STAT_IFHBMAX_WERT | real | Anlaufstrom Fensterheber Beifahrer Bereich: 0 bis 61,2 [A] |
| STAT_SWINT_WERT | real | Wischer-Intervall-Potistufenspannung Bereich: 0 bis 25,5 [V] |
| STAT_I_ULQ_WERT | real | Summenstrom IC17 (ULQ2003) Bereich: 0 bis 5,100 [A] |
| STAT_SPANNUNG_EINH | string | Einheit: Volt |
| STAT_STROM_EINH | string | Einheit: Ampere |
| STAT_KMH_WERT | int | Geschwindigkeit ueber KBUS Bereich: 0 bis 510 [km/h] |
| STAT_KMH_EINH | string | Einheit: km/h |
| STAT_GKL_WERT | int | Geschwindigkeitsklasse fuer Wisch/Wasch Bereich: 0 bis 5 |
| STAT_GKL_EINH | string | Einheit: 1 |
| STAT_POTI_STUFE_WERT | int | Potentiometer-Stufe Wischer-Intervall-Stufenschalter Bereich: 0 bis 5 |
| STAT_POTI_STUFE_EINH | string | Einheit: 1 |
| STAT_EKSFT_WERT | int | Einklemmschutz-Spannungs-Verhaeltnis Fahrertuer Bereich: 0 bis 255 |
| STAT_EKSFT_EINH | string | Einheit: 1 |
| STAT_EKSBT_WERT | int | Einklemmschutz-Spannungs-Verhaeltnis Beifahrertuer Bereich: 0 bis 255 |
| STAT_EKSBT_EINH | string | Einheit: 1 |
| STAT_EKSFH_WERT | int | Einklemmschutz-Spannungs-Verhaeltnis Fahrertuer hinten Bereich: 0 bis 255 |
| STAT_EKSFH_EINH | string | Einheit: 1 |
| STAT_EKSBH_WERT | int | Einklemmschutz-Spannungs-Verhaeltnis Beifahrertuer hinten Bereich: 0 bis 255 |
| STAT_EKSBH_EINH | string | Einheit: 1 |
| STAT_V_KL30_EKS_WERT | real | Spannung Klemme 30 für Einklemmschutz Bereich: 0 bis 25,5 [V] |
| STAT_V_VA1_WERT | real | Spannung Verbraucherabschaltung 1 Bereich: 0 bis 25,5 [V] |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

Ansteuern eines digitalen Ein- oder Ausgangs v. GM5 ! erlaubte Namen des Arguments 'ORT' ueber Tool XTRACT.exe ! Aufruf 'XTRACT [-F] ZKE5.prg'

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | gewuenschte Komponente table BITS NAME TEXT |
| EIN | int | '1', wenn einschalten / '0', wenn ausschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-cod-lesen"></a>
### COD_LESEN

Auslesen der Codierdaten des GM V (Block 0) (Block 1 mit Parameter '1')

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK | int | Blocknummer 0 bis n |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| COD_MIT_DWA | int | Diebstahlwarnanlage |
| COD_MIT_AUST | int | Elektrische Ausstellfenster hinten |
| COD_MIT_FH_V | int | Fensterheber vorne |
| COD_MIT_FH_H | int | Fensterheber hinten |
| COD_MIT_FB | int | Funkfernbedienung |
| COD_MIT_FIS1 | int | Funkinnenraumschutz 1 |
| COD_MIT_FIS2 | int | Funkinnenraumschutz 2 |
| COD_MIT_IR | int | Infrarot-Fernbedienung |
| COD_MIT_NG | int | Neigungsgeber |
| COD_MIT_SRA | int | Scheinwerferreinigungsanlage |
| COD_OHNE_SWPOTI | int | Wischer: ohne Wischer-Poti |
| COD_OHNE_RSCHALT | int | Wischer: nicht rueckschalten im Stand |
| COD_MIT_AIC | int | Wischer: mit Regensensor |
| COD_OHNE_FH_NACH_KLR | int | Fensterheber1: FH deaktiv nach Kl.R aus |
| COD_OHNE_FH_TUER_AUF | int | Fensterheber1: FH deaktiv nach Tuere auf |
| COD_MIT_FH_TUER_VO | int | Fensterheber1: FH aktiv bei Tuere vorne offen |
| COD_MIT_EKS_VO | int | Fensterheber2: FH mit EKS vorne |
| COD_MIT_EKS_HI | int | Fensterheber2: FH mit EKS hinten |
| COD_TIPA_FT | int | FH Tippfunktionen: Tipp auf FT moeglich |
| COD_TIPZ_FT | int | FH Tippfunktionen: Tipp zu FT moeglich |
| COD_TIPA_BT | int | FH Tippfunktionen: Tipp auf BT moeglich |
| COD_TIPZ_BT | int | FH Tippfunktionen: Tipp zu BT moeglich |
| COD_TIPA_HI | int | FH Tippfunktionen: Tipp auf hinten moeglich |
| COD_TIPZ_HI | int | FH Tippfunktionen: Tipp zu hinten moeglich |
| COD_TIPA_ZS | int | FH Tippfunktionen: Tipp auf Zentralschalter moeglich |
| COD_TIPZ_ZS | int | FH Tippfunktionen: Tipp zu Zentralschalter moeglich |
| COD_SEL_ER | int | ZV: mit selektiv Entriegeln |
| COD_AUT_VR4KMH | int | ZV: mit automatischem Verriegeln ab 4km/h |
| COD_AUT_VR2MIN | int | ZV: mit automatischem Verriegeln ab 2min |
| COD_OHNE_IB_ENTRIEGELN_UEBER_SCHLOSS | int | IB: Nicht einschalten bei Entriegeln ueber Schloss |
| COD_OHNE_IB_KLR_AUS_NACH_KL58 | int | IB: Nicht Ein bei Kl. R deaktivieren, Kl. 58 war aktiv |
| COD_MIT_SCHARF_NUR_FB | int | DWA Funktionen: Schaerfen/Entschaerfen nur ueber Fernbedienung |
| COD_MIT_DAUERTON | int | DWA Funktionen: Sirene Dauerton (0=Intervall) |
| COD_MIT_HEULTON | int | DWA Funktionen: Sirene Heulton (US) |
| COD_MIT_OPTISCHER_ALARM_WARNBLINKER | int | DWA Funktionen: mit optischem Alarm ueber Warnblinker |
| COD_MIT_OPTISCHER_ALARM_ABBLENDLICHT | int | DWA Funktionen: mit optischem Alarm ueber Abblendlicht |
| COD_MIT_OPTISCHER_ALARM_FERNLICHT | int | DWA Funktionen: mit optischem Alarm ueber Fernlicht |
| COD_MIT_KOMFORTOEFFNEN | int | FB Funktionen: mit Komfortoeffnung |
| COD_MIT_KOMFORTSCHLIESSEN | int | FB Funktionen: mit Komfortschliessung |
| COD_DATEN | binary | alle Codierdaten als reine Datenbytes |
| DATENSICHERUNG_BLOCK_0 | string | Datensicherungsbyte fuer Block 0 |
| DATENSICHERUNG_BLOCK_1 | string | Datensicherungsbyte fuer Block 1 |
| _TEL_ANTWORT | binary |  |

<a id="job-is-lesen"></a>
### IS_LESEN

Infospeicher lesen Info-Speicher ist im Aufbau analog zum Fehlerspeicher Low-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_HEX_CODE | binary | Infodaten pro Fehler als Hexcode |
| F_ORT_NR | int | Index fuer Infoort momentan identisch Infobyte |
| F_ORT_TEXT | string | Infoort als Text table IOrtTexte ORTTEXT |
| F_HFK | int | Infohaeufigkeit Bereich: 0 - 31 |
| F_ART_ANZ | int | Anzahl der Infoarten Bereich: immer 1 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Bereich: immer 0 |
| F_ART1_NR | int | 1. (einzige) Infoart Bereich: 0, 1 |
| F_ART1_TEXT | string | 1. (einzige) Infoart als Text table IArtTexte ARTTEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-lesen-zv"></a>
### IS_LESEN_ZV

Infospeicher lesen / Sonderfall: ZV-Ringspeicher Analog zu FS_LESEN gibt es mehrere (15+1) Ergebnis-Saetze Im Satz  1 steht die Information zum letzten ZV-Befehl. Im Satz 15 steht die aelteste Information. Im Satz 16 steht das Ergebnis JOB_STATUS.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| I_ZEIGER_RS | int | Zeigerwert des ZV-Ringspeichers Bereich: 0-28 |
| I_HEX_CODE_RS | binary | Ringspeicherdaten (alle 15 ZV-Befehle) als Hexcode |
| I_HEX_CODE | binary | Ringspeicherdaten (einzelner ZV-Befehl) als Hexcode |
| I_ZV_BEFEHL_WERT | int | zuletzt ausgefuehrter ZV-Befehl moegliche Werte: 0=SER, 1=VR, 2=ER, 3=ZS, 4=ES |
| I_ZV_BEFEHL | string | zuletzt ausgefuehrter ZV-Befehl Bereich: SER, VR, ER, ZS, ES |
| I_SCHLOSS_FT | int | Fahrerschloss Bereich: 0, wenn FALSE / 1, wenn TRUE |
| I_SCHLOSS_BT | int | Beifahrerschloss Bereich: 0, wenn FALSE / 1, wenn TRUE |
| I_FB | int | Fernbedienung Bereich: 0, wenn FALSE / 1, wenn TRUE |
| I_CL | int | Centerlock Bereich: 0, wenn FALSE / 1, wenn TRUE |
| I_CS | int | Crash-Sensor Bereich: 0, wenn FALSE / 1, wenn TRUE |
| I_4KMH | int | groesser 4 km/h Bereich: 0, wenn FALSE / 1, wenn TRUE |
| I_EWS | int | Elektronische Wegfahrsperre Bereich: 0, wenn FALSE / 1, wenn TRUE |
| I_FB_2MIN | int | 2 Minuten nach Fernbedienung entriegeln Bereich: 0, wenn FALSE / 1, wenn TRUE |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Lesen des internen Speichers der ZKE V Als Argumente werden die Anzahl und die Adresse der Datenbytes uebergeben.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANZAHL | int | 1 - 32 |
| ADRESSE | int | 0x0000 - 0xFFFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | ausgelesene Daten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |

<a id="job-speicher-schreiben"></a>
### SPEICHER_SCHREIBEN

Speicherinhalt lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | string | Codierdaten |
| SPEICHER_DATEN | string | Speicherinhalt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_SENDE | binary | Sendetelegramm anzeigen Write Telegram to ECU |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG Write response |

<a id="job-status-key-memory"></a>
### STATUS_KEY_MEMORY

Auslesen der Nummer des Funkschluessels, mit dem zuletzt entriegelt wurde

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NR | int | 0   : ungueltig ! (z.B.: mechanisch entriegelt) 1-4 : Nr. des Funkschluessels, mit dem entriegelt wurde |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary |  |

<a id="job-status-funkschluessel"></a>
### STATUS_FUNKSCHLUESSEL

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!! !!!        A C H T U N G         !!! !!! Dieser Job ist abhaengig von !!! !!! der Softwarenummer des SG's. !!! !!! Es liegen derzeit nur Daten  !!! !!! fuer folgende SW-Nr. vor :   !!! !!! 1.1, 1.2, 1.4, 1.5, 1.6, 2.0 !!! !!! 3.0, 3.1, 3.3                     !!! !!! bzw. für folgende Diag.Index !!! !!! 41, 51, 42, 52               !!! !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!! Auslesen der Funkschluesseldaten aus dem internen Speicher der ZKE V

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NR_AKTUELL_CODE | int | Zahlencode der momentan eingelesenen Schluesselnummer Bereich: 0 bis 255 (Zufallszahl) Wenn der momentane Schluessel zum Fahrzeug gehoert, muss dieser Wert identisch mit einem der Werte STAT_NR_n sein. |
| STAT_NR_AKTUELL | int | momentan eingelesene Schluesselnummer Bereich: IO  (Schluessel gehoert zum FZG)      : 1 bis 4 NIO (Schluessel gehoert NICHT zum FZG): 0 |
| STAT_INIT_ANZ | int | Anzahl der initialisierten Schluessel Bereich: 0 bis 4 |
| STAT_NR_1 | int | Speicher von Schluesselnummer 1 (auf ZKE V initialisiert) Bereich: 0 bis 255 |
| STAT_NR_2 | int | Speicher von Schluesselnummer 2 (auf ZKE V initialisiert) Bereich: 0 bis 255 |
| STAT_NR_3 | int | Speicher von Schluesselnummer 3 (auf ZKE V initialisiert) Bereich: 0 bis 255 |
| STAT_NR_4 | int | Speicher von Schluesselnummer 4 (auf ZKE V initialisiert) Bereich: 0 bis 255 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-ib-aus"></a>
### STEUERN_IB_AUS

dauerhaftes Ausschalten der Innenbeleuchtung Das Innenlicht kann nur manuell durch Druecken des Tasters wieder aktiviert werden.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen-dwa"></a>
### FS_LESEN_DWA

Fehlerspeicher lesen (nur DWA-Fehler) Sonderjob für Hr. Mühlbauer, TR-443

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_DWA | int | 1 bei Fehler 0x06, 0x07, 0x41, 0x42, 0x43 0 sonst |
| _TEL_ANTWORT0 | binary | 0. Hex-Antwort von SG |
| _TEL_ANTWORT1 | binary | 1. Hex-Antwort von SG |

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
- [LIEFERANTEN](#table-lieferanten) (67 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [FORTTEXTE](#table-forttexte) (87 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [IORTTEXTE](#table-iorttexte) (32 × 2)
- [IARTTEXTE](#table-iarttexte) (3 × 2)
- [BITS](#table-bits) (95 × 6)

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

Dimensions: 67 rows × 2 columns

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

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 87 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | Interner Fehler im Grundmodul V: interne Spannung |
| 0x04 | Energiesparmode gesetzt |
| 0x20 | Interner Fehler im Grundmodul V: Prozessor Watchdog |
| 0x21 | Interner Fehler im Grundmodul V: Prozessor ROM |
| 0x22 | Interner Fehler im Grundmodul V: Taktgeber |
| 0x23 | Interner Fehler im Grundmodul V: EEPROM |
| 0x47 | Interner Fehler im Grundmodul V: Prozessor Interrupt |
| 0x24 | Zentralverriegelung Relais Verriegeln: Oeffnerkontakt unterbricht oder Schliesserkontakt klebt |
| 0x25 | Zentralverriegelung Relais Entriegeln: Oeffnerkontakt unterbricht oder Schliesserkontakt klebt |
| 0x26 | Zentralverriegelung Relais Sichern: Oeffnerkontakt unterbricht oder Schliesserkontakt klebt |
| 0x27 | Zentralverriegelung Relais Verriegeln Fahrertuer: Oeffnerkontakt unterbricht oder Schliesserkontakt klebt |
| 0x28 | Zentralverriegelung: Relais zieht nicht an bei Verriegeln |
| 0x29 | Zentralverriegelung: Relais zieht nicht an bei Entriegeln |
| 0x2A | Zentralverriegelung: Relais zieht nicht an bei Sichern |
| 0x2B | Zentralverriegelung: Relais zieht nicht an bei Verriegeln Fahrertuer |
| 0x2C | Fensterheber: Relais klebt bei Fahrertuer |
| 0x2D | Fensterheber: Relais klebt bei Beifahrertuer |
| 0x2E | Fensterheber: Relais klebt bei Fahrerseite hinten |
| 0x2F | Fensterheber: Relais klebt bei Beifahrerseite hinten |
| 0x30 | K-Bus oder Steuergeraet fuer Instrumenten-Kombination (Gateway) |
| 0x44 | Grundmodul V: uncodiert oder Codierung verloren |
| 0x4B | Interner Fehler im Grundmodul V: Checksum ROM |
| 0x31 | Wischerschalter (Potentiometer): Leitungsunterbrechung oder Kurzschluss gegen U-Batt |
| 0x32 | Wischerschalter (Potentiometer): Kurzschluss gegen Masse |
| 0x33 | Wischer: blockiert oder Rueckstellkontakt |
| 0x36 | Wischer: Relais oder Leitung fuer Wischer ein |
| 0x37 | Wischer: Relais fehlt oder Relais / Leitung fuer Wischerstufe 2 |
| 0x38 | Wischer: Pumpe fuer Scheibenwaschen oder Behaelter leer |
| 0x01 | Wischer: Sicherung fuer Pumpe, Innenlicht, Verbraucherabschaltung |
| 0x3A | Wischer: Relais Pumpe oder Leitung fuer Scheinwerferreinigung |
| 0x3B | Innenlicht: Kurzschluss |
| 0x48 | Innenlicht: Leitungsunterbrechung |
| 0x49 | Verbraucherabschaltung 2: Kurzschluss gegen U-Batt |
| 0x3c | Verbraucherabschaltung 2: Kurzschluss gegen Masse |
| 0x4A | Verbraucherabschaltung 1: Kurzschluss gegen Masse |
| 0x02 | Zentralverriegelung: Sicherung |
| 0x03 | Zentralverriegelung: Crash-Eingang dauernd aktiv |
| 0x45 | Zentralverriegelung: Schlosskontakt Fahrertuer |
| 0x46 | Zentralverriegelung: Schlosskontakt Beifahrertuer |
| 0x3D | Zentralverriegelung: Kurzschluss oder Leitungsunterbrechung bei Antrieb Heckklappe |
| 0x3F | Zentralverriegelung: Kurzschluss gegen Masse oder Leitungsunterbrechung bei Relais fuer Entriegeln Heckscheibe |
| 0x06 | Diebstahlwarnanlage: Sirene, Funkinnenraumschutz, Neigungsgeber oder Leitung STDWA Kurzschluss gegen U-Batt |
| 0x07 | Diebstahlwarnanlage: Sirene, Funkinnenraumschutz, Neigungsgeber oder Leitung STDWA Kurzschluss gegen Masse oder Leitungsunterbrechung |
| 0x41 | Diebstahlwarnanlage: Neigungsgeber |
| 0x42 | Diebstahlwarnanlage: Innenraumschutz |
| 0x43 | Diebstahlwarnanlage: Innenraumschutz hinten |
| 0x08 | Fensterheber: Sicherung |
| 0x09 | Fensterheber: Unterbrechung Motor oder Relais Fahrertuer |
| 0x0A | Fensterheber: Unterbrechung Motor oder Relais Beifahrertuer |
| 0x0D | Fensterheber: Unterbrechung Einklemmschutzleiste oder Denormierung/Fehler EKS-Elektronik Fahrertuer |
| 0x0E | Fensterheber: Unterbrechung Einklemmschutzleiste oder Denormierung/Fehler EKS-Elektronik Beifahrertuer |
| 0x0B | Fensterheber: Unterbrechung Motor oder Relais Fahrerseite hinten |
| 0x0C | Fensterheber: Unterbrechung Motor oder Relais Beifahrerseite hinten |
| 0x0F | Fensterheber: Unterbrechung Einklemmschutzleiste oder Denormierung/Fehler EKS-Elektronik Fahrerseite hinten |
| 0x10 | Fensterheber: Unterbrechung Einklemmschutzleiste oder Denormierung/Fehler EKS-Elektronik Beifahrerseite hinten |
| 0x4C | Beifahrerspiegel: Interner Fehler: Timer Watchdog |
| 0x4D | Beifahrerspiegel: Unterbrechung Heizung |
| 0x4E | Beifahrerspiegel: Kurzschluss Heizung |
| 0x4F | Beifahrerspiegel: Potentiometer Achse 1/3 |
| 0x50 | Beifahrerspiegel: Potentiometer Achse 2/4 |
| 0x51 | Beifahrerspiegel: Unterbrechung Motor Achse 1/3 |
| 0x52 | Beifahrerspiegel: Kurzschluss Motor Achse 1/3 |
| 0x53 | Beifahrerspiegel: Unterbrechung Motor Achse 2/4 |
| 0x54 | Beifahrerspiegel: Kurzschluss Motor Achse 2/4 |
| 0x55 | Beifahrerspiegel: Unterbrechung Motor Einklappen |
| 0x56 | Beifahrerspiegel: Kurzschluss Motor Einklappen |
| 0x5B | Fahrerspiegel: Interner Fehler: Timer Watchdog |
| 0x5C | Fahrerspiegel: Unterbrechung Heizung |
| 0x5D | Fahrerspiegel: Kurzschluss Heizung |
| 0x5E | Fahrerspiegel: Potentiometer Achse 1/3 |
| 0x5F | Fahrerspiegel: Potentiometer Achse 2/4 |
| 0x60 | Fahrerspiegel: Unterbrechung Motor Achse 1/3 |
| 0x61 | Fahrerspiegel: Kurzschluss Motor Achse 1/3 |
| 0x62 | Fahrerspiegel: Unterbrechung Motor Achse 2/4 |
| 0x63 | Fahrerspiegel: Kurzschluss Motor Achse 2/4 |
| 0x64 | Fahrerspiegel: Unterbrechung Motor Einklappen |
| 0x65 | Fahrerspiegel: Kurzschluss Motor Einklappen |
| 0x6A | keine Antwort Schalterblock |
| 0x6B | keine Antwort Beifahrerspiegel |
| 0x6C | keine Antwort Fahrerspiegel |
| 0x6D | Fensterheberschalter VL Signal ungültig |
| 0x6E | Fensterheberschalter VR Signal ungültig |
| 0x6F | Fensterheberschalter HL Signal ungültig |
| 0x70 | Fensterheberschalter HR Signal ungültig |
| 0x71 | Spiegelverstellschalter (Horizontal) Signal ungültig |
| 0x72 | Spiegelverstellschalter (Vertikal) Signal ungültig |
| 0xXY | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ART | ARTTEXT |
| --- | --- |
| 0x00 | sporadischer Fehler |
| 0x01 | statischer Fehler |
| 0xXY | unbekannte Fehlerart |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 32 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x80 | Alarmspeicher: Klemme R |
| 0x81 | Alarmspeicher: Tuerkontakt Fahrertuer |
| 0x82 | Alarmspeicher: Tuerkontakt Beifahrertuer |
| 0x83 | Alarmspeicher: Tuerkontakt Fahrerseite hinten / Verdeckklappe |
| 0x84 | Alarmspeicher: Tuerkontakt Beifahrerseite hinten |
| 0x85 | Alarmspeicher: Heckklappe |
| 0x86 | Alarmspeicher: Heckscheibe |
| 0x87 | Alarmspeicher: RDC |
| 0x88 | Alarmspeicher: Motorhaube |
| 0x89 | Alarmspeicher: Neigungsgeber |
| 0x8A | Alarmspeicher: Funkinnenraumschutz |
| 0x8B | Alarmspeicher: Funkinnenraumschutz hinten (E46/3) / Handschuhfach (E46/C) |
| 0x8C | Alarmspeicher: Reserve |
| 0x8D | Alarmspeicher: Schlosskontakt Fahrertuer |
| 0x8E | Alarmspeicher: Schlosskontakt Beifahrertuer |
| 0x8F | Alarmspeicher: Panik-Mode wurde ausgeloest |
| 0x98 | Beifahrerspiegel: Unterspannung SPM |
| 0x99 | Beifahrerspiegel: Überspannung SPM |
| 0x9A | Beifahrerspiegel: Unterspannung Spiegelheizung |
| 0x9B | Beifahrerspiegel: Übertemperatur Baustein Ud13 |
| 0x9C | Fahrerspiegel: Unterspannung SPM |
| 0x9D | Fahrerspiegel: Überspannung SPM |
| 0x9E | Fahrerspiegel: Unterspannung Spiegelheizung |
| 0x9F | Fahrerspiegel: Übertemperatur Baustein Ud13 |
| 0x90 | Batteriespannung: Unterbrechung |
| 0x91 | Crash: wurde ausgeloest |
| 0x92 | Wiederholsperre: Zentralverriegelung |
| 0x93 | Wiederholsperre: Entriegelung Heckklappe |
| 0x94 | Wiederholsperre: Entriegelung Heckscheibe |
| 0x95 | Wiederholsperre: Fensterheber |
| 0x97 | Wiederholsperre: Spiegelbeiklappen |
| 0xXY | unbekannter Info-Ort |

<a id="table-iarttexte"></a>
### IARTTEXTE

Dimensions: 3 rows × 2 columns

| ART | ARTTEXT |
| --- | --- |
| 0x00 | sporadischer Fehler |
| 0x01 | statischer Fehler |
| 0xXY | unbekannte Fehlerart |

<a id="table-bits"></a>
### BITS

Dimensions: 95 rows × 6 columns

| ZELLE | BYTE | MASK | VALUE | NAME | TEXT |
| --- | --- | --- | --- | --- | --- |
| 1 | 0 | 0x02 | 0x02 | SIB | Schalter Innenbeleuchtung |
| 2 | 0 | 0x04 | 0x04 | TOEHK | Taster Entriegeln Heckklappe |
| 3 | 0 | 0x08 | 0x08 | TZV | Taster Centerlock |
| 4 | 0 | 0x10 | 0x10 | TOEHS | Taster Entriegeln Heckscheibe |
| 5 | 0 | 0x20 | 0x20 | TOEHKI | Taster Entriegeln Heckklappe innen |
| 6 | 0 | 0x40 | 0x40 | HKK | Heckklappenkontakt |
| 7 | 0 | 0x80 | 0x80 | ERHK | Entriegeln Heckklappe |
| 9 | 1 | 0x02 | 0x02 | RSK | Rueckstellkontakt Wischer |
| 10 | 1 | 0x04 | 0x04 | SFFA | Schalter FH Fahrer auf |
| 11 | 1 | 0x08 | 0x08 | SFFZ | Schalter FH Fahrer zu |
| 12 | 1 | 0x10 | 0x10 | SFBA | Schalter FH Beifahrer auf |
| 13 | 1 | 0x20 | 0x20 | SFBZ | Schalter FH Beifahrer zu |
| 14 | 1 | 0x40 | 0x40 | SW2 | Wischerschalter 2 |
| 15 | 1 | 0x80 | 0x80 | KISI | Kindersicherung FH hinten |
| 17 | 2 | 0x02 | 0x02 | MHK | Motor-Hauben-Kontakt |
| 18 | 2 | 0x04 | 0x04 | HFK | Handschuhfach-Kontakt |
| 19 | 2 | 0x08 | 0x08 | HSK | Heck-Scheiben-Kontakt |
| 20 | 2 | 0x10 | 0x10 | INRS | Innenraumschutz |
| 21 | 2 | 0x20 | 0x20 | NG | Neigungsgebereingang |
| 22 | 2 | 0x40 | 0x40 | INRS2 | Innenraumschutz 2 |
| 23 | 2 | 0x80 | 0x80 | KL_R_HW | Klemme R (Hardware) |
| 25 | 3 | 0x02 | 0x02 | REE1 | Reserve Eingang 1 |
| 26 | 3 | 0x04 | 0x04 | REE3 | Reserve Eingang 3 |
| 27 | 3 | 0x08 | 0x08 | CS | Crash-Eingang |
| 28 | 3 | 0x10 | 0x10 | KL30BTS | Versorgung fuer IB, WP, MERHK und VA |
| 29 | 3 | 0x20 | 0x20 | KL30ZV | Versorgung fuer Zentral-Verriegelung |
| 30 | 3 | 0x40 | 0x40 | KL30FHV | Versorgung Klemme 30 FH vorne |
| 32 | 4 | 0x01 | 0x01 | SFFHA | Schalter FH Fahrer hinten auf |
| 33 | 4 | 0x02 | 0x02 | SFFHZ | Schalter FH Fahrer hinten zu |
| 34 | 4 | 0x04 | 0x04 | SFBHA | Schalter FH Beifahrer hinten auf |
| 35 | 4 | 0x08 | 0x08 | SFBHZ | Schalter FH Beifahrer hinten zu |
| 36 | 4 | 0x10 | 0x10 | SFFHA2 | Schalter 2 FH Fahrer hinten auf |
| 37 | 4 | 0x20 | 0x20 | SFFHZ2 | Schalter 2 FH Fahrer hinten zu |
| 38 | 4 | 0x40 | 0x40 | SFBHA2 | Schalter 2 FH Beifahrer hinten auf |
| 39 | 4 | 0x80 | 0x80 | SFBHZ2 | Schalter 2 FH Beifahrer hinten zu |
| 40 | 5 | 0x01 | 0x01 | REE2 | Reserve Eingang 2 |
| 41 | 5 | 0x02 | 0x02 | VRHK | Verriegeln Heckklappe |
| 42 | 5 | 0x04 | 0x04 | SWA | Schalter Waschen |
| 43 | 5 | 0x08 | 0x08 | SW1 | Schalter Wischerstufe 1 |
| 48 | 6 | 0x01 | 0x01 | TKFT | Tuerkontakt Fahrertuer |
| 49 | 6 | 0x02 | 0x02 | TKBT | Tuerkontakt Beifahrertuer |
| 50 | 6 | 0x04 | 0x04 | TKFH | Tuerkontakt Fahrertuer hinten |
| 51 | 6 | 0x08 | 0x08 | TKBH | Tuerkontakt Beifahrer hinten |
| 52 | 6 | 0x10 | 0x10 | VRFT | Verriegeln Fahrertuer |
| 53 | 6 | 0x20 | 0x20 | ERFT | Entriegeln Fahrertuer |
| 54 | 6 | 0x40 | 0x40 | VRBT | Verriegeln Beifahrertuer |
| 55 | 6 | 0x80 | 0x80 | ERBT | Entriegeln Beifahrertuer |
| 65 | 8 | 0x02 | 0x02 | MFFHA | Motor FH Fahrer hinten auf |
| 66 | 8 | 0x04 | 0x04 | MFFHZ | Motor FH Fahrer hinten zu |
| 67 | 8 | 0x08 | 0x08 | MFBHZ | Motor FH Beifahrer hinten zu |
| 68 | 8 | 0x10 | 0x10 | MFBHA | Motor FH Beifahrer hinten auf |
| 69 | 8 | 0x20 | 0x20 | MER | Motor Entriegeln |
| 70 | 8 | 0x40 | 0x40 | MZS | Motor Sichern |
| 71 | 8 | 0x80 | 0x80 | MVRFT | Motor Verriegeln Fahrertuer |
| 72 | 9 | 0x01 | 0x01 | REA3 | Reserve Ausgang 3 |
| 73 | 9 | 0x02 | 0x02 | WI1 | Wischerrelais Stufe 1 |
| 74 | 9 | 0x04 | 0x04 | WI2 | Wischerrelais Stufe 2 |
| 75 | 9 | 0x08 | 0x08 | SRA | Relais Scheinwerferreinigung |
| 76 | 9 | 0x10 | 0x10 | RERHS | Relais Entriegeln Heckscheibe |
| 77 | 9 | 0x20 | 0x20 | SIRENE | Sirene, bzw. Alarmhorn |
| 78 | 9 | 0x40 | 0x40 | DWAL | DWA-LED |
| 79 | 9 | 0x80 | 0x80 | MVR | Motor Verriegeln |
| 82 | 10 | 0x04 | 0x04 | MFFA | Motor FH Fahrer auf |
| 83 | 10 | 0x08 | 0x08 | MFFZ | Motor FH Fahrer zu |
| 84 | 10 | 0x10 | 0x10 | MFBA | Motor FH Beifahrer auf |
| 85 | 10 | 0x20 | 0x20 | MFBZ | Motor FH Beifahrer zu |
| 89 | 11 | 0x02 | 0x02 | STDWA | Status DWA |
| 90 | 11 | 0x04 | 0x04 | ENEKS | EKS-Schwelle aktiv |
| 91 | 11 | 0x08 | 0x08 | ENPU | Enable Pull Up |
| 92 | 11 | 0x10 | 0x10 | REA1 | Reserve Ausgang 1 |
| 93 | 11 | 0x20 | 0x20 | REA2 | Reserve Ausgang 2 |
| 95 | 11 | 0x80 | 0x80 | VA2 | Verbraucherabschaltung 2 EIN |
| 96 | 12 | 0x01 | 0x01 | IB | Innenbeleuchtung |
| 97 | 12 | 0x02 | 0x02 | VA | Verbraucherabschaltung EIN |
| 98 | 12 | 0x04 | 0x04 | WP | Waschpumpe |
| 99 | 12 | 0x08 | 0x08 | MERHK | Motor Entriegeln Heckklappe |
| 136 | 17 | 0x01 | 0x01 | SEND_L | Sender-Nummer (Low-Bit) |
| 137 | 17 | 0x02 | 0x02 | SEND_H | Sender-Nummer (High-Bit) |
| 138 | 17 | 0x04 | 0x04 | FZVSIG | Funksignal empfangen |
| 139 | 17 | 0x08 | 0x08 | FZVKEY | Funkschluesselsignale empfangen |
| 140 | 17 | 0x10 | 0x10 | TASTE1 | Fernbedienung Taste 1 betaetigt |
| 141 | 17 | 0x20 | 0x20 | TASTE2 | Fernbedienung Taste 2 betaetigt |
| 142 | 17 | 0x40 | 0x40 | TASTE3 | Fernbedienung Taste 3 betaetigt |
| 143 | 17 | 0x80 | 0x80 | FUINIT | Initialisierung Funkschluessel moeglich |
| 144 | 18 | 0x01 | 0x01 | LOBAT1 | Schluessel Sender 1 Batterie schwach |
| 145 | 18 | 0x02 | 0x02 | LOBAT2 | Schluessel Sender 2 Batterie schwach |
| 146 | 18 | 0x04 | 0x04 | LOBAT3 | Schluessel Sender 3 Batterie schwach |
| 147 | 18 | 0x08 | 0x08 | LOBAT4 | Schluessel Sender 4 Batterie schwach |
| 148 | 18 | 0x10 | 0x10 | FSIB | FS IB-Befehl |
| 149 | 18 | 0x20 | 0x20 | FSAHK | Heckklappentaste Entriegeln Heckklappe |
| 150 | 18 | 0x40 | 0x40 | ZV1FS | ZV-Befehl entriegeln |
| 151 | 18 | 0x80 | 0x80 | ZV0FS | ZV-Befehl verriegeln |
| 43 | 5 | 0x08 | 0x08 | SW1_2 | Schalter Wischerstufe 1 + 2 |
| 73 | 9 | 0x02 | 0x02 | WI1_2 | Wischerrelais Stufe 1 + 2 |
| XY | XY | 0xXY | 0xXY | XY | nicht definiertes Signal |
