# IHKA39_4.prg

- Jobs: [37](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Integrierte Heiz- Klimaautomatik E39 03/99 |
| ORIGIN | BMW TI-433 Drexel |
| REVISION | 1.00 |
| AUTHOR | BMW TI-433 Drexel, BMW TI-433 Mellersh |
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
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode aufrechterhalten Vorbereitungsbefehl fuer Ansteuerbefehle
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden Beenden von Ansteuerbefehlen
- [SLEEP_MODE](#job-sleep-mode) - SG in Power-Down-Mode versetzen
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
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
- [STEUERN_STANDHEIZUNG](#job-steuern-standheizung) - Ansteuern der Standheizung Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_LWS_UMSCHALTVENTIL](#job-steuern-lws-umschaltventil) - Ansteuern des Umschaltventils Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_LWS_ABSPERRVENTIL](#job-steuern-lws-absperrventil) - Ansteuern des Absperrventils des Latentwaermespeichers Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_MOTOR_KLAPPENPOSITION](#job-steuern-motor-klappenposition) - Ansteuern der Schrittmotoren in Prozent 0-100 % Es ist moeglich auch nur einzelne Argumente zu schreiben. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_WASSERVENTIL](#job-steuern-wasserventil) - Ansteuern des linken und rechten Wasserventils 0-100 % Es ist moeglich auch nur einzelne Argumente zu schreiben. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_GEBLAESE](#job-steuern-geblaese) - Ansteuern des Geblaeses Das Geblaese kann von 0-100 % angesteuert werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_REGLERGROESSE](#job-steuern-reglergroesse) - Ansteuern der linken und rechten Reglergroesse Y 0-100 % Es ist moeglich auch nur einzelne Argumente zu schreiben. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [KOMPRESSOR_SPERRE](#job-kompressor-sperre) - Codieren der Kompressortransportsperre

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
| ID_VARIANTE | string | Variante: BASIS, BAS_FON, SH, SH_FON, LWS, LWS_FON, IHK? |
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

Diagnosemode aufrechterhalten Vorbereitungsbefehl fuer Ansteuerbefehle

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden Beenden von Ansteuerbefehlen

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
| STAT_FONDRAUM_VERSORGUNG_WERT | real | Spannungsversorgung Fondraumpoti |
| STAT_FONDRAUM_VERSORGUNG_EINH | string | Volt |
| STAT_GEBLAESE_PWM_WERT | real | PWM-Geblaesesteuerspannung |
| STAT_GEBLAESE_PWM_EINH | string | Volt |
| STAT_FONDRAUM_WERT | real | Fondraumpoti |
| STAT_FONDRAUM_EINH | string | Volt |
| STAT_DRUCKSENSOR_WERT | real | Drucksensor |
| STAT_DRUCKSENSOR_EINH | string | Volt |
| STAT_AUC_VERSORGUNG_WERT | real | Spannungsversorgung AUC-Sensor |
| STAT_AUC_VERSORGUNG_EINH | string | Volt |
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
| STAT_MONITOR_WASSERVENTIL_LI_RE_EIN | int |  |
| STAT_MONITOR_WASSERPUMPE_SPERRVENTIL_EIN | int |  |
| STAT_MONITOR_KOMPRESSOR_EIN | int |  |
| STAT_ZUSATZLUEFTER_STUFE_1_EIN | int |  |
| STAT_RELAIS_HECKSCHEIBE_EIN | int |  |
| STAT_SPRITZDUESENHEIZUNG_EIN | int |  |
| STAT_STANDHEIZEN_TELESTART_EIN | int |  |
| STAT_STANDHEIZEN_EIN | int |  |
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

<a id="job-steuern-standheizung"></a>
### STEUERN_STANDHEIZUNG

Ansteuern der Standheizung Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen

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

## Tables

### Index

- [JOBRESULT](#table-jobresult) (10 × 2)
- [LIEFERANTEN](#table-lieferanten) (45 × 2)
- [FORTTEXTE](#table-forttexte) (48 × 2)

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

Dimensions: 45 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
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
| 0xFF | unbekannter Hersteller |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 48 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | Belueftungsklappenmotor |
| 0x01 | Staudruckklappenmotor |
| 0x02 | Fussraumklappenmotor |
| 0x03 | Entfrostungsklappenmotor |
| 0x04 | Fondraumklappenmotor |
| 0x05 | Frischluft/Umluftklappenmotor |
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
| 0x13 | frei 0x13 |
| 0x14 | frei 0x14 |
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
| 0x29 | Zuheizer |
| 0x2A | Innenfuehlergeblaese |
| 0x2B | Versorgungsspannung Fondraumpotentiometer |
| 0x2C | frei 0x2C |
| 0x2D | Fondraumpotentiometer |
| 0x2E | Drucksensor |
| 0x2F | unbekannter Fehlerort |
