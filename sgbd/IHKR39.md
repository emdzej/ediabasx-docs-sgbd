# IHKR39.prg

- Jobs: [40](#jobs)
- Tables: [7](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Integrierte Heiz- Klimaregelung E39 |
| ORIGIN | BMW TI-435 Drexel |
| REVISION | 1.3 |
| AUTHOR | BMW TI-435 Drexel |
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
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen des internen Speichers Als Argumente werden die Adresse, die Anzahl der Datenbytes uebergeben.
- [RAM_SCHREIBEN](#job-ram-schreiben) - Beschreiben des internen Speichers Als Argumente werden die Adresse, die Anzahl der Datenbytes und das Datenfeld uebergeben. Die Daten werden als String uebergeben und durch ein Komma getrennt.
- [EEPROM_SCHREIBEN](#job-eeprom-schreiben) - Beschreiben des internen EEPROM-Speichers Als Argumente werden die Adresse, die Anzahl der Datenbytes und das Datenfeld uebergeben. Die Daten werden als String uebergeben und durch ein Komma getrennt.
- [CODIERUNG_SCHREIBEN](#job-codierung-schreiben) - Codierdaten Schreiben Es muessen immer alle vier Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [CODIERUNG_LESEN](#job-codierung-lesen) - Auslesen der Codierdaten
- [STATUS_ANALOGEINGAENGE](#job-status-analogeingaenge) - Status lesen
- [STATUS_REGLERGROESSEN](#job-status-reglergroessen) - Status lesen
- [STATUS_BEDIENTEIL](#job-status-bedienteil) - Status lesen
- [STATUS_MOTOR_KLAPPENPOSITION](#job-status-motor-klappenposition) - Status lesen
- [STATUS_IO](#job-status-io) - Status lesen
- [DIAGNOSE_TESTBIT](#job-diagnose-testbit) - Ansteuern des Diagnosetest-Bits Das Bit kann ein- bzw. ausgeschaltet werden.
- [STEUERN_EICHLAUF](#job-steuern-eichlauf) - Anstossen des Schrittmotoreichlaufs
- [STEUERN_RELAIS_HECKSCHEIBE](#job-steuern-relais-heckscheibe) - Ansteuern des Heckscheibenrelais Das Relais kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_SPRITZDUESENHEIZUNG](#job-steuern-spritzduesenheizung) - Ansteuern des Spritzduesenheizung Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_RELAIS_ZUSATZLUEFTER](#job-steuern-relais-zusatzluefter) - Ansteuern des Zusatzluefterrelais Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_ZUSATZWASSERPUMPE](#job-steuern-zusatzwasserpumpe) - Ansteuern der Zusatzwasserpumpe Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_KLIMAKOMPRESSOR](#job-steuern-klimakompressor) - Ansteuern des Klimakompressors Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_SPERRVENTIL](#job-steuern-sperrventil) - Ansteuern des Sperrventils Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_STANDHEIZUNG](#job-steuern-standheizung) - Ansteuern der Standheizung Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_LWS_UMSCHALTVENTIL](#job-steuern-lws-umschaltventil) - Ansteuern des Umschaltventils Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_LWS_ABSPERRVENTIL](#job-steuern-lws-absperrventil) - Ansteuern des Absperrventils des Latentwaermespeichers Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_MOTOR_KLAPPENPOSITION](#job-steuern-motor-klappenposition) - Ansteuern des Schrittmotors in Prozent 0-100 % Es ist moeglich auch nur einzelne Argumente zu schreiben. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_WASSERVENTIL](#job-steuern-wasserventil) - Ansteuern des Wasserventils Das Wasserventil kann von 0-100 % angesteuert werden. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_GEBLAESE](#job-steuern-geblaese) - Ansteuern des Geblaeses Das Geblaese kann von 0-100 % angesteuert werden. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_DREHZAHL](#job-steuern-drehzahl) - Vorgabe der Drehzahl Die Drehzahl kann von 0-8000 1/min vorgegeben werden. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_GESCHWINDIGKEIT](#job-steuern-geschwindigkeit) - Vorgabe der Geschwindigkeit vom K-Bus Die Geschwindigkeit kann von 0-200 km/h vorgegeben werden. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_AUSSENTEMPERATUR](#job-steuern-aussentemperatur) - Vorgabe der Aussentemperatur vom K-Bus Die Aussentemperatur kann von -45 - +40 Grad C vorgegeben werden. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_REGLERGROESSE](#job-steuern-reglergroesse) - Ansteuern der Reglergroesse Y 0-100 % Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [KOMPRESSOR_SPERRE](#job-kompressor-sperre) - Codieren der Kompressortransportsperre

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
| F_ORT_TEXT | string | table FOrtTexte Text zu Fehlerort |
| F_HFK | int | Fehlerhaeufigkeit |
| F_ART_ANZ | int | Anzahl der Fehlerarten = 6 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen = 0 |
| F_ART1_NR | int | 1 oder 0 |
| F_ART1_TEXT | string | table FArtTexte 'Kurzschluss gegen U-Batt' oder '--' |
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

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Lesen des internen Speichers Als Argumente werden die Adresse, die Anzahl der Datenbytes uebergeben.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int | 0x0000 - 0x09FF |
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
| ADRESSE | int | 0x0000 - 0x02CF |
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
| ADRESSE | int | 0x0800 - 0x09FF |
| ANZAHL | int | 1 - 27 |
| DATEN | string | z.B. "1,2,03,0x04,0x05..." |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

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

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Auslesen der Codierdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| CODE | string | 4 Codierbytes in Hex |
| MOTORVARIANTE | string | 'Benzinmotor' 'Dieselmotor' |
| ZYLINDERZAHL | string | '4 Zylinder' '6 Zylinder' '8 Zylinder' '12 Zylinder' 'unbekannter Code' |
| LEERLAUFANHEBUNG_1 | string | 'default' 'bei elektrischen Verbrauchern' 'bei Unterspannung' |
| LEERLAUFANHEBUNG_2 | string | 'bei Unterspannung' ( nicht wenn in .._1 ) '' |
| AUSSTATTUNG_1 | string | 'default' 'Standheizung' '' |
| AUSSTATTUNG_2 | string | 'Latentwaermespeicher' '' |
| AUSSTATTUNG_3 | string | 'Zuheizer' '' |
| AUSSTATTUNG_4 | string | 'Wasserpumpe' '' |
| ALLGEMEIN_1 | string | 'default' 'Kennfeldkuehlung' |
| ALLGEMEIN_2 | string | 'Kompressortransportsperre' '' |
| COD_IHK_AUC | int | immer 0 |
| COD_IHK_LWS | int | 1 wenn LWS |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-status-analogeingaenge"></a>
### STATUS_ANALOGEINGAENGE

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_TEMPERATUR_EINH | string | Grad Celsius |
| STAT_SOLL_WERT | real | Stellung des Temperatur-Potis |
| STAT_TINNEN_WERT | real | Innentemperaturfuehler ( Fussraum ) |
| STAT_WT_WERT | real | Waermetauscherfuehler |
| STAT_TVERDAMPFER_WERT | real | Verdampfertemperaturfuehler |
| STAT_LWS_FUEHLER_WERT | int | Latentwaermefuehler |
| STAT_TAUSSEN_WERT | real | Aussentemperatur |
| STAT_TKUEHLERWASSER_WERT | int | Kuehlwassertemperatur |
| STAT_DRUCKSENSOR_WERT | real | Drucksensor |
| STAT_DRUCKSENSOR_EINH | string | bar |
| STAT_KLEMME30_WERT | real | Klemme 30 |
| STAT_KLEMME30_EINH | string | Volt |
| STAT_GEBLAESE_WERT | int | Stellung des Geblaese-Potis |
| STAT_GEBLAESE_EINH | string | % |
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
| STAT_TAUSSEN_WERT | real | Aussentemperatur |
| STAT_TVERDAMPFER_WERT | real | Verdampfertemperaturfuehler |
| STAT_SOLL_WERT | real | Stellung des Temperatur-Potis |
| STAT_SOLL_KORRIGIERT_WERT | real | korrigierter Sollwert |
| STAT_TINNEN_WERT | real | Innentemperaturfuehler ( Fussraum ) |
| STAT_TINNEN_VERZOEGERT_WERT | real | verzoegerter Innentemperaturfuehler ( Fussraum ) |
| STAT_WTSOLL_WERT | real | Waermetauscher Solltemperatur |
| STAT_WT_WERT | real | Waermetauscherfuehler |
| STAT_DRUCKSENSOR_WERT | real | Drucksensor |
| STAT_DRUCKSENSOR_EINH | string | bar |
| STAT_FUEHR_WERT | int | Stellgroesse Fuehrungsregler |
| STAT_FUEHR_EINH | string | % |
| STAT_YWT_WERT | int | Stellgroesse Waermetauscher |
| STAT_YWT_EINH | string | % |
| STAT_WASSERVENTIL_WERT | int | Wasserventiloeffnungszeit |
| STAT_WASSERVENTIL_EINH | string | ms |
| STAT_GESCHWINDIGKEIT_WERT | int | Fahrzeuggeschwindigkeit |
| STAT_GESCHWINDIGKEIT_EINH | string | km/h |
| STAT_DREHZAHL_WERT | int | Motordrehzahl |
| STAT_DREHZAHL_EINH | string | 1/min |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-status-bedienteil"></a>
### STATUS_BEDIENTEIL

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_SOLL_WERT | real | Stellung des Temperatur-Potis |
| STAT_GEBLAESE_WERT | int | Stellung des Geblaese-Potis |
| STAT_GEBLAESE_EINH | string | % |
| STAT_SOLL_EINH | string | 'Grad Celsius' |
| STAT_FUNKTION_EIN | int | SG Funktion ein / aus |
| STAT_FUNKTION_AC_EIN | int | Klimabetrieb |
| STAT_FUNKTION_UMLUFT_EIN | int | Umluftbetrieb |
| STAT_FUNKTION_HHS_EIN | int | Heckscheibenheizung |
| STAT_KLEMME_58G_WERT | int |  |
| STAT_KLEMME_58G_EINH | string | '%' |

<a id="job-status-motor-klappenposition"></a>
### STATUS_MOTOR_KLAPPENPOSITION

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_MOTOR_EINH | string | % |
| STAT_UMLUFT_WERT | int | Position Umluftklappe |
| STAT_FRISCHLUFT_WERT | int | Position Frischluftklappe |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-status-io"></a>
### STATUS_IO

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_KLEMME_15_EIN | int | Einlesen der Klemme 15 |
| STAT_SENSORVERSORGUNG_EIN | int | Monitor fuer Sensorversorgung |
| STAT_DME_KKAB_EIN | int | Eingang Klimakompressor Abfall bei Vollast |
| STAT_TASTE_AC_EIN | int | Klima Taste |
| STAT_TASTE_UMLUFT_EIN | int | Umluft Taste |
| STAT_TASTE_HECKSCHEIBE_EIN | int | Heckscheibenheizung Taste |
| STAT_SPRITZDUESENHEIZUNG_EIN | int | Ausgang Spritzduesenheizung |
| STAT_RELAIS_HECKSCHEIBE_EIN | int | Ausgang Heckscheibenheizung Relais |
| STAT_ANSTEUERUNG_KOMPRESSOR_EIN | int | Ausgang Kompressorkupplung |
| STAT_ZUSATZLUEFTER_STUFE_1_EIN | int | Ausgang Zusatzluefter Stufe 1 |
| STAT_ZUSATZWASSERPUMPE_EIN | int | Ausgang Zusatzwasserpumpe |
| STAT_WASSERVENTIL_EIN | int | Ausgang Wasserventil |
| STAT_STANDHEIZEN_TELESTART_EIN | int | Eingang Standheizung Telestart |
| STAT_STANDHEIZEN_EIN | int | Ausgang Standheizung Weckleitung |
| STAT_ANSTEUERUNG_SPERRVENTIL_EIN | int | Ausgang Standheizung Sperrventil identisch mit Ausgang Latentwaermespeicher Umschaltventil |
| STAT_LWS_UMSCHALTVENTIL_EIN | int | Ausgang Latentwaermespeicher Umschaltventil identisch mit Ausgang Standheizung Sperrventil |
| STAT_LWS_ABSPERRVENTIL_EIN | int | Ausgang Latentwaermespeicher Absperrventil |
| TELEGRAMM | binary | Antworttelegramm |

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

<a id="job-steuern-relais-heckscheibe"></a>
### STEUERN_RELAIS_HECKSCHEIBE

Ansteuern des Heckscheibenrelais Das Relais kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RELAIS_HECKSCHEIBE | string | EIN, AUS |
| DIAGNOSE_AUFRECHT | string | ja, wenn nicht '' |

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
| DIAGNOSE_AUFRECHT | string | ja, wenn nicht '' |

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
| DIAGNOSE_AUFRECHT | string | ja, wenn nicht '' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-zusatzwasserpumpe"></a>
### STEUERN_ZUSATZWASSERPUMPE

Ansteuern der Zusatzwasserpumpe Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZUSATZWASSERPUMPE | string | EIN, AUS |
| DIAGNOSE_AUFRECHT | string | ja, wenn nicht '' |

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
| DIAGNOSE_AUFRECHT | string | ja, wenn nicht '' |

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
| DIAGNOSE_AUFRECHT | string | ja, wenn nicht '' |

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
| DIAGNOSE_AUFRECHT | string | ja, wenn nicht '' |

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
| DIAGNOSE_AUFRECHT | string | ja, wenn nicht '' |

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
| DIAGNOSE_AUFRECHT | string | ja, wenn nicht '' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-motor-klappenposition"></a>
### STEUERN_MOTOR_KLAPPENPOSITION

Ansteuern des Schrittmotors in Prozent 0-100 % Es ist moeglich auch nur einzelne Argumente zu schreiben. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FRISCHLUFT | int | Frischluft- / Umluftmotor 0 - 100 % |
| DIAGNOSE_AUFRECHT | string | ja, wenn nicht '' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-wasserventil"></a>
### STEUERN_WASSERVENTIL

Ansteuern des Wasserventils Das Wasserventil kann von 0-100 % angesteuert werden. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WASSERVENTIL | int | Wasserventiltaktung 0-100 % |
| DIAGNOSE_AUFRECHT | string | ja, wenn nicht '' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-geblaese"></a>
### STEUERN_GEBLAESE

Ansteuern des Geblaeses Das Geblaese kann von 0-100 % angesteuert werden. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GEBLAESE | int | Geblaesesteuerspannung 0 - 100 % |
| DIAGNOSE_AUFRECHT | string | ja, wenn nicht '' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-drehzahl"></a>
### STEUERN_DREHZAHL

Vorgabe der Drehzahl Die Drehzahl kann von 0-8000 1/min vorgegeben werden. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DREHZAHL | int | DREHZAHL 0-8000 1/min |
| DIAGNOSE_AUFRECHT | string | ja, wenn nicht '' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-geschwindigkeit"></a>
### STEUERN_GESCHWINDIGKEIT

Vorgabe der Geschwindigkeit vom K-Bus Die Geschwindigkeit kann von 0-200 km/h vorgegeben werden. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GESCHWINDIGKEIT | int | GESCHWINDIGKEIT 0-200 km/h |
| DIAGNOSE_AUFRECHT | string | ja, wenn nicht '' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-aussentemperatur"></a>
### STEUERN_AUSSENTEMPERATUR

Vorgabe der Aussentemperatur vom K-Bus Die Aussentemperatur kann von -45 - +40 Grad C vorgegeben werden. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSSENTEMPERATUR | int | AUSSENTEMPERATUR -45 - +40 Grad C |
| DIAGNOSE_AUFRECHT | string | ja, wenn nicht '' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-reglergroesse"></a>
### STEUERN_REGLERGROESSE

Ansteuern der Reglergroesse Y 0-100 % Vor dem Ansteuern den Job DIAGNOSE_AUFECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| REGLERGROESSE | int | Reglergroesse Y 0-100 % |
| DIAGNOSE_AUFRECHT | string | ja, wenn nicht '' |

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
- [LIEFERANTEN](#table-lieferanten) (56 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [FORTTEXTE](#table-forttexte) (37 × 2)
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

Dimensions: 37 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | frei 0x00 |
| 0x01 | Frischluftklappenmotor |
| 0x02 | Innenraumtemperaturfuehler ( Fussraum ) |
| 0x03 | Waermetauscherfuehler |
| 0x04 | Verdampferfuehler |
| 0x05 | Drucksensor |
| 0x06 | Latentwaermespeicher Temperaturfuehler |
| 0x07 | Klemme 30 |
| 0x08 | Geblaesepotentiometer |
| 0x09 | Sollwertsteller |
| 0x0A | Relais Zusatzluefter |
| 0x0B | Relais Spritzduesenheizung |
| 0x0C | Relais Heckscheibenheizung |
| 0x0D | Magnetkupplung Klimakompressor |
| 0x0E | Zusatzwasserpumpe |
| 0x0F | Wasserventil |
| 0x10 | Standheizung Sperrventil |
| 0x11 | Standheizung Weckleitung |
| 0x12 | Latentwaermespeicher Absperrventil |
| 0x13 | Zuheizer |
| 0x14 | Geblaesesteuerspannung |
| 0x15 | Versorgungsspannung Sensor |
| 0x16 | Stellgroesse Y |
| 0x17 | Waermetauschersolltemperatur |
| 0x18 | DME-KO |
| 0x19 | DME-AC |
| 0x1A | Aussentemperatur |
| 0x1B | Fahrzeuggeschwindigkeit |
| 0x1C | Kuehlwassertemperatur |
| 0x1D | Motordrehzahl |
| 0x1E | Klemme 58g |
| 0x1F | frei 0x1F |
| 0x20 | Motor laeuft |
| 0x21 | Standlueftung ein/aus |
| 0x22 | Standheizung ein/aus |
| 0x23 | Energiesparmode aktiviert |
| 0xFF | unbekannter Fehlerort |

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
