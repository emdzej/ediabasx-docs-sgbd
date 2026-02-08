# KOMBI361.prg

- Jobs: [18](#jobs)
- Tables: [5](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Kombi E36 |
| ORIGIN | BMW TI-433 Dennert |
| REVISION | 2.06 |
| AUTHOR | BMW TP-421 Teepe, BMW TP-421 Drexel, BMW TI-433 Dennert |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung
- [IDENT](#job-ident) - Auslesen der Identifikationsdaten
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Beenden der Diagnose
- [GWSZ_RESET](#job-gwsz-reset) - Ruecksetzen des Gesamtwegstreckenzaehlers
- [SIA_RESET](#job-sia-reset) - Ruecksetzen der Service-Intervall-Anzeige
- [FG_NR_LESEN](#job-fg-nr-lesen) - Auslesen der Fahrgestellnummer
- [CODIERUNG_LESEN](#job-codierung-lesen) - Auslesen der Fahrgestellnummer
- [STATUS_LESEN](#job-status-lesen) - Auslesen der Stati
- [EEPROM_LESEN](#job-eeprom-lesen)
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Speicherinhaltes
- [STEUERN_ANALOG](#job-steuern-analog) - Vorgeben der Analog-Signale
- [STEUERN_TACHO_A](#job-steuern-tacho-a) - Vorgeben des Tacho-A-Signals
- [SELBSTTEST](#job-selbsttest) - Vorgeben des Tacho-Selbsttests
- [STEUERN_SELBSTTEST](#job-steuern-selbsttest) - Vorgeben des Tacho-Selbsttests
- [STEUERN_DIGITAL](#job-steuern-digital) - Vorgeben der Digital-Ausgaenge

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

Initialisierung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn i.O. |

<a id="job-ident"></a>
### IDENT

Auslesen der Identifikationsdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| ID_GEN_NR | int | Generationsnummer |
| ID_HW_NR | int | Hardwarenummer |
| ID_SW_NR | string | Softwarenummer |
| ID_PP_NR | string | Pruefplannummer |
| ID_DATUM_KW | string | Herstelldatum KW |
| ID_DATUM_JAHR | string | Herstelldatum Jahr |
| _ANTWORT | binary | Antwort-Telegramm |

<a id="job-fs-lesen"></a>
### FS_LESEN

Auslesen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| F_ORT_NR | int | Nr des Fehlers (entspricht dem Fehlercode) |
| F_ORT_TEXT | string | Fehlertext |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_ART1_NR | int | Textindex fuer Fehlerart 1 |
| F_ART1_TEXT | string | Text fuer Fehlerart 1 |
| F_ART2_NR | int | Textindex fuer Fehlerart 2 |
| F_ART2_TEXT | string | Text fuer Fehlerart 2 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen, hier immer 0 |
| F_ZAHL | int | Anzahl der Fehler |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Beenden der Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-gwsz-reset"></a>
### GWSZ_RESET

Ruecksetzen des Gesamtwegstreckenzaehlers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-sia-reset"></a>
### SIA_RESET

Ruecksetzen der Service-Intervall-Anzeige

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG1 | string | Oel/Weg oder Zeit - Reset |
| ARG2 | string | Oel/Weg oder Zeit - Reset |
| ARG3 | string | Oel/Weg oder Zeit - Reset |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY, ERROR_NACK od. ERROR_PARAMETER |

<a id="job-fg-nr-lesen"></a>
### FG_NR_LESEN

Auslesen der Fahrgestellnummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| FG_NR | string | Fahrgestellnummer |
| FG_NR2 | string | Fahrgestellnummer aus eingeloetetem EEPROM |

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Auslesen der Fahrgestellnummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| K_ZAHL | int | Wegimpulszahl k |
| CODIERSTECKER_CODIERT | int | steckbarer Codierstecker codiert j/n |
| EEPROM_CODIERT | int | EEPROM Codierstecker codiert j/n |
| TACHO_ENDWERT | string | Skalenendwert des Tachometers |
| TACHO_ENDWERT_TEXT | string | LA-unabhaengiger Skalenendwert des Tachometers |
| SCHALTPUNKT_V1_WERT | int | Schaltschwelle der Geschwindigkeitswarnung |
| SCHALTPUNKT_V1_EINH | string | Einheit der Schaltschwelle der Geschwindigkeitswarnung [km/h] |
| SI_DREHZAHLGRENZE_WERT | int | Drehzahlgrenze fuer Verschleissfaktor Drehzahl |
| SI_DREHZAHLGRENZE_EINH | string | "1/min" |
| WEGINSPEKTIONS_INTERVALL_WERT | int | Wert der Weginspektionsintervalle |
| WEGINSPEKTIONS_INTERVALL_EINH | string | Einheit fuer den Wert der Weginspektionsintervalle [SI km] |
| ZEITINSPEKTIONS_INTERVALL_WERT | int | Wert der Zeitinspektionsintervalle |
| ZEITINSPEKTIONS_INTERVALL_EINH | string | Einheit fuer den Wert der Zeitinspektionsintervalle [Tage] |
| OELSERVICE_INTERVALL_WERT | int | Wert der Oelserviceintervalle |
| OELSERVICE_INTERVALL_EINH | string | Einheit fuer den Wert der Oelinspektionsintervalle ["-"] |
| ZEITINSPEKTION_FUEHREN | int | Zeitinspektion ja oder nein |
| DREHZAHLFAKTOR | int | Verschleissfaktor Drehzahl |
| TEMPERATURFAKTOR | int | Verschleissfaktor Temperatur |
| STEIGUNG_EINSPRITZKENNLINIE | string | Steigung der Einspritzkennlinie |
| WEGSTRECKENZAEHLER_EINHEIT | string |  |
| COD_WEGSTRECKEN_EINHEIT_MILES | int | 0 oder 1 |
| AUSTAUSCH_KOMBI_VERBAUT | int | Ausstauschkombi ja nein |
| AUSTAUSCH_CODIERSTECKER_VERBAUT | int | Ausstauschstecker ja nein |
| KVA_VERBAUT | string | KVA oder OELTEMPERATUR |
| TANKGEBER_TYP | string | Typ des Tankgebers |
| MOTOR_ART | string | Motortyp bzw Gruppe |
| AKUSTISCHE_GURTWARNUNG_CODIERT | int |  |
| BC_VERBAUT | int |  |
| DZM_VERBAUT | string | Drehzahlmesser j/n |
| EGS_VERBAUT | int |  |
| GONG_VON_KOMBI_ANSTEUERBAR | int |  |
| GRENZDREHZAHL | string |  |
| DZM_SKALENENDWERT | string | 6000, 7000 oder 8000 |
| SIA_AUS_VERZOEGERUNGSZEIT_WERT | int | Dauer der Abschaltung der SIA-Anzeige nach Motorstart |
| SIA_AUS_VERZOEGERUNGSZEIT_EINH | string | "sec" |
| LAENDERCODE_KOMBI | string | Laendercode des Kombis |
| FG_NR | string | Fahrgestellnummer |
| FG_NR_2 | string | redundante FG-NR im Codierstecker |
| LICHT_EINSCHALTDAUER_WERT | int |  |
| LICHT_EINSCHALTDAUER_EINH | string | "sec" |
| LICHT_EINSCHALTVERZOEGERUNG_WERT | int |  |
| LICHT_EINSCHALTVERZOEGERUNG_EINH | string | "sec" |
| GURTWARNUNG_AUSSCHALTZEIT_WERT | int |  |
| GURTWARNUNG_AUSSCHALTZEIT_EINH | string | "ms" |
| GURTWARNUNG_EINSCHALTZEIT_WERT | int |  |
| GURTWARNUNG_EINSCHALTZEIT_EINH | string | "ms" |
| V1_SCHWELLE_AUSSCHALTZEIT_WERT | int |  |
| V1_SCHWELLE_AUSSCHALTZEIT_EINH | string | "ms" |
| V1_SCHWELLE_EINSCHALTZEIT_WERT | int |  |
| V1_SCHWELLE_EINSCHALTZEIT_EINH | string | "ms" |
| SCHLUESSELWARNUNG_AUSSCHALTZEIT_WERT | int |  |
| SCHLUESSELWARNUNG_AUSSCHALTZEIT_EINH | string | "ms" |
| SCHLUESSELWARNUNG_EINSCHALTZEIT_WERT | int |  |
| SCHLUESSELWARNUNG_EINSCHALTZEIT_EINH | string | "ms" |
| LICHTWARNUNG_AUSSCHALTZEIT_WERT | int |  |
| LICHTWARNUNG_AUSSCHALTZEIT_EINH | string | "ms" |
| LICHTWARNUNG_EINSCHALTZEIT_WERT | int |  |
| LICHTWARNUNG_EINSCHALTZEIT_EINH | string | "ms" |
| Z_CODE_GM | string | Grundmerkmaleschluessel Zentralcode |
| Z_CODE_SA | string | Sonderausstattungsschluessel Zentralcode |
| Z_CODE_VN | string | Versionsnummernschluessel Zentralcode |
| Z_CODE_AM | string | Antriebsmerkmaleschluessel Zentralcode |
| TYP_CODE | string | Typencode |
| BMW_NR | string | Teilenummer BMW |
| AENDERUNGS_INDEX | int | Aenderungsindex |
| CODIER_INDEX | int |  |
| HW_STAND | int | Hardwarestand |
| DATUM_KW | int |  |
| DATUM_JAHR | int |  |
| CODIERDATEN_HEX | binary | alle Daten |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Auslesen der Stati

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| K_ZAHL | int | gleich STAT_K_ZAHL |
| KVA | int | gleich STAT_KVA |
| MOTORFAKTOR | int | gleich STAT_MOTORFAKTOR |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_K_ZAHL | int |  |
| STAT_KVA | int |  |
| STAT_MOTORFAKTOR | int |  |
| STAT_HELLIGKEIT_FOTOTRANSISTOR_WERT | int | Liefert: |
| STAT_HELLIGKEIT_FOTOTRANSISTOR_EINH | string | Liefert: [%] |
| STAT_KLEMME_58g_LOW_WERT | int | Liefert: 0 bis 255 |
| STAT_KLEMME_58g_HIGH_WERT | int | Liefert: 0 bis 255 |
| STAT_KLEMME_58g_EINH | string | Liefert: [ms] |
| STAT_U_BATT_WERT | int | Liefert: 2 bis 24,8 |
| STAT_U_BATT_EINH | string | Liefert: [V] |
| STAT_TEMPERATUR_WERT | int | Liefert: |
| STAT_TEMPERATUR_EINH | string | Liefert: [Grad C] |
| STAT_TANKINHALT_WERT | int | Liefert: |
| STAT_TANKINHALT_EINH | string | Liefert: [l] |
| STAT_KVA_ODER_OELTEMPERATUR_VERBAUT | string | Liefert: "KVA" oder "OELTEMPERATUR" |
| STAT_KVA_SIGNAL_WERT | int | Liefert: |
| STAT_OELTEMPERATUR_WERT | int | Liefert: |
| STAT_OELTEMPERATUR_EINH | string | Liefert: [Grad C] |
| STAT_KVA_SIGNAL_EINH | string | Liefert: [ms] |
| STAT_DREHZAHL_SIGNAL_WERT | int | Liefert: 0 bis 10000 |
| STAT_DREHZAHL_SIGNAL_EINH | string | Liefert: [1/min] |
| STAT_GESCHWINDIGKEIT_SIGNAL_WERT | int | Liefert: |
| STAT_GESCHWINDIGKEIT_SIGNAL_EINH | string | Liefert: [km/h] |
| STAT_KLEMME_R_EIN | int | Liefert: 0 oder 1 |
| STAT_KLEMME_15_EIN | int | Liefert: 0 oder 1 |
| STAT_SIA_RESET_EIN | int | Liefert: 0 oder 1 |
| STAT_BREMSBELAGVERSCHLEISSANZEIGE_EIN | int | Liefert: 0 oder 1 |
| STAT_GURTKONTAKT_EIN | int | Liefert: 0 der 1 |
| STAT_ZUENDSCHLOSSKONTAKT_EIN | int | Liefert: 0 oder 1 |
| STAT_FAHRERTUERKONTAKT_EIN | int | Liefert: 0 oder 1 |
| TELEGRAMM | binary | Liefert: Antworttelegramm |

<a id="job-eeprom-lesen"></a>
### EEPROM_LESEN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | string | Hexwert (0x00) der Adresse ,ab der das EEPROM gelesen werden soll |
| BYTE_ANZAHL | int | Anzahl der Bytes (max. 16 !) die ausgelesen werden sollen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B.: ACK) |
| _ANTWORT | binary | Liefert: Antworttelegramm |
| DATEN | binary | Datenfeld |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Auslesen des Speicherinhaltes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANZAHL | int | Anzahl der Datenbytes: 1 bis 16 (0x10) |
| ADRESSE_HIGH | int | Startadresse high |
| ADRESSE_LOW | int | Startadresse low |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| _ANTWORT | binary | Liefert: Antworttelegramm |
| DATEN | binary | Liefert: Hexdump des angeforderten Speicherbereiches |

<a id="job-steuern-analog"></a>
### STEUERN_ANALOG

Vorgeben der Analog-Signale

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSGANG | string | anzusteuernder Ausgang |
| WERT | int | Tastverhaeltnis anzusteuernder Ausgang |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-steuern-tacho-a"></a>
### STEUERN_TACHO_A

Vorgeben des Tacho-A-Signals

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GESCHWINDIGKEIT | int | gewuenschte Vorgabegeschwindigkeit |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-selbsttest"></a>
### SELBSTTEST

Vorgeben des Tacho-Selbsttests

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-steuern-selbsttest"></a>
### STEUERN_SELBSTTEST

Vorgeben des Tacho-Selbsttests

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

Vorgeben der Digital-Ausgaenge

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSGANG | string | anzusteuernder Ausgang |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| _ANTWORT | binary | Antworttelegramm |
| _SENDEN | binary | Sendetelegramm |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (22 × 2)
- [FARTTEXTE](#table-farttexte) (7 × 2)
- [SIARESET](#table-siareset) (4 × 2)
- [STEUERNANALOG](#table-steuernanalog) (8 × 2)
- [STEUERNDIGITAL](#table-steuerndigital) (10 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 22 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | Interner Fehler (RAM) |
| 0x05 | EEPROM Lesefehler |
| 0x07 | K-Zahl fehlerhaft |
| 0x08 | A/D-Wandler, Wandlerzeit ueberschritten |
| 0x09 | Bordnetzfehler, Kl.15 high / Kl.R low |
| 0x0a | Klemme 15 Ueberspannung |
| 0x0D | Ueberstrom Messinstrumente |
| 0x0E | PCVA thermisch ueberlastet |
| 0x0F | SIA-Eingang defekt |
| 0x10 | Tankgeber defekt |
| 0x11 | Kuehlmitteltemperaturgeber defekt |
| 0x13 | Oeltemperaturgeber defekt |
| 0x15 | 5-Volt-Spannung gestoert |
| 0x16 | KOMBI-Taste defekt |
| 0x18 | Geschwindigkeits-Signal gestoert |
| 0x19 | Drehzahlsignal gestoert |
| 0x1A | Einspritzsignal gestoert |
| 0x1B | Bremsbelagverschleiss |
| 0x1c | Tankreservekontakt |
| 0x1E | Fahrertuerkontakt |
| 0x1F | Zuendschluesselkontakt |
| 0xff | unbekannter Fehler |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 7 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | Kurzschluss gegen U-Batt |
| 0x01 | Kurzschluss gegen Masse |
| 0x02 | Leitungsunterbrechung |
| 0x03 | ungueltiger Arbeitsbereich |
| 0x04 | sporadischer Fehler |
| 0x05 | statischer Fehler |
| 0xFF | unbekannte Fehlerart |

<a id="table-siareset"></a>
### SIARESET

Dimensions: 4 rows × 2 columns

| SELECTOR | RESET |
| --- | --- |
| OEL_RESET | 0x01 |
| WEG_RESET | 0x02 |
| ZEIT_RESET | 0x04 |
| unbekannt | 0x00 |

<a id="table-steuernanalog"></a>
### STEUERNANALOG

Dimensions: 8 rows × 2 columns

| SELECTOR | BYTE |
| --- | --- |
| TACHO | 0x01 |
| DZM | 0x02 |
| KVA | 0x03 |
| TANK | 0x04 |
| TEMP | 0x05 |
| OELTEMP | 0x06 |
| IK_LCD | 0x07 |
| unbekannt | 0x00 |

<a id="table-steuerndigital"></a>
### STEUERNDIGITAL

Dimensions: 10 rows × 2 columns

| SELECTOR | BYTE |
| --- | --- |
| GONG_T3 | 0x01 |
| TANKRES | 0x02 |
| UEBERTEMP | 0x04 |
| BVA | 0x08 |
| GURT | 0x10 |
| EGS | 0x20 |
| AKUSTIK | 0x40 |
| ALLE_AN | 0x7F |
| ALLE_AUS | 0x00 |
| unbekannt | 0x00 |
