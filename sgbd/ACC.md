# ACC.prg

- Jobs: [25](#jobs)
- Tables: [9](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Radar-Tempomat ACC |
| ORIGIN | BMW EE-232 Dr. Sauer |
| REVISION | 2.02 |
| AUTHOR | BMW TI-433 Huber, BMW EE-232 Dr. Sauer |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information bzgl. SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung / Kommunikationsparameter fuer ACC automatischer Aufruf beim ersten Zugriff auf die SGBD
- [START_MODUS](#job-start-modus) - Starten eines Diagnose-Modus fuer ACC
- [STOP_MODUS](#job-stop-modus) - Stop des aktuellen Diagnose-Modus fuer ACC
- [IDENT](#job-ident) - Ident-Daten fuer ACC Modus: Default
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [OTL_DATEN_RESET](#job-otl-daten-reset) - Ruecksetzen der OTL-Daten
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen
- [CODIERDATEN_LESEN](#job-codierdaten-lesen) - Lesen der Codierdaten
- [STATUS_RADARZIEL](#job-status-radarziel) - Radarziel auslesen Modus: Default
- [STATUS_RADARZIEL_ONLINE](#job-status-radarziel-online) - Radarziel waehrend der Fahrt auslesen Modus: Default
- [STATUS_JUSTAGEDATEN](#job-status-justagedaten) - Justagedaten lesen Modus: ECUAdjustmentMode (ECU)
- [STATUS_JUSTAGEDATEN_NEU](#job-status-justagedaten-neu) - Justagedaten lesen, auszuwertende Spektrallinie frei waehlbar Modus: ECUAdjustmentMode (ECU)
- [SPU_DYNAMISCH_LESEN](#job-spu-dynamisch-lesen) - Lesen von Dejustage und Verschmutzungsinformationen
- [SPU_SCHREIBEN](#job-spu-schreiben) - Dynamische Daten SPU schreiben Modi: Default
- [SPU_DYN_DATEN_RESET](#job-spu-dyn-daten-reset) - Reset der Dynamischen Daten SPU Modi: Default
- [SCHALTER_EOL_EIN](#job-schalter-eol-ein) - Sonderfunktionen fuer Bandende aktivieren Modi: Default
- [SCHALTER_EOL_AUS](#job-schalter-eol-aus) - Sonderfunktionen fuer Rollenpruefstand deaktivieren Modi: Default
- [RPU_DYNAMISCH_LESEN](#job-rpu-dynamisch-lesen) - Dynamische RPU-Daten lesen
- [OPERATION_CONSTRAINTS_LESEN](#job-operation-constraints-lesen) - Operation-Constraints lesen
- [SW_RESET](#job-sw-reset) - Ausloesen eines SW_Resets
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Lesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Schreiben des Pruefstempels
- [JUSTAGEKENNLINIE_LESEN](#job-justagekennlinie-lesen) - Auslesen der Steilheiten der vertikalen und horizontalen Justagekennlinien im linearen Bereich Modus: Default
- [SUCHE_PROGRAMMBLOCKFEHLER](#job-suche-programmblockfehler) - durchsucht den Historyspeicher nach dem Programmblockfehler RB-Codes: 0x3002, 0x3003, 0x3081 oder 0x3084

<a id="job-info"></a>
### INFO

Information bzgl. SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ECU | string | Steuergeraet im Klartext |
| ORIGIN | string | Steuergeraete-Verantwortlicher |
| REVISION | string | Versions-Nummer |
| AUTHOR | string | Namen aller Autoren |
| COMMENT | string | wichtige Hinweise |
| SPRACHE | string | deutsch / english |

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung / Kommunikationsparameter fuer ACC automatischer Aufruf beim ersten Zugriff auf die SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-start-modus"></a>
### START_MODUS

Starten eines Diagnose-Modus fuer ACC

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODUS | string | gewuenschter Diagnose-Modus table DiagModus MODUS MODUS_TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-modus"></a>
### STOP_MODUS

Stop des aktuellen Diagnose-Modus fuer ACC

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer ACC Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Text table Lieferanten LIEF_TEXT |
| ID_SW_NR | int | Softwarenummer |
| ID_SERIEN_NR | string | Seriennummer |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-otl-daten-reset"></a>
### OTL_DATEN_RESET

Ruecksetzen der OTL-Daten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | int | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_HFK | int | Fehlerhaeufigkeit Bereich: 0 - 31 |
| F_ART_ANZ | int | Anzahl der Fehlerarten Bereich: immer 3 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Bereich: immer 7 |
| F_LZ | int | Logistikzaehler Bereich: 0 - 40 |
| F_UW_SATZ | int | Anzahl der Umweltsaetze Bereich: immer 1 |
| F_ART1_NR | int | 1. Fehlerart Bereich: |
| F_ART1_TEXT | string | 1. Fehlerart als Text table FArtTexte ARTTEXT |
| F_ART2_NR | int | 2. Fehlerart Bereich: |
| F_ART2_TEXT | string | 2. Fehlerart als Text table FArtTexte ARTTEXT |
| F_ART3_NR | int | 3. Fehlerart Bereich: |
| F_ART3_TEXT | string | 3. Fehlerart als Text table FArtTexte ARTTEXT |
| F_UW1_NR | int | Index der 1. Umweltbedingung |
| F_UW1_TEXT | string | Kilometerstand |
| F_UW1_WERT | long | Wert der 1. Umweltbedingung |
| F_UW1_EINH | string | Einheit |
| F_UW2_NR | int | Index der 2. Umweltbedingung |
| F_UW2_TEXT | string | Betriebsstundenzaehler |
| F_UW2_WERT | real | Wert der 2. Umweltbedingung |
| F_UW2_EINH | string | Einheit |
| F_UW3_NR | int | Index der 3. Umweltbedingung |
| F_UW3_TEXT | string | Aussentemperatur |
| F_UW3_WERT | real | Wert der 3. Umweltbedingung |
| F_UW3_EINH | string | Einheit |
| F_UW4_NR | int | Index der 4. Umweltbedingung |
| F_UW4_TEXT | string | SCU-Innentemperatur |
| F_UW4_WERT | real | Wert der 4. Umweltbedingung |
| F_UW4_EINH | string | Einheit |
| F_UW5_NR | int | Index der 5. Umweltbedingung |
| F_UW5_TEXT | string | Betriebsspannung |
| F_UW5_WERT | int | Wert der 5. Umweltbedingung |
| F_UW5_EINH | string | Einheit |
| F_UW6_NR | int | Index der 6. Umweltbedingung |
| F_UW6_TEXT | string | Dejustagegrad des Sensors |
| F_UW6_WERT | int | Wert der 6. Umweltbedingung |
| F_UW6_EINH | string | Einheit |
| F_UW7_NR | int | Index der 7. Umweltbedingung |
| F_UW7_TEXT | string | Linsenheizung aktiv / nicht aktiv |
| F_UW7_WERT | int | Wert der 7. Umweltbedingung |
| F_UW7_EINH | string | Einheit |
| F_UW8_NR | int | Index der 8. Umweltbedingung |
| F_UW8_TEXT | string | Linse (nicht) verschmutzt |
| F_UW8_WERT | int | Wert der 8. Umweltbedingung |
| F_UW8_EINH | string | Einheit |
| F_UW9_NR | int | Index der 9. Umweltbedingung |
| F_UW9_TEXT | string | Abschaltung durch SPU (CANSTOP) aktiv / inaktiv |
| F_UW9_WERT | int | Wert der 9. Umweltbedingung |
| F_UW9_EINH | string | Einheit |
| F_UW10_NR | int | Index der 10. Umweltbedingung |
| F_UW10_TEXT | string | oberer / unterer Flash-Programm-Block |
| F_UW10_WERT | int | Wert der 10. Umweltbedingung |
| F_UW10_EINH | string | Einheit |
| _TEL_ANTWORT0 | binary | 0. Hex-Antwort von SG |
| _TEL_ANTWORT1 | binary | 1. Hex-Antwort von SG |

<a id="job-codierdaten-lesen"></a>
### CODIERDATEN_LESEN

Lesen der Codierdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| CODIER_DATA | binary | Codierdaten |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-radarziel"></a>
### STATUS_RADARZIEL

Radarziel auslesen Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| D_MIN | int | 0...150 m |
| D_MAX | int | 0...150 m |
| V_MIN | int | -60 m/s ... 60 m/s |
| V_MAX | int | -60 m/s ... 60 m/s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ABSTAND_1_WERT | real | Radarobjekt Nr. 1: Abstand Bereich: 0 bis 512 [m] |
| STAT_VR_1_WERT | real | Radarobjekt Nr. 1: VR Bereich: -256 bis +256 [m/s] |
| STAT_QV_1_WERT | real | Radarobjekt Nr. 1: Querversatz Bereich: -128 bis +128 [m] |
| STAT_WIGUE_1_WERT | real | Radarobjekt Nr. 1: Winkelguete Bereich: 0 bis +2 [] |
| STAT_PLAUS_1_WERT | real | Radarobjekt Nr. 1: Plausibilitaet Bereich: 0 bis 128 [] |
| STAT_AMPL_1_WERT | real | Radarobjekt Nr. 1: Amplitude Bereich: 0 bis 2 [] |
| STAT_ABSTAND_2_WERT | real | Radarobjekt Nr. 2: Abstand Bereich: 0 bis 512 [m] |
| STAT_VR_2_WERT | real | Radarobjekt Nr. 2: VR Bereich: -256 bis +256 [m/s] |
| STAT_QV_2_WERT | real | Radarobjekt Nr. 2: Querversatz Bereich: -128 bis +128 [m] |
| STAT_WIGUE_2_WERT | real | Radarobjekt Nr. 2: Winkelguete Bereich: 0 bis +2 [] |
| STAT_PLAUS_2_WERT | real | Radarobjekt Nr. 2: Plausibilitaet Bereich: 0 bis 128 [] |
| STAT_AMPL_2_WERT | real | Radarobjekt Nr. 2: Amplitude Bereich: 0 bis 2 [] |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-radarziel-online"></a>
### STATUS_RADARZIEL_ONLINE

Radarziel waehrend der Fahrt auslesen Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ABSTAND_1_WERT | real | Radarobjekt Nr. 1: Abstand Bereich: ? bis ? [?] |
| STAT_VR_1_WERT | real | Radarobjekt Nr. 1: VR Bereich: ? bis ? [?] |
| STAT_AR_1_WERT | real | Radarobjekt Nr. 1: AR Bereich: ? bis ? [?] |
| STAT_QV_1_WERT | real | Radarobjekt Nr. 1: Querversatz Bereich: ? bis ? [?] |
| STAT_KV_1_WERT | real | Radarobjekt Nr. 1: Kursversatz Bereich: ? bis ? [?] |
| STAT_PLAUS_1_WERT | real | Radarobjekt Nr. 1: Plausibilitaet Bereich: ? bis ? [?] |
| STAT_ABSTAND_2_WERT | real | Radarobjekt Nr. 2: Abstand Bereich: ? bis ? [?] |
| STAT_VR_2_WERT | real | Radarobjekt Nr. 2: VR Bereich: ? bis ? [?] |
| STAT_AR_2_WERT | real | Radarobjekt Nr. 2: AR Bereich: ? bis ? [?] |
| STAT_QV_2_WERT | real | Radarobjekt Nr. 2: Querversatz Bereich: ? bis ? [?] |
| STAT_KV_2_WERT | real | Radarobjekt Nr. 2: Kursversatz Bereich: ? bis ? [?] |
| STAT_PLAUS_2_WERT | real | Radarobjekt Nr. 2: Plausibilitaet Bereich: ? bis ? [?] |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-justagedaten"></a>
### STATUS_JUSTAGEDATEN

Justagedaten lesen Modus: ECUAdjustmentMode (ECU)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AMPLITUDE_L_WERT | real | Amplitude Links ? Bereich: ? bis ? [?] |
| STAT_AMPLITUDE_M_WERT | real | Amplitude Mitte ? Bereich: ? bis ? [?] |
| STAT_AMPLITUDE_R_WERT | real | Amplitude Rechts ? Bereich: ? bis ? [?] |
| STAT_PLAUS_AMPLITUDE_WERT | real | Plausibilitaet Amplitude ? Bereich: ? bis ? [?] |
| STAT_PLAUS_DISTANZ_WERT | real | Plausibilitaet Distanz ? Bereich: ? bis ? [?] |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-justagedaten-neu"></a>
### STATUS_JUSTAGEDATEN_NEU

Justagedaten lesen, auszuwertende Spektrallinie frei waehlbar Modus: ECUAdjustmentMode (ECU)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPEKTRALLINIE | int | Nummer der auszuwertenden Spektrallinie |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AMPLITUDE_L_WERT | real | Amplitude Links ? Bereich: ? bis ? [?] |
| STAT_AMPLITUDE_M_WERT | real | Amplitude Mitte ? Bereich: ? bis ? [?] |
| STAT_AMPLITUDE_R_WERT | real | Amplitude Rechts ? Bereich: ? bis ? [?] |
| STAT_PLAUS_AMPLITUDE_WERT | real | Plausibilitaet Amplitude ? Bereich: ? bis ? [?] |
| STAT_PLAUS_DISTANZ_WERT | real | Plausibilitaet Distanz ? Bereich: ? bis ? [?] |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-spu-dynamisch-lesen"></a>
### SPU_DYNAMISCH_LESEN

Lesen von Dejustage und Verschmutzungsinformationen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DEJUHOR_WINK | real | horizontaler Dejustagewinkel in Grad |
| DEJUHOR_PLAUS | real | Plausibilitaet des horizontalen Dejustagewinkels |
| DEJUVER_WINK | real | vertikaler Dejustagewinkel in Grad |
| DEJUVER_PLAUS | real | Plausibilitaet des vertikalen Dejustagewinkels |
| STATUS_VERSCHMUTZ | real | Status der Verschmutzungserkennung |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-spu-schreiben"></a>
### SPU_SCHREIBEN

Dynamische Daten SPU schreiben Modi: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DEJUHOR_WINK | int | normierter horizontaler Dejustagewinkel |
| DEJUHOR_PLAUS | int | Plausibilitaet des horizontalen Dejustagewinkels |
| DEJUVER_WINK | int | normierter vertikaler Dejustagewinkel |
| DEJUVER_PLAUS | int | Plausibilitaet des vertikalen Dejustagewinkels |
| STATUS_VERSCHMUTZ | int | Status der Verschmutzungserkennung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-spu-dyn-daten-reset"></a>
### SPU_DYN_DATEN_RESET

Reset der Dynamischen Daten SPU Modi: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-schalter-eol-ein"></a>
### SCHALTER_EOL_EIN

Sonderfunktionen fuer Bandende aktivieren Modi: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-schalter-eol-aus"></a>
### SCHALTER_EOL_AUS

Sonderfunktionen fuer Rollenpruefstand deaktivieren Modi: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-rpu-dynamisch-lesen"></a>
### RPU_DYNAMISCH_LESEN

Dynamische RPU-Daten lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BETRSTD_ZAEHLER | real | Betriebsstundenzaehler |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-operation-constraints-lesen"></a>
### OPERATION_CONSTRAINTS_LESEN

Operation-Constraints lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ACTIVATION_CONSTRAINT1 | string |  |
| ACTIVATION_CONSTRAINT2 | string |  |
| ACTIVATION_CONSTRAINT3 | string |  |
| ACTIVATION_CONSTRAINT4 | string |  |
| ACTIVATION_CONSTRAINT5 | string |  |
| OPERATION_CONSTRAINT1 | string |  |
| OPERATION_CONSTRAINT2 | string |  |
| OPERATION_CONSTRAINT3 | string |  |
| OPERATION_CONSTRAINT4 | string |  |
| OPERATION_CONSTRAINT5 | string |  |
| OPERATION_CONSTRAINT6 | string |  |
| SWITCH_OFF_CONSTRAINT1 | string |  |
| SWITCH_OFF_CONSTRAINT2 | string |  |
| SWITCH_OFF_CONSTRAINT3 | string |  |
| SWITCH_OFF_CONSTRAINT4 | string |  |
| SWITCH_OFF_CONSTRAINT5 | string |  |
| SWITCH_OFF_CONSTRAINT6 | string |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sw-reset"></a>
### SW_RESET

Ausloesen eines SW_Resets

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Lesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PRUEFSTEMP_WERT1 | int | Pruefstempel Byte1 |
| PRUEFSTEMP_WERT2 | int | Pruefstempel Byte2 |
| PRUEFSTEMP_WERT3 | int | Pruefstempel Byte3 |
| FG_ZIFFERN | string | die letzten vier Stellen der Fahrgestellnummer |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Schreiben des Pruefstempels

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PRUEFSTEMP_WERT1 | string | Pruefstempel Byte1 |
| PRUEFSTEMP_WERT2 | string | Pruefstempel Byte2 |
| PRUEFSTEMP_WERT3 | string | Pruefstempel Byte3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-justagekennlinie-lesen"></a>
### JUSTAGEKENNLINIE_LESEN

Auslesen der Steilheiten der vertikalen und horizontalen Justagekennlinien im linearen Bereich Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| JUSKENN_VER | real | Steilheit der vertikalen Justagekennlinie im linearen Bereich Einheit: 1/Grad Wertebereich: 0.0 ... 6.0 |
| JUSKENN_HOR | real | Steilheit der horizontalen Justagekennlinie im linearen Bereich Einheit: 1/Grad Wertebereich: 0.0 ... 6.0 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-suche-programmblockfehler"></a>
### SUCHE_PROGRAMMBLOCKFEHLER

durchsucht den Historyspeicher nach dem Programmblockfehler RB-Codes: 0x3002, 0x3003, 0x3081 oder 0x3084

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SUCH_ERGEBNIS | int | 0: kein Fehler / 1: Fehler gefunden |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [DIAGMODUS](#table-diagmodus) (5 × 3)
- [JOBRESULT](#table-jobresult) (34 × 2)
- [LIEFERANTEN](#table-lieferanten) (33 × 2)
- [FORTTEXTE](#table-forttexte) (31 × 2)
- [FARTTEXTE](#table-farttexte) (10 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (11 × 3)
- [ACTCON](#table-actcon) (6 × 2)
- [OPCON](#table-opcon) (7 × 2)
- [SWOFFCON](#table-swoffcon) (7 × 2)

<a id="table-diagmodus"></a>
### DIAGMODUS

Dimensions: 5 rows × 3 columns

| NR | MODUS | MODUS_TEXT |
| --- | --- | --- |
| 0x82 | PT | Periodic-Transmission |
| 0x87 | ECU | ECUAdjustmentMode |
| 0xFA | RB | RB-Werk |
| 0x86 | E | Entwicklung |
| 0xXY | -- | unbekannter Diagnose-Modus |

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 34 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | OKAY |
| 0x00 | ERROR_ECU_RESERVED_BY_DOCUMENT |
| 0x10 | ERROR_ECU_GENERAL_REJECT |
| 0x11 | ERROR_ECU_SERVICE_NOT_SUPPORTED |
| 0x12 | ERROR_ECU_SUBFUNCTION_NOT_SUPPORTED_INVALID_FORMAT |
| 0x21 | ERROR_ECU_BUSY_REPEAT_REQUEST |
| 0x22 | ERROR_ECU_CONDITIONS_NOT_CORRECT_OR_REQUEST_SEQUENCE_ERROR |
| 0x23 | ERROR_ECU_ROUTINE_NOT_COMPLETE |
| 0x31 | ERROR_ECU_REQUEST_OUT_OF_RANGE |
| 0x33 | ERROR_ECU_SECURITY_ACCESS_DENIED_SECURITY_ACCESS_REQUESTED |
| 0x35 | ERROR_ECU_INVALID_KEY |
| 0x36 | ERROR_ECU_EXCEED_NUMBER_OF_ATTEMPTS |
| 0x37 | ERROR_ECU_REQUIRED_TIME_DELAY_NOT_EXPIRED |
| 0x40 | ERROR_ECU_DOWNLOAD_NOT_ACCEPTED |
| 0x41 | ERROR_ECU_IMPROPER_DOWNLOAD_TYPE |
| 0x42 | ERROR_ECU_CANNOT_DOWNLOAD_TO_SPECIFIED_ADDRESS |
| 0x43 | ERROR_ECU_CANNOT_DOWNLOAD_NUMBER_OF_BYTES_REQUESTED |
| 0x50 | ERROR_ECU_UPLOAD_NOT_ACCEPTED |
| 0x51 | ERROR_ECU_IMPROPER_UPLOAD_TYPE |
| 0x52 | ERROR_ECU_CANNOT_UPLOAD_FROM_SPECIFIED_ADDRESS |
| 0x53 | ERROR_ECU_CANNOT_UPLOAD_NUMBER_OF_BYTES_REQUESTED |
| 0x71 | ERROR_ECU_TRANSFER_SUSPENDED |
| 0x72 | ERROR_ECU_TRANSFER_ABORTED |
| 0x74 | ERROR_ECU_ILLEGAL_ADDRESS_IN_BLOCK_TRANSFER |
| 0x75 | ERROR_ECU_ILLEGAL_BYTE_COUNT_IN_BLOCK_TRANSFER |
| 0x76 | ERROR_ECU_ILLEGAL_BLOCK_TRANSFER_TYPE |
| 0x77 | ERROR_ECU_BLOCKTRANSFER_DATA_CHECKSUM_ERROR |
| 0x78 | ERROR_ECU_REQ_CORRECTLY_RCVD_RSP_PENDING |
| 0x79 | ERROR_ECU_INCORRECT_BYTE_COUNT_DURING_BLOCK_TRANSFER |
| 0x80 | ERROR_ECU_SERVICE_NOT_SUPPORTED_IN_ACTIVE_DIGNOSTICMODE |
| 0xF9 | ERROR_ECU_VEHICLE_MANUFACTURER_SPECIFIC |
| 0xFE | ERROR_ECU_SYSTEM_SUPPLIER_SPECIFIC |
| 0xFF | ERROR_ECU_RESERVED_BY_DOCUMENT |
| 0xXY | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 33 rows × 2 columns

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
| 0xXY | unbekannter Hersteller |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 31 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x5D0C | Steuergeraetefehler |
| 0x5D0D | Steuergeraetefehler: Botschaftsplausibilitaet |
| 0x5D0E | Betriebsspannung |
| 0x5D0F | Fehler Linsenheizung |
| 0x5D10 | Plausibilitaet Applikationsparameter |
| 0x5D11 | HW-Fehler CAN |
| 0x5D12 | Abweichender CAN-Stand |
| 0x5D13 | Sensor blind |
| 0x5D14 | Sensor dejustiert |
| 0x5D15 | Fehler Bremspedal |
| 0x5D16 | ACC-relevanter Fehler Motorsteuerung |
| 0x5D17 | ACC-relevanter Fehler DSC |
| 0x5D18 | ACC-relevanter Fehler DSC-Gierrate |
| 0x5D19 | ACC-relevanter Fehler ECD |
| 0x5D1A | ACC-relevanter Fehler Kombi |
| 0x5D1B | ACC-relevanter Fehler EGS |
| 0x5D1C | CAN-Timeout Motorsteuerung |
| 0x5D1D | CAN-Timeout DSC |
| 0x5D1E | CAN-Timeout Kombi |
| 0x5D1F | CAN-Timeout EGS |
| 0x5D20 | Fehler CAN-Daten Motorsteuerung |
| 0x5D21 | Fehler CAN-Daten DSC |
| 0x5D22 | Fehler CAN-Daten Kombi |
| 0x5D23 | Fehler CAN-Daten EGS |
| 0x5D24 | Fehler CAN-Daten DSC-Gierrate |
| 0x5D25 | Temperaturabschaltung SCU |
| 0x5D26 | Fehler Programmblock 1 |
| 0x5D27 | ACC Sicherheitsabschaltung Bremsueberhitzung |
| 0x5D28 | Fehler Umsetzung Beschleunigungssollwert im Antriebsfall |
| 0x5D29 | Fehler Umsetzung Beschleunigungssollwert im Bremsfall |
| 0xXY | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 10 rows × 2 columns

| ART | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | Wert oberhalb Schwelle |
| 0x02 | Wert unterhalb Schwelle |
| 0x04 | kein Signal |
| 0x08 | unplausibles Signal |
| 0x10 | Testbedingung erfuellt |
| 0x20 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x40 | Fehler momentan vorhanden, aber noch nicht gespeichert (Entprellphase) |
| 0x60 | Fehler momentan vorhanden und bereits gespeichert |
| 0xXY | unbekannte Fehlerart |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 11 rows × 3 columns

| UWNR | UWTEXT | UW_EINH |
| --- | --- | --- |
| 0x01 | Kilometerstand | km |
| 0x02 | Betriebsstundenzaehler | Stunden |
| 0x03 | Aussentemperatur | Grad C |
| 0x04 | SCU-Innentemperatur | Grad C |
| 0x05 | Betriebsspannung | Volt |
| 0x06 | Dejustagegrad des Sensors | 0-n |
| 0x07 | Linsenheizung | 0/1 |
| 0x08 | Linse | 0/1 |
| 0x09 | Abschaltung durch SPU (CANSTOP) | 0/1 |
| 0x0A | verwendeter Flash-Block: | 0/1 |
| 0xXY | unbekannte Umweltbedingung | ? |

<a id="table-actcon"></a>
### ACTCON

Dimensions: 6 rows × 2 columns

| CODE | TEXT |
| --- | --- |
| 0x01 | Motormindestdrehzahl unterschritten |
| 0x02 | Mindestaktivierungsgeschwindigkeit unterschritten |
| 0x04 | mind. eine der Operation Constraints verletzt |
| 0x08 | mind. eine der Switch Off Constraints verletzt |
| 0x10 | externe Aktivierungsbedingung verletzt |
| 0xXY |  |

<a id="table-opcon"></a>
### OPCON

Dimensions: 7 rows × 2 columns

| CODE | TEXT |
| --- | --- |
| 0x01 | Handbremse aktiv |
| 0x02 | Niedriger Reibwert erkannt |
| 0x04 | Mindestfunktionsgeschwindigkeit unterschritten |
| 0x08 | Brake Only Abschaltreaktion |
| 0x10 | externe Funktionsbedingung verletzt |
| 0x20 | Linse verschmutzt |
| 0xXY |  |

<a id="table-swoffcon"></a>
### SWOFFCON

Dimensions: 7 rows × 2 columns

| CODE | TEXT |
| --- | --- |
| 0x01 | Hauptschalter nicht aktiv |
| 0x02 | Abschaltgrenzgeschwindigkeit unterschritten |
| 0x04 | Bremspedal betaetigt |
| 0x08 | kein gueltiger Vorwaertsgang |
| 0x10 | Harte Abschaltreaktion |
| 0x20 | externe Abschaltbedingung |
| 0xXY |  |
