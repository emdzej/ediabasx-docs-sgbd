# EHC_2N.PRG

- Jobs: [36](#jobs)
- Tables: [10](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | EHC_2, 2-Achs-Luftfederung Steuergeraet |
| ORIGIN | BMW EE-230 Stefan Reisinger |
| REVISION | 0.91 |
| AUTHOR | BMW EE-230 Stefan Reisinger |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung / Kommunikationsparameter fuer &lt;SG&gt; automatischer Aufruf beim ersten Zugriff auf SGBD
- [INFO](#job-info) - Information bzgl. SGBD
- [IDENTIFIKATION](#job-identifikation) - Ermittlung der SG-Variante
- [IDENT](#job-ident) - Ident-Daten fuer EHC
- [FS_QUICK_LESEN](#job-fs-quick-lesen) - Fehlerspeicher quick lesen
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [CODE_LESEN](#job-code-lesen) - gibt die Codierinformation als BYTE-STRING aus
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels
- [SPEICHER_LOESCHEN](#job-speicher-loeschen) - EEPROM loeschen bis auf SG-Identifikation
- [SG_RESET](#job-sg-reset) - Reset des Steuergeraetes
- [FS_SHADOW_LESEN](#job-fs-shadow-lesen) - auslesen des Fehlershadowspeichers
- [ABGLEICHWERT_LESEN](#job-abgleichwert-lesen) - Hoehenstand lesen
- [ABGLEICHWERT_PROGRAMMIEREN](#job-abgleichwert-programmieren) - Offset fuer Hoehenstaende eingeben
- [HERSTELLDATEN_LESEN](#job-herstelldaten-lesen) - Auslesen des Herstelldaten
- [HERSTELLDATEN_SCHREIBEN](#job-herstelldaten-schreiben) - Schreiben der Herstelldaten
- [DIAGNOSEMODE_ERHALTEN](#job-diagnosemode-erhalten) - Zaehler fuer Diagnosemode zuruecksetzen
- [DIAGNOSEMODE_BEENDEN](#job-diagnosemode-beenden) - beendet den Diagnosemode vorzeitig
- [FAHRZEUG_HOEHE_ABGLEICHEN](#job-fahrzeug-hoehe-abgleichen) - automatischer Hoehenabgleich
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Speicherinhaltes
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Auslesen des Speicherinhaltes
- [HOEHE_SPEICHERN](#job-hoehe-speichern) - Hoehe in den leak-Bereich
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers
- [IO_STATUS_SCHREIBEN_AKTOREN](#job-io-status-schreiben-aktoren) - Ansteuern der Steuergeraeteausgaenge
- [IO_STATUS_LESEN_AKTOREN](#job-io-status-lesen-aktoren) - I/O Status lesen Aktoren
- [IO_STATUS_LESEN_SENSOREN](#job-io-status-lesen-sensoren) - I/O Status lesen
- [SG_STATUS_SCHREIBEN_MODI](#job-sg-status-schreiben-modi) - Verschiedene Softwaremodi koennen aktiviert, bzw deaktiviert werden
- [SG_STATUS_LESEN_MODI](#job-sg-status-lesen-modi) - Verschiedene Softwaremodi koennen
- [SG_STATUS_SCHREIBEN_REGLER](#job-sg-status-schreiben-regler) - Vorgeben des Zielniveaus
- [SG_STATUS_LESEN_REGLER](#job-sg-status-lesen-regler) - Verschiedene Softwaremodi koennen
- [COD_C_LESEN](#job-cod-c-lesen) - Codierdaten lesen
- [COD_C_SCHREIBEN](#job-cod-c-schreiben) - Codierdaten schreiben
- [EEPROM_LOEHNERT_LESEN](#job-eeprom-loehnert-lesen) - EEPROM Daten lesen
- [EEPROM_LOEHNERT_SCHREIBEN](#job-eeprom-loehnert-schreiben) - EEPROM Daten schreiben
- [KEY_SEED_NORMAL](#job-key-seed-normal) - Freischaltung fuer Zugriffsebene 1
- [KEY_SEED_EXPERT](#job-key-seed-expert) - Freischaltung fuer Zugriffsebene 2

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung / Kommunikationsparameter fuer &lt;SG&gt; automatischer Aufruf beim ersten Zugriff auf SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-info"></a>
### INFO

Information bzgl. SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ECU | string | Steuergerat im Klartext |
| ORIGIN | string | Steuergeraete-Verantwortlicher |
| REVISION | string | Versions-Nummer |
| AUTHOR | string | Namen aller Autoren |
| COMMENT | string | wichtige Hinweise |
| SPRACHE | string | deutsch / english |

<a id="job-identifikation"></a>
### IDENTIFIKATION

Ermittlung der SG-Variante

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| VARIANT | string | Programmname |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer EHC

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | string | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Variantenindex |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Text |
| ID_SW_NR | string | Software-Nummer |
| ID_AIF_VORHANDEN | int | 1, wenn Anwender-Info-Feld vorhanden |
| ID_BUS_ANZ | int | Anzahl Busse |
| ID_BUS1_TYP | int | Bustyp 1 |
| ID_BUS1_INDEX | string | Busindex 1 |
| ID_BUS2_TYP | int | Bustyp 2 |
| ID_BUS2_INDEX | string | Busindex 2 |
| _TEL_ANTWORT | binary |  |

<a id="job-fs-quick-lesen"></a>
### FS_QUICK_LESEN

Fehlerspeicher quick lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| F_ANZ | int | Anzahl der Fehler |
| FS_DATUM_KW | int | Loeschdatum KW [0-53] |
| FS_DATUM_JAHR | int | Loeschdatum Jahr [0-99] |
| _TEL_ANTWORT | binary |  |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-code-lesen"></a>
### CODE_LESEN

gibt die Codierinformation als BYTE-STRING aus

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODIERBLOCK | int | Codierblock Nr. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |
| _TEL_SEND | binary |  |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| BYTE1 | int | nach Codierung soll hier ein Teil der Fahrgestell-Nr. stehen |
| BYTE2 | int | nach Codierung soll hier ein Teil der Fahrgestell-Nr. stehen |
| BYTE3 | int | nach Codierung soll hier ein Teil der Fahrgestell-Nr. stehen |
| _TEL_ANTWORT | binary |  |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | nach Codierung soll hier ein Teil der Fahrgestell-Nr. stehenn |
| BYTE2 | int | nach Codierung soll hier ein Teil der Fahrgestell-Nr. stehen |
| BYTE3 | int | nach Codierung soll hier ein Teil der Fahrgestell-Nr. stehen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-speicher-loeschen"></a>
### SPEICHER_LOESCHEN

EEPROM loeschen bis auf SG-Identifikation

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-sg-reset"></a>
### SG_RESET

Reset des Steuergeraetes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-fs-shadow-lesen"></a>
### FS_SHADOW_LESEN

auslesen des Fehlershadowspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-abgleichwert-lesen"></a>
### ABGLEICHWERT_LESEN

Hoehenstand lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| EE_H_FL_ZERO | int | Nullabgleich fuer Hoehenstandssensor |
| EE_H_FR_ZERO | int | Nullabgleich fuer Hoehenstandssensor |
| EE_H_RL_ZERO | int | Nullabgleich fuer Hoehenstandssensor |
| EE_H_RR_ZERO | int | Nullabgleich fuer Hoehenstandssensor |
| EE_H_ZERO_EINH | string | Einheit fuer Nullabgleich [in AD-Counts] |
| EE_H_FR_LEAK | int | Eingeschriebender Hoehenstand zur Grobleckagepruefung |
| EE_H_FL_LEAK | int | Eingeschriebender Hoehenstand zur Grobleckagepruefung |
| EE_H_RR_LEAK | int | Eingeschriebender Hoehenstand zur Grobleckagepruefung |
| EE_H_RL_LEAK | int | Eingeschriebender Hoehenstand zur Grobleckagepruefung |
| EE_H_LEAK_EINH | string | Einheit fuer Hoehenstand zur Grobleckagepruefung [mm] |
| _TEL_ANTWORT | binary |  |

<a id="job-abgleichwert-programmieren"></a>
### ABGLEICHWERT_PROGRAMMIEREN

Offset fuer Hoehenstaende eingeben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| OFFSETBYTE_FL_A | int | Offset fuer Hoehenstandssensor |
| OFFSETBYTE_FL_B | int | Offset fuer Hoehenstandssensor |
| OFFSETBYTE_FR_A | int | Offset fuer Hoehenstandssensor |
| OFFSETBYTE_FR_B | int | Offset fuer Hoehenstandssensor |
| OFFSETBYTE_RL_A | int | Offset fuer Hoehenstandssensor |
| OFFSETBYTE_RL_B | int | Offset fuer Hoehenstandssensor |
| OFFSETBYTE_RR_A | int | Offset fuer Hoehenstandssensor |
| OFFSETBYTE_RR_B | int | Offset fuer Hoehenstandssensor |
| VOREINST_BYTE_FR_A | int | Im Bandablauf voreingestellter Offset fuer Hoehenstandssensor |
| VOREINST_BYTE_FR_B | int | Im Bandablauf voreingestellter Offset fuer Hoehenstandssensor |
| VOREINST_BYTE_FL_A | int | Im Bandablauf voreingestellter Offset fuer Hoehenstandssensor |
| VOREINST_BYTE_FL_B | int | Im Bandablauf voreingestellter Offset fuer Hoehenstandssensor |
| VOREINST_BYTE_RR_A | int | Im Bandablauf voreingestellter Offset fuer Hoehenstandssensor |
| VOREINST_BYTE_RR_B | int | Im Bandablauf voreingestellter Offset fuer Hoehenstandssensor |
| VOREINST_BYTE_RL_A | int | Im Bandablauf voreingestellter Offset fuer Hoehenstandssensor |
| VOREINST_BYTE_RL_B | int | Im Bandablauf voreingestellter Offset fuer Hoehenstandssensor |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-herstelldaten-lesen"></a>
### HERSTELLDATEN_LESEN

Auslesen des Herstelldaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| DATA | binary | 22 Bytes Herstelldaten |
| _TEL_ANTWORT | binary |  |

<a id="job-herstelldaten-schreiben"></a>
### HERSTELLDATEN_SCHREIBEN

Schreiben der Herstelldaten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | zur Dokumentierung |
| BYTE2 | int | zur Dokumentierung |
| BYTE3 | int | zur Dokumentierung |
| BYTE4 | int | zur Dokumentierung |
| BYTE5 | int | zur Dokumentierung |
| BYTE6 | int | zur Dokumentierung |
| BYTE7 | int | zur Dokumentierung |
| BYTE8 | int | zur Dokumentierung |
| BYTE9 | int | zur Dokumentierung |
| BYTE10 | int | zur Dokumentierung |
| BYTE11 | int | zur Dokumentierung |
| BYTE12 | int | zur Dokumentierung |
| BYTE13 | int | zur Dokumentierung |
| BYTE14 | int | zur Dokumentierung |
| BYTE15 | int | zur Dokumentierung |
| BYTE16 | int | zur Dokumentierung |
| BYTE17 | int | zur Dokumentierung |
| BYTE18 | int | zur Dokumentierung |
| BYTE19 | int | zur Dokumentierung |
| BYTE20 | int | zur Dokumentierung |
| BYTE21 | int | zur Dokumentierung |
| BYTE22 | int | zur Dokumentierung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-diagnosemode-erhalten"></a>
### DIAGNOSEMODE_ERHALTEN

Zaehler fuer Diagnosemode zuruecksetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-diagnosemode-beenden"></a>
### DIAGNOSEMODE_BEENDEN

beendet den Diagnosemode vorzeitig

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-fahrzeug-hoehe-abgleichen"></a>
### FAHRZEUG_HOEHE_ABGLEICHEN

automatischer Hoehenabgleich

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DELTA_HOEHE_LINKS | int | mm |
| DELTA_HOEHE_RECHTS | int | mm |
| MINDEST_DELTA | int | mm |
| ACHSE | int | 1 Vorne und 2 Hinten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| OFFSET_LINKS_ALT | int | alter offset |
| OFFSET_RECHTS_ALT | int | alter offset |
| OFFSET_LINKS_NEU | int | alter offset |
| OFFSET_RECHTS_NEU | int | alter offset |
| SG_HOEHE_LINKS | int | aktuelle Fahrzeughoehe laut Fastfilter |
| SG_HOEHE_RECHTS | int | aktuelle Fahrzeughoehe laut Fastfilter |
| AUFLOESUNG_LINKS_WERT | real | Sensoraufloesung links laut Kodierdaten |
| AUFLOESUNG_RECHTS_WERT | real | Sensoraufloesung rechts laut Kodierdaten |
| ABWEICHUNG_LINKS_WERT | int | Abweichung links |
| ABWEICHUNG_RECHTS_WERT | int | Abweichung rechts |
| TEL_ABGLEICH | binary | gesendetes Abgleichtelegramm |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Auslesen des Speicherinhaltes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT | int | gewuenschtes Startsegment (0 fuer EEPROM) |
| HIGH | int | gewuenschte Startadresse high |
| MIDDLE | int | gewuenschte Startadresse midle |
| LOW | int | gewuenschte Startadresse low |
| ANZAHL | int | gewuenschte Anzahl Bytes (2-28) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| _TEL_SENDE | binary |  |
| _TEL_ANTWORT | binary |  |
| DATEN | binary | angeforderter Datenblock (max. 16 Bytes!) |

<a id="job-speicher-schreiben"></a>
### SPEICHER_SCHREIBEN

Auslesen des Speicherinhaltes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT | int | gewuenschtes Startsegment (0 fuer EEPROM) |
| HIGH | int | gewuenschte Startadresse high |
| MIDDLE | int | gewuenschte Startadresse middle |
| LOW | int | gewuenschte Startadresse low |
| WERT | int | Wert, der an die entspr. Addresse geschrieben werden soll |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| _TEL_SENDE | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-hoehe-speichern"></a>
### HOEHE_SPEICHERN

Hoehe in den leak-Bereich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-fs-lesen"></a>
### FS_LESEN

Auslesen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. table JobResult STATUS_TEXT |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_HFK | int | Fehlerhaufigkeit Bereich: 0-255 |
| F_ART_ANZ | int | Anzahl der Fehlerarten (hier immer 5) |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen (hier immer 16) |
| F_UW_SATZ | int | Anzahl der Umweltbedingungssaetze (hier immer 1) |
| F_ART1_NR | int | 1. Fehlerart |
| F_ART1_TEXT | string | 1. Fehlerart als Text |
| F_ART2_NR | int | 2. Fehlerart |
| F_ART2_TEXT | string | 2. Fehlerart als Text |
| F_ART3_NR | int | 3. Fehlerart |
| F_ART3_TEXT | string | 3. Fehlerart als Text |
| F_ART4_NR | int | 4. Fehlerart |
| F_ART4_TEXT | string | 4. Fehlerart als Text |
| F_ART5_NR | int | 5. Fehlerart |
| F_ART5_TEXT | string | 5. Fehlerart als Text |
| F_UW1_NR | int | Index der 1. Umweltbedingung |
| F_UW1_TEXT | string | Kilometerstand |
| F_UW1_WERT | long | Wert zur 1. Umweltbedingung |
| F_UW1_EINH | string | Einheit der 1. Umweltbedingung |
| F_UW2_NR | int | Index der 2. Umweltbedingung |
| F_UW2_TEXT | string | Batteriespannung |
| F_UW2_WERT | real | Wert zur 2. Umweltbedingung |
| F_UW2_EINH | string | Einheit der 2. Umweltbedingung |
| F_UW3_NR | int | Index der 3. Umweltbedingung |
| F_UW3_TEXT | string | Speicherdruck |
| F_UW3_WERT | real | Wert zur 3. Umweltbedingung |
| F_UW3_EINH | string | Einheit der 3. Umweltbedingung |
| F_UW4_NR | int | Index der 4. Umweltbedingung |
| F_UW4_TEXT | string | Balgventil VR |
| F_UW4_WERT | int | Wert zur 4. Umweltbedingung |
| F_UW4_EINH | string | Einheit der 4. Umweltbedingung |
| F_UW5_NR | int | Index der 5. Umweltbedingung |
| F_UW5_TEXT | string | Balgventil VL |
| F_UW5_WERT | int | Wert zur 5. Umweltbedingung |
| F_UW5_EINH | string | Einheit der 5. Umweltbedingung |
| F_UW6_NR | int | Index der 6. Umweltbedingung |
| F_UW6_TEXT | string | Balgventil HR |
| F_UW6_WERT | int | Wert zur 6. Umweltbedingung |
| F_UW6_EINH | string | Einheit der 6. Umweltbedingung |
| F_UW7_NR | int | Index der 6. Umweltbedingung |
| F_UW7_TEXT | string | Balgventil HL |
| F_UW7_WERT | int | Wert zur 7. Umweltbedingung |
| F_UW7_EINH | string | Einheit der 7. Umweltbedingung |
| F_UW8_NR | int | Index der 8. Umweltbedingung |
| F_UW8_TEXT | string | Speicherventil |
| F_UW8_WERT | int | Wert zur 8. Umweltbedingung |
| F_UW8_EINH | string | Einheit der 8. Umweltbedingung |
| F_UW9_NR | int | Index der 9. Umweltbedingung |
| F_UW9_TEXT | string | Ablassventil |
| F_UW9_WERT | int | Wert zur 9. Umweltbedingung |
| F_UW9_EINH | string | Einheit der 9. Umweltbedingung |
| F_UW10_NR | int | Index der 10. Umweltbedingung |
| F_UW10_TEXT | string | Kompressorschalter |
| F_UW10_WERT | int | Wert zur 10. Umweltbedingung |
| F_UW10_EINH | string | Einheit der 10. Umweltbedingung |
| F_UW11_NR | int | Index der 11. Umweltbedingung |
| F_UW11_TEXT | string | Hochdruckablassventil |
| F_UW11_WERT | int | Wert zur 11. Umweltbedingung |
| F_UW11_EINH | string | Einheit der 11. Umweltbedingung |
| F_UW12_NR | int | Index der 12. Umweltbedingung |
| F_UW12_TEXT | string | Crosslinkventil vorne |
| F_UW12_WERT | int | Wert zur 12. Umweltbedingung |
| F_UW12_EINH | string | Einheit der 12. Umweltbedingung |
| F_UW13_NR | int | Index der 13. Umweltbedingung |
| F_UW13_TEXT | string | Crosslinkventil hinten |
| F_UW13_WERT | int | Wert zur 13. Umweltbedingung |
| F_UW13_EINH | string | Einheit der 13. Umweltbedingung |
| F_UW14_NR | int | Index der 14. Umweltbedingung |
| F_UW14_TEXT | string | Kompressortemperatur |
| F_UW14_WERT | int | Wert zur 14. Umweltbedingung |
| F_UW14_EINH | string | Einheit der 14. Umweltbedingung |
| F_UW15_NR | int | Index der 15. Umweltbedingung |
| F_UW15_TEXT | string | Fahrzeuggeschwindigkeit |
| F_UW15_WERT | int | Wert zur 15. Umweltbedingung |
| F_UW15_EINH | string | Einheit der 15. Umweltbedingung |
| F_UW16_NR | int | Index der 16. Umweltbedingung |
| F_UW16_TEXT | string | Durchschnittliche Fahrzeughoehe |
| F_UW16_WERT | int | Wert zur 16. Umweltbedingung |
| F_UW16_EINH | string | Einheit der 16. Umweltbedingung |

<a id="job-io-status-schreiben-aktoren"></a>
### IO_STATUS_SCHREIBEN_AKTOREN

Ansteuern der Steuergeraeteausgaenge

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTORENLISTE | string | gewuenschte Komponenten, getrennt durch Leerzeichen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _TEL_AUFTRAG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-io-status-lesen-aktoren"></a>
### IO_STATUS_LESEN_AKTOREN

I/O Status lesen Aktoren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |
| STAT_MV_FR | int | Magnetventil vorne rechts |
| STAT_MV_FL | int | Magnetventil vorne links |
| STAT_MV_RR | int | Magnetventil hinten rechts |
| STAT_MV_RL | int | Magnetventil hinten links |
| STAT_MV_RES | int | Speicherventil |
| STAT_MV_EX | int | Ablassventil |
| STAT_C_SW | int | Kompressorschalter |
| STAT_MV_HPEX | int | Hochdruckablassventil |
| STAT_MV_CR | int | Crosslinktventil hinten |
| STAT_MV_CF | int | Crosslinkventil vorne |
| STAT_HSS_C_FRONTREAR | int | Highsideschalter Crosslinkventile vorne |
| STAT_HSS_HPEX | int | Highsideschalter Crosslinkventile hinten |
| STAT_ACCESS_STATIC | int | LED Access |
| STAT_MOTORWAY_STATIC | int | LED Motorway |
| STAT_STANDARD_STATIC | int | LED Standard |
| STAT_OFFROAD_STATIC | int | LED Offroad |
| STAT_HOLD_STATIC | int | LED Hold |
| STAT_HSS_FRONT | int | Highsideschalter vorne |
| STAT_HSS_REAR | int | Highsideschalter hinten |
| STAT_HSS_RES | int | Highsideschalter reservoir und exhaust |
| STAT_PWR_SENS1 | int | Spannungsversorgung Sensoren (vorne links und hinten rechts) |
| STAT_PWR_SENS2 | int | Spannungsversorgung Sensoren (vorne rechts und hinten links) |
| STAT_PWR_SENS3 | int | Spannungsversorgung Sensoren (Drucksensor Speicher) |
| STAT_PWR_SENS4 | int | Spannungsversorgung Sensoren (Drucksensoren Crosslinks) |

<a id="job-io-status-lesen-sensoren"></a>
### IO_STATUS_LESEN_SENSOREN

I/O Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANALOG_H_FL_WERT | int | Hoehenstand vom Sensor vorne links [mm] |
| STAT_ANALOG_H_FR_WERT | int | Hoehenstand vom Sensor vorne rechts [mm] |
| STAT_ANALOG_H_RL_WERT | int | Hoehenstand vom Sensor hinten links [mm] |
| STAT_ANALOG_H_RR_WERT | int | Hoehenstand vom Sensor hinten rechts [mm] |
| STAT_ANALOG_H_EINH | string | [mm] |
| STAT_ANALOG_P_RES_WERT | real | Speicherdruck [Bar] |
| STAT_ANALOG_P_QUSP_F_WERT | real | Druck des Quersperrdrucksensors VA [Bar] |
| STAT_ANALOG_P_QUSP_R_WERT | real | Druck des Quersperrdrucksensors HA [Bar] |
| STAT_ANALOG_P_EINH | string | [Bar] |
| STAT_ANALOG_TE_COMP_WERT | int | Komoressortemperatur [Grad Celsius] |
| STAT_ANALOG_TE_COMP_EINH | string | [Grad Celsius] |
| STAT_ANALOG_U_KL_30_WERT | real | gemessene Versorgungsspannung [Volt] |
| STAT_ANALOG_U_KL_30_EINH | string | [Volt] |
| STAT_SWITCH_ACCESS_EIN | int | Access Taster [High Aktiv] |
| STAT_SWITCH_UP_EIN | int | Tasterwippe rauf [High Aktiv] |
| STAT_SWITCH_DOWN_EIN | int | Tasterwippe runter [High Aktiv] |
| STAT_SWITCH_HOLD_EIN | int | Hold Taster [High Aktiv] |
| STAT_VALVE_STAT_VORHANDEN | binary | Ventile ueberhitzt, Kompressor ueberhitzt |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |
| _TEL_AUFTRAG | binary |  |

<a id="job-sg-status-schreiben-modi"></a>
### SG_STATUS_SCHREIBEN_MODI

Verschiedene Softwaremodi koennen aktiviert, bzw deaktiviert werden

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODUSLISTE | string | gewuenschte Modi, getrennt durch Leerzeichen |
| SET | int | SET != 0: die gewaehlten modi werden gesetzt, ansonsten zurueckgesetzt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _TEL_AUFTRAG_LESEN | binary |  |
| _TEL_ANTWORT_LESEN | binary |  |
| _TEL_AUFTRAG_SCHREIBEN | binary |  |
| _TEL_ANTWORT_SCHREIBEN | binary |  |

<a id="job-sg-status-lesen-modi"></a>
### SG_STATUS_LESEN_MODI

Verschiedene Softwaremodi koennen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DUMP_MODUS_EIN | int | Zusatzbotschaften fuer FESTUS [High Aktiv] MODUS 1 |
| STAT_BAND_MODUS_EIN | int | Aktivierungs-Sperre [High Aktiv] MODUS 1 |
| STAT_VERLADE_MODUS_EIN | int | Einstellungen fuer den Transport [High Aktiv] MODUS 1 |
| STAT_LOWTOL_MODUS_EIN | int | Aktiviert sehr enge Toleranzen MODUS 1 |
| STAT_EMV_KUNDEN_MODUS_EIN | int | fuer webaco EMV-Tests [High Aktiv] MODUS 1 |
| STAT_HANDSTEUER_MODUS_EIN | int | Freischaltung fuer I/O Status-Vorgabe [High Aktiv] MODUS 1 |
| STAT_NOPLAU_MODUS_EIN | int | fuer Laborauto Tests [High Aktiv] MODUS 1 |
| STAT_NOUSER_MODUS_EIN | int | SG reagiert nicht mehr auf Benutzeranforderungen MODUS 1 |
| STAT_ZYKEMV_MODUS_EIN | int | Modus um im EMV Test zyklische Ventilansteuerungen zu haben MODUS 2 |
| STAT_TESTMODUS_EIN | int | Modus um Lebensdauertests etc. durchzufuehren MODUS 2 |
| JOB_STATUS | string | OKAY, FEHLER |
| _TEL_AUFTRAG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-sg-status-schreiben-regler"></a>
### SG_STATUS_SCHREIBEN_REGLER

Vorgeben des Zielniveaus

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NIVEAU | string | gewuenschtes Zielniveau |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _TEL_AUFTRAG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-sg-status-lesen-regler"></a>
### SG_STATUS_LESEN_REGLER

Verschiedene Softwaremodi koennen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ACCESS_NIVEAU_EIN | int | Niveau 1 |
| STAT_MOTORWAY_NIVEAU_EIN | int | Niveau 1 |
| STAT_STANDARD_NIVEAU_EIN | int | Niveau 1 |
| STAT_OFFROAD_NIVEAU_EIN | int | Niveau 1 |
| STAT_REGELUNG_DOWN_EIN | int | Niveau 1 |
| STAT_REGELUNG_UP_EIN | int | Niveau 1 |
| JOB_STATUS | string | OKAY, FEHLER |
| _TEL_AUFTRAG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-cod-c-lesen"></a>
### COD_C_LESEN

Codierdaten lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | 21 Byte Headerdaten (0 - 20) + ETX Kennung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten |
| JOB_STATUS | string | OKAY, ERROR_.. |
| HEADER_UND_CODIER_DATEN | binary | Codierdaten |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _BIN_BUFF | binary | Ausgabe des Eingabepuffers fuer Testzwecke |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |

<a id="job-cod-c-schreiben"></a>
### COD_C_SCHREIBEN

Codierdaten schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | 21 Byte Headerdaten (0 - 20) + 25 Byte Daten + 1 Byte ETX Kennung (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| CODIER_DATEN | binary | Hex Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _BIN_BUFF | binary | Ausgabe des Eingabepuffers fuer Testzwecke |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |

<a id="job-eeprom-loehnert-lesen"></a>
### EEPROM_LOEHNERT_LESEN

EEPROM Daten lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LOEHNERT_HEADER | binary | Headerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| EEPROM_DATEN | binary | Codierdaten |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _BIN_BUFF | binary | Ausgabe des Eingabepuffers fuer Testzwecke |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| EEPROM_DATEN_ERROR | binary | Hex Auftrag an SG |

<a id="job-eeprom-loehnert-schreiben"></a>
### EEPROM_LOEHNERT_SCHREIBEN

EEPROM Daten schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LOEHNERT_HEADER | binary | Headerdaten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _BIN_BUFF | binary | Ausgabe des Eingabepuffers fuer Testzwecke |
| _TEL_AUFTRAG | binary | Hex Auftrag an SG |
| EEPROM_DATEN | binary | Codierdaten |
| EEPROM_DATEN_ERROR | binary | Hex Auftrag an SG |

<a id="job-key-seed-normal"></a>
### KEY_SEED_NORMAL

Freischaltung fuer Zugriffsebene 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-key-seed-expert"></a>
### KEY_SEED_EXPERT

Freischaltung fuer Zugriffsebene 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (7 × 2)
- [LIEFERANTEN](#table-lieferanten) (31 × 2)
- [FORTTEXTE](#table-forttexte) (61 × 2)
- [FARTMATRIX](#table-fartmatrix) (61 × 11)
- [FARTTEXTE](#table-farttexte) (12 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (2 × 19)
- [FUMWELTTEXTE](#table-fumwelttexte) (17 × 4)
- [AKTOREN](#table-aktoren) (27 × 3)
- [MODI](#table-modi) (12 × 3)
- [HOEHEN](#table-hoehen) (7 × 3)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 7 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_REJECTED |
| 0xB0 | ERROR_PARAMETER |
| 0xB1 | ERROR_FUNCTION |
| 0xFF | ERROR_NOT_ACKNOWLEDGE |
| 0xXY | ERROR_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 31 rows × 2 columns

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
| 0x43 | WABCO |
| 0xFF | unbekannter Hersteller |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 61 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Balgentil vorne links |
| 0x02 | Balgentil vorne rechts |
| 0x03 | Balgentil hinten links |
| 0x04 | Balgentil hinten rechts |
| 0x05 | Quersperrventil vorne |
| 0x06 | Quersperrventil hinten |
| 0x07 | Ablassventil |
| 0x08 | Hochdruckablassventil |
| 0x09 | Speicherventil |
| 0x0A | Kompressorrelais |
| 0x14 | Versorgung vorne |
| 0x15 | Versorgung hinten |
| 0x16 | Versorgung Quersperrventile |
| 0x17 | Versorgung Speicher |
| 0x18 | Versorgung Hochdruckablassventil |
| 0x1E | Hoehenstandssensor vorne links |
| 0x1F | Hoehenstandssensor vorne rechts |
| 0x20 | Hoehenstandssensor hinten links |
| 0x21 | Hoehenstandssensor hinten rechts |
| 0x22 | Speicherdrucksensor |
| 0x23 | Versorgung Speicherdrucksensor |
| 0x24 | Kompressortemperatursensor |
| 0x25 | VA Signal |
| 0x32 | CAN Bus |
| 0x33 | KBUS |
| 0x34 | Speicher Steuergeraet |
| 0x35 | Steuergeraet |
| 0x36 | Codierdaten |
| 0x37 | Abgleichfehler |
| 0x64 | Verschraenkungsplausibilitaet |
| 0x65 | Kein/zu langsames Verfahren (ganzes Fzg) wenn heben angefordert |
| 0x66 | Kein/zu langsames Verfahren (ganzes Fzg) wenn absenken angefordert |
| 0x67 | Zu viel Energie fuer eine Regelung benoetigt: Vorderachse |
| 0x68 | Zu viel Energie fuer eine Regelung benoetigt: hinten links |
| 0x69 | Zu viel Energie fuer eine Regelung benoetigt: hinten rechts |
| 0x6A | Zu viel Energie um die Zielhoehe zu erreichen: Vorderachse |
| 0x6B | Zu viel Energie um die Zielhoehe zu erreichen: hinten links |
| 0x6C | Zu viel Energie um die Zielhoehe zu erreichen: hinten rechts |
| 0x6D | Hoehenaenderung in die falsche Richtung (mind. ein Rad), wenn heben angefordert |
| 0x6E | Hoehenaenderung in die falsche Richtung (mind. ein Rad), wenn absenken angefordert |
| 0x6F | Kompressortemperatur steigt, wenn Kompressor nicht angesteuert wird |
| 0x70 | Kompressortemperatur steigt nicht, wenn Kompressor angesteuert wird |
| 0x71 | Kompressortemperatur faellt nicht, wenn Kompressor nicht angesteuert wird |
| 0x72 | Speicherdruck steigt, wenn Speicher nicht aktiv ist |
| 0x73 | Speicherdruck sinkt, wenn Speicher nicht aktiv ist |
| 0x74 | Speicherdruck bleibt konstant, wenn Speicherfuellen angefordert wird |
| 0x75 | Speicherdruck sinkt anfaenglich, wenn Speicherfuellen angefordert wird |
| 0x76 | Speicherdruck sinkt, wenn Speicherfuellen angefordert wird |
| 0x77 | Speicherdruck bleibt konstant, wenn Entlueftung angefordert wird |
| 0x78 | Speicherdruck steigt, wenn Entlueftung angefordert wird |
| 0x79 | Speicherdruck bleibt konstant, wenn aus dem Speicher nach oben verfahren wird |
| 0x7A | Speicherdruck steigt, wenn aus dem Speicher nach oben verfahren wird |
| 0x7B | Quersperrplausibilitaet Vorderachse |
| 0x7C | Quersperrplausibilitaet Hinterachse |
| 0x7D | links vorne bewegt sich zu langsam |
| 0x7E | rechts vorne bewegt sich zu langsam |
| 0x7F | Aktivitaetsplausibilitaet vorne links |
| 0x80 | Aktivitaetsplausibilitaet vorne rechts |
| 0x81 | Aktivitaetsplausibilitaet hinten links |
| 0x82 | Aktivitaetsplausibilitaet hinten rechts |
| 0xFF | unbekannter Fehlerort |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 61 rows × 11 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x02 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x03 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x04 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x05 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x06 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x07 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x08 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x09 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x0A | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x14 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x15 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x16 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x17 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x18 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x1E | 0x00 | 0x0A | 0x00 | 0x0B | 0x00 | 0x0C | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x1F | 0x00 | 0x0A | 0x00 | 0x0B | 0x00 | 0x0C | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x20 | 0x00 | 0x0A | 0x00 | 0x0B | 0x00 | 0x0C | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x21 | 0x00 | 0x0A | 0x00 | 0x0B | 0x00 | 0x0C | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x22 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x23 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x24 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x25 | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x32 | 0x00 | 0xFE | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x33 | 0x00 | 0xFE | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x34 | 0x00 | 0xFE | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x35 | 0x00 | 0xFE | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x36 | 0x00 | 0xFE | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x37 | 0x00 | 0xFE | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x07 |
| 0x64 | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x65 | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x66 | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x67 | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x68 | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x69 | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x6A | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x6B | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x6C | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x6D | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x6E | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x6F | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x70 | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x71 | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x72 | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x73 | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x74 | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x75 | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x76 | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x77 | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x78 | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x79 | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x7A | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x7B | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x7C | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x7D | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x7E | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x7F | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x80 | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x81 | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0x82 | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0x04 | 0x00 | 0x07 |
| 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 12 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | Kurzschluss gegen U-Batt |
| 0x02 | Kurzschluss gegen Masse |
| 0x03 | Leitungsunterbrechung |
| 0x04 | Plausibilitaetsfehler |
| 0x07 | Fehler momentan vorhanden |
| 0x08 | sporadischer Fehler |
| 0x0A | Hardwarefehler |
| 0x0B | Fehler Sensorversorgung |
| 0x0C | Eingang Floating Plausibilitaetsfehler |
| 0xFE | allg. Fehler |
| 0xFF | unbekannte Fehlerart |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 2 rows × 19 columns

| ORT | UW_ANZ | UW_SATZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR | UW15_NR | UW16_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | 16 | 1 | 0x01 | 0x02 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0A | 0x0B | 0x0C | 0x0D | 0x0E | 0x0F | 0x10 |
| 0xXY | 0 | 0 | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 17 rows × 4 columns

| UWNR | UWTEXT | UW_EINH | MASK |
| --- | --- | --- | --- |
| 0x01 | Kilometerstand | km | -- |
| 0x02 | Batteriespannung | Volt | -- |
| 0x03 | Speicherdruck | Bar | -- |
| 0x04 | Balgventil vorne rechts | 0/1 | 0x01 |
| 0x05 | Balgventil vorne links | 0/1 | 0x02 |
| 0x06 | Balgventil hinten rechts | 0/1 | 0x04 |
| 0x07 | Balgventil hinten links | 0/1 | 0x08 |
| 0x08 | Speicherventil | 0/1 | 0x10 |
| 0x09 | Ablassventil | 0/1 | 0x20 |
| 0x0A | Kompressorschalter | 0/1 | 0x40 |
| 0x0B | Hochdruckablassventil | 0/1 | 0x01 |
| 0x0C | Crosslinkventil hinten | 0/1 | 0x04 |
| 0x0D | Crosslinkventil vorne | 0/1 | 0x08 |
| 0x0E | Kompressortemperatur | Grad C | -- |
| 0x0F | Fahrzeuggeschwindigkeit | km/h | -- |
| 0x10 | durchschn. Fahrzeughoehe | mm | -- |
| 0xXY | unbekannte Umweltbedingung | XY | 1 |

<a id="table-aktoren"></a>
### AKTOREN

Dimensions: 27 rows × 3 columns

| AKTOREN | BYTE | BITWERT |
| --- | --- | --- |
| MV_FR | 0 | 0x01 |
| MV_FL | 0 | 0x02 |
| MV_RR | 0 | 0x04 |
| MV_RL | 0 | 0x08 |
| MV_RES | 0 | 0x10 |
| MV_EX | 0 | 0x20 |
| C_SW | 0 | 0x40 |
| MV_HPEX | 1 | 0x01 |
| MV_CR | 1 | 0x04 |
| MV_CF | 1 | 0x08 |
| HSS_C_FRONTREAR | 1 | 0x40 |
| HSS_HPEX | 1 | 0x80 |
| ACCESS_STATIC | 2 | 0x02 |
| MOTORWAY_STATIC | 2 | 0x08 |
| STANDARD_STATIC | 2 | 0x20 |
| OFFROAD_STATIC | 2 | 0x80 |
| HOLD_STATIC | 3 | 0x02 |
| HSS_FRONT | 4 | 0x01 |
| HSS_REAR | 4 | 0x02 |
| HSS_RES | 4 | 0x04 |
| UPULL | 4 | 0x08 |
| PWR_SENS1 | 4 | 0x10 |
| PWR_SENS2 | 4 | 0x20 |
| PWR_SENS3 | 4 | 0x40 |
| PWR_SENS4 | 4 | 0x80 |
| FULL_ACCESS | 5 | 0x80 |
| XXX | Y | Z |

<a id="table-modi"></a>
### MODI

Dimensions: 12 rows × 3 columns

| MODI | BYTE | BITWERT |
| --- | --- | --- |
| DUMPMODUS | 0 | 0x01 |
| BANDMODUS | 0 | 0x02 |
| VERLADEMODUS | 0 | 0x04 |
| LOWTOLMODUS | 0 | 0x08 |
| EMVMODUS | 0 | 0x10 |
| HANDSTEUERMODUS | 0 | 0x20 |
| NOPLAUSMODUS | 0 | 0x40 |
| NOUSERMODUS | 0 | 0x80 |
| ZYKEMVMODUS | 1 | 0x01 |
| TESTMODUS | 1 | 0x02 |
| ALLE | 99 | 0xFF |
| XXX | Y | Z |

<a id="table-hoehen"></a>
### HOEHEN

Dimensions: 7 rows × 3 columns

| HOEHEN | BYTE | BITWERT |
| --- | --- | --- |
| ACCESS | 0 | 0x02 |
| MOTORWAY | 0 | 0x04 |
| STANDARD | 0 | 0x08 |
| OFFROAD | 0 | 0x10 |
| REG_DOWN | 0 | 0x40 |
| REG_UP | 0 | 0x80 |
| XXX | Y | Z |
