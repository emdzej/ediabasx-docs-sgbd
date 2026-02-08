# atc40.prg

- Jobs: [12](#jobs)
- Tables: [2](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Klimaautomatik R40 |
| ORIGIN | BMW TI-433 Drexel |
| REVISION | 0.03 |
| AUTHOR | BMW TI-433 Drexel |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode aufrechterhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [IDENT](#job-ident) - Identdaten
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen
- [STATUS_ANALOGEINGAENGE](#job-status-analogeingaenge) - Status lesen
- [STATUS_REGLERGROESSEN](#job-status-reglergroessen) - Status lesen
- [STATUS_MOTOR_KLAPPENPOSITION](#job-status-motor-klappenposition) - Status lesen
- [STATUS_IO](#job-status-io) - Status lesen
- [STATUS_BEDIENTEIL](#job-status-bedienteil) - Status lesen

<a id="job-info"></a>
### INFO

Information SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ECU | string | Steuergeraet im Klartext |
| ORIGIN | string | Steuergeraete-Verantwortlicher |
| REVISION | string | Versions-Nummer |
| AUTHOR | string | Namen aller Autoren |
| COMMENT | string | wichtige Hinweise |
| SPRACHE | string | deutsch, english |

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung und Kommunikationsparameter DS2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Sleep-Mode versetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

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

<a id="job-ident"></a>
### IDENT

Identdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Nummer |
| ID_SW_NR | int | Softwarenummer |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Text zu Fehlerort table FOrtTexte ORTTEXT |
| F_ART_ANZ | int | Anzahl der Fehlerarten immer 0 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen immer 0 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-status-analogeingaenge"></a>
### STATUS_ANALOGEINGAENGE

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_WT_WERT | real | Waermetauscherfuehler |
| STAT_WT_EINH | string | Grad Celsius |
| STAT_TVERDAMPFER_WERT | real | Verdampfertemperaturfuehler |
| STAT_TVERDAMPFER_EINH | string | Grad Celsius |
| STAT_TINNEN_WERT | real | Innentemperaturfuehler |
| STAT_TINNEN_EINH | string | Grad Celsius |
| STAT_TAUSSEN_WERT | long | Aussentemperatur |
| STAT_TAUSSEN_EINH | string | Grad Celsius |
| STAT_SOLARSENSOR_RE_WERT | real | Solarsensor rechts |
| STAT_SOLARSENSOR_RE_EINH | string | W/m2 |
| STAT_SOLARSENSOR_LI_WERT | real | Solarsensor links |
| STAT_SOLARSENSOR_LI_EINH | string | W/m2 |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-status-reglergroessen"></a>
### STATUS_REGLERGROESSEN

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_SOLL_LI_WERT | int | Sollwert Temperatur links |
| STAT_SOLL_LI_EINH | string | Grad Celsius |
| STAT_SOLL_RE_WERT | int | Sollwert Temperatur rechts |
| STAT_SOLL_RE_EINH | string | Grad Celsius |
| STAT_TINNEN_WERT | real | Innentemperatur |
| STAT_TINNEN_EINH | string | Grad Celsius |
| STAT_TAUSSEN_WERT | real | Aussentemperatur |
| STAT_TAUSSEN_EINH | string | Grad Celsius |
| STAT_WT_WERT | real | Waermetauscherfuehler |
| STAT_WT_EINH | string | Grad Celsius |
| STAT_GEBLAESE_WERT | int | Geblaesestufe |
| STAT_GEBLAESE_EINH | string | % |
| STAT_LUFTTEMPERATUR_SOLL_LI_WERT | real | erforderliche Luftauslasstemperatur links |
| STAT_LUFTTEMPERATUR_SOLL_LI_EINH | string | Grad Celsius |
| STAT_LUFTTEMPERATUR_SOLL_RE_WERT | real | erforderliche Luftauslasstemperatur rechts |
| STAT_LUFTTEMPERATUR_SOLL_RE_EINH | string | Grad Celsius |
| STAT_LUFTTEMPERATUR_LI_WERT | real | Luftauslasstemperatur links |
| STAT_LUFTTEMPERATUR_LI_EINH | string | Grad Celsius |
| STAT_LUFTTEMPERATUR_RE_WERT | real | Luftauslasstemperatur rechts |
| STAT_LUFTTEMPERATUR_RE_EINH | string | Grad Celsius |
| STAT_GESCHWINDIGKEIT_WERT | int | Fahrzeuggeschwindigkeit |
| STAT_GESCHWINDIGKEIT_EINH | string | km/h |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-status-motor-klappenposition"></a>
### STATUS_MOTOR_KLAPPENPOSITION

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_MOTOR_EINH | string | % |
| STAT_TEMPERATURMISCHUNG_LI_WERT | int | Temperaturmischmotor links 0 - 100 % |
| STAT_TEMPERATURMISCHUNG_RE_WERT | int | Temperaturmischmotor rechts 0 - 100 % |
| STAT_LUFTVERTEILUNG_WERT | int | Luftverteilungsmotor |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-status-io"></a>
### STATUS_IO

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_LINKSLENKER_EIN | int | Linkslenkerfahrzeug |
| STAT_NORMALFUNKTION_EIN | int | Normalfunktion |
| STAT_ANSTEUERUNG_KOMPRESSOR_EIN | int | Klimakompressor |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-status-bedienteil"></a>
### STATUS_BEDIENTEIL

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_SOLL_LI_WERT | int | Sollwert Temperatur links |
| STAT_SOLL_LI_EINH | string | Grad Celsius |
| STAT_SOLL_RE_WERT | int | Sollwert Temperatur rechts |
| STAT_SOLL_RE_EINH | string | Grad Celsius |
| STAT_GEBLAESE_WERT | int | Geblaesestufe |
| STAT_GEBLAESE_EINH | string | % |
| STAT_FUNKTION_AC_EIN | int | Klimabetrieb |
| STAT_FUNKTION_FRISCHLUFT_EIN | int | Frischluftbetrieb |
| STAT_FUNKTION_UMLUFT_EIN | int | Umluftbetrieb |
| TELEGRAMM | binary | Antworttelegramm |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (10 × 2)
- [FORTTEXTE](#table-forttexte) (10 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 10 rows × 2 columns

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
| 0x?? | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 10 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x11 | Innenraumtemperaturfuehler |
| 0x12 | Aussentemperatur |
| 0x13 | Verdampferfuehler |
| 0x14 | Waermetauscherfuehler |
| 0x21 | Solarsensor links |
| 0x22 | Solarsensor rechts |
| 0x31 | Temperatur-Mischklappenmotor oder Potentiometer links |
| 0x32 | Temperatur-Mischklappenmotor oder Potentiometer rechts |
| 0x33 | Luftverteilungsklappenmotor oder Potentiometer |
| 0xFF | unbekannter Fehlerort |
