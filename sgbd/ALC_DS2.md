# ALC_DS2.prg

- Jobs: [58](#jobs)
- Tables: [11](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | ALC E46 |
| ORIGIN | BMW EI-63 Bilz |
| REVISION | 3.01 |
| AUTHOR | BMW L. Dennert, LEAR W. Hoffmann, C. Ahrens |
| COMMENT | SGBD fuer ALC_SG |
| PACKAGE | 1.03 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [IDENT](#job-ident) - Identdaten
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode aufrechterhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [C_CI_LESEN](#job-c-ci-lesen) - Codierindex lesen Standard Codierjob
- [C_FG_LESEN](#job-c-fg-lesen) - Fahrgestellnummer lesen Standard Codierjob
- [C_FG_SCHREIBEN](#job-c-fg-schreiben) - Fahrgestellnummer schreiben Standard Codierjob
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Fahrgestellnummer schreiben und ruecklesen Standard Codierjob
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen Read codingdata
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und verifizieren Write and check codingdata
- [FS_ZAEHLER](#job-fs-zaehler) - Default fs_zaehler job
- [FS_LESEN](#job-fs-lesen) - fs_lesen job
- [FS_LOESCHEN](#job-fs-loeschen) - Default FS_LOESCHEN job
- [IS_LESEN](#job-is-lesen) - infospeicherlesen job Liest NUR die Infospeichereintraege des ALC_SG
- [IS_LESEN_ALC_SG](#job-is-lesen-alc-sg) - infospeicherlesen job
- [IS_LESEN_SMC](#job-is-lesen-smc) - infospeicherlesen job
- [IS_LOESCHEN](#job-is-loeschen) - Default FS_LOESCHEN job Loescht NUR die Infospeichereintraege des ALC_SG
- [IS_LOESCHEN_ALC_SG](#job-is-loeschen-alc-sg) - Default FS_LOESCHEN job
- [IS_LOESCHEN_SMC_L](#job-is-loeschen-smc-l) - Default FS_LOESCHEN job
- [IS_LOESCHEN_SMC_R](#job-is-loeschen-smc-r) - Default FS_LOESCHEN job
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - "Prüfstempel" lesen DS2:  $0E Prüfstempel lesen Modus = Default
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - "Prüfstempel" schreiben DS2:  $0F Prüfstempel schreiben Modus = Default
- [STATUS_ALC_SG_LESEN](#job-status-alc-sg-lesen) - STATUS_LESEN job
- [STATUS_BETR_H_ALC](#job-status-betr-h-alc) - Status von ALC lesen
- [STEUERN_BETR_H_ALC_LOESCHEN](#job-steuern-betr-h-alc-loeschen) - Status von ALC schreiben
- [STATUS_CAN_SIGNALE](#job-status-can-signale) - Status von ALC lesen
- [STATUS_CAN_SIGNALE_TIMEOUT](#job-status-can-signale-timeout) - Status von ALC lesen
- [FGNR_ALC_LESEN](#job-fgnr-alc-lesen) - 7Byte Fahrgestellnummer von ALC lesen
- [FGNR_ALC_SCHREIBEN](#job-fgnr-alc-schreiben) - Status von ALC schreiben
- [BLOCK_SMC_ALC_LESEN](#job-block-smc-alc-lesen) - Block (Codierdaten, Herstellerdanten) lesen Read codingdata
- [BLOCK_SMC_ALC_SCHREIBEN](#job-block-smc-alc-schreiben) - Block (Codierdaten, Herstellerdanten) schreiben Read codingdata
- [CODIERDATEN_ALC_LESEN_KOMPLETT_LEAR](#job-codierdaten-alc-lesen-komplett-lear) - Auslesen der kompletten Codierdaten vom ALC Modus  : Default
- [CODIERDATEN_SMC_LINKS_LESEN_KOMPLETT_LEAR](#job-codierdaten-smc-links-lesen-komplett-lear) - Auslesen der kompletten Codierdaten der SMC links Modus  : Default
- [CODIERDATEN_SMC_RECHTS_LESEN_KOMPLETT_LEAR](#job-codierdaten-smc-rechts-lesen-komplett-lear) - Auslesen der kompletten Codierdaten der SMC rechts Modus  : Default
- [STEUERGERAETE_RESET_ALC](#job-steuergeraete-reset-alc) - Steuergeraete reset vom ALC-SG ausloesen
- [NUR_DATEN_SCHREIBEN_LEAR](#job-nur-daten-schreiben-lear) - Schreiben von Daten aus Datei
- [STATUS_SMC_LESEN](#job-status-smc-lesen) - STATUS_LESEN job
- [STATUS_SMC_POSITION_LESEN](#job-status-smc-position-lesen) - STATUS_LESEN job
- [STEUERN_REFERENZLAUF_SMC](#job-steuern-referenzlauf-smc) - Referenzlauf der SMC starten STATUS_SCHREIBEN job
- [STEUERN_POSITION_SMC](#job-steuern-position-smc) - bestimmte Position der SMC anfahren STATUS_SCHREIBEN job
- [STATUS_BETR_H_SMC](#job-status-betr-h-smc) - Status von SMC lesen
- [STEUERN_BETR_H_SMC_LOESCHEN](#job-steuern-betr-h-smc-loeschen) - STATUS_SCHREIBEN job
- [STATUS_VERTEILUNG_WINKEL_ANSTEUERUNG_SMC](#job-status-verteilung-winkel-ansteuerung-smc) - Status von SMC lesen
- [STEUERN_VERTEILUNG_WINKEL_ANSTEUERUNG_SMC_LOESCHEN](#job-steuern-verteilung-winkel-ansteuerung-smc-loeschen) - STATUS_SCHREIBEN job
- [STATUS_TEMPERATURVERTEILUNG_SMC](#job-status-temperaturverteilung-smc) - Status von SMC lesen
- [STEUERN_TEMPERATURVERTEILUNG_SMC_LOESCHEN](#job-steuern-temperaturverteilung-smc-loeschen) - STATUS_SCHREIBEN job
- [STATUS_SCHRITTVERLUSTE_SMC](#job-status-schrittverluste-smc) - Status von SMC lesen
- [STEUERN_SCHRITTVERLUSTE_SMC_LOESCHEN](#job-steuern-schrittverluste-smc-loeschen) - STATUS_SCHREIBEN job
- [FAHRGESTELL_NR_SMC_SCHREIBEN](#job-fahrgestell-nr-smc-schreiben) - Schreiben der VIN in die linke SMC
- [FG_NR_SMC_LESEN](#job-fg-nr-smc-lesen) - Fahrgestellnummer fuer SMC links und rechts lesen
- [ID_SMC_LESEN](#job-id-smc-lesen) - ID SMC links und rechts lesen
- [SCHEINWERFERHERSTELLERDATEN_SCHREIBEN](#job-scheinwerferherstellerdaten-schreiben) - Beschreiben der Scheinwerfer-Herstellerdaten
- [SCHEINWERFERHERSTELLERDATEN_LESEN](#job-scheinwerferherstellerdaten-lesen) - Auslesen der Scheinwerfer-Herstellerdaten
- [PRUEFSTEMPEL_SCHEINWERFER_SCHREIBEN](#job-pruefstempel-scheinwerfer-schreiben) - Beschreiben des Scheinwerfer-Pruefstempel
- [PRUEFSTEMPEL_SCHEINWERFER_LESEN](#job-pruefstempel-scheinwerfer-lesen) - Auslesen der Scheinwerfer-Pruefstempel

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

<a id="job-c-c-lesen"></a>
### C_C_LESEN

Codierdaten lesen Read codingdata

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten Codingdata |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten Codingdata |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-c-c-auftrag"></a>
### C_C_AUFTRAG

Codierdaten schreiben und verifizieren Write and check codingdata

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Codierdaten Codingdata |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |

<a id="job-fs-zaehler"></a>
### FS_ZAEHLER

Default fs_zaehler job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ZAHL | int |  |

<a id="job-fs-lesen"></a>
### FS_LESEN

fs_lesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ORT_TEXT | string |  |
| F_ORT_NR | int |  |
| F_ART_ANZ | int |  |
| F_UW_ANZ | int |  |
| F_ART1_NR | int |  |
| F_ART1_TEXT | string |  |
| F_HFK | int | Haeufigkeit des Einzelfehlers |
| F_HEX_CODE | binary | Hexdaten des Fehlers |
| F_ZAHL | int | Anzahl der Gesamtfehler |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Default FS_LOESCHEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-is-lesen"></a>
### IS_LESEN

infospeicherlesen job Liest NUR die Infospeichereintraege des ALC_SG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ORT_TEXT | string |  |
| F_ORT_NR | int |  |
| F_ART_ANZ | int |  |
| F_UW_ANZ | int |  |
| F_ART1_NR | int |  |
| F_ART1_TEXT | string |  |
| F_HFK | int | Haeufigkeit des Einzelfehlers |
| F_HEX_CODE | binary | Hexdaten des Fehlers |
| F_ZAHL_BLOCK_2 | int | Anzahl der Fehler im Block 2 |
| F_ZAHL_BLOCK_3 | int | Anzahl der Fehler im Block 3 |
| F_ZAHL_BLOCK_4 | int | Anzahl der Fehler im Block 4 |

<a id="job-is-lesen-alc-sg"></a>
### IS_LESEN_ALC_SG

infospeicherlesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ORT_TEXT | string |  |
| F_ORT_NR | int |  |
| F_ART_ANZ | int |  |
| F_UW_ANZ | int |  |
| F_ART1_NR | int |  |
| F_ART1_TEXT | string |  |
| F_HFK | int | Haeufigkeit des Einzelfehlers |
| F_HEX_CODE | binary | Hexdaten des Fehlers |
| F_ZAHL_BLOCK_2 | int | Anzahl der Fehler im Block 2 |
| F_ZAHL_BLOCK_3 | int | Anzahl der Fehler im Block 3 |
| F_ZAHL_BLOCK_4 | int | Anzahl der Fehler im Block 4 |

<a id="job-is-lesen-smc"></a>
### IS_LESEN_SMC

infospeicherlesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ORT_TEXT | string |  |
| F_ORT_NR | int |  |
| F_ART_ANZ | int |  |
| F_UW_ANZ | int |  |
| F_ART1_NR | int |  |
| F_ART1_TEXT | string |  |
| F_HFK | int | Haeufigkeit des Einzelfehlers |
| F_HEX_CODE | binary | Hexdaten des Fehlers |
| F_ZAHL_BLOCK_5 | int | Anzahl der Fehler im Block 5 |
| F_ZAHL_BLOCK_6 | int | Anzahl der Fehler im Block 6 |
| F_ZAHL_BLOCK_7 | int | Anzahl der Fehler im Block 7 |
| F_ZAHL_BLOCK_8 | int | Anzahl der Fehler im Block 8 |
| F_ZAHL_BLOCK_9 | int | Anzahl der Fehler im Block 9 |
| F_ZAHL_BLOCK_10 | int | Anzahl der Fehler im Block 10 |
| F_ZAHL_BLOCK_11 | int | Anzahl der Fehler im Block 11 |
| F_ZAHL_BLOCK_12 | int | Anzahl der Fehler im Block 12 |

<a id="job-is-loeschen"></a>
### IS_LOESCHEN

Default FS_LOESCHEN job Loescht NUR die Infospeichereintraege des ALC_SG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-is-loeschen-alc-sg"></a>
### IS_LOESCHEN_ALC_SG

Default FS_LOESCHEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-is-loeschen-smc-l"></a>
### IS_LOESCHEN_SMC_L

Default FS_LOESCHEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-is-loeschen-smc-r"></a>
### IS_LOESCHEN_SMC_R

Default FS_LOESCHEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

"Prüfstempel" lesen DS2:  $0E Prüfstempel lesen Modus = Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| JOB0E_BYT0 | int | number 1 out of 3 valid:  0x00-0xFF |
| JOB0E_BYT1 | int | number 2 out of 3 valid:  0x00-0xFF |
| JOB0E_BYT2 | int | number 3 out of 3 valid:  0x00-0xFF |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

"Prüfstempel" schreiben DS2:  $0F Prüfstempel schreiben Modus = Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| JOB07_BYT0 | int | number 1 out of 3 valid:  0x00-0xFF |
| JOB07_BYT1 | int | number 2 out of 3 valid:  0x00-0xFF |
| JOB07_BYT2 | int | number 3 out of 3 valid:  0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-status-alc-sg-lesen"></a>
### STATUS_ALC_SG_LESEN

STATUS_LESEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_WAKELEITUNG_EIN | int | CAN-HW-Wakeleitung |
| STAT_S_BL_EIN | int | Bremslichtschalter bis C1-Muster |
| STAT_S_RUECKW_GANG_EIN | int | Rueckwaertsgang ein |
| STAT_S_DUMMY_EIN | int | unbelegt |
| STAT_SPANNUNG_BELADUNGSSENSOR_VORN_WERT | real | Spannung Sensor Hoehenstandsmesser vorne Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_BELADUNGSSENSOR_HINTEN_WERT | real | Spannung Sensor Hoehenstandsmesser hinten Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_KLEMME_30A_WERT | real | Spannung Klemme 30A Bereich: 0 V bis 25 V |
| STAT_SPANNUNG_S_BL_WERT | real | Spannung Bremslichtschalter Bereich: 0 V bis 5 V |
| STAT_SPANNUNG_VERSORGUNG_SMC_WERT | real | Spannungsversorgung SMC Bereich: 0 V bis 25 V |
| STAT_SPANNUNG_EINH | string | Einheit fuer alle Analogwerte: Volt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-betr-h-alc"></a>
### STATUS_BETR_H_ALC

Status von ALC lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BETRIEBSZEIT_ALC_WERT | real | Betriebsstunden ALC auslesen |
| STAT_BETRIEBSZEIT_SCHWENKEN_WERT | real | Betriebsstunden Schwenken aktiv auslesen |
| STAT_BETRIEBSZEIT_SMC_BESTROMT_WERT | real | Betriebsstunden SMCs bestromt auslesen |
| STAT_BETRIEBSZEIT_EINH | string | Einheit fuer Betriebszeit [min] |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-betr-h-alc-loeschen"></a>
### STEUERN_BETR_H_ALC_LOESCHEN

Status von ALC schreiben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-can-signale"></a>
### STATUS_CAN_SIGNALE

Status von ALC lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LENKWINKEL_WERT | int |  |
| STAT_GESCHWINDIGKEIT_WERT | unsigned int |  |
| STAT_GIERRATE_WERT | int |  |
| STAT_ABBLENDLICHT_WERT | unsigned char |  |
| STAT_POSITIONSLICHT_WERT | unsigned char |  |
| STAT_CONTROL_ALC_WERT | unsigned char |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-can-signale-timeout"></a>
### STATUS_CAN_SIGNALE_TIMEOUT

Status von ALC lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_INSTR3_CAN_11H_EIN | int |  |
| STAT_EGS1_CAN_11H_EIN | int |  |
| STAT_GANG_RUECKWAERTS_EIN | int |  |
| STAT_CTR_ALC_EIN | int |  |
| STAT_DME2_CAN_11H_EIN | int |  |
| STAT_DME1_CAN_11H_EIN | int |  |
| STAT_A_TEMP_RELATIVZEIT_EIN | int |  |
| STAT_LAMPENZUSTAND_EIN | int |  |
| STAT_LWS1_CAN_11H_EIN | int |  |
| STAT_ASC3_CAN_11H_EIN | int |  |
| STAT_ENGINE_1_EIN | int |  |
| STAT_GESCHWINDIGKEIT_EIN | int |  |
| STAT_STAT_DSC_EIN | int |  |
| STAT_ASC1_CAN_11H_EIN | int |  |
| STAT_KLEMMENSTATUS_EIN | int |  |
| STAT_LENKRADWINKEL_EIN | int |  |
| STAT_GETRIEBEDATEN_EIN | int |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fgnr-alc-lesen"></a>
### FGNR_ALC_LESEN

7Byte Fahrgestellnummer von ALC lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FGNR_ALC | string | Fahrgestellnummer 7-stellig fuer ALC |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fgnr-alc-schreiben"></a>
### FGNR_ALC_SCHREIBEN

Status von ALC schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FGNR_ALC | string | 7stellige Fahrgestellnummer |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-block-smc-alc-lesen"></a>
### BLOCK_SMC_ALC_LESEN

Block (Codierdaten, Herstellerdanten) lesen Read codingdata

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK | int | Block fuer Codierdaten, Herstellerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK_DATEN | string | Daten fuer Codierdaten, Herstellerdaten |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-block-smc-alc-schreiben"></a>
### BLOCK_SMC_ALC_SCHREIBEN

Block (Codierdaten, Herstellerdanten) schreiben Read codingdata

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK_DATEN | string | Block+Daten Block+Daten (z.B. 300001020304...) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-alc-lesen-komplett-lear"></a>
### CODIERDATEN_ALC_LESEN_KOMPLETT_LEAR

Auslesen der kompletten Codierdaten vom ALC Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_ALC | string | die kompletten Codierdaten |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-smc-links-lesen-komplett-lear"></a>
### CODIERDATEN_SMC_LINKS_LESEN_KOMPLETT_LEAR

Auslesen der kompletten Codierdaten der SMC links Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_1 | string | Teil 1 der kompletten Codierdaten |
| CODIERDATEN_2 | string | Teil 2 der kompletten Codierdaten |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-smc-rechts-lesen-komplett-lear"></a>
### CODIERDATEN_SMC_RECHTS_LESEN_KOMPLETT_LEAR

Auslesen der kompletten Codierdaten der SMC rechts Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERDATEN_1 | string | Teil 1 der kompletten Codierdaten |
| CODIERDATEN_2 | string | Teil 2 der kompletten Codierdaten |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuergeraete-reset-alc"></a>
### STEUERGERAETE_RESET_ALC

Steuergeraete reset vom ALC-SG ausloesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-nur-daten-schreiben-lear"></a>
### NUR_DATEN_SCHREIBEN_LEAR

Schreiben von Daten aus Datei

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN_DATEI | string | Dateiname mit Daten Datei muss in ediabas/ecu liegen bei leerem Argument wird die Datei cod_lm.dat codiert letztes Zeichen muss ein LF sein |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| CODIERTE_DATEI | string | Datei die codiert wurde |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-smc-lesen"></a>
### STATUS_SMC_LESEN

STATUS_LESEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_U_BATT_SMC_L_WERT | unsigned int | Batteriespannung SMC_L |
| STAT_SPANNUNG_BATT_SMC_L_WERT | real | Batteriespannung SMC_L Bereich: 0 .. 18 Volt |
| STAT_U_KOD_SMC_L_WERT | unsigned int | Kodierspannung SMC_L |
| STAT_U_SENSE_SMC_L_WERT | unsigned int | Sensespannung SMC_L |
| STAT_SPANNUNG_SENSE_SMC_L_WERT | real | Sensespannung SMC_L Bereich: 0 .. 5 Volt |
| STAT_COD_1_SMC_L_EIN | unsigned int | Hardwarekodierungseingang 1 SMC_L |
| STAT_COD_2_SMC_L_EIN | unsigned int | Hardwarekodierungseingang 2 SMC_L |
| STAT_COD_3_SMC_L_EIN | unsigned int | Hardwarekodierungseingang 3 SMC_L |
| STAT_SENSE_UP_DOWN_SMC_L_EIN | unsigned int | Zustand von Sensor-Pullup SMC_L |
| STAT_U_SENSE_SMC_L_EIN | unsigned int | Sensorspannung ein SMC_L |
| STAT_KONTROLL_SMC_L_WERT | unsigned long | Sensor Kontrollwert SMC_L |
| STAT_SENSOR_SMC_L_WERT | unsigned long | Sensorwert SMC_L |
| STAT_U_BATT_SMC_R_WERT | unsigned int | Batteriespannung SMC_R |
| STAT_SPANNUNG_BATT_SMC_R_WERT | real | Batteriespannung SMC_R Bereich: 0 .. 18 Volt |
| STAT_U_KOD_SMC_R_WERT | unsigned int | Kodierspannung SMC_R |
| STAT_U_SENSE_SMC_R_WERT | unsigned int | Sensespannung SMC_R |
| STAT_SPANNUNG_SENSE_SMC_R_WERT | real | Sensespannung SMC_R Bereich: 0 .. 5 Volt |
| STAT_COD_1_SMC_R_EIN | unsigned int | Hardwarekodierungseingang 1 SMC_R |
| STAT_COD_2_SMC_R_EIN | unsigned int | Hardwarekodierungseingang 2 SMC_R |
| STAT_COD_3_SMC_R_EIN | unsigned int | Hardwarekodierungseingang 3 SMC_R |
| STAT_SENSE_UP_DOWN_SMC_R_EIN | unsigned int | Zustand von Sensor-Pullup SMC_R |
| STAT_U_SENSE_SMC_R_EIN | unsigned int | Sensorspannung ein SMC_R |
| STAT_KONTROLL_SMC_R_WERT | unsigned long | Sensor Kontrollwert SMC_R |
| STAT_SENSOR_SMC_R_WERT | unsigned long | Sensorwert SMC_R |
| STAT_SPANNUNG_EINH | string | Einheit fuer alle Analogwerte: Volt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-smc-position-lesen"></a>
### STATUS_SMC_POSITION_LESEN

STATUS_LESEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_POS_KURVENLICHT_SMC_L | long | Winkel fuer Kurvenlicht SMC_L |
| STAT_POS_LWR_SMC_L | long | Winkel fuer LWR SMC_L |
| STAT_POS_KURVENLICHT_SMC_R | long | Winkel fuer Kurvenlicht SMC_R |
| STAT_POS_LWR_SMC_R | long | Winkel fuer LWR SMC_R |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-referenzlauf-smc"></a>
### STEUERN_REFERENZLAUF_SMC

Referenzlauf der SMC starten STATUS_SCHREIBEN job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |
| REFERENZLAUF | string | Referenzlauf auswaehlen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-position-smc"></a>
### STEUERN_POSITION_SMC

bestimmte Position der SMC anfahren STATUS_SCHREIBEN job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |
| POS_KURVENLICHT | long | Winkel fuer Kurvenlicht |
| GESCHW_KURVENLICHT | unsigned char | Geschwindigkeit fuer Kurvenlicht |
| POS_LWR | long | Winkel fuer LWR |
| GESCHW_LWR | unsigned char | Geschwindigkeit fuer LWR |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-betr-h-smc"></a>
### STATUS_BETR_H_SMC

Status von SMC lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_BETRIEBSZEIT_SMC_L_WERT | unsigned long | Betr_h SMC_L |
| STAT_RESETCOUNTER_SMC_L_WERT | unsigned long | Anzahl Resets SMC_L |
| STAT_ANZ_HS_KURVENLICHT_SMC_L_WERT | unsigned long | Anzahl Halbschritte Kurvenlicht SMC_L |
| STAT_ANZ_HS_LWR_SMC_L_WERT | unsigned long | Anzahl Halbschritte LWR SMC_L |
| STAT_ACHSEN_VERFAHRZEIT_KURVENLICHT_SMC_L_WERT | unsigned long | Achsenverfahrzeit fuer Kurvenlicht SMC_L |
| STAT_ACHSEN_VERFAHRZEIT_LWR_SMC_L_WERT | unsigned long | Achsenverfahrzeit fur LWR SMC_L |
| STAT_BETRIEBSZEIT_SMC_R_WERT | unsigned long | Betr_h SMC_R |
| STAT_RESETCOUNTER_SMC_R_WERT | unsigned long | Anzahl Resets SMC_R |
| STAT_ANZ_HS_KURVENLICHT_SMC_R_WERT | unsigned long | Anzahl Halbschritte Kurvenlicht SMC_R |
| STAT_ANZ_HS_LWR_SMC_R_WERT | unsigned long | Anzahl Halbschritte LWR SMC_R |
| STAT_ACHSEN_VERFAHRZEIT_KURVENLICHT_SMC_R_WERT | unsigned long | Achsenverfahrzeit fuer Kurvenlicht SMC_R |
| STAT_ACHSEN_VERFAHRZEIT_LWR_SMC_R_WERT | unsigned long | Achsenverfahrzeit fur LWR SMC_R |
| STAT_BETRIEBSZEIT_EINH | string | Einheit fuer Betriebsstunden |
| STAT_VERFAHRZEIT_EINH | string | Einheit fuer Achsenverfahrzeit |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-betr-h-smc-loeschen"></a>
### STEUERN_BETR_H_SMC_LOESCHEN

STATUS_SCHREIBEN job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-verteilung-winkel-ansteuerung-smc"></a>
### STATUS_VERTEILUNG_WINKEL_ANSTEUERUNG_SMC

Status von SMC lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_WINKEL_0_2_SMC_L_WERT | unsigned int | SMC_L_WINKEL zwischen 0° und 2° |
| STAT_WINKEL_2_4_SMC_L_WERT | unsigned int | SMC_L_WINKEL zwischen 2° und 4° |
| STAT_WINKEL_4_6_SMC_L_WERT | unsigned int | SMC_L_WINKEL zwischen 4° und 6° |
| STAT_WINKEL_6_8_SMC_L_WERT | unsigned int | SMC_L_WINKEL zwischen 6° und 8° |
| STAT_WINKEL_8_10_SMC_L_WERT | unsigned int | SMC_L_WINKEL zwischen 8° und 10° |
| STAT_WINKEL_10_12_SMC_L_WERT | unsigned int | SMC_L_WINKEL zwischen 10° und 12° |
| STAT_WINKEL_12_14_SMC_L_WERT | unsigned int | SMC_L_WINKEL zwischen 12° und 14° |
| STAT_WINKEL_14_16_SMC_L_WERT | unsigned int | SMC_L_WINKEL zwischen 14° und 16° |
| STAT_WINKEL_MINUS_0_2_SMC_L_WERT | unsigned int | SMC_L_WINKEL zwischen 0° und -2° |
| STAT_WINKEL_MINUS_2_4_SMC_L_WERT | unsigned int | SMC_L_WINKEL zwischen -2° und -4° |
| STAT_WINKEL_MINUS_4_6_SMC_L_WERT | unsigned int | SMC_L_WINKEL zwischen -4° und -6° |
| STAT_WINKEL_MINUS_6_8_SMC_L_WERT | unsigned int | SMC_L_WINKEL zwischen -6° und -8° |
| STAT_WINKEL_MINUS_8_10_SMC_L_WERT | unsigned int | SMC_L_WINKEL zwischen -8° und -10° |
| STAT_WINKEL_MINUS_10_12_SMC_L_WERT | unsigned int | SMC_L_WINKEL zwischen -10° und -12° |
| STAT_WINKEL_MINUS_12_14_SMC_L_WERT | unsigned int | SMC_L_WINKEL zwischen -12° und -14° |
| STAT_WINKEL_0_2_SMC_R_WERT | unsigned int | SMC_R_WINKEL zwischen 0° und 2° |
| STAT_WINKEL_2_4_SMC_R_WERT | unsigned int | SMC_R_WINKEL zwischen 2° und 4° |
| STAT_WINKEL_4_6_SMC_R_WERT | unsigned int | SMC_R_WINKEL zwischen 4° und 6° |
| STAT_WINKEL_6_8_SMC_R_WERT | unsigned int | SMC_R_WINKEL zwischen 6° und 8° |
| STAT_WINKEL_8_10_SMC_R_WERT | unsigned int | SMC_R_WINKEL zwischen 8° und 10° |
| STAT_WINKEL_10_12_SMC_R_WERT | unsigned int | SMC_R_WINKEL zwischen 10° und 12° |
| STAT_WINKEL_12_14_SMC_R_WERT | unsigned int | SMC_R_WINKEL zwischen 12° und 14° |
| STAT_WINKEL_14_16_SMC_R_WERT | unsigned int | SMC_R_WINKEL zwischen 14° und 16° |
| STAT_WINKEL_MINUS_0_2_SMC_R_WERT | unsigned int | SMC_R_WINKEL zwischen 0° und -2° |
| STAT_WINKEL_MINUS_2_4_SMC_R_WERT | unsigned int | SMC_R_WINKEL zwischen -2° und -4° |
| STAT_WINKEL_MINUS_4_6_SMC_R_WERT | unsigned int | SMC_R_WINKEL zwischen -4° und -6° |
| STAT_WINKEL_MINUS_6_8_SMC_R_WERT | unsigned int | SMC_R_WINKEL zwischen -6° und -8° |
| STAT_WINKEL_MINUS_8_10_SMC_R_WERT | unsigned int | SMC_R_WINKEL zwischen -8° und -10° |
| STAT_WINKEL_MINUS_10_12_SMC_R_WERT | unsigned int | SMC_R_WINKEL zwischen -10° und -12° |
| STAT_WINKEL_MINUS_12_14_SMC_R_WERT | unsigned int | SMC_R_WINKEL zwischen -12° und -14° |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-verteilung-winkel-ansteuerung-smc-loeschen"></a>
### STEUERN_VERTEILUNG_WINKEL_ANSTEUERUNG_SMC_LOESCHEN

STATUS_SCHREIBEN job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-temperaturverteilung-smc"></a>
### STATUS_TEMPERATURVERTEILUNG_SMC

Status von SMC lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_10_PROZENT_ABSCHALTUNG_SMC_L_WERT | unsigned int | SMC_L: 10% werden nicht mehr angefahren |
| STAT_20_PROZENT_ABSCHALTUNG_SMC_L_WERT | unsigned int | SMC_L: 20% werden nicht mehr angefahren |
| STAT_30_PROZENT_ABSCHALTUNG_SMC_L_WERT | unsigned int | SMC_L: 30% werden nicht mehr angefahren |
| STAT_40_PROZENT_ABSCHALTUNG_SMC_L_WERT | unsigned int | SMC_L: 40% werden nicht mehr angefahren |
| STAT_50_PROZENT_ABSCHALTUNG_SMC_L_WERT | unsigned int | SMC_L: 50% werden nicht mehr angefahren |
| STAT_60_PROZENT_ABSCHALTUNG_SMC_L_WERT | unsigned int | SMC_L: 60% werden nicht mehr angefahren |
| STAT_70_PROZENT_ABSCHALTUNG_SMC_L_WERT | unsigned int | SMC_L: 70% werden nicht mehr angefahren |
| STAT_80_PROZENT_ABSCHALTUNG_SMC_L_WERT | unsigned int | SMC_L: 80% werden nicht mehr angefahren |
| STAT_90_PROZENT_ABSCHALTUNG_SMC_L_WERT | unsigned int | SMC_L: 90% werden nicht mehr angefahren |
| STAT_100_PROZENT_ABSCHALTUNG_SMC_L_WERT | unsigned int | SMC_L: 100% werden nicht mehr angefahren |
| STAT_10_PROZENT_ABSCHALTUNG_SMC_R_WERT | unsigned int | SMC_R: 10% werden nicht mehr angefahren |
| STAT_20_PROZENT_ABSCHALTUNG_SMC_R_WERT | unsigned int | SMC_R: 20% werden nicht mehr angefahren |
| STAT_30_PROZENT_ABSCHALTUNG_SMC_R_WERT | unsigned int | SMC_R: 30% werden nicht mehr angefahren |
| STAT_40_PROZENT_ABSCHALTUNG_SMC_R_WERT | unsigned int | SMC_R: 40% werden nicht mehr angefahren |
| STAT_50_PROZENT_ABSCHALTUNG_SMC_R_WERT | unsigned int | SMC_R: 50% werden nicht mehr angefahren |
| STAT_60_PROZENT_ABSCHALTUNG_SMC_R_WERT | unsigned int | SMC_R: 60% werden nicht mehr angefahren |
| STAT_70_PROZENT_ABSCHALTUNG_SMC_R_WERT | unsigned int | SMC_R: 70% werden nicht mehr angefahren |
| STAT_80_PROZENT_ABSCHALTUNG_SMC_R_WERT | unsigned int | SMC_R: 80% werden nicht mehr angefahren |
| STAT_90_PROZENT_ABSCHALTUNG_SMC_R_WERT | unsigned int | SMC_R: 90% werden nicht mehr angefahren |
| STAT_100_PROZENT_ABSCHALTUNG_SMC_R_WERT | unsigned int | SMC_R: 100% werden nicht mehr angefahren |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-temperaturverteilung-smc-loeschen"></a>
### STEUERN_TEMPERATURVERTEILUNG_SMC_LOESCHEN

STATUS_SCHREIBEN job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-schrittverluste-smc"></a>
### STATUS_SCHRITTVERLUSTE_SMC

Status von SMC lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_SCHRITTVERLUSTGRENZE_1_SMC_L_WERT | unsigned int | SMC_L: Schrittverluste in Bereich 1 |
| STAT_SCHRITTVERLUSTGRENZE_2_SMC_L_WERT | unsigned int | SMC_L: Schrittverluste in Bereich 2 |
| STAT_SCHRITTVERLUSTGRENZE_3_SMC_L_WERT | unsigned int | SMC_L: Schrittverluste in Bereich 3 |
| STAT_SCHRITTVERLUSTGRENZE_4_SMC_L_WERT | unsigned int | SMC_L: Schrittverluste in Bereich 4 |
| STAT_SCHRITTVERLUSTGRENZE_5_SMC_L_WERT | unsigned int | SMC_L: Schrittverluste in Bereich 5 |
| STAT_SCHRITTVERLUSTGRENZE_6_SMC_L_WERT | unsigned int | SMC_L: Schrittverluste in Bereich 6 |
| STAT_SCHRITTVERLUSTGRENZE_1_SMC_R_WERT | unsigned int | SMC_R: Schrittverluste in Bereich 1 |
| STAT_SCHRITTVERLUSTGRENZE_2_SMC_R_WERT | unsigned int | SMC_R: Schrittverluste in Bereich 2 |
| STAT_SCHRITTVERLUSTGRENZE_3_SMC_R_WERT | unsigned int | SMC_R: Schrittverluste in Bereich 3 |
| STAT_SCHRITTVERLUSTGRENZE_4_SMC_R_WERT | unsigned int | SMC_R: Schrittverluste in Bereich 4 |
| STAT_SCHRITTVERLUSTGRENZE_5_SMC_R_WERT | unsigned int | SMC_R: Schrittverluste in Bereich 5 |
| STAT_SCHRITTVERLUSTGRENZE_6_SMC_R_WERT | unsigned int | SMC_R: Schrittverluste in Bereich 6 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-schrittverluste-smc-loeschen"></a>
### STEUERN_SCHRITTVERLUSTE_SMC_LOESCHEN

STATUS_SCHREIBEN job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fahrgestell-nr-smc-schreiben"></a>
### FAHRGESTELL_NR_SMC_SCHREIBEN

Schreiben der VIN in die linke SMC

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |
| FG_DATEN | string | 7stellige FG-Nr |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fg-nr-smc-lesen"></a>
### FG_NR_SMC_LESEN

Fahrgestellnummer fuer SMC links und rechts lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FG_NR_SMC_LINKS | string | Fahrgestellnummer 7-stellig fuer SMC links |
| FG_NR_SMC_LINKS_KONFIG | int | Konfigbyte Fahrgestellnummer fuer SMC links |
| FG_NR_SMC_RECHTS | string | Fahrgestellnummer 7-stellig fuer SMC rechts |
| FG_NR_SMC_RECHTS_KONFIG | int | Konfigbyte Fahrgestellnummer fuer SMC rechts |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-id-smc-lesen"></a>
### ID_SMC_LESEN

ID SMC links und rechts lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SW_VERSION_SMC_LINKS | string | SW-Version fuer SMC links |
| HW_VERSION_SMC_LINKS | string | HW-Version fuer SMC links |
| CODING_INDEX_SMC_LINKS | string | Codierindex fuer SMC links |
| MCV_VERSION_SMC_LINKS | string | MCV-Version fuer SMC links |
| SW_VERSION_SMC_RECHTS | string | SW-Version fuer SMC rechts |
| HW_VERSION_SMC_RECHTS | string | HW-Version fuer SMC rechts |
| CODING_INDEX_SMC_RECHTS | string | Codierindex fuer SMC rechts |
| MCV_VERSION_SMC_RECHTS | string | MCV-Version fuer SMC rechts |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-scheinwerferherstellerdaten-schreiben"></a>
### SCHEINWERFERHERSTELLERDATEN_SCHREIBEN

Beschreiben der Scheinwerfer-Herstellerdaten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |
| SCHEINWERFER_HERSTELLERDATEN | string | Herstellerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-scheinwerferherstellerdaten-lesen"></a>
### SCHEINWERFERHERSTELLERDATEN_LESEN

Auslesen der Scheinwerfer-Herstellerdaten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SCHEINWERFER_HERSTELLERDATEN | string | Herstellerdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-scheinwerfer-schreiben"></a>
### PRUEFSTEMPEL_SCHEINWERFER_SCHREIBEN

Beschreiben des Scheinwerfer-Pruefstempel

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |
| SCHEINWERFER_PRUEFSTEMPEL | string | Scheinwerfer-Pruefstempel |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-scheinwerfer-lesen"></a>
### PRUEFSTEMPEL_SCHEINWERFER_LESEN

Auslesen der Scheinwerfer-Pruefstempel

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SMC | string | SMC links bzw. rechts |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SCHEINWERFER_PRUEFSTEMPEL | string | Herstellerdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (77 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (4 × 2)
- [FORTTEXTE](#table-forttexte) (13 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (1 × 9)
- [IORTTEXTE](#table-iorttexte) (48 × 2)
- [STEUERN_SMCS](#table-steuern-smcs) (6 × 3)

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

Dimensions: 77 rows × 2 columns

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

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | nein |
| F_HFK | ja |
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 13 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | interner Fehler ALC-SG |
| 0x01 | Kommunikation mit StepperMotorBox 1 gestoert |
| 0x02 | Kommunikation mit StepperMotorBox 2 gestoert |
| 0x03 | Sensor Hoehenstand vorne defekt |
| 0x04 | Sensor Hoehenstand hinten defekt |
| 0x05 | Bremslichtschalter defekt |
| 0x06 | Energiesparmode aktiv |
| 0x07 | Fehler WAKE-Leitung |
| 0x08 | Achtung: Elektronik am linken Scheinwerfer (SMC) meldet Fehler |
| 0x09 | Achtung: Elektronik am rechten Scheinwerfer (SMC) meldet Fehler |
| 0x0A | Vergleich Fahrgestellnummer ALC mit SMC links unterschiedlich |
| 0x0B | Vergleich Fahrgestellnummer ALC mit SMC rechts unterschiedlich |
| 0xFF | unbekannter Fehlerort |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | - | - | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 1 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 48 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x10 | EEPROM SMC links defekt |
| 0x11 | Motor Kurvenlicht SMC links defekt |
| 0x12 | Motor LWR SMC links defekt |
| 0x13 | Treiber Kurvenlicht SMC links defekt |
| 0x14 | Spannungsversorgung Sensor SMC links defekt |
| 0x15 | Signal Sensor SMC links defekt |
| 0x16 | Flanke Sensor SMC links defekt |
| 0x17 | LIN SMC links defekt |
| 0x18 | Schrittverlust Grenze 1 SMC links |
| 0x19 | Schrittverlust Grenze 2 SMC links |
| 0x1A | Schrittverlust Grenze 3 SMC links |
| 0x1B | Schrittverlust Grenze 4 SMC links |
| 0x1C | Schrittverlust Grenze 5 SMC links |
| 0x1D | Schrittverlust Grenze 6 SMC links |
| 0x1E | Spike auf Sensor SMS links |
| 0x1F | Notlauf aktiv SMC links |
| 0x20 | unbekannter Fehler 2 SMC links |
| 0x21 | unbekannter Fehler 3 SMC links |
| 0x22 | unbekannter Fehler 4 SMC links |
| 0x23 | unbekannter Fehler 5 SMC links |
| 0x24 | EEPROM SMC rechts defekt |
| 0x25 | Motor Kurvenlicht SMC rechts defekt |
| 0x26 | Motor LWR SMC rechts defekt |
| 0x27 | Treiber Kurvenlicht SMC rechts defekt |
| 0x28 | Spannungsversorgung Sensor SMC rechts defekt |
| 0x29 | Signal Sensor SMC rechts defekt |
| 0x2A | Flanke Sensor SMC rechts defekt |
| 0x2B | LIN SMC rechts defekt |
| 0x2C | Schrittverlust Grenze 1 SMC rechts |
| 0x2D | Schrittverlust Grenze 2 SMC rechts |
| 0x2E | Schrittverlust Grenze 3 SMC rechts |
| 0x2F | Schrittverlust Grenze 4 SMC rechts |
| 0x31 | Schrittverlust Grenze 5 SMC rechts |
| 0x32 | Schrittverlust Grenze 6 SMC rechts |
| 0x33 | Spike auf Sensor SMS rechts |
| 0x34 | Notlauf aktiv SMC rechts |
| 0x35 | unbekannter Fehler 2 SMC rechts |
| 0x36 | unbekannter Fehler 3 SMC rechts |
| 0x37 | unbekannter Fehler 4 SMC rechts |
| 0x38 | unbekannter Fehler 5 SMC rechts |
| 0x39 | Telegramm Geschwindigkeit ungueltig |
| 0x3A | Telegramm Gierrate ungueltig |
| 0x3B | Telegramm Lenkwinkel ungueltig |
| 0x3C | Telegramm Lampenzustand ungueltig |
| 0x3D | Telegramm Klemmenstatus Timeout oder ungueltig |
| 0x3E | Telegramm Steuerung ALC Timeout oder ungueltig |
| 0x3F | ALC meldet Fehler an Lichtschaltzentrum |
| 0xFF | unbekannter Fehlerort |

<a id="table-steuern-smcs"></a>
### STEUERN_SMCS

Dimensions: 6 rows × 3 columns

| ST_SMC | NAME | TEXT |
| --- | --- | --- |
| 0x10 | ALC_SG | ALC-Steuergeraet |
| 0x89 | SMC_L | SMC links |
| 0x8A | SMC_R | SMC rechts |
| 0x00 | REF_ALC_MIT | Referenzlauf Kurvenlicht mit Sensor |
| 0x01 | REF_ALC_OHNE | Referenzlauf Kurvenlicht ohne Sensor |
| 0x02 | REF_LWR | Referenzlauf LWR |
