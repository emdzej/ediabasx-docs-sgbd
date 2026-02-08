# ABS5.prg

- Jobs: [31](#jobs)
- Tables: [11](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Antiblockiersytem 5 E31,E32,E34,E38 |
| ORIGIN | BMW TP-421 Hirsch |
| REVISION | 2.08 |
| AUTHOR | BMW TP-421 Hirsch |
| COMMENT | Keine Diagnose bei v &gt; 6km/h |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer ABS5
- [IDENT](#job-ident) - Ident-Daten fuer ABS5
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen fuer ABS5 High-Konzept nach Lastenheft Codierung/Diagnose
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen fuer ABS5
- [STATUS_IO_LESEN](#job-status-io-lesen) - Status Eingaenge ABS5
- [DOWNLOAD_STELLGLIED](#job-download-stellglied) - Stellglied ansteuern ABS5
- [DOWNLOAD_D4_STELLGLIED](#job-download-d4-stellglied) - Stellglied ansteuern ABS5
- [DOWNLOAD_I_O_DIAGNOSE](#job-download-i-o-diagnose) - I/O-Diagnose ABS5
- [DOWNLOAD_FUEHLER_EINZELN](#job-download-fuehler-einzeln) - Ansprechschwelle u. Impulsrad ABS5
- [DOWNLOAD_STATISCH](#job-download-statisch) - Statischer Test der Komponenten ABS5
- [DOWNLOAD_FUEHLER_ALLE](#job-download-fuehler-alle) - Alle Ansprechschwellen u. Impulsraeder ABS5
- [DOWNLOAD_VAKUUM_LINIE](#job-download-vakuum-linie) - Befuelroutine in Fertigungslinie ABS5
- [DOWNLOAD_VAKUUM_REPAIR](#job-download-vakuum-repair) - Befuelroutine in Nacharbeit ABS5
- [DOWNLOAD_FS_RESET](#job-download-fs-reset) - Fehlerspeicher zuruecksetzen ABS5
- [TEST_D_STELLGLIED](#job-test-d-stellglied) - Digitale Stellglieder ansteuern ABS5
- [TEST_D4_STELLGLIED](#job-test-d4-stellglied) - Digitale Stellglieder ansteuern ABS
- [TEST_PUMPENLEISTUNG_VORNE](#job-test-pumpenleistung-vorne) - Test der Pumpenfoerderleistung ABS_ASC5
- [TEST_PUMPENLEISTUNG_HINTEN](#job-test-pumpenleistung-hinten) - Test der Pumpenfoerderleistung ABS_ASC5
- [ABS_SIMULATION_4_KANAL](#job-abs-simulation-4-kanal) - Simulation ABS5
- [ABS_SIMULATION_3_KANAL](#job-abs-simulation-3-kanal) - Simulation ABS5
- [TEST_I_O_DIAGNOSE](#job-test-i-o-diagnose) - I/O-Diagnose
- [TEST_FUEHLER_EINZELN](#job-test-fuehler-einzeln) - Ansprechschwelle ABS5
- [TEST_FUEHLER_IMPULS](#job-test-fuehler-impuls) - Test Fuehler u. Impulsrad
- [TEST_STATISCH](#job-test-statisch) - Statischer Test der Komponenten ABS5
- [TEST_FUEHLER_ALLE](#job-test-fuehler-alle) - Alle Ansprechschwellen u. Impulsraeder ABS5
- [TEST_VAKUUM_LINIE](#job-test-vakuum-linie) - Befuelroutine in Fertigungslinie ABS5
- [TEST_VAKUUM_REPAIR](#job-test-vakuum-repair) - Befuelroutine in Nacharbeit ABS5
- [TEST_FS_SCHREIBEN](#job-test-fs-schreiben) - Fehlerspeicher zuruecksetzen
- [DIAGNOSE_WEITER](#job-diagnose-weiter) - Diagnose beenden
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden

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

Init-Job fuer ABS5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer ABS5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferantenname |
| ID_SW_NR | int | Softwarenummer |
| ID_TT_NR | string | RB-Teilenummer |
| ID_BB_NR | string | RB-BB-Nummer |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |
| _AUFTRAG2 | binary | Anforderungstelegramm |
| _ANTWORT2 | binary | Antworttelegramm |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen fuer ABS5 High-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| F_ORT_NR | int | momentan identisch Fehlerbytemaske |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_HFK | int | Fehlerhaeufigkeit des jeweiligen Fehlers |
| F_ART_ANZ | int | Anzahl der Fehlerarten bei ABS = 2 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen bei ABS = 1 |
| F_ART1_NR | int | Fehlerartenbyte |
| F_ART1_TEXT | string | Fehlerart als Text, Kombination aus mehreren Texten |
| F_ART2_NR | int | Fehlerartenbyte |
| F_ART2_TEXT | string | Fehlerart als Text, Kombination aus mehreren Texten |
| F_UW1_NR | int | Index der 1. Umweltbedingung |
| F_UW1_TEXT | string | Text der 1. Umweltbedingung |
| F_UW1_WERT | long | Wert der 1. Umweltbedingung |
| F_UW1_EINH | string | Einheit = km/h |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen fuer ABS5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-status-io-lesen"></a>
### STATUS_IO_LESEN

Status Eingaenge ABS5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_RAD_GESCHW_VL_WERT | long | Radgeschwindigkeit vorne links |
| STAT_RAD_GESCHW_VR_WERT | long | Radgeschwindigkeit vorne rechts |
| STAT_RAD_GESCHW_HL_WERT | long | Radgeschwindigkeit hinten links |
| STAT_RAD_GESCHW_HR_WERT | long | Radgeschwindigkeit hinten rechts |
| STAT_RAD_GESCHW_EINH | string | Einheit = km/h |
| STAT_BREMSLICHT_SCHALTER_EIN | int | 0 oder 1 |
| STAT_PUMPENMOTOR_EIN | int | 0 oder 1 |
| STAT_VENTILRELAIS_EIN | int | 0 oder 1 |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-download-stellglied"></a>
### DOWNLOAD_STELLGLIED

Stellglied ansteuern ABS5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-download-d4-stellglied"></a>
### DOWNLOAD_D4_STELLGLIED

Stellglied ansteuern ABS5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-download-i-o-diagnose"></a>
### DOWNLOAD_I_O_DIAGNOSE

I/O-Diagnose ABS5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-download-fuehler-einzeln"></a>
### DOWNLOAD_FUEHLER_EINZELN

Ansprechschwelle u. Impulsrad ABS5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-download-statisch"></a>
### DOWNLOAD_STATISCH

Statischer Test der Komponenten ABS5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-download-fuehler-alle"></a>
### DOWNLOAD_FUEHLER_ALLE

Alle Ansprechschwellen u. Impulsraeder ABS5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-download-vakuum-linie"></a>
### DOWNLOAD_VAKUUM_LINIE

Befuelroutine in Fertigungslinie ABS5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-download-vakuum-repair"></a>
### DOWNLOAD_VAKUUM_REPAIR

Befuelroutine in Nacharbeit ABS5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-download-fs-reset"></a>
### DOWNLOAD_FS_RESET

Fehlerspeicher zuruecksetzen ABS5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-test-d-stellglied"></a>
### TEST_D_STELLGLIED

Digitale Stellglieder ansteuern ABS5

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E, Wiederholung = W |
| BEFEHL_1 | string | Ein = FF, Aus = 00 |
| ST_1 | string | Stellglied 1 |
| BEFEHL_2 | string | Ein = FF, Aus = 00 |
| ST_2 | string | Stellglied 2 |
| W_ZEIT | int | Wartezeit vor Ansteuerung 3. u. 4. Stellglied |
| BEFEHL_3 | string | Ein = FF, Aus = 00 |
| ST_3 | string | Stellglied 3 |
| BEFEHL_4 | string | Ein = FF, Aus = 00 |
| ST_4 | string | Stellglied 4 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |
| _AUFTRAG2 | binary | Anforderungstelegramm |
| _ANTWORT2 | binary | Antworttelegramm |

<a id="job-test-d4-stellglied"></a>
### TEST_D4_STELLGLIED

Digitale Stellglieder ansteuern ABS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E, Wiederholung = W |
| BEFEHL_1 | string | Ein = 01, Aus = 00 |
| ST_1 | string | Stellglied 1 |
| BEFEHL_2 | string | Ein = 01, Aus = 00 |
| ST_2 | string | Stellglied 2 |
| BEFEHL_3 | string | Ein = 01, Aus = 00 |
| ST_3 | string | Stellglied 3 |
| BEFEHL_4 | string | Ein = 01, Aus = 00 |
| ST_4 | string | Stellglied 4 |
| W_ZEIT | int | Wartezeit vor Ansteuerung 3. u. 4. Stellglied |
| BEFEHL_5 | string | Ein = 01, Aus = 00 |
| ST_5 | string | Stellglied 5 |
| BEFEHL_6 | string | Ein = 01, Aus = 00 |
| ST_6 | string | Stellglied 6 |
| BEFEHL_7 | string | Ein = 01, Aus = 00 |
| ST_7 | string | Stellglied 7 |
| BEFEHL_8 | string | Ein = 01, Aus = 00 |
| ST_8 | string | Stellglied 8 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |
| _AUFTRAG2 | binary | Anforderungstelegramm |
| _ANTWORT2 | binary | Antworttelegramm |

<a id="job-test-pumpenleistung-vorne"></a>
### TEST_PUMPENLEISTUNG_VORNE

Test der Pumpenfoerderleistung ABS_ASC5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |
| _AUFTRAG2 | binary | Anforderungstelegramm |
| _ANTWORT2 | binary | Antworttelegramm |

<a id="job-test-pumpenleistung-hinten"></a>
### TEST_PUMPENLEISTUNG_HINTEN

Test der Pumpenfoerderleistung ABS_ASC5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |
| _AUFTRAG2 | binary | Anforderungstelegramm |
| _ANTWORT2 | binary | Antworttelegramm |

<a id="job-abs-simulation-4-kanal"></a>
### ABS_SIMULATION_4_KANAL

Simulation ABS5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-abs-simulation-3-kanal"></a>
### ABS_SIMULATION_3_KANAL

Simulation ABS5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-test-i-o-diagnose"></a>
### TEST_I_O_DIAGNOSE

I/O-Diagnose

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BEFEHL_1 | string | Ein = FF, Aus = 00 oder Analogwert |
| KANAL_1 | string | I/O Kanalnummer |
| BEFEHL_2 | string | Ein = FF, Aus = 00 oder Analogwert |
| KANAL_2 | string | I/O Kanalnummer |
| BEFEHL_3 | string | Ein = FF, Aus = 00 oder Analogwert |
| KANAL_3 | string | I/O Kanalnummer |
| BEFEHL_4 | string | Ein = FF, Aus = 00 oder Analogwert |
| KANAL_4 | string | I/O Kanalnummer |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| ERGEBNISDATEN | binary | Antwortdatenbytes |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |
| _AUFTRAG2 | binary | Anforderungstelegramm |
| _ANTWORT2 | binary | Antworttelegramm |
| _ANTWORT3 | binary | Antworttelegramm |

<a id="job-test-fuehler-einzeln"></a>
### TEST_FUEHLER_EINZELN

Ansprechschwelle ABS5

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RAD_NR | string | Radnummer |
| A_ZEIT | int | Ausfuehrungszeit |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| GESCHW_V1 | long | Radgeschwindigkeit bei Beginn d. Tests |
| GESCHW_V2 | long | Radgeschwindigkeit &gt; Startgeschwindigkeit |
| GESCHW_EINH | string | Einheit = km/h |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |
| _AUFTRAG2 | binary | Anforderungstelegramm |
| _ANTWORT2 | binary | Antworttelegramm |

<a id="job-test-fuehler-impuls"></a>
### TEST_FUEHLER_IMPULS

Test Fuehler u. Impulsrad

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RAD_NR | string | Radnummer |
| A_ZEIT | int | Ausfuehrungszeit |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| GESCHW_V1 | long | Radgeschwindigkeit bei Beginn d. Tests |
| GESCHW_V2 | long | Radgeschwindigkeit waehrend Test |
| GESCHW_EINH | string | Einheit = km/h |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |
| _AUFTRAG2 | binary | Anforderungstelegramm |
| _ANTWORT2 | binary | Antworttelegramm |

<a id="job-test-statisch"></a>
### TEST_STATISCH

Statischer Test der Komponenten ABS5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |
| _AUFTRAG2 | binary | Anforderungstelegramm |
| _ANTWORT2 | binary | Antworttelegramm |

<a id="job-test-fuehler-alle"></a>
### TEST_FUEHLER_ALLE

Alle Ansprechschwellen u. Impulsraeder ABS5

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| A_ZEIT | int | Ausfuehrungszeit |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| VR_MIN | long | Radgeschwindigkeit vorne rechts min |
| VR_MAX | long | Radgeschwindigkeit vorne rechts max |
| VL_MIN | long | Radgeschwindigkeit vorne links min |
| VL_MAX | long | Radgeschwindigkeit vorne rechts max |
| HR_MIN | long | Radgeschwindigkeit hinten rechts min |
| HR_MAX | long | Radgeschwindigkeit hinten rechts max |
| HL_MIN | long | Radgeschwindigkeit hinten links min |
| HL_MAX | long | Radgeschwindigkeit hinten links max |
| GESCHW_EINH | string | Einheit = km/h |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |
| _AUFTRAG2 | binary | Anforderungstelegramm |
| _ANTWORT2 | binary | Antworttelegramm |

<a id="job-test-vakuum-linie"></a>
### TEST_VAKUUM_LINIE

Befuelroutine in Fertigungslinie ABS5

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| T_ON | int | Einschaltzeit |
| T_OFF | int | Ausschaltzeit |
| ZYKLEN | int | Schaltzyklen |
| ST_1 | string | Stellglied 1 |
| ST_2 | string | Stellglied 2 |
| ST_3 | string | Stellglied 3 |
| ST_4 | string | Stellglied 4 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |
| _AUFTRAG2 | binary | Anforderungstelegramm |
| _ANTWORT2 | binary | Antworttelegramm |

<a id="job-test-vakuum-repair"></a>
### TEST_VAKUUM_REPAIR

Befuelroutine in Nacharbeit ABS5

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| T_ON | int | Einschaltzeit |
| T_OFF | int | Ausschaltzeit |
| ZYKLEN | int | Schaltzyklen |
| A_VENTIL | string | Stellglied 1 |
| ST_1 | string | Stellglied 1 |
| ST_2 | string | Stellglied 2 |
| ST_3 | string | Stellglied 3 |
| ST_4 | string | Stellglied 4 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |
| _AUFTRAG2 | binary | Anforderungstelegramm |
| _ANTWORT2 | binary | Antworttelegramm |

<a id="job-test-fs-schreiben"></a>
### TEST_FS_SCHREIBEN

Fehlerspeicher zuruecksetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| FS_STATUS | string | Fehlerstatus |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |
| _AUFTRAG2 | binary | Anforderungstelegramm |
| _ANTWORT2 | binary | Antworttelegramm |

<a id="job-diagnose-weiter"></a>
### DIAGNOSE_WEITER

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (7 × 2)
- [FORTTEXTE](#table-forttexte) (25 × 2)
- [FARTTEXTE](#table-farttexte) (5 × 2)
- [FARTMATRIX](#table-fartmatrix) (24 × 5)
- [FUMWELTMATRIX](#table-fumweltmatrix) (24 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (2 × 3)
- [STG_TABELLE](#table-stg-tabelle) (11 × 2)
- [A_VENTIL_TABELLE](#table-a-ventil-tabelle) (5 × 2)
- [E_A_STATUS](#table-e-a-status) (2 × 2)
- [RAD_NR_TABELLE](#table-rad-nr-tabelle) (4 × 2)
- [LIEFERANTEN](#table-lieferanten) (27 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 7 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xFF | ERROR_ECU_NACK |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 25 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x04 | Drehzahlfuehler hinten links |
| 0x05 | Drehzahlfuehler hinten rechts |
| 0x06 | Drehzahlfuehler vorne rechts |
| 0x07 | Drehzahlfuehler vorne links |
| 0x2F | ABS Ventil Auslass hinten links oder Hinterachse |
| 0x30 | ABS Ventil Auslass hinten rechts |
| 0x31 | ABS Ventil Auslass vorne rechts |
| 0x32 | ABS Ventil Auslass vorne links |
| 0x33 | ABS Ventil Einlass hinten links oder Hinterachse |
| 0x34 | ABS Ventil Einlass hinten rechts |
| 0x35 | ABS Ventil Einlass vorne rechts |
| 0x36 | ABS Ventil Einlass vorne links |
| 0x0E | Ventilrelais Fehler |
| 0x0F | Rueckfoerderpumpen Fehler |
| 0x15 | Steuergeraete Fehler |
| 0x18 | Falsches Zahnrad an einem der 4 Raeder |
| 0x19 | Bremslichtschalter Leitungsunterbrechung |
| 0x1E | Drehzahlfuehler hinten links |
| 0x1F | Drehzahlfuehler hinten rechts |
| 0x20 | Drehzahlfuehler vorne rechts |
| 0x21 | Drehzahlfuehler vorne links |
| 0x3F | V-Vergleich |
| 0x40 | Dauerregelung / Einsteuerung |
| 0x42 | Versorgungssp. Drehzahlf. (aktive DF), SG-Fehler (passive DF) |
| 0xXY | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 5 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | BLS betaetigt |
| 0x01 | BLS nicht betaetigt |
| 0x02 | ABS-Regelung aktiv |
| 0x03 | ABS-Regelung passiv |
| 0xFF | nicht belegt |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 24 rows × 5 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 |
| --- | --- | --- | --- | --- |
| 0x04 | 0x01 | 0x00 | 0x03 | 0x02 |
| 0x05 | 0x01 | 0x00 | 0x03 | 0x02 |
| 0x06 | 0x01 | 0x00 | 0x03 | 0x02 |
| 0x07 | 0x01 | 0x00 | 0x03 | 0x02 |
| 0x2F | 0x01 | 0x00 | 0x03 | 0x02 |
| 0x30 | 0x01 | 0x00 | 0x03 | 0x02 |
| 0x31 | 0x01 | 0x00 | 0x03 | 0x02 |
| 0x32 | 0x01 | 0x00 | 0x03 | 0x02 |
| 0x33 | 0x01 | 0x00 | 0x03 | 0x02 |
| 0x34 | 0x01 | 0x00 | 0x03 | 0x02 |
| 0x35 | 0x01 | 0x00 | 0x03 | 0x02 |
| 0x36 | 0x01 | 0x00 | 0x03 | 0x02 |
| 0x0E | 0x01 | 0x00 | 0x03 | 0x02 |
| 0x0F | 0x01 | 0x00 | 0x03 | 0x02 |
| 0x15 | 0x01 | 0x00 | 0x03 | 0x02 |
| 0x18 | 0x01 | 0x00 | 0x03 | 0x02 |
| 0x19 | 0x01 | 0x00 | 0x03 | 0x02 |
| 0x1E | 0x01 | 0x00 | 0x03 | 0x02 |
| 0x1F | 0x01 | 0x00 | 0x03 | 0x02 |
| 0x20 | 0x01 | 0x00 | 0x03 | 0x02 |
| 0x21 | 0x01 | 0x00 | 0x03 | 0x02 |
| 0x3F | 0x01 | 0x00 | 0x03 | 0x02 |
| 0x40 | 0x01 | 0x00 | 0x03 | 0x02 |
| 0x42 | 0x01 | 0x00 | 0x03 | 0x02 |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 24 rows × 5 columns

| ORT | UW_ANZ | UW1_NR | UW1_A | UW1_B |
| --- | --- | --- | --- | --- |
| 0x04 | 0x01 | 0x00 | 256 | 1 |
| 0x05 | 0x01 | 0x00 | 256 | 1 |
| 0x06 | 0x01 | 0x00 | 256 | 1 |
| 0x07 | 0x01 | 0x00 | 256 | 1 |
| 0x2F | 0x01 | 0x00 | 256 | 1 |
| 0x30 | 0x01 | 0x00 | 256 | 1 |
| 0x31 | 0x01 | 0x00 | 256 | 1 |
| 0x32 | 0x01 | 0x00 | 256 | 1 |
| 0x33 | 0x01 | 0x00 | 256 | 1 |
| 0x34 | 0x01 | 0x00 | 256 | 1 |
| 0x35 | 0x01 | 0x00 | 256 | 1 |
| 0x36 | 0x01 | 0x00 | 256 | 1 |
| 0x0E | 0x01 | 0x00 | 256 | 1 |
| 0x0F | 0x01 | 0x00 | 256 | 1 |
| 0x15 | 0x01 | 0x00 | 256 | 1 |
| 0x18 | 0x01 | 0x00 | 256 | 1 |
| 0x19 | 0x01 | 0x00 | 256 | 1 |
| 0x1E | 0x01 | 0x00 | 256 | 1 |
| 0x1F | 0x01 | 0x00 | 256 | 1 |
| 0x20 | 0x01 | 0x00 | 256 | 1 |
| 0x21 | 0x01 | 0x00 | 256 | 1 |
| 0x3F | 0x01 | 0x00 | 256 | 1 |
| 0x40 | 0x01 | 0x00 | 256 | 1 |
| 0x42 | 0x01 | 0x00 | 256 | 1 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 2 rows × 3 columns

| UWNR | UWTEXT | UW_EINH |
| --- | --- | --- |
| 0x00 | Fahrzeuggeschwindigkeit | km/h |
| 0xXY | unbekannte Umweltbedingung | XY |

<a id="table-stg-tabelle"></a>
### STG_TABELLE

Dimensions: 11 rows × 2 columns

| SIGNAL | BYTE |
| --- | --- |
| MRA | 0x22 |
| EVVL | 0x30 |
| AVVL | 0x32 |
| EVVR | 0x34 |
| AVVR | 0x36 |
| EVHR | 0x38 |
| AVHR | 0x3A |
| EVHL | 0x3C |
| AVHL | 0x3E |
| EVHA | 0x3C |
| AVHA | 0x3E |

<a id="table-a-ventil-tabelle"></a>
### A_VENTIL_TABELLE

Dimensions: 5 rows × 2 columns

| SIGNAL | BYTE |
| --- | --- |
| AVVL | 0x32 |
| AVVR | 0x36 |
| AVHR | 0x3A |
| AVHL | 0x3E |
| AVHA | 0x3E |

<a id="table-e-a-status"></a>
### E_A_STATUS

Dimensions: 2 rows × 2 columns

| SIGNAL | BYTE |
| --- | --- |
| EIN | 0xFF |
| AUS | 0x00 |

<a id="table-rad-nr-tabelle"></a>
### RAD_NR_TABELLE

Dimensions: 4 rows × 2 columns

| SIGNAL | BYTE |
| --- | --- |
| V_LINKS | 0xA0 |
| V_RECHTS | 0xA2 |
| H_RECHTS | 0xA4 |
| H_LINKS | 0xA6 |

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
