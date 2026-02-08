# ZUHEIZ_B.prg

- Jobs: [16](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Zuheizer Backup Steuergeraet |
| ORIGIN | BMW TP-423 Drexel |
| REVISION | 1.03 |
| AUTHOR | BMW TP-423 Drexel, BMW TP-423 Teepe |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [KEY_BYTES](#job-key-bytes)
- [IDENT](#job-ident)
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose Ende
- [STEUERN_KRAFTSTOFFPUMPE](#job-steuern-kraftstoffpumpe) - Ansteuern der Kraftstoffpumpe
- [STEUERN_ZUHEIZER](#job-steuern-zuheizer) - Ansteuern des Zuheizers Der Ausgang kann ein- bzw. ausgeschaltet werden.
- [STATUS_MESSWERTE](#job-status-messwerte) - Messwerteblock auswerten
- [EEPROM_LESEN](#job-eeprom-lesen) - nur mit ADS moeglich
- [EEPROM_SCHREIBEN](#job-eeprom-schreiben) - nur mit ADS moeglich
- [ZUHEIZER_NOT_AUS](#job-zuheizer-not-aus) - nur mit ADS moeglich Zuheizer wird zwangsweise in den AUS-Zustand gebracht
- [BRENNDAUER_LESEN](#job-brenndauer-lesen) - nur mit ADS moeglich
- [STARTZAEHLER_LESEN](#job-startzaehler-lesen) - nur mit ADS moeglich
- [STARTZAEHLER_SPEICHERN](#job-startzaehler-speichern) - nur mit ADS moeglich

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

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-key-bytes"></a>
### KEY_BYTES

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| KEYBYTE_1 | int |  |
| KEYBYTE_2 | int |  |
| ID_1 | string |  |
| ID_2 | string |  |
| ID_3 | string |  |
| ID_4 | binary |  |
| ANTWORT | binary |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-ident"></a>
### IDENT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_1 | string |  |
| ID_2 | string |  |
| ID_3 | string |  |
| ID_4 | binary |  |
| ANTWORT | binary |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Text zu Fehlerort table FArtTexte |
| F_HFK | int | Fehlerhaeufigkeit = 1 |
| F_ART_ANZ | int | Anzahl der Fehlerarten = 1 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen = 0 |
| F_ART1_NR | int | table FArtTexte |
| F_ART1_TEXT | string | table FArtTexte |
| F_HEX_CODE | binary | Fehlerspeicherdaten |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose Ende

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-kraftstoffpumpe"></a>
### STEUERN_KRAFTSTOFFPUMPE

Ansteuern der Kraftstoffpumpe

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ANTWORT | binary |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-zuheizer"></a>
### STEUERN_ZUHEIZER

Ansteuern des Zuheizers Der Ausgang kann ein- bzw. ausgeschaltet werden.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZUHEIZER | string | EIN, AUS |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ANTWORT | binary |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-status-messwerte"></a>
### STATUS_MESSWERTE

Messwerteblock auswerten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KLEMME30_WERT | real | Batteriespannung |
| STAT_KLEMME30_EINH | string | Volt |
| STAT_KUEHLMITTEL_WERT | int | Kuehlmitteltemperatur |
| STAT_KUEHLMITTEL_EINH | string | Grad Celsius |
| STAT_LEISTUNG_BRENNLUFTGEBLAESE_WERT | int | Leistung Brennluftgeblaese |
| STAT_LEISTUNG_BRENNLUFTGEBLAESE_EINH | string | % |
| STAT_LEISTUNG_GLUEHSTIFT_WERT | int | Leistung Gluehelement |
| STAT_LEISTUNG_GLUEHSTIFT_EINH | string | % |
| STAT_LEISTUNG_DOSIERPUMPE_WERT | int | Leistung Kraftstoff Dosierpumpe |
| STAT_LEISTUNG_DOSIERPUMPE_EINH | string | % |
| STAT_BETRIEBSZUSTAND_WERT | int | Betriebszustand |
| STAT_BETRIEBSZUSTAND_EINH | string | - |
| STAT_BETRIEBSZUSTAND | string | table MWTexte |
| STAT_EINSCHALTSIGNAL_EIN | int | Eingang Pin 3 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-eeprom-lesen"></a>
### EEPROM_LESEN

nur mit ADS moeglich

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int | 0-255 bzw. 0x00-0xFF |
| ANZAHL | int | 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ANTWORT_EOL | binary |  |
| DATEN | binary |  |
| I | int |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-eeprom-schreiben"></a>
### EEPROM_SCHREIBEN

nur mit ADS moeglich

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int | 0-255 bzw. 0x00-0xFF |
| WERT | int | 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ANTWORT_EOL | binary |  |
| I | int |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-zuheizer-not-aus"></a>
### ZUHEIZER_NOT_AUS

nur mit ADS moeglich Zuheizer wird zwangsweise in den AUS-Zustand gebracht

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ANTWORT_EOL | binary |  |
| I | int |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-brenndauer-lesen"></a>
### BRENNDAUER_LESEN

nur mit ADS moeglich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| BRENNDAUER_MINUTEN | int | Brenndauer Minuten |
| BRENNDAUER_STUNDEN | int | Brenndauer Stunden |
| BRENNDAUER | real | Brenndauer gesamt |
| ANTWORT_EOL | binary |  |
| I | int |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-startzaehler-lesen"></a>
### STARTZAEHLER_LESEN

nur mit ADS moeglich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STARTZAEHLER | int | Anzahl erfolgreicher Starts |
| STARTZAEHLER_KOPIE | int | Kopie des Startzaehlers |
| STARTZAEHLER_DIFFERENZ | int | Differenz Startzaehler und Kopie des Startzaehlers |
| ANTWORT_EOL | binary |  |
| I | int |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-startzaehler-speichern"></a>
### STARTZAEHLER_SPEICHERN

nur mit ADS moeglich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STARTZAEHLER | int | Anzahl erfolgreicher Starts |
| ANTWORT_EOL | binary |  |
| I | int |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (15 × 2)
- [FARTTEXTE](#table-farttexte) (11 × 2)
- [MWTEXTE](#table-mwtexte) (17 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 15 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x0000FFFF | Steuergeraet defekt |
| 0x00000414 | Steuergeraet falsch codiert |
| 0x0000057E | keine Flammbildung |
| 0x0000057F | Flammabbruch |
| 0x00000214 | Versorgungsspannung Signal zu gross |
| 0x00000580 | Unterspannungsabschaltung |
| 0x00000581 | wiederholter Flammabbruch im Heizzyklus |
| 0x00000582 | Heizgeraet ueberhitzt |
| 0x00000583 | Temperaturfuehler defekt |
| 0x00000584 | Gluehstift Flammwaechter |
| 0x00000585 | Dosierpumpe |
| 0x00000586 | Verbrennungsluftgeblaese |
| 0x00000587 | Umwaelzpumpe |
| 0x00000588 | Ansteuerung Fahrzeuggeblaese |
| 0x00000000 | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 11 rows × 2 columns

| ART | ARTTEXT |
| --- | --- |
| 0x88 | kein Fehler |
| 0x00 | interner Fehler |
| 0x06 | Grenzwertueberschreitung |
| 0x1B | unplausibles Signal |
| 0x1C | Kurzschluss gegen U-Batt |
| 0x1D | Kurzschluss gegen Masse |
| 0x1E | Leitungsunterbrechung, Kurzschluss gegen U-Batt |
| 0x23 | ungueltiger Arbeitsbereich |
| 0x24 | Leitungsunterbrechung |
| 0x25 | Kurzschluss gegen Masse |
| 0xFF | unbekannte Fehlerart |

<a id="table-mwtexte"></a>
### MWTEXTE

Dimensions: 17 rows × 2 columns

| MW | MWTEXT |
| --- | --- |
| 0 |  |
| 6 | Teillast |
| 7 | Vollast |
| 30 | Start |
| 31 | Nachlauf |
| 32 | Regelpause |
| 33 | Stoerung |
| 135 | ein |
| 136 | aus |
| 19 | Heizung EIN |
| 20 | Heizung AUS |
| 21 | zuheizen |
| 22 | lueften |
| 23 | heizen |
| 24 | Geblaese EIN |
| 25 | Geblaese AUS |
| ?? | unbekannter Messwerttext |
