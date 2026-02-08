# IHR39.prg

- Jobs: [32](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Integrierte Heizregelung E39 |
| ORIGIN | BMW TP-421 Drexel |
| REVISION | 1.03 |
| AUTHOR | BMW TP-421 Drexel |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Kommunikationsparameter
- [IDENT](#job-ident) - Identifikation
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [DIAGNOSE_TESTBIT](#job-diagnose-testbit) - Ansteuern des Diagnosetest-Bits
- [SLEEP_MODE](#job-sleep-mode) - SG in Power-Down-Mode versetzen
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode aufrechterhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels
- [CODIERUNG_LESEN](#job-codierung-lesen) - Auslesen der Codierdaten
- [CODIERUNG_SCHREIBEN](#job-codierung-schreiben) - Codierdaten Schreiben
- [STATUS_REGLERGROESSEN](#job-status-reglergroessen) - Status lesen
- [STATUS_MOTOR_KLAPPENPOSITION](#job-status-motor-klappenposition) - Status lesen
- [STATUS_IO](#job-status-io) - Status lesen
- [STATUS_ANALOGEINGAENGE](#job-status-analogeingaenge) - Status lesen Analogeingaenge
- [STATUS_BEDIENTEIL](#job-status-bedienteil) - Status lesen
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen des internen Speichers
- [RAM_SCHREIBEN](#job-ram-schreiben) - Beschreiben des internen Speichers
- [EEPROM_SCHREIBEN](#job-eeprom-schreiben) - Beschreiben des internen Speichers
- [STEUERN_RELAIS_HECKSCHEIBE](#job-steuern-relais-heckscheibe) - Ansteuern des Heckscheibenrelais
- [STEUERN_SPRITZDUESENHEIZUNG](#job-steuern-spritzduesenheizung) - Ansteuern des Spritzduesenheizung
- [STEUERN_ZUSATZWASSERPUMPE](#job-steuern-zusatzwasserpumpe) - Ansteuern der Zusatzwasserpumpe
- [STEUERN_SH_SPERRVENTIL](#job-steuern-sh-sperrventil) - Ansteuern des Sperrventils
- [STEUERN_SH_WECKEN](#job-steuern-sh-wecken) - Ansteuern der Standheizung
- [STEUERN_LWS_GEBLAESERELAIS](#job-steuern-lws-geblaeserelais) - Ansteuern des Latentwaermespeicher Geblaeserelais.
- [STEUERN_LWS_UMSCHALTVENTIL](#job-steuern-lws-umschaltventil) - Ansteuern des Sperrventils
- [STEUERN_LWS_ABSPERRVENTIL](#job-steuern-lws-absperrventil) - Ansteuern des Absperrventils des Latentwaermespeichers
- [STEUERN_WASSERVENTIL](#job-steuern-wasserventil) - Ansteuern des linken und rechten Wasserventils
- [STEUERN_MOTOR](#job-steuern-motor) - Ansteuern des Schrittmotors
- [STEUERN_TOGGLE_UMLUFT](#job-steuern-toggle-umluft) - Ansteuern des Schrittmotors

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
| AUTHOR | string | Name aller Autoren |
| COMMENT | string | wichtige Hinweise |
| SPRACHE | string | deutsch, english |

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-ident"></a>
### IDENT

Identifikation

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

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Text zu Fehlerort |
| F_HFK | int | Fehlerhaeufigkeit |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen |
| F_ART1_NR | int |  |
| F_ART1_TEXT | string |  |
| F_ART2_NR | int |  |
| F_ART2_TEXT | string |  |
| F_ART3_NR | int |  |
| F_ART3_TEXT | string |  |
| F_ART4_NR | int |  |
| F_ART4_TEXT | string |  |
| FEHLERTELEGRAMM | binary | Antworttelegramm ohne Header und Checksumme |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-diagnose-testbit"></a>
### DIAGNOSE_TESTBIT

Ansteuern des Diagnosetest-Bits

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TESTBIT | string | 'EIN','AUS' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Power-Down-Mode versetzen

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

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | kann beliebig verwendet werden 0x00-0xFF |
| BYTE2 | int | kann beliebig verwendet werden 0x00-0xFF |
| BYTE3 | int | kann beliebig verwendet werden 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Auslesen der Codierdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| CODE | string | 4 Codierbytes in Hex |
| STEUERGERAET | string | 'IHKA E38' 'IHKA E39' 'IHKR E38' 'IHKR E39' 'IHR E38' 'IHR E39' 'FHK E38' 'FHK E39' 'frei' 'unbekannter Code' |
| LENKUNG | string | 'Linkslenker' 'Rechtslenker' |
| LAENDERVARIANTE | string | 'ECE' 'US' 'frei' 'Nordland' 'unbekannter Code' |
| MOTORVARIANTE | string | 'Benzinmotor' 'Dieselmotor' 'unbekannter Code' |
| ZYLINDERZAHL | string | '4 Zylinder' '6 Zylinder' '8 Zylinder' '12 Zylinder' 'unbekannter Code' |
| AUSSTATTUNG_1 | string | 'default' 'Standheizung low' 'Standheizung high' '' |
| AUSSTATTUNG_2 | string | 'Latentwaermespeicher low' 'Latentwaermespeicher high' '' |
| AUSSTATTUNG_3 | string | 'Sperrventil' '' |
| AUSSTATTUNG_4 | string | 'Zusatzwasserpumpe' '' |
| ALLGEMEIN_1 | string | 'Kennfeldkuehlung' '' |
| ALLGEMEIN_2 | string | 'ohne AT-Korrektur' '' |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-codierung-schreiben"></a>
### CODIERUNG_SCHREIBEN

Codierdaten Schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODE1 | int | kann beliebig verwendet werden 0x00-0xFF |
| CODE2 | int | kann beliebig verwendet werden 0x00-0xFF |
| CODE3 | int | kann beliebig verwendet werden 0x00-0xFF |
| CODE4 | int | kann beliebig verwendet werden 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-status-reglergroessen"></a>
### STATUS_REGLERGROESSEN

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_TAUSSEN_WERT | int |  |
| STAT_TAUSSEN_EINH | string | Grad Celsius |
| STAT_SOLL_LI_WERT | real |  |
| STAT_SOLL_LI_EINH | string | Grad Celsius |
| STAT_SOLL_RE_WERT | real |  |
| STAT_SOLL_RE_EINH | string | Grad Celsius |
| STAT_SOLL_LI_KORRIGIERT_WERT | real |  |
| STAT_SOLL_LI_KORRIGIERT_EINH | string | Grad Celsius |
| STAT_SOLL_RE_KORRIGIERT_WERT | real |  |
| STAT_SOLL_RE_KORRIGIERT_EINH | string | Grad Celsius |
| STAT_FUSSRAUM_LI_WERT | real |  |
| STAT_FUSSRAUM_LI_EINH | string | Volt |
| STAT_FUSSRAUM_RE_WERT | real |  |
| STAT_FUSSRAUM_RE_EINH | string | Volt |
| STAT_FUSSRAUM_LI_VERZ_WERT | real |  |
| STAT_FUSSRAUM_LI_VERZ_EINH | string | Grad Celsius |
| STAT_FUSSRAUM_RE_VERZ_WERT | real |  |
| STAT_FUSSRAUM_RE_VERZ_EINH | string | Grad Celsius |
| STAT_Y_LI_WERT | real |  |
| STAT_Y_LI_EINH | string | % |
| STAT_Y_RE_WERT | real |  |
| STAT_Y_RE_EINH | string | % |
| STAT_WTSOLL_LI_WERT | real |  |
| STAT_WTSOLL_LI_EINH | string | Grad Celsius |
| STAT_WTSOLL_RE_WERT | real |  |
| STAT_WTSOLL_RE_EINH | string | Grad Celsius |
| STAT_WT_LI_WERT | real |  |
| STAT_WT_LI_EINH | string | Volt |
| STAT_WT_RE_WERT | real |  |
| STAT_WT_RE_EINH | string | Volt |
| STAT_WT_LI_VERZ_WERT | real |  |
| STAT_WT_LI_VERZ_EINH | string | Grad Celsius |
| STAT_WT_RE_VERZ_WERT | real |  |
| STAT_WT_RE_VERZ_EINH | string | Grad Celsius |
| STAT_YWT_LI_WERT | real |  |
| STAT_YWT_LI_EINH | string | % |
| STAT_YWT_RE_WERT | real |  |
| STAT_YWT_RE_EINH | string | % |
| STAT_WASSERVENTIL_LI_WERT | int |  |
| STAT_WASSERVENTIL_LI_EINH | string | ms |
| STAT_WASSERVENTIL_RE_WERT | int |  |
| STAT_WASSERVENTIL_RE_EINH | string | ms |
| STAT_DREHZAHL_WERT | int |  |
| STAT_DREHZAHL_EINH | string | 1/min |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-status-motor-klappenposition"></a>
### STATUS_MOTOR_KLAPPENPOSITION

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_MOTOR_EINH | string |  |
| STAT_UMLUFT_WERT | int |  |
| STAT_FRISCHLUFT_WERT | int |  |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-status-io"></a>
### STATUS_IO

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_TASTE_UMLUFT_EIN | int |  |
| STAT_TASTE_HECKSCHEIBE_EIN | int |  |
| STAT_RELAIS_HECKSCHEIBE_EIN | int |  |
| STAT_SPRITZDUESENHEIZUNG_EIN | int |  |
| STAT_WASSERVENTIL_RE_EIN | int |  |
| STAT_WASSERVENTIL_LI_EIN | int |  |
| STAT_ZUSATZWASSERPUMPE_EIN | int |  |
| STAT_SH_WECKEN_EIN | int |  |
| STAT_SH_SPERRVENTIL_EIN | int |  |
| STAT_SH_TELESTART_EIN | int |  |
| STAT_LWS_GEBLAESERELAIS_EIN | int |  |
| STAT_LWS_UMSCHALTVENTIL_EIN | int |  |
| STAT_LWS_ABSPERRVENTIL_EIN | int |  |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-status-analogeingaenge"></a>
### STATUS_ANALOGEINGAENGE

Status lesen Analogeingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_SOLL_LI_WERT | real |  |
| STAT_SOLL_LI_EINH | string | Grad Celsius |
| STAT_SOLL_RE_WERT | real |  |
| STAT_SOLL_RE_EINH | string | Grad Celsius |
| STAT_FUSSRAUM_LI_WERT | real |  |
| STAT_FUSSRAUM_LI_EINH | string | Volt |
| STAT_FUSSRAUM_RE_WERT | real |  |
| STAT_FUSSRAUM_RE_EINH | string | Volt |
| STAT_FUSSRAUM_LI_VERZ_WERT | real |  |
| STAT_FUSSRAUM_LI_VERZ_EINH | string | Grad Celsius |
| STAT_FUSSRAUM_RE_VERZ_WERT | real |  |
| STAT_FUSSRAUM_RE_VERZ_EINH | string | Grad Celsius |
| STAT_WT_LI_WERT | real |  |
| STAT_WT_LI_EINH | string | Volt |
| STAT_WT_RE_WERT | real |  |
| STAT_WT_RE_EINH | string | Volt |
| STAT_WT_LI_VERZ_WERT | real |  |
| STAT_WT_LI_VERZ_EINH | string | Grad Celsius |
| STAT_WT_RE_VERZ_WERT | real |  |
| STAT_WT_RE_VERZ_EINH | string | Grad Celsius |
| STAT_LWS_FUEHLER_WERT | int |  |
| STAT_LWS_FUEHLER_EINH | string | Grad Celsius |
| TELEGRAMM1 | binary | Antworttelegramm |
| TELEGRAMM2 | binary | Antworttelegramm |

<a id="job-status-bedienteil"></a>
### STATUS_BEDIENTEIL

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_SOLL_LI_WERT | real |  |
| STAT_SOLL_LI_EINH | string | 'Grad Celsius' |
| STAT_SOLL_RE_WERT | real |  |
| STAT_SOLL_RE_EINH | string | 'Grad Celsius' |
| STAT_TASTE_UMLUFT_EIN | int |  |
| STAT_TASTE_HHS_EIN | int |  |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Lesen des internen Speichers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int |  |
| ANZAHL | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-ram-schreiben"></a>
### RAM_SCHREIBEN

Beschreiben des internen Speichers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int |  |
| ANZAHL | int |  |
| DATEN | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-eeprom-schreiben"></a>
### EEPROM_SCHREIBEN

Beschreiben des internen Speichers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int |  |
| ANZAHL | int |  |
| DATEN | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-relais-heckscheibe"></a>
### STEUERN_RELAIS_HECKSCHEIBE

Ansteuern des Heckscheibenrelais

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RELAIS_HECKSCHEIBE | string | 'EIN','AUS' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-spritzduesenheizung"></a>
### STEUERN_SPRITZDUESENHEIZUNG

Ansteuern des Spritzduesenheizung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPRITZDUESENHEIZUNG | string | 'EIN','AUS' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-zusatzwasserpumpe"></a>
### STEUERN_ZUSATZWASSERPUMPE

Ansteuern der Zusatzwasserpumpe

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZUSATZWASSERPUMPE | string | 'EIN','AUS' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-sh-sperrventil"></a>
### STEUERN_SH_SPERRVENTIL

Ansteuern des Sperrventils

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SH_SPERRVENTIL | string | 'EIN','AUS' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-sh-wecken"></a>
### STEUERN_SH_WECKEN

Ansteuern der Standheizung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SH_WECKEN | string | 'EIN','AUS' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-lws-geblaeserelais"></a>
### STEUERN_LWS_GEBLAESERELAIS

Ansteuern des Latentwaermespeicher Geblaeserelais.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LWS_GEBLAESERELAIS | string | 'EIN','AUS' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-lws-umschaltventil"></a>
### STEUERN_LWS_UMSCHALTVENTIL

Ansteuern des Sperrventils

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LWS_UMSCHALTVENTIL | string | 'EIN','AUS' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-lws-absperrventil"></a>
### STEUERN_LWS_ABSPERRVENTIL

Ansteuern des Absperrventils des Latentwaermespeichers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LWS_ABSPERRVENTIL | string | 'EIN','AUS' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-wasserventil"></a>
### STEUERN_WASSERVENTIL

Ansteuern des linken und rechten Wasserventils

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WASSERVENTIL_LINKS | int | Einschaltdauer in Prozentschritten 0-100 % |
| WASSERVENTIL_RECHTS | int | Einschaltdauer in Prozentschritten 0-100 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-motor"></a>
### STEUERN_MOTOR

Ansteuern des Schrittmotors

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MOTOR | string | 0-100 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-toggle-umluft"></a>
### STEUERN_TOGGLE_UMLUFT

Ansteuern des Schrittmotors

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (8 × 2)
- [LIEFERANTEN](#table-lieferanten) (27 × 2)
- [FORTTEXTE](#table-forttexte) (19 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 8 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xB2 | ERROR_ECU_NUMBER |
| 0xFF | ERROR_ECU_NACK |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 27 rows × 2 columns

| LIEF_NR | LIEF_NAME |
| --- | --- |
| 0x01 | Reinshagen |
| 0x02 | Kostal |
| 0x03 | Hella |
| 0x04 | Siemens |
| 0x05 | Eaton |
| 0x06 | UTA |
| 0x07 | Helbako |
| 0x08 | Bosch |
| 0x09 | Loewe |
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
| 0xFF | unbekannter Hersteller |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 19 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x0B | Frischluftklappenmotor |
| 0x0D | Sollwertsteller links |
| 0x0E | Sollwertsteller rechts |
| 0x10 | Waermetauscherfuehler links |
| 0x11 | Waermetauscherfuehler rechts |
| 0x20 | Fussraumtemperaturfuehler links |
| 0x21 | Fussraumtemperaturfuehler rechts |
| 0x24 | Heckscheibenheizung Taste mit LED |
| 0x26 | Umluft Taste mit LED |
| 0x2A | Relais Spritzduesenheizung |
| 0x2B | Relais Heckscheibenheizung |
| 0x2D | Zusatzwasserpumpe |
| 0x2E | Wasserventil links |
| 0x2F | Wasserventil rechts |
| 0x30 | Standheizung Sperrventil, Latentwaermespeicher Umschaltventil |
| 0x31 | Standheizung Weckleitung, Latentwaermespeicher Geblaeserelais |
| 0x32 | Latentwaermespeicher Temperaturfuehler |
| 0x33 | Latentwaermespeicher Absperrventil |
| 0xFF | unbekannter Fehlerort |
