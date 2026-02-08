# IHKA39.prg

- Jobs: [38](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Integrierte Heiz- Klimaautomatik E39 |
| ORIGIN | BMW TP-421 Drexel |
| REVISION | 1.07 |
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
- [STATUS_MOTOR_KLAPPENPOSITION](#job-status-motor-klappenposition) - Status lesen
- [STATUS_IO](#job-status-io) - Status lesen
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen des internen Speichers
- [RAM_SCHREIBEN](#job-ram-schreiben) - Beschreiben des internen Speichers
- [EEPROM_SCHREIBEN](#job-eeprom-schreiben) - Beschreiben des internen Speichers
- [DIAGNOSE_TESTBIT](#job-diagnose-testbit) - Ansteuern des Diagnosetest-Bits
- [EICHLAUF_STARTEN](#job-eichlauf-starten) - Anstossen der internen Eichlaufroutine
- [DISPLAY_TEST](#job-display-test) - Einschalten eines Testmusters in den Displays Es muss der Displaytest immer ausgeschalten werden
- [STEUERN_RELAIS_HECKSCHEIBE](#job-steuern-relais-heckscheibe) - Ansteuern des Heckscheibenrelais
- [STEUERN_SPRITZDUESENHEIZUNG](#job-steuern-spritzduesenheizung) - Ansteuern des Spritzduesenheizung
- [STEUERN_RELAIS_ZUSATZLUEFTER](#job-steuern-relais-zusatzluefter) - Ansteuern des Zusatzluefterrelais
- [STEUERN_ZUSATZWASSERPUMPE](#job-steuern-zusatzwasserpumpe) - Ansteuern der Zusatzwasserpumpe
- [STEUERN_DME_AC](#job-steuern-dme-ac) - Ansteuern des DME-AC-Signals
- [STEUERN_DME_KO](#job-steuern-dme-ko) - Ansteuern des DME-KO-Signals
- [STEUERN_KLIMAKOMPRESSOR](#job-steuern-klimakompressor) - Ansteuern des Klimakompressors
- [STEUERN_SPERRVENTIL](#job-steuern-sperrventil) - Ansteuern des Sperrventils
- [STEUERN_STANDHEIZUNG](#job-steuern-standheizung) - Ansteuern der Standheizung
- [STEUERN_LWS_UMSCHALTVENTIL](#job-steuern-lws-umschaltventil) - Ansteuern des Umschaltventils
- [STEUERN_LWS_ABSPERRVENTIL](#job-steuern-lws-absperrventil) - Ansteuern des Absperrventils des Latentwaermespeichers
- [STEUERN_MOTOR_KLAPPENPOSITION](#job-steuern-motor-klappenposition) - Ansteuern der Schrittmotoren
- [STEUERN_WASSERVENTIL](#job-steuern-wasserventil) - Ansteuern des linken und rechten Wasserventils
- [STEUERN_GEBLAESE](#job-steuern-geblaese) - Ansteuern des Geblaeses
- [KOMPRESSOR_SPERRE](#job-kompressor-sperre) - Ansteuern des Geblaeses

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
| F_HEX_CODE | binary | Fehlerspeicherdaten |
| FEHLERTELEGRAMM | binary | Antworttelegramm ohne Header und Checksumme |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

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
| STEUERGERAET | string | 'IHKA' |
| LENKUNG | string | 'Linkslenker' 'Rechtslenker' |
| LAENDERVARIANTE | string | 'ECE' 'US' 'frei' 'unbekannter Code' |
| MOTORVARIANTE | string | 'Benzinmotor' 'Dieselmotor' 'unbekannter Code' |
| ZYLINDERZAHL | string | '4 Zylinder' '6 Zylinder' '8 Zylinder' '12 Zylinder' 'unbekannter Code' |
| AUSGANGSPEGEL_AC | string | 'DME-AC HIGH-aktiv' 'DME-AC LOW-aktiv' 'DME-AC Entfall' |
| AUSGANGSPEGEL_KO | string | 'DME-KO HIGH-aktiv' 'DME-KO LOW-aktiv' |
| LEERLAUFANHEBUNG_1 | string | 'default' 'bei elektrischen Verbrauchern' 'bei Unterspannung' |
| LEERLAUFANHEBUNG_2 | string | 'bei Unterspannung' ( nicht wenn in .._1 ) '' |
| AUSSTATTUNG_1 | string | 'default' 'Standheizung' '' |
| AUSSTATTUNG_2 | string | 'LOW-Kabelbaum' '' |
| AUSSTATTUNG_3 | string | 'Umluft Memoryfunktion' '' |
| AUSSTATTUNG_4 | string | 'Kompressortransportsperre' '' |
| AUSSTATTUNG_5 | string | 'Kompressoraustaktung' '' |
| AUSSTATTUNG_6 | string | 'Kompressorabschaltung' '' |
| ALLGEMEIN_1 | string | 'default' 'DME-Schnittstelle konventionell' 'DME-Schnittstelle PWM-Signal' |
| ALLGEMEIN_2 | string | 'High/Low-Anzeige' '' |
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
| STAT_TEMPERATUR_EINH | string | Grad Celsius |
| STAT_LWS_FUEHLER_WERT | int |  |
| STAT_WT_LI_WERT | real |  |
| STAT_WT_RE_WERT | real |  |
| STAT_TVERDAMPFER_WERT | real |  |
| STAT_TINNEN_WERT | real |  |
| STAT_TAUSSEN_WERT | real |  |
| STAT_TKUEHLERWASSER_WERT | int |  |
| STAT_AUC_WERT | real |  |
| STAT_AUC_EINH | string | Volt |
| STAT_KLEMME30_WERT | real |  |
| STAT_KLEMME30_EINH | string | Volt |
| STAT_PHOTOTRANSISTOR_WERT | real |  |
| STAT_PHOTOTRANSISTOR_EINH | string | % |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-status-reglergroessen"></a>
### STATUS_REGLERGROESSEN

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_TEMPERATUR_EINH | string | Grad Celsius |
| STAT_SOLL_LI_WERT | real |  |
| STAT_SOLL_RE_WERT | real |  |
| STAT_TINNEN_WERT | real |  |
| STAT_TAUSSEN_WERT | real |  |
| STAT_WT_LI_WERT | real |  |
| STAT_WT_RE_WERT | real |  |
| STAT_SOLL_LI_KORRIGIERT_WERT | real |  |
| STAT_SOLL_RE_KORRIGIERT_WERT | real |  |
| STAT_WTSOLL_LI_WERT | real |  |
| STAT_WTSOLL_RE_WERT | real |  |
| STAT_DIFFSOLL_WERT | real |  |
| STAT_DIFFSOLL_VERZOEGERT_WERT | real |  |
| STAT_YWT_LI_WERT | int |  |
| STAT_YWT_LI_EINH | string | % |
| STAT_YWT_RE_WERT | int |  |
| STAT_YWT_RE_EINH | string | % |
| STAT_FUEHR_LI_WERT | int |  |
| STAT_FUEHR_LI_EINH | string | % |
| STAT_FUEHR_RE_WERT | int |  |
| STAT_FUEHR_RE_EINH | string | % |
| STAT_DREHZAHL_WERT | int |  |
| STAT_DREHZAHL_EINH | string | 1/min |
| STAT_Y_LI_WERT | int |  |
| STAT_Y_LI_EINH | string | % |
| STAT_Y_RE_WERT | int |  |
| STAT_Y_RE_EINH | string | % |
| TELEGRAMM | binary | Antworttelegramm |

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
| STAT_GEBLAESE_WERT | int |  |
| STAT_GEBLAESE_EINH | string | '%' |
| STAT_PHOTOTRANSISTOR_WERT | int |  |
| STAT_PHOTOTRANSISTOR_EINH | string | '%' |
| STAT_KLEMME_58G_WERT | int |  |
| STAT_KLEMME_58G_EINH | string | '%' |
| STAT_DISPLAY_HI_LO_EIN | int |  |
| STAT_FUNKTION_UMLUFT_EIN | int |  |
| STAT_FUNKTION_AUC_EIN | int |  |
| STAT_FUNKTION_REST_EIN | int |  |
| STAT_FUNKTION_AC_EIN | int |  |
| STAT_FUNKTION_HHS_EIN | int |  |
| STAT_FUNKTION_DEFROST_EIN | int |  |
| STAT_FUNKTION_OBEN_EIN | int |  |
| STAT_FUNKTION_MITTE_EIN | int |  |
| STAT_FUNKTION_FUSS_EIN | int |  |
| STAT_FUNKTION_AUTO_EIN | int |  |
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
| STAT_BELUEFTUNG_WERT | int |  |
| STAT_UMLUFT_WERT | int |  |
| STAT_FUSSRAUM_WERT | int |  |
| STAT_ENTFROSTUNG_WERT | int |  |
| STAT_FONDRAUM_WERT | int |  |
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
| STAT_WASSERVENTIL_LI_EIN | int |  |
| STAT_WASSERVENTIL_RE_EIN | int |  |
| STAT_ZUSATZWASSERPUMPE_EIN | int |  |
| STAT_ANSTEUERUNG_SPERRVENTIL_EIN | int |  |
| STAT_ANSTEUERUNG_KOMPRESSOR_EIN | int |  |
| STAT_MONITOR_WASSERVENTIL_LI_RE_EIN | int |  |
| STAT_MONITOR_WASSERPUMPE_SPERRVENTIL_EIN | int |  |
| STAT_MONITOR_KOMPRESSOR_EIN | int |  |
| STAT_ZUSATZLUEFTER_STUFE_1_EIN | int |  |
| STAT_RELAIS_HECKSCHEIBE_EIN | int |  |
| STAT_SPRITZDUESENHEIZUNG_EIN | int |  |
| STAT_STANDHEIZEN_TELESTART_EIN | int |  |
| STAT_STANDHEIZEN_EIN | int |  |
| STAT_KLEMME_15_EIN | int |  |
| STAT_DME_AC_EIN | int |  |
| STAT_DME_KO_EIN | int |  |
| STAT_LWS_UMSCHALTVENTIL_EIN | int |  |
| STAT_LWS_ABSPERRVENTIL_EIN | int |  |
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

<a id="job-eichlauf-starten"></a>
### EICHLAUF_STARTEN

Anstossen der internen Eichlaufroutine

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-display-test"></a>
### DISPLAY_TEST

Einschalten eines Testmusters in den Displays Es muss der Displaytest immer ausgeschalten werden

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TEST_MUSTER | int | 0    = Testmuster aus 1..4 = Testmuster 1..4 |

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

<a id="job-steuern-lws-umschaltventil"></a>
### STEUERN_LWS_UMSCHALTVENTIL

Ansteuern des Umschaltventils

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

<a id="job-steuern-motor-klappenposition"></a>
### STEUERN_MOTOR_KLAPPENPOSITION

Ansteuern der Schrittmotoren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FRISCHLUFT | int |  |
| FUSSRAUM | int |  |
| UMLUFT | int |  |
| BELUEFTUNG | int |  |
| ENTFROSTUNG | int |  |

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

<a id="job-steuern-geblaese"></a>
### STEUERN_GEBLAESE

Ansteuern des Geblaeses

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GEBLAESE | int | 0 - 100 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-kompressor-sperre"></a>
### KOMPRESSOR_SPERRE

Ansteuern des Geblaeses

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPERRE | string | 'EIN','AUS','1','0' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (8 × 2)
- [LIEFERANTEN](#table-lieferanten) (30 × 2)
- [FORTTEXTE](#table-forttexte) (48 × 2)

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

Dimensions: 30 rows × 2 columns

| LIEF_NR | LIEF_NAME |
| --- | --- |
| 0x01 | Reinshagen / Delphi |
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
| 0x27 | Delphi PHI |
| 0x28 | DODUCO |
| 0x29 | DENSO |
| 0xFF | unbekannter Hersteller |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 48 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | Belueftungsklappenmotor |
| 0x01 | Umluftklappenmotor |
| 0x02 | Fussraumklappenmotor |
| 0x03 | Entfrostungsklappenmotor |
| 0x04 | Fondraumklappenmotor |
| 0x05 | Frischluftklappenmotor |
| 0x06 | Latentwaermespeicher Temperaturfuehler |
| 0x07 | Waermetauscherfuehler links |
| 0x08 | Waermetauscherfuehler rechts |
| 0x09 | Verdampferfuehler |
| 0x0A | AUC Sensor |
| 0x0B | Klemme 30 |
| 0x0C | frei 0x0C |
| 0x0D | Innenraumtemperaturfuehler |
| 0x0E | AUC Heizung |
| 0x0F | Relais Zusatzluefter |
| 0x10 | Relais Spritzduesenheizung |
| 0x11 | Relais Heckscheibenheizung |
| 0x12 | Magnetkupplung Klimakompressor |
| 0x13 | DME-KO |
| 0x14 | DME-AC |
| 0x15 | Zusatzwasserpumpe |
| 0x16 | Wasserventil links |
| 0x17 | Wasserventil rechts |
| 0x18 | Standheizung Sperrventil, Latentwaermespeicher Umschaltventil |
| 0x19 | Standheizung Weckleitung |
| 0x1A | Geblaesesteuerspannung |
| 0x1B | Stellgroesse Y links |
| 0x1C | Stellgroesse Y rechts |
| 0x1D | Waermetauschersolltemperatur links |
| 0x1E | Waermetauschersolltemperatur rechts |
| 0x1F | Aussentemperatur |
| 0x20 | Fahrzeuggeschwindigkeit |
| 0x21 | Kuehlwassertemperatur |
| 0x22 | Motordrehzahl |
| 0x23 | Klemme 58g |
| 0x24 | LCD Hinterleuchtung |
| 0x25 | Latentwaermespeicher Absperrventil |
| 0x26 | Motor laeuft |
| 0x27 | Standlueftung ein/aus |
| 0x27 | Standheizung ein/aus |
| 0x29 | AUC Sensor |
| 0x2A | Innenfuehlergeblaese |
| 0x2B | frei 0x2B |
| 0x2C | frei 0x2C |
| 0x2D | frei 0x2D |
| 0x2E | frei 0x2E |
| 0x2F | unbekannter Fehlerort |
