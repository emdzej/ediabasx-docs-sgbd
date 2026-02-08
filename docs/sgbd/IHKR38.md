# IHKR38.prg

- Jobs: [35](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Integrierte Heiz- Klimaregelung E38 |
| ORIGIN | BMW TP-421 Drexel |
| REVISION | 1.12 |
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
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode aufrechterhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [SLEEP_MODE](#job-sleep-mode) - SG in Power-Down-Mode versetzen
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels
- [CODIERUNG_LESEN](#job-codierung-lesen) - Auslesen der Codierdaten
- [CODIERUNG_SCHREIBEN](#job-codierung-schreiben) - Codierdaten Schreiben
- [STATUS_ANALOGEINGAENGE](#job-status-analogeingaenge) - Status lesen
- [STATUS_REGLERGROESSEN](#job-status-reglergroessen) - Status lesen
- [STATUS_BEDIENTEIL](#job-status-bedienteil) - Status lesen
- [STATUS_AUSGAENGE](#job-status-ausgaenge) - Status lesen
- [STATUS_MOTOR_KLAPPENPOSITION](#job-status-motor-klappenposition) - Status lesen
- [STATUS_IO](#job-status-io) - Status lesen
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen des internen Speichers
- [RAM_SCHREIBEN](#job-ram-schreiben) - Beschreiben des internen Speichers
- [EEPROM_SCHREIBEN](#job-eeprom-schreiben) - Beschreiben des internen Speichers
- [EICHLAUF_STARTEN](#job-eichlauf-starten) - Anstossen der internen Eichlaufroutine
- [STEUERN_RELAIS_HECKSCHEIBE](#job-steuern-relais-heckscheibe) - Ansteuern des Heckscheibenrelais
- [STEUERN_RELAIS_FRONTSCHEIBE](#job-steuern-relais-frontscheibe) - Ansteuern des Frontscheibenrelais
- [STEUERN_RELAIS_ZUSATZLUEFTER](#job-steuern-relais-zusatzluefter) - Ansteuern des Zusatzluefterrelais
- [STEUERN_ZUSATZWASSERPUMPE](#job-steuern-zusatzwasserpumpe) - Ansteuern der Zusatzwasserpumpe
- [STEUERN_DME_AC](#job-steuern-dme-ac) - Ansteuern des DME-AC-Signals
- [STEUERN_DME_KO](#job-steuern-dme-ko) - Ansteuern des DME-KO-Signals
- [STEUERN_KLIMAKOMPRESSOR](#job-steuern-klimakompressor) - Ansteuern des Klimakompressors
- [STEUERN_SPERRVENTIL](#job-steuern-sperrventil) - Ansteuern des Sperrventils
- [STEUERN_STANDHEIZUNG](#job-steuern-standheizung) - Ansteuern der Standheizung
- [STEUERN_MOTOR_KLAPPENPOSITION](#job-steuern-motor-klappenposition) - Ansteuern der Schrittmotoren
- [STEUERN_WASSERVENTIL](#job-steuern-wasserventil) - Ansteuern des linken und rechten Wasserventils
- [STEUERN_AUSGAENGE](#job-steuern-ausgaenge) - Ansteuern der Ausgaenge

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
| F_ART5_NR | int |  |
| F_ART5_TEXT | string |  |
| F_ART6_NR | int |  |
| F_ART6_TEXT | string |  |
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

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Power-Down-Mode versetzen

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
| FAHRZEUGTYP | string | 'E38' 'frei' |
| LAENDERVARIANTE | string | 'ECE' 'US' 'ohne Heizregelung' 'frei' 'unbekannter Code' |
| AUSGANGSPEGEL_AC | string | 'DME-AC HIGH-aktiv' 'DME-AC LOW-aktiv' 'DME-AC Entfall' |
| AUSGANGSPEGEL_KO | string | 'DME-KO HIGH-aktiv' 'DME-KO LOW-aktiv' |
| AUSSTATTUNG_1 | string | 'Filter' 'AUC' |
| AUSSTATTUNG_2 | string | 'Kompressoraustaktung' '' |
| AUSSTATTUNG_3 | string | 'Standheizung' '' |
| AUSSTATTUNG_4 | string | 'FHK' '' |
| AUSSTATTUNG_5 | string | 'Umluft Memoryfunktion' '' |
| AUSSTATTUNG_6 | string | 'Kompressorabschaltung' '' |
| STEUERGERAET | string | 'IHKA' 'IHKR' |
| ZYLINDERZAHL | string | '4-Zylinder' '6-Zylinder' '8-Zylinder' '12-Zylinder' 'unbekannter Code' |
| MOTORVARIANTE | string | 'Benzinmotor' 'Dieselmotor' 'unbekannter Code' |
| LENKUNG | string | 'Linkslenker' 'Rechtslenker' |
| SENSORIK | string | 'default' 'Schrittmotordiagnose deaktiviert' 'frei' 'unbekannter Code' |
| LEERLAUFANHEBUNG_1 | string | 'default' 'bei elektrischen Verbrauchern' 'bei Unterspannung' |
| LEERLAUFANHEBUNG_2 | string | 'bei Unterspannung' ( nicht wenn in .._1 ) '' |
| ALLGEMEIN_1 | string | 'default' 'Eichlauf Entfrostung speziell' 'Fuss-Fond-Kurve variabel' |
| ALLGEMEIN_2 | string | 'Fuss-Fond-Kurve variabel' ( nicht wenn in .._1 ) '' |
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

<a id="job-status-analogeingaenge"></a>
### STATUS_ANALOGEINGAENGE

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_SOLL_LI_WERT | real | Grad Celsius |
| STAT_SOLL_RE_WERT | real | Grad Celsius |
| STAT_WT_LI_WERT | real | Grad Celsius |
| STAT_WT_RE_WERT | real | Grad Celsius |
| STAT_TVERDAMPFER_WERT | real | Grad Celsius |
| STAT_TINNEN_WERT | real | Grad Celsius |
| STAT_GEBL_RUECK_WERT | real | % |
| STAT_GEBL_RUECK_TEXT | string | 'aus','Stufe 1','Stufe 2' 'Stufe 3','Stufe 4','defrost' |
| STAT_KLEMME30_WERT | real | Volt |
| STAT_LUFTVERT_WERT | real | % |
| STAT_LUFTVERT_TEXT | string | 'oben','vorne','unten' 'normal','oben und unten' |
| STAT_TI_FUEGEBL_WERT | real | Volt |
| STAT_DME_KO_WERT | real | Volt |
| STAT_DME_AC_WERT | real | Volt |
| STAT_TAUSSEN_WERT | real | Grad Celsius |
| STAT_TKUEHLERWASSER_WERT | real | Grad Celsius |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-status-reglergroessen"></a>
### STATUS_REGLERGROESSEN

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_SOLL_LI_WERT | real | Grad Celsius |
| STAT_SOLL_RE_WERT | real | Grad Celsius |
| STAT_TINNEN_WERT | real | Grad Celsius |
| STAT_TAUSSEN_WERT | real | Grad Celsius |
| STAT_WT_LI_WERT | real | Grad Celsius |
| STAT_WT_RE_WERT | real | Grad Celsius |
| STAT_SOLL_LI_KORRIGIERT_WERT | real | Grad Celsius |
| STAT_SOLL_RE_KORRIGIERT_WERT | real | Grad Celsius |
| STAT_WTSOLL_LI_WERT | real | Grad Celsius |
| STAT_WTSOLL_RE_WERT | real | Grad Celsius |
| STAT_YWT_LI_WERT | real | % |
| STAT_YWT_RE_WERT | real | % |
| STAT_DIFFSOLL_WERT | real | Grad Celsius |
| STAT_DIFFSOLL_VERZOEGERT_WERT | real | Grad Celsius |
| STAT_FUEHR_LI_WERT | real | % |
| STAT_FUEHR_RE_WERT | real | % |
| STAT_DREHZAHL_WERT | real | 1/min |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-status-bedienteil"></a>
### STATUS_BEDIENTEIL

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_SOLL_LI_WERT | long |  |
| STAT_SOLL_LI_EINH | string | Grad Celsius |
| STAT_SOLL_RE_WERT | long |  |
| STAT_SOLL_RE_EINH | string | Grad Celsius |
| STAT_GEBL_RUECK_WERT | real |  |
| STAT_GEBL_RUECK_EINH | string | % |
| STAT_GEBL_RUECK_TEXT | string | 'aus','Stufe 1','Stufe 2' 'Stufe 3','Stufe 4','defrost' |
| STAT_LUFTVERT_WERT | real |  |
| STAT_LUFTVERT_EINH | string | % |
| STAT_LUFTVERT_TEXT | string | 'oben','vorne','unten' 'normal','oben und unten' |
| STAT_FUNKTION_UMLUFT_EIN | int |  |
| STAT_FUNKTION_AC_EIN | int |  |
| STAT_FUNKTION_HHS_EIN | int |  |

<a id="job-status-ausgaenge"></a>
### STATUS_AUSGAENGE

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_SOLL_LI_WERT | real | Grad Celsius |
| STAT_SOLL_RE_WERT | real | Grad Celsius |
| STAT_Y_LI_WERT | real | % |
| STAT_Y_RE_WERT | real | % |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-status-motor-klappenposition"></a>
### STATUS_MOTOR_KLAPPENPOSITION

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_FRISCHLUFT_WERT | int | % |
| STAT_ZENTRALANTRIEB_WERT | int | % |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-status-io"></a>
### STATUS_IO

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_FUNKTION_HHS_EIN | int |  |
| STAT_FUNKTION_AC_EIN | int |  |
| STAT_FUNKTION_UMLUFT_EIN | int |  |
| STAT_ZUSATZLUEFTER_STUFE_1_EIN | int |  |
| STAT_RELAIS_FRONTSCHEIBE_EIN | int |  |
| STAT_RELAIS_HECKSCHEIBE_EIN | int |  |
| STAT_LED_AC_EIN | int |  |
| STAT_LED_UMLUFT_EIN | int |  |
| STAT_LED_HHS_EIN | int |  |
| STAT_EICHSCHALTER_EIN | int |  |
| STAT_ANSTEUERUNG_KOMPRESSOR_EIN | int |  |
| STAT_ANSTEUERUNG_SPERRVENTIL_EIN | int |  |
| STAT_STAT_ANSTEUERUNG_KOMP_EIN | int |  |
| STAT_STANDHEIZEN_EIN | int |  |
| STAT_TASTER_UMLUFT_EIN | int |  |
| STAT_TASTER_AC_EIN | int |  |
| STAT_TASTER_HHS_EIN | int |  |
| STAT_WASSERVENTIL_LI_EIN | int |  |
| STAT_WASSERVENTIL_RE_EIN | int |  |
| STAT_ZUSATZWASSERPUMPE_EIN | int |  |
| STAT_MONITOR_ZUSATZWASSERPUMPE_EIN | int |  |
| STAT_DME_AC_EIN | int |  |
| STAT_DME_KO_EIN | int |  |
| STAT_MONITOR_WASSERVENTIL_LI_EIN | int |  |
| STAT_MONITOR_WASSERVENTIL_RE_EIN | int |  |
| TELEGRAMM | binary | Antworttelegramm |

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

<a id="job-eichlauf-starten"></a>
### EICHLAUF_STARTEN

Anstossen der internen Eichlaufroutine

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

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

<a id="job-steuern-relais-frontscheibe"></a>
### STEUERN_RELAIS_FRONTSCHEIBE

Ansteuern des Frontscheibenrelais

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RELAIS_FRONTSCHEIBE | string | 'EIN','AUS' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-relais-zusatzluefter"></a>
### STEUERN_RELAIS_ZUSATZLUEFTER

Ansteuern des Zusatzluefterrelais

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RELAIS_ZUSATZLUEFTER | string | 'EIN','AUS' |

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

<a id="job-steuern-dme-ac"></a>
### STEUERN_DME_AC

Ansteuern des DME-AC-Signals

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DME_AC | string | 'EIN','AUS' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-dme-ko"></a>
### STEUERN_DME_KO

Ansteuern des DME-KO-Signals

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DME_KO | string | 'EIN','AUS' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-klimakompressor"></a>
### STEUERN_KLIMAKOMPRESSOR

Ansteuern des Klimakompressors

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KLIMAKOMPRESSOR | string | 'EIN','AUS' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-sperrventil"></a>
### STEUERN_SPERRVENTIL

Ansteuern des Sperrventils

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPERRVENTIL | string | 'EIN','AUS' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-standheizung"></a>
### STEUERN_STANDHEIZUNG

Ansteuern der Standheizung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STANDHEIZUNG | string | 'EIN','AUS' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-motor-klappenposition"></a>
### STEUERN_MOTOR_KLAPPENPOSITION

Ansteuern der Schrittmotoren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FRISCHLUFT | int |  |
| ZENTRALANTRIEB | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

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

<a id="job-steuern-ausgaenge"></a>
### STEUERN_AUSGAENGE

Ansteuern der Ausgaenge

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSGAENGE | string | 'EIN','AUS','ENDE' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (8 × 2)
- [LIEFERANTEN](#table-lieferanten) (27 × 2)
- [FORTTEXTE](#table-forttexte) (68 × 2)

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

Dimensions: 68 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | Belueftungsklappenmotor links IHKA |
| 0x01 | Belueftungsklappenmotor rechts IHKA |
| 0x02 | Umluftklappenmotor IHKA |
| 0x03 | Entfrostungsklappenmotor IHKA |
| 0x04 | Fussraumklappenmotor links IHKA |
| 0x05 | Fussraumklappenmotor rechts IHKA |
| 0x06 | Schichtungsklappenmotor links IHKA |
| 0x07 | Schichtungsklappenmotor rechts IHKA |
| 0x08 | Fondraumklappenmotor IHKA |
| 0x09 | frei 0x09 |
| 0x0A | Frischluftklappenmotor IHKA |
| 0x0B | Frischluftklappenmotor |
| 0x0C | Zentralantrieb |
| 0x0D | Geblaesepotentiometer links IHKA |
| 0x0E | Geblaesepotentiometer rechts IHKA |
| 0x0F | AUC Sensor |
| 0x10 | Waermetauscherfuehler links |
| 0x11 | Waermetauscherfuehler rechts |
| 0x12 | Verdampferfuehler |
| 0x13 | Innenraumtemperaturfuehler |
| 0x14 | Geblaesepotentiometer |
| 0x15 | Klemme 30 |
| 0x16 | Potentiometer Luftverteilung |
| 0x17 | Innenfuehlergeblaese |
| 0x18 | frei 0x018 |
| 0x19 | AUC Heizung |
| 0x1A | DME-KO |
| 0x1B | DME-AC |
| 0x1C | frei 0x1C |
| 0x1D | Fondraumschalter |
| 0x1E | frei 0x1E |
| 0x1F | frei 0x1F |
| 0x20 | Belueftungstemperaturfuehler links IHKA |
| 0x21 | Belueftungstemperaturfuehler rechts IHKA |
| 0x22 | Schichtungspotentiometer vorne IHKA |
| 0x23 | Schichtungspotentiometer hinten IHKA |
| 0x24 | LED Heckscheibenheizung |
| 0x25 | LED Klima |
| 0x26 | LED Umluft |
| 0x27 | frei 0x27 |
| 0x28 | AUC Heizung |
| 0x29 | Relais Zusatzluefter |
| 0x2A | Relais Frontscheibenheizung |
| 0x2B | Relais Heckscheibenheizung |
| 0x2C | Magnetkupplung Klimakompressor |
| 0x2D | Zusatzwasserpumpe |
| 0x2E | Wasserventil links |
| 0x2F | Wasserventil rechts |
| 0x30 | Standheizung Sperrventil |
| 0x31 | Standheizung Weckleitung |
| 0x32 | Stellgroesse Y links |
| 0x33 | Stellgroesse Y rechts |
| 0x34 | Waermetauschersolltemperatur links |
| 0x35 | Waermetauschersolltemperatur rechts |
| 0x36 | Aussentemperatur |
| 0x37 | Fahrzeuggeschwindigkeit |
| 0x38 | Kuehlwassertemperatur |
| 0x39 | Motordrehzahl |
| 0x3A | Klemme 58 g |
| 0x3B | Motorhaube offen |
| 0x3C | Rueckwaertsgang eingelegt |
| 0x3D | Motor laeuft |
| 0x3E | Standlueftung ein/aus |
| 0x3F | Standheizung ein/aus |
| 0x40 | AUC Sensor |
| 0x41 | Eichschalter |
| 0x42 | Geblaesesteuerspannung |
| 0xFF | unbekannter Fehlerort |
