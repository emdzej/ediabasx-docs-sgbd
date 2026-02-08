# IHKA39_5.prg

- Jobs: [38](#jobs)
- Tables: [7](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Integrierte Heiz- Klimaautomatik E39 09/2000 |
| ORIGIN | BMW TI-433 Drexel |
| REVISION | 1.1 |
| AUTHOR | BMW TI-433 Drexel, BMW TI-433 Mellersh |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter DS2
- [IDENT](#job-ident) - Identdaten
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode aufrechterhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen
- [CODIERUNG_LESEN](#job-codierung-lesen) - Auslesen der Codierdaten
- [CODIERUNG_SCHREIBEN](#job-codierung-schreiben) - Codierdaten Schreiben Es muessen immer alle vier Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [STATUS_ANALOGEINGAENGE](#job-status-analogeingaenge) - Status lesen
- [STATUS_REGLERGROESSEN](#job-status-reglergroessen) - Status lesen
- [STATUS_BEDIENTEIL](#job-status-bedienteil) - Status lesen
- [STATUS_MOTOR_KLAPPENPOSITION](#job-status-motor-klappenposition) - Status lesen
- [STATUS_IO](#job-status-io) - Status lesen
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen des internen Speichers Als Argumente werden die Adresse, die Anzahl der Datenbytes uebergeben.
- [RAM_SCHREIBEN](#job-ram-schreiben) - Beschreiben des internen Speichers Als Argumente werden die Adresse, die Anzahl der Datenbytes und das Datenfeld uebergeben. Die Daten werden als String uebergeben und durch ein Komma getrennt.
- [EEPROM_SCHREIBEN](#job-eeprom-schreiben) - Beschreiben des internen EEPROM-Speichers Als Argumente werden die Adresse, die Anzahl der Datenbytes und das Datenfeld uebergeben. Die Daten werden als String uebergeben und durch ein Komma getrennt.
- [DIAGNOSE_TESTBIT](#job-diagnose-testbit) - Ansteuern des Diagnosetest-Bits Das Bit kann ein- bzw. ausgeschaltet werden.
- [STEUERN_EICHLAUF](#job-steuern-eichlauf) - Anstossen des Schrittmotoreichlaufs
- [STEUERN_DISPLAY](#job-steuern-display) - Einschalten eines Testmusters in den Displays Es muss der Displaytest immer ausgeschalten werden Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_RELAIS_HECKSCHEIBE](#job-steuern-relais-heckscheibe) - Ansteuern des Heckscheibenrelais Das Relais kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_SPRITZDUESENHEIZUNG](#job-steuern-spritzduesenheizung) - Ansteuern des Spritzduesenheizung Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_RELAIS_ZUSATZLUEFTER](#job-steuern-relais-zusatzluefter) - Ansteuern des Zusatzluefterrelais Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_ZUSATZWASSERPUMPE](#job-steuern-zusatzwasserpumpe) - Ansteuern der Zusatzwasserpumpe Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_KLIMAKOMPRESSOR](#job-steuern-klimakompressor) - Ansteuern des Klimakompressors Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_SPERRVENTIL](#job-steuern-sperrventil) - Ansteuern des Sperrventils Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_LWS_UMSCHALTVENTIL](#job-steuern-lws-umschaltventil) - Ansteuern des Umschaltventils Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_LWS_ABSPERRVENTIL](#job-steuern-lws-absperrventil) - Ansteuern des Absperrventils des Latentwaermespeichers Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_MOTOR_KLAPPENPOSITION](#job-steuern-motor-klappenposition) - Ansteuern der Schrittmotoren in Prozent 0-100 % Es ist moeglich auch nur einzelne Argumente zu schreiben. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_WASSERVENTIL](#job-steuern-wasserventil) - Ansteuern des linken und rechten Wasserventils 0-100 % Es ist moeglich auch nur einzelne Argumente zu schreiben. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_GEBLAESE](#job-steuern-geblaese) - Ansteuern des Geblaeses Das Geblaese kann von 0-100 % angesteuert werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_REGLERGROESSE](#job-steuern-reglergroesse) - Ansteuern der linken und rechten Reglergroesse Y 0-100 % Es ist moeglich auch nur einzelne Argumente zu schreiben. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [KOMPRESSOR_SPERRE](#job-kompressor-sperre) - Codieren der Kompressortransportsperre
- [UNTERSPANNUNG_ABSCHALTZAEHLER_LESEN](#job-unterspannung-abschaltzaehler-lesen) - Sonder-Job fuer FASTA Er dient zum Auslesen des Unterspannungs- Abschaltzaehlers.

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
| F_ART_ANZ | int | Anzahl der Fehlerarten = 6 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen = 0 |
| F_ART1_NR | int | 1 oder 0 |
| F_ART1_TEXT | string | 'Kurzschluss gegen U-Batt' oder '--' |
| F_ART2_NR | int | 2 oder 0 |
| F_ART2_TEXT | string | 'Kurzschluss gegen Masse' oder '--' |
| F_ART3_NR | int | 4 oder 0 |
| F_ART3_TEXT | string | 'Leitungsunterbrechung' oder '--' |
| F_ART4_NR | int | 8 oder 0 |
| F_ART4_TEXT | string | 'unplausibler Wert, ungueltiger Arbeitsbereich' oder '--' |
| F_ART5_NR | int | 64 oder 0 |
| F_ART5_TEXT | string | 'Fehler momentan vorhanden' oder '--' |
| F_ART6_NR | int | 128 oder 0 |
| F_ART6_TEXT | string | 'sporadischer Fehler' oder '--' |
| F_HEX_CODE | binary | Fehlerspeicherdaten |

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Auslesen der Codierdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| CODE | string | 4 Codierbytes in Hex |
| KOMPRESSOR_SPERRE | int | Klimakompressor deaktiviert |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-codierung-schreiben"></a>
### CODIERUNG_SCHREIBEN

Codierdaten Schreiben Es muessen immer alle vier Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODE1 | int | 0-255 bzw. 0x00-0xFF |
| CODE2 | int | 0-255 bzw. 0x00-0xFF |
| CODE3 | int | 0-255 bzw. 0x00-0xFF |
| CODE4 | int | 0-255 bzw. 0x00-0xFF |

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
| STAT_LWS_FUEHLER_WERT | int | Latentwaermefuehler |
| STAT_WT_LI_WERT | real | Waermetauscherfuehler links |
| STAT_WT_RE_WERT | real | Waermetauscherfuehler rechts |
| STAT_TVERDAMPFER_WERT | real | Verdampfertemperaturfuehler |
| STAT_TINNEN_WERT | real | Innentemperaturfuehler |
| STAT_TAUSSEN_WERT | real | Aussentemperatur |
| STAT_TKUEHLERWASSER_WERT | int | Kuehlwassertemperatur |
| STAT_AUC_WERT | real | Sensorsignal AUC |
| STAT_AUC_EINH | string | Volt |
| STAT_KLEMME30_WERT | real | Klemme 30 |
| STAT_KLEMME30_EINH | string | Volt |
| STAT_PHOTOTRANSISTOR_WERT | real | Phototransistor |
| STAT_PHOTOTRANSISTOR_EINH | string | % |
| STAT_GEBLAESE_PWM_WERT | real | PWM-Geblaesesteuerspannung |
| STAT_GEBLAESE_PWM_EINH | string | Volt |
| STAT_FONDRAUM_VERSORGUNG_WERT | real | Spannungsversorgung Fondraumpoti |
| STAT_FONDRAUM_VERSORGUNG_EINH | string | Volt |
| STAT_FONDRAUM_WERT | real | Fondraumpoti |
| STAT_FONDRAUM_EINH | string | Volt |
| STAT_GEBLAESE_FOND_WERT | real | Fond-Geblaesesteuerspannung |
| STAT_GEBLAESE_FOND_EINH | string | Volt |
| STAT_DRUCKSENSOR_WERT | real | Drucksensor |
| STAT_DRUCKSENSOR_EINH | string | Volt |
| STAT_SOLARSENSOR_LI_WERT | int | Solarsensor links |
| STAT_SOLARSENSOR_LI_EINH | string | Volt |
| STAT_SOLARSENSOR_RE_WERT | int | Solarsensor |
| STAT_SOLARSENSOR_RE_EINH | string | Volt |
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
| STAT_GESCHWINDIGKEIT_WERT | int |  |
| STAT_GESCHWINDIGKEIT_EINH | string | km/h |
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
| STAT_FUNKTION_MAX_AC_EIN | int |  |
| STAT_GEBLAESE_AUTO_EIN | int |  |
| STAT_FUNKTION_EIN | int | SG Funktion ein / aus |
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
| STAT_STAUDRUCK_WERT | int |  |
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
| STAT_ZUSATZLUEFTER_STUFE_1_EIN | int |  |
| STAT_RELAIS_HECKSCHEIBE_EIN | int |  |
| STAT_SPRITZDUESENHEIZUNG_EIN | int |  |
| STAT_KLEMME_15_EIN | int |  |
| STAT_LWS_UMSCHALTVENTIL_EIN | int |  |
| STAT_LWS_ABSPERRVENTIL_EIN | int |  |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Lesen des internen Speichers Als Argumente werden die Adresse, die Anzahl der Datenbytes uebergeben.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int | 0x0000 - 0x0FFF |
| ANZAHL | int | 1 - 32 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | ausgelesene Daten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-ram-schreiben"></a>
### RAM_SCHREIBEN

Beschreiben des internen Speichers Als Argumente werden die Adresse, die Anzahl der Datenbytes und das Datenfeld uebergeben. Die Daten werden als String uebergeben und durch ein Komma getrennt.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int | 0x0000 - 0x03FF |
| ANZAHL | int | 1 - 27 |
| DATEN | string | z.B. "1,2,03,0x04,0x05..." |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-eeprom-schreiben"></a>
### EEPROM_SCHREIBEN

Beschreiben des internen EEPROM-Speichers Als Argumente werden die Adresse, die Anzahl der Datenbytes und das Datenfeld uebergeben. Die Daten werden als String uebergeben und durch ein Komma getrennt.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int | 0x0D80 - 0x0FFF |
| ANZAHL | int | 1 - 27 |
| DATEN | string | z.B. "1,2,03,0x04,0x05..." |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-diagnose-testbit"></a>
### DIAGNOSE_TESTBIT

Ansteuern des Diagnosetest-Bits Das Bit kann ein- bzw. ausgeschaltet werden.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TESTBIT | string | 'EIN','AUS' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-eichlauf"></a>
### STEUERN_EICHLAUF

Anstossen des Schrittmotoreichlaufs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-display"></a>
### STEUERN_DISPLAY

Einschalten eines Testmusters in den Displays Es muss der Displaytest immer ausgeschalten werden Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen

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

Ansteuern des Heckscheibenrelais Das Relais kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen

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

Ansteuern des Spritzduesenheizung Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen

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

Ansteuern des Zusatzluefterrelais Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen

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

Ansteuern der Zusatzwasserpumpe Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZUSATZWASSERPUMPE | string | 'EIN','AUS' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-klimakompressor"></a>
### STEUERN_KLIMAKOMPRESSOR

Ansteuern des Klimakompressors Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen

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

Ansteuern des Sperrventils Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPERRVENTIL | string | 'EIN','AUS' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-lws-umschaltventil"></a>
### STEUERN_LWS_UMSCHALTVENTIL

Ansteuern des Umschaltventils Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen

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

Ansteuern des Absperrventils des Latentwaermespeichers Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen

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

Ansteuern der Schrittmotoren in Prozent 0-100 % Es ist moeglich auch nur einzelne Argumente zu schreiben. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FRISCHLUFT | int | Frischluftmotor 0 - 100 % oder '' |
| FUSSRAUM | int | Fussraummotor 0 - 100 % oder '' |
| STAUDRUCK | int | Staudruckmotor 0 - 100 % oder '' |
| BELUEFTUNG | int | Belueftungsmotor 0 - 100 % oder '' |
| ENTFROSTUNG | int | Entfrostungsmotor 0 - 100 % oder '' |
| FONDRAUM | int | Fondraummotor 0 - 100 % oder '' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-wasserventil"></a>
### STEUERN_WASSERVENTIL

Ansteuern des linken und rechten Wasserventils 0-100 % Es ist moeglich auch nur einzelne Argumente zu schreiben. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen

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

Ansteuern des Geblaeses Das Geblaese kann von 0-100 % angesteuert werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GEBLAESE | int | Geblaesesteuerspannung 0 - 100 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-reglergroesse"></a>
### STEUERN_REGLERGROESSE

Ansteuern der linken und rechten Reglergroesse Y 0-100 % Es ist moeglich auch nur einzelne Argumente zu schreiben. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| REGLERGROESSE_LINKS | int | Reglergroesse Y links 0-100 % |
| REGLERGROESSE_RECHTS | int | Reglergroesse Y rechts 0-100 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-kompressor-sperre"></a>
### KOMPRESSOR_SPERRE

Codieren der Kompressortransportsperre

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPERRE | string | 'EIN','AUS','1','0' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-unterspannung-abschaltzaehler-lesen"></a>
### UNTERSPANNUNG_ABSCHALTZAEHLER_LESEN

Sonder-Job fuer FASTA Er dient zum Auslesen des Unterspannungs- Abschaltzaehlers.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| ZAEHLERSTAND | int | 0-255 bzw. 0x00-0xFF |
| TELEGRAMM | binary | Antworttelegramm |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (10 × 2)
- [LIEFERANTEN](#table-lieferanten) (56 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [FORTTEXTE](#table-forttexte) (54 × 2)
- [FARTTEXTE](#table-farttexte) (8 × 2)
- [FARTMATRIX](#table-fartmatrix) (1 × 13)

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

Dimensions: 54 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | Belueftungsklappenmotor |
| 0x01 | Staudruckklappenmotor |
| 0x02 | Fussraumklappenmotor |
| 0x03 | Entfrostungsklappenmotor |
| 0x04 | Fondraumklappenmotor |
| 0x05 | Frischluft/Umluftklappenmotor |
| 0x06 | Reserve-Motor |
| 0x07 | Geblaesesteuerspannung |
| 0x08 | Innenraumtemperaturfuehler im Bedienteil |
| 0x09 | Phototransistor im Bedienteil |
| 0x0A | AUC Sensor |
| 0x0B | Waermetauscherfuehler rechts |
| 0x0C | Latentwaermespeicher Temperaturfuehler |
| 0x0D | Beschlagsensor |
| 0x0E | Fondraumpotentiometer |
| 0x0F | Fondgeblaese |
| 0x10 | Klemme 30 |
| 0x11 | Solarsensor rechts |
| 0x12 | Verdampferfuehler |
| 0x13 | Waermetauscherfuehler links |
| 0x14 | Solarsensor links |
| 0x15 | Drucksensor |
| 0x16 | Versorgungsspannung Fondraumpotentiometer |
| 0x17 | AUC Heizung |
| 0x18 | Relais Zusatzluefter |
| 0x19 | Relais Spritzduesenheizung |
| 0x1A | Relais Heckscheibenheizung |
| 0x1B | Magnetkupplung Klimakompressor |
| 0x1C | frei 28 |
| 0x1D | frei 29 |
| 0x1E | Zusatzwasserpumpe |
| 0x1F | Wasserventil links |
| 0x20 | Wasserventil rechts |
| 0x21 | Standheizung Sperrventil, Latentwaermespeicher Umschaltventil |
| 0x22 | frei 34 |
| 0x23 | Geblaesesteuerspannung |
| 0x24 | Stellgroesse Y links |
| 0x25 | Stellgroesse Y rechts |
| 0x26 | Waermetauschersolltemperatur links |
| 0x27 | Waermetauschersolltemperatur rechts |
| 0x27 | Aussentemperatur |
| 0x29 | Fahrzeuggeschwindigkeit |
| 0x2A | Kuehlwassertemperatur |
| 0x2B | Motordrehzahl |
| 0x2C | Klemme 58g |
| 0x2D | LCD Hinterleuchtung |
| 0x2E | Latentwaermespeicher Absperrventil |
| 0x2F | Motor laeuft |
| 0x30 | Standlueftung ein/aus |
| 0x31 | Standheizung ein/aus |
| 0x32 | Zuheizer |
| 0x33 | Innenfuehlergeblaese |
| 0x34 | Energiesparmode aktiviert |
| 0x35 | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 8 rows × 2 columns

| ART | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | Kurzschluss gegen U-Batt |
| 0x02 | Kurzschluss gegen Masse |
| 0x04 | Leitungsunterbrechung |
| 0x08 | unplausibler Wert, ungueltiger Arbeitsbereich |
| 0x40 | Fehler momentan vorhanden |
| 0x80 | sporadischer Fehler |
| 0xFF | unbekannte Fehlerart |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 1 rows × 13 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 | A6_0 | A6_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x04 | 0x00 | 0x08 | 0x00 | 0x40 | 0x00 | 0x80 |
