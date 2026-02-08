# IHKA46_2.prg

- Jobs: [38](#jobs)
- Tables: [7](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Integrierte Heiz- Klimaautomatik E46 PU 98 / PU 99 |
| ORIGIN | BMW TI-430 Drexel |
| REVISION | 2.00 |
| AUTHOR | BMW TI-430 Drexel, BMW TI-433 Mellersh |
| COMMENT | N/A |
| PACKAGE | 0.09 |
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
- [CODIERUNG_SCHREIBEN](#job-codierung-schreiben) - Codierdaten Schreiben fuer IHKA E46 Es muessen immer alle vier Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [CODIERUNG_LESEN](#job-codierung-lesen) - Auslesen der Codierdaten
- [STATUS_ANALOGEINGAENGE](#job-status-analogeingaenge) - Status lesen
- [STATUS_REGLERGROESSEN](#job-status-reglergroessen) - Status lesen
- [STATUS_BEDIENTEIL](#job-status-bedienteil) - Status lesen
- [STATUS_IO](#job-status-io) - Status lesen
- [STATUS_MOTOR_KLAPPENPOSITION](#job-status-motor-klappenposition) - Status lesen
- [DIAGNOSE_TESTBIT](#job-diagnose-testbit) - Ansteuern des Diagnosetest-Bits Das Bit kann ein- bzw. ausgeschaltet werden.
- [STEUERN_EICHLAUF](#job-steuern-eichlauf) - Anstossen des Schrittmotoreichlaufs Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_DISPLAY](#job-steuern-display) - Einschalten eines Testmusters in den Displays Es muss der Displaytest immer ausgeschalten werden Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_RELAIS_HECKSCHEIBE](#job-steuern-relais-heckscheibe) - Ansteuern des Heckscheibenrelais Das Relais kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_TASTE_HECKSCHEIBE](#job-steuern-taste-heckscheibe) - Ansteuern der Taste Heckscheibenheizung Voraussetzung ist, dass der Motor laeuft.
- [STEUERN_ZUSATZWASSERPUMPE](#job-steuern-zusatzwasserpumpe) - Ansteuern der Zusatzwasserpumpe Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_RELAIS_FRONTSCHEIBE](#job-steuern-relais-frontscheibe) - Ansteuern des Frontscheibenrelais Das Relais kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen Identisch mit STEUERN_ZUHEIZER, da gleicher Ausgang
- [STEUERN_ZUHEIZER](#job-steuern-zuheizer) - Ansteuern des Zuheizers Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen Identisch mit STEUERN_RELAIS_FRONTSCHEIBE, da gleicher Ausgang
- [STEUERN_MOTOR_KLAPPENPOSITION](#job-steuern-motor-klappenposition) - Ansteuern der Schrittmotoren in Prozent 0-100 % Es ist moeglich auch nur einzelne Argumente zu schreiben. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_WASSERVENTIL](#job-steuern-wasserventil) - Ansteuern des Wasserventils Das Wasserventil kann von 0-100 % angesteuert werden. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_GEBLAESE](#job-steuern-geblaese) - Ansteuern des Geblaeses Das Geblaese kann von 0-100 % angesteuert werden. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
- [STEUERN_BELEUCHTUNG](#job-steuern-beleuchtung) - Ansteuern der Displaybeleuchtung Die Displaybeleuchtung kann von 0-100 % angesteuert werden. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen
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

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Lesen des internen Speichers Als Argumente werden die Adresse, die Anzahl der Datenbytes uebergeben.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int | 0x0000 - 0xFFFF |
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

<a id="job-codierung-schreiben"></a>
### CODIERUNG_SCHREIBEN

Codierdaten Schreiben fuer IHKA E46 Es muessen immer alle vier Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.

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
| LAENDERVARIANTE | string | 'ECE' 'US' |
| MOTORVARIANTE | string | 'Benzinmotor' 'Dieselmotor' |
| ZYLINDERZAHL | string | '4 Zylinder' '6 Zylinder' '8 Zylinder' '12 Zylinder' 'unbekannter Code' |
| LEERLAUFANHEBUNG_1 | string | 'default' 'bei elektrischen Verbrauchern' 'bei Unterspannung' |
| LEERLAUFANHEBUNG_2 | string | 'bei Unterspannung' ( nicht wenn in .._1 ) '' |
| AUSSTATTUNG_1 | string | 'default' 'AUC' '' |
| AUSSTATTUNG_2 | string | 'Zuheizer konventionell' 'Zuheizer K-Bus' 'unbekannter Code' |
| AUSSTATTUNG_3 | string | 'Solarsensor' '' |
| AUSSTATTUNG_4 | string | 'Bordmonitor' '' |
| ALLGEMEIN_1 | string | 'default' 'Kennfeldkuehlung' |
| ALLGEMEIN_2 | string | 'Kompressortransportsperre' '' |
| COD_IHK_AUC | int | 1 wenn AUC |
| COD_IHK_SOL | int | 1 wenn Solarsensor |
| COD_IHK_ZHZ | int | 1 wenn Zuheizer |
| KOMPRESSOR_SPERRE | int | Klimakompressor deaktiviert |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-status-analogeingaenge"></a>
### STATUS_ANALOGEINGAENGE

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_AUC_VERSORGUNG_WERT | real | Spannungsversorgung AUC-Sensor |
| STAT_AUC_VERSORGUNG_EINH | string | Volt |
| STAT_KLEMME30_WERT | real | Klemme 30 |
| STAT_KLEMME30_EINH | string | Volt |
| STAT_AUC_HEIZUNG_WERT | real | Spannungsversorgung Heizung AUC |
| STAT_AUC_HEIZUNG_EINH | string | Volt |
| STAT_GEBLAESE_PWM_WERT | real | PWM-Geblaesesteuerspannung |
| STAT_GEBLAESE_PWM_EINH | string | Volt |
| STAT_TINNEN_WERT | real | Innentemperaturfuehler |
| STAT_TINNEN_EINH | string | Grad Celsius |
| STAT_TVERDAMPFER_WERT | real | Verdampfertemperaturfuehler |
| STAT_TVERDAMPFER_EINH | string | Grad Celsius |
| STAT_AUC_WERT | real | Sensorsignal AUC |
| STAT_AUC_EINH | string | Volt |
| STAT_WT_WERT | real | Waermetauscherfuehler |
| STAT_WT_EINH | string | Grad Celsius |
| STAT_KLEMME30G_WERT | real | Klemme 30g |
| STAT_KLEMME30G_EINH | string | Volt |
| STAT_UMSCHALTVENTIL_WERT | real | Status Umschaltventil |
| STAT_UMSCHALTVENTIL_EINH | string | Volt |
| STAT_KLEMME15_WERT | real | Klemme 15 |
| STAT_KLEMME15_EINH | string | Volt |
| STAT_ABSPERRVENTIL_WERT | real | Status Absperrventil |
| STAT_ABSPERRVENTIL_EINH | string | Volt |
| STAT_TINNEN_SPANNUNG_WERT | real | Innentemperaturfuehler Spannungswert |
| STAT_TINNEN_SPANNUNG_EINH | string | Volt |
| STAT_DRUCKSENSOR_WERT | real | Drucksensor |
| STAT_DRUCKSENSOR_EINH | string | bar |
| STAT_SOLARSENSOR_WERT | int | Solarsensor |
| STAT_SOLARSENSOR_EINH | string | % |
| TELEGRAMM | binary | Antworttelegramm |

<a id="job-status-reglergroessen"></a>
### STATUS_REGLERGROESSEN

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_SOLL_WERT | real | Sollwert Temperatur |
| STAT_SOLL_EINH | string | Grad Celsius |
| STAT_TINNEN_WERT | real | Innentemperatur |
| STAT_TINNEN_EINH | string | Grad Celsius |
| STAT_TAUSSEN_WERT | real | Aussentemperatur |
| STAT_TAUSSEN_EINH | string | Grad Celsius |
| STAT_WT_WERT | real | Waermetauscherfuehler |
| STAT_WT_EINH | string | Grad Celsius |
| STAT_SOLL_KORRIGIERT_WERT | real | Sollwert Temperatur korregiert |
| STAT_SOLL_KORRIGIERT_EINH | string | Grad Celsius |
| STAT_FUEHR_WERT | real | Fuehrungsgroesse |
| STAT_FUEHR_EINH | string | % |
| STAT_GEBLAESE_WERT | int | Geblaesesteuerspannung |
| STAT_GEBLAESE_EINH | string | % |
| STAT_TINNEN_VERZOEGERT_WERT | real | Innentemperatur verzoegert |
| STAT_TINNEN_VERZOEGERT_EINH | string | Grad Celsius |
| STAT_Y_WERT | int | Stellgroesse |
| STAT_Y_EINH | string | % |
| STAT_WTSOLL_WERT | real | Waermetauscher Solltemperatur |
| STAT_WTSOLL_EINH | string | Grad Celsius |
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
| STAT_SOLL_WERT | real | Sollwert Temperatur |
| STAT_SOLL_EINH | string | Grad Celsius |
| STAT_GEBLAESESTUFE_WERT | int | Geblaesestufe |
| STAT_GEBLAESESTUFE_EINH | int | -- |
| STAT_GEBLAESE_WERT | int | Geblaese |
| STAT_GEBLAESE_EINH | string | % |
| STAT_BITLISTE_WERT | int | Bedienteildaten 2 (High-Byte) und 1 (Low-Byte) |
| STAT_BITLISTE_EINH | string | -- |
| STAT_FUNKTION_DEFROST_EIN | int | Defrost |
| STAT_FUNKTION_EIN | int | SG Funktion ein / aus |
| STAT_FUNKTION_AC_EIN | int | Klimabetrieb |
| STAT_FUNKTION_HHS_EIN | int | Heckscheibenheizung |
| STAT_FUNKTION_UMLUFT_EIN | int | Umluftbetrieb |
| STAT_FUNKTION_AUC_EIN | int | AUC-Betrieb |
| STAT_FUNKTION_AUTO_EIN | int | Automatikbetrieb |
| STAT_FUNKTION_FUSS_EIN | int | Belueftung Unten |
| STAT_FUNKTION_MITTE_EIN | int | Belueftung Mitte |
| STAT_FUNKTION_OBEN_EIN | int | Belueftung Oben |
| STAT_GEBLAESE_PLUS_EIN | int | Taste Geblaese + |
| STAT_GEBLAESE_MINUS_EIN | int | Taste Geblaese - |
| STAT_SOLLWERT_PLUS_EIN | int | Taste Temperatur + |
| STAT_SOLLWERT_MINUS_EIN | int | Taste Temperatur - |
| TELEGRAMM | binary | Antworttelegramm |
| TELEGRAMM2 | binary | Antworttelegramm Tastenstati |

<a id="job-status-io"></a>
### STATUS_IO

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_WASSERVENTIL_EIN | int | Wasserventil |
| STAT_ZUSATZWASSERPUMPE_EIN | int | Zusatzwasserpumpe |
| STAT_ZUHEIZER_EIN | int | Zusatzheizung |
| STAT_RELAIS_HECKSCHEIBE_EIN | int | Relais Heckscheibenheizung |
| STAT_KLIMABEREITSCHAFT_EIN | int | Klimabereitschaft nach Kompressoreinlauf |
| TELEGRAMM | binary | Antworttelegramm |
| TELEGRAMM2 | binary | Antworttelegramm 2 |

<a id="job-status-motor-klappenposition"></a>
### STATUS_MOTOR_KLAPPENPOSITION

Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_MOTOR_EINH | string | % |
| STAT_BELUEFTUNG_WERT | int | Belueftungsmotor |
| STAT_ENTFROSTUNG_WERT | int | Entfrostungsmotor |
| STAT_FUSSRAUM_WERT | int | Fussraummotor |
| STAT_FRISCHLUFT_LI_WERT | int | Frischluft- / Umluftmotor links |
| STAT_FRISCHLUFT_RE_WERT | int | Frischluft- / Umluftmotor rechts |
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

Anstossen des Schrittmotoreichlaufs Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DIAGNOSE_AUFRECHT | string | ja, wenn nicht '' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-display"></a>
### STEUERN_DISPLAY

Einschalten eines Testmusters in den Displays Es muss der Displaytest immer ausgeschalten werden Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TEST_MUSTER | int | 0    = Testmuster aus 1..4 = Testmuster 1..4 |
| DIAGNOSE_AUFRECHT | string | ja, wenn nicht '' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

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

<a id="job-steuern-taste-heckscheibe"></a>
### STEUERN_TASTE_HECKSCHEIBE

Ansteuern der Taste Heckscheibenheizung Voraussetzung ist, dass der Motor laeuft.

_No arguments._

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

<a id="job-steuern-relais-frontscheibe"></a>
### STEUERN_RELAIS_FRONTSCHEIBE

Ansteuern des Frontscheibenrelais Das Relais kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen Identisch mit STEUERN_ZUHEIZER, da gleicher Ausgang

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RELAIS_FRONTSCHEIBE | string | EIN, AUS |
| DIAGNOSE_AUFRECHT | string | ja, wenn nicht '' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-zuheizer"></a>
### STEUERN_ZUHEIZER

Ansteuern des Zuheizers Der Ausgang kann ein- bzw. ausgeschaltet werden. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen Identisch mit STEUERN_RELAIS_FRONTSCHEIBE, da gleicher Ausgang

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZUHEIZER | string | EIN, AUS |
| DIAGNOSE_AUFRECHT | string | ja, wenn nicht '' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-steuern-motor-klappenposition"></a>
### STEUERN_MOTOR_KLAPPENPOSITION

Ansteuern der Schrittmotoren in Prozent 0-100 % Es ist moeglich auch nur einzelne Argumente zu schreiben. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BELUEFTUNG | int | Belueftungsmotor 0 - 100 % oder '' |
| ENTFROSTUNG | int | Entfrostungsmotor 0 - 100 % oder '' |
| FUSSRAUM | int | Fussraummotor 0 - 100 % oder '' |
| FRISCHLUFT_LI | int | Frischluft- / Umluftmotor links 0 - 100 % oder '' |
| FRISCHLUFT_RE | int | Frischluft- / Umluftmotor rechts 0 - 100 % oder '' |
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

<a id="job-steuern-beleuchtung"></a>
### STEUERN_BELEUCHTUNG

Ansteuern der Displaybeleuchtung Die Displaybeleuchtung kann von 0-100 % angesteuert werden. Vor dem Ansteuern den Job DIAGNOSE_AUFRECHT aufrufen Nach dem Ansteuern den Job DIAGNOSE_ENDE aufrufen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BELEUCHTUNG | int | Beleuchtung 0 - 100 % |
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

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (63 × 2)
- [ROVERPARTNUMPREFIX](#table-roverpartnumprefix) (21 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (16 × 2)
- [FORTTEXTE](#table-forttexte) (53 × 2)
- [FARTTEXTE](#table-farttexte) (8 × 2)
- [FARTMATRIX](#table-fartmatrix) (1 × 13)

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

Dimensions: 63 rows × 2 columns

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

Dimensions: 53 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | Belueftungsklappenmotor |
| 0x01 | Entfrostungsklappenmotor |
| 0x02 | Fussraumklappenmotor |
| 0x03 | Frischluft/Umluftklappenmotor links |
| 0x04 | Frischluft/Umluftklappenmotor rechts |
| 0x05 | frei 5 |
| 0x06 | Drucksensor, AUC Versorgung |
| 0x07 | frei 7 |
| 0x08 | frei 8 |
| 0x09 | frei 9 |
| 0x0A | frei 10 |
| 0x0B | Verdampferfuehler |
| 0x0C | frei 12 |
| 0x0D | Waermetauscherfuehler |
| 0x0E | frei 14 |
| 0x0F | frei 15 |
| 0x10 | frei 16 |
| 0x11 | frei 17 |
| 0x12 | Innenraumtemperaturfuehler |
| 0x13 | frei 19 |
| 0x14 | frei 20 |
| 0x15 | Relais Heckscheibenheizung |
| 0x16 | Zuheizer, Relais Frontscheibenheizung |
| 0x17 | Zusatzwasserpumpe |
| 0x18 | Wasserventil |
| 0x19 | Geblaesesteuerspannung |
| 0x1A | Innenfuehlergeblaese |
| 0x1B | Kommunikation mit dem Zuheizer |
| 0x1C | AUC Sensor |
| 0x1D | Drucksensor |
| 0x1E | AUC Heizung |
| 0x1F | Latentwaermespeicher Umschaltventil |
| 0x20 | Latentwaermespeicher Absperrventil |
| 0x21 | Solarsensor oder Latentwaermespeicher Temperaturfuehler |
| 0x22 | frei 34 |
| 0x23 | frei 35 |
| 0x24 | frei 36 |
| 0x25 | frei 37 |
| 0x26 | frei 38 |
| 0x27 | frei 39 |
| 0x28 | frei 40 |
| 0x29 | frei 41 |
| 0x2A | frei 42 |
| 0x2B | frei 43 |
| 0x2C | frei 44 |
| 0x2D | frei 45 |
| 0x2E | frei 46 |
| 0x2F | frei 47 |
| 0x30 | frei 48 |
| 0x31 | frei 49 |
| 0x32 | Falscher Klimakasten verbaut |
| 0xFF | Energiesparmode aktiviert |
| 0x?? | unbekannter Fehlerort |

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
