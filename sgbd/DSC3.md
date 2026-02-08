# DSC3.prg

- Jobs: [42](#jobs)
- Tables: [11](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Antiblockiersystem u. Dynamisches Stabilitaets Controll 3 E38-M73 |
| ORIGIN | BMW TP-421 Hirsch |
| REVISION | 1.09 |
| AUTHOR | BMW TP-421 Hirsch |
| COMMENT | Keine Diagnose bei V &gt; 6 km/h |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer ABS_DSC3
- [IDENT](#job-ident) - Ident-Daten fuer ABS_DSC3
- [LOGIN](#job-login) - Erweiterter Diagnosebereich
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen fuer ABS_DSC3 High-Konzept nach Lastenheft Codierung/Diagnose
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen fuer ABS_DSC3
- [STATUS_IO_LESEN_GESCHW](#job-status-io-lesen-geschw) - Status Eingaenge ABS_DSC3
- [STATUS_IO_LESEN_ANALOG](#job-status-io-lesen-analog) - Status Eingaenge ABS_DSC3
- [STATUS_4_DRUCKWERTE](#job-status-4-druckwerte) - 4 aufeinanderfolgende Druckwerte
- [STATUS_IO_LESEN_DIGITAL](#job-status-io-lesen-digital) - Status Eingaenge ABS_DSC3
- [STATUS_IO_LESEN_CAN](#job-status-io-lesen-can) - Status CAN ABS_DSC3
- [DOWNLOAD_STELLGLIED](#job-download-stellglied) - Stellglied ansteuern ABS_DSC3
- [DOWNLOAD_D4_STELLGLIED](#job-download-d4-stellglied) - Stellglied ansteuern ABS_DSC3
- [DOWNLOAD_FUEHLER_EINZELN](#job-download-fuehler-einzeln) - Ansprechschwelle u. Impulsrad ABS_DSC3
- [DOWNLOAD_STATISCH](#job-download-statisch) - Statischer Test der Komponenten ABS_DSC3
- [DOWNLOAD_FUEHLER_ALLE](#job-download-fuehler-alle) - Alle Ansprechschwellen u. Impulsraeder ABS_DSC3
- [DOWNLOAD_VAKUUM_LINIE](#job-download-vakuum-linie) - Befuelroutine in Fertigungslinie ABS_DSC3
- [DOWNLOAD_VAKUUM_REPAIR](#job-download-vakuum-repair) - Befuelroutine in Nacharbeit ABS_DSC3
- [DOWNLOAD_AKTUATORIK](#job-download-aktuatorik) - Aktuatorik Test ABS_DSC3
- [DOWNLOAD_EEPROM](#job-download-eeprom) - Aktuatorik Test ABS_DSC3
- [DOWNLOAD_FS_RESET](#job-download-fs-reset) - Fehlerspeicher zuruecksetzen ABS_ASC5
- [TEST_D_STELLGLIED](#job-test-d-stellglied) - Digitale Stellglieder ansteuern ABS_DSC3
- [TEST_D4_STELLGLIED](#job-test-d4-stellglied) - Digitale Stellglieder ansteuern ABS_DSC3
- [TEST_ZUENDWINKEL](#job-test-zuendwinkel) - Digitale Stellglieder ansteuern ABS_DSC3
- [TEST_PUMPENLEISTUNG_VORNE](#job-test-pumpenleistung-vorne) - Test der Pumpenfoerderleistung ABS_DSC3
- [TEST_PUMPENLEISTUNG_HINTEN](#job-test-pumpenleistung-hinten) - Test der Pumpenfoerderleistung ABS_DSC3
- [TEST_A_STELLGLIED](#job-test-a-stellglied) - Fuellung ABS_DSC3
- [TEST_FUEHLER_EINZELN](#job-test-fuehler-einzeln) - Ansprechschwelle ABS_DSC3
- [TEST_FUEHLER_IMPULS](#job-test-fuehler-impuls) - Test Fuehler u. Impulsrad
- [TEST_STATISCH](#job-test-statisch) - Statischer Test der Komponenten ABS_DSC3
- [TEST_FUEHLER_ALLE](#job-test-fuehler-alle) - Alle Ansprechschwellen u. Impulsraeder ABS_DSC3
- [TEST_VAKUUM_LINIE](#job-test-vakuum-linie) - Befuelroutine in Fertigungslinie ABS_DSC3
- [TEST_VAKUUM_REPAIR](#job-test-vakuum-repair) - Befuelroutine in Nacharbeit ABS_DSC3
- [TEST_AKTUATORIK](#job-test-aktuatorik) - Statischer Test der Komponenten ABS_DSC3
- [TEST_LENKWINKEL](#job-test-lenkwinkel) - Lenkwinkel Initialisierung DSC3
- [TEST_EEPROM_LESEN](#job-test-eeprom-lesen) - Schreiben, Lesesn EEPROM
- [TEST_EEPROM_SCHREIBEN](#job-test-eeprom-schreiben) - Schreiben, EEPROM
- [TEST_FS_SCHREIBEN](#job-test-fs-schreiben) - Fehlerspeicher zuruecksetzen
- [ABS_SIMULATION_4_KANAL](#job-abs-simulation-4-kanal) - Simulation ABS5
- [DIAGNOSE_WEITER](#job-diagnose-weiter) - Diagnose beenden
- [TEST_DROSSELKLAPPE](#job-test-drosselklappe) - Drosselklappen-Reduzierung ABS_ASC5
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

Init-Job fuer ABS_DSC3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer ABS_DSC3

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

<a id="job-login"></a>
### LOGIN

Erweiterter Diagnosebereich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen fuer ABS_DSC3 High-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| F_ORT_NR | int | momentan identisch Fehlerbytemaske |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_HFK | int | Fehlerhaeufigkeit des jeweiligen Fehlers |
| F_ART_ANZ | int | Anzahl der Fehlerarten bei ABS/DSC3 = 4 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen bei ABS/DSC3 = 1 |
| F_ART1_NR | int | Fehlerartenbyte |
| F_ART1_TEXT | string | Fehlerart als Text, Kombination aus mehreren Texten |
| F_ART2_NR | int | Fehlerartenbyte |
| F_ART2_TEXT | string | Fehlerart als Text, Kombination aus mehreren Texten |
| F_ART3_NR | int | Fehlerartenbyte |
| F_ART3_TEXT | string | Fehlerart als Text, Kombination aus mehreren Texten |
| F_ART4_NR | int | Fehlerartenbyte |
| F_ART4_TEXT | string | Fehlerart als Text, Kombination aus mehreren Texten |
| F_UW1_NR | int | Index der 1. Umweltbedingung |
| F_UW1_TEXT | string | Text der 1. Umweltbedingung |
| F_UW1_WERT | long | Wert der 1. Umweltbedingung |
| F_UW1_EINH | string | Einheit = km/h |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen fuer ABS_DSC3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-status-io-lesen-geschw"></a>
### STATUS_IO_LESEN_GESCHW

Status Eingaenge ABS_DSC3

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E, Wiederholung = W |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_RAD_GESCHW_VL_WERT | long | Radgeschwindigkeit vorne links |
| STAT_RAD_GESCHW_VR_WERT | long | Radgeschwindigkeit vorne rechts |
| STAT_RAD_GESCHW_HL_WERT | long | Radgeschwindigkeit hinten links |
| STAT_RAD_GESCHW_HR_WERT | long | Radgeschwindigkeit hinten rechts |
| STAT_RAD_GESCHW_EINH | string | Einheit = km/h |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-status-io-lesen-analog"></a>
### STATUS_IO_LESEN_ANALOG

Status Eingaenge ABS_DSC3

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E, Wiederholung = W |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_LENKWINKEL_WERT | real | Lenkwinekl in Grad, kann + u.- Wert haben |
| STAT_LENKWINKEL_EINH | string | Einheit = Winkelgrad |
| STAT_DREHRATE_WERT | real | Drehrate in Winkelgrad/sec |
| STAT_DREHRATE_EINH | string | Einheit = Winkelgrad/sec |
| STAT_DRUCK_WERT | real | Druck in bar, kann + u.- Wert haben |
| STAT_DRUCK_EINH | string | Einheit = bar |
| STAT_QUERBESCHLEUNIGUNG_WERT | real | Querbeschleunigung , kann + u.- Wert haben |
| STAT_QUERBESCHLEUNIGUNG_EINH | string | Einheit = m/(s*s) |
| STAT_PASSIVTASTER_WERT | real | Schlupfschwellenumschalter in V |
| STAT_PASSIVTASTER_EINH | string | Einheit = V |
| STAT_BREMSLICHTSCHALTER_SPANNUNG_WERT | real |  |
| STAT_BREMSLICHTSCHALTER_SPANNUNG_EINH | string | Einheit = V |
| STAT_ZUENDUNG_WERT | real | Spannung Kl. 15 in V |
| STAT_ZUENDUNG_EINH | string | Einheit = V |
| STAT_DREHZAHLFUEHLER_SPANNUNG_WERT | real | Schlupfschwellenumschalter in V |
| STAT_DREHZAHLFUEHLER_SPANNUNG_EINH | string | Einheit = V |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-status-4-druckwerte"></a>
### STATUS_4_DRUCKWERTE

4 aufeinanderfolgende Druckwerte

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E, Wiederholung = W |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_DRUCK_WERT_1 | real | Druck in bar, kann + u.- Wert haben |
| STAT_DRUCK_WERT_2 | real | Druck in bar, kann + u.- Wert haben |
| STAT_DRUCK_WERT_3 | real | Druck in bar, kann + u.- Wert haben |
| STAT_DRUCK_WERT_4 | real | Druck in bar, kann + u.- Wert haben |

<a id="job-status-io-lesen-digital"></a>
### STATUS_IO_LESEN_DIGITAL

Status Eingaenge ABS_DSC3

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E, Wiederholung = W |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_HANDBREMSSCHALTER_EIN | int | 0 oder 1 |
| STAT_BREMSLICHT_SCHALTER_EIN | int | 0 oder 1 |
| STAT_EVVL_EIN | int | 0 oder 1 |
| STAT_AVVL_EIN | int | 0 oder 1 |
| STAT_EVHR_EIN | int | 0 oder 1 |
| STAT_AVHR_EIN | int | 0 oder 1 |
| STAT_EVVR_EIN | int | 0 oder 1 |
| STAT_AVVR_EIN | int | 0 oder 1 |
| STAT_EVHL_EIN | int | 0 oder 1 |
| STAT_AVHL_EIN | int | 0 oder 1 |
| STAT_VENTILRELAIS_EIN | int | 1 Ventilrelais angezogen 0 Ventilrelais nicht angezogen |
| STAT_UMSCHALTVENTIL_VORDERACHSE_EIN | int | 0 oder 1 |
| STAT_UMSCHALTVENTIL_HINTERACHSE_EIN | int | 0 oder 1 |
| STAT_VORLADEVENTIL_VORDERACHSE_EIN | int | 0 oder 1 |
| STAT_VORLADEVENTIL_HINTERACHSE_EIN | int | 0 oder 1 |
| STAT_PUMPENMOTOR_EIN | int | 0 oder 1 |
| STAT_VORLADEPUMPE_EIN | int | 0 oder 1 |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-status-io-lesen-can"></a>
### STATUS_IO_LESEN_CAN

Status CAN ABS_DSC3

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E, Wiederholung = W |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_MOTORDREHZAHL_WERT | int | Momentane Motordrehzahl in 1/min |
| STAT_MOTORDREHZAHL_EINH | string | Einheit = 1/min |
| STAT_NORM_FUELLUNG_SOLL_WERT | real | Wert in % |
| STAT_NORM_FUELLUNG_FAHRER_WERT | real | Wert in % |
| STAT_NORM_FUELLUNG_EINH | string | Einheit ist % |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-download-stellglied"></a>
### DOWNLOAD_STELLGLIED

Stellglied ansteuern ABS_DSC3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-download-d4-stellglied"></a>
### DOWNLOAD_D4_STELLGLIED

Stellglied ansteuern ABS_DSC3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-download-fuehler-einzeln"></a>
### DOWNLOAD_FUEHLER_EINZELN

Ansprechschwelle u. Impulsrad ABS_DSC3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-download-statisch"></a>
### DOWNLOAD_STATISCH

Statischer Test der Komponenten ABS_DSC3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-download-fuehler-alle"></a>
### DOWNLOAD_FUEHLER_ALLE

Alle Ansprechschwellen u. Impulsraeder ABS_DSC3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-download-vakuum-linie"></a>
### DOWNLOAD_VAKUUM_LINIE

Befuelroutine in Fertigungslinie ABS_DSC3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-download-vakuum-repair"></a>
### DOWNLOAD_VAKUUM_REPAIR

Befuelroutine in Nacharbeit ABS_DSC3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-download-aktuatorik"></a>
### DOWNLOAD_AKTUATORIK

Aktuatorik Test ABS_DSC3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-download-eeprom"></a>
### DOWNLOAD_EEPROM

Aktuatorik Test ABS_DSC3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-download-fs-reset"></a>
### DOWNLOAD_FS_RESET

Fehlerspeicher zuruecksetzen ABS_ASC5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |

<a id="job-test-d-stellglied"></a>
### TEST_D_STELLGLIED

Digitale Stellglieder ansteuern ABS_DSC3

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

Digitale Stellglieder ansteuern ABS_DSC3

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

<a id="job-test-zuendwinkel"></a>
### TEST_ZUENDWINKEL

Digitale Stellglieder ansteuern ABS_DSC3

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
| STAT_MOTORDREHZAHL_WERT | int | Momentane Motordrehzahl in 1/min |
| STAT_MOTORDREHZAHL_EINH | string | Einheit = 1/min |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |
| _AUFTRAG2 | binary | Anforderungstelegramm |
| _ANTWORT2 | binary | Antworttelegramm |

<a id="job-test-pumpenleistung-vorne"></a>
### TEST_PUMPENLEISTUNG_VORNE

Test der Pumpenfoerderleistung ABS_DSC3

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

Test der Pumpenfoerderleistung ABS_DSC3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |
| _AUFTRAG2 | binary | Anforderungstelegramm |
| _ANTWORT2 | binary | Antworttelegramm |

<a id="job-test-a-stellglied"></a>
### TEST_A_STELLGLIED

Fuellung ABS_DSC3

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E, Wiederholung = W |
| BEFEHL_1 | int | Max. Stellung Fuellung in % |
| W_ZEIT | int | Wartezeit vor Ansteuerung 3. u. 4. Stellglied |
| BEFEHL_2 | int | Max. Stellung Fuellung in % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |
| _AUFTRAG2 | binary | Anforderungstelegramm |
| _ANTWORT2 | binary | Antworttelegramm |

<a id="job-test-fuehler-einzeln"></a>
### TEST_FUEHLER_EINZELN

Ansprechschwelle ABS_DSC3

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

Statischer Test der Komponenten ABS_DSC3

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

Alle Ansprechschwellen u. Impulsraeder ABS_DSC3

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

Befuelroutine in Fertigungslinie ABS_DSC3

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| T_ON | int | Einschaltzeit |
| T_OFF | int | Ausschaltzeit |
| ZYKLEN | int | Schaltzyklen |
| ST_1 | string | Stellglied 1 |
| ST_2 | string | Stellglied 2 |
| ST_3 | string | Stellglied 3 |

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

Befuelroutine in Nacharbeit ABS_DSC3

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

<a id="job-test-aktuatorik"></a>
### TEST_AKTUATORIK

Statischer Test der Komponenten ABS_DSC3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| WARTEZEIT | int | Wartezeit in msec |
| WARTEZEIT_EINH | string | Einheit = msec |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |
| _AUFTRAG2 | binary | Anforderungstelegramm |
| _ANTWORT2 | binary | Antworttelegramm |

<a id="job-test-lenkwinkel"></a>
### TEST_LENKWINKEL

Lenkwinkel Initialisierung DSC3

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LFD_NR | int | Laufende Nummer fuer Eintrag in LW-SG und DSC3-SG |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |
| _AUFTRAG2 | binary | Anforderungstelegramm |
| _ANTWORT2 | binary | Antworttelegramm |

<a id="job-test-eeprom-lesen"></a>
### TEST_EEPROM_LESEN

Schreiben, Lesesn EEPROM

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INPUT | string | Adresse u. Anzahl |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| STATUS | string | Status EEPROM Zugriff |
| DATEN | binary | Status EEPROM Zugriff |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |
| _AUFTRAG2 | binary | Anforderungstelegramm |
| _ANTWORT2 | binary | Antworttelegramm |

<a id="job-test-eeprom-schreiben"></a>
### TEST_EEPROM_SCHREIBEN

Schreiben, EEPROM

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | Adresse,Anzahl,Daten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| STATUS | string | Status EEPROM Zugriff |
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

<a id="job-test-drosselklappe"></a>
### TEST_DROSSELKLAPPE

Drosselklappen-Reduzierung ABS_ASC5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _AUFTRAG1 | binary | Anforderungstelegramm |
| _ANTWORT1 | binary | Antworttelegramm |
| _AUFTRAG2 | binary | Anforderungstelegramm |
| _ANTWORT2 | binary | Antworttelegramm |

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
- [FORTTEXTE](#table-forttexte) (65 × 2)
- [FARTTEXTE](#table-farttexte) (9 × 2)
- [FARTMATRIX](#table-fartmatrix) (34 × 9)
- [FUMWELTMATRIX](#table-fumweltmatrix) (34 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (2 × 3)
- [STG_TABELLE](#table-stg-tabelle) (17 × 2)
- [A_VENTIL_TABELLE](#table-a-ventil-tabelle) (4 × 2)
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

Dimensions: 65 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x02 | CAN Motorleistungssteuerung |
| 0x04 | Drehzahlfuehler hinten links |
| 0x05 | Drehzahlfuehler hinten rechts |
| 0x06 | Drehzahlfuehler vorne rechts |
| 0x07 | Drehzahlfuehler vorne links |
| 0x0E | Ventilrelais Fehler |
| 0x0F | Rueckfoerderpumpen Fehler |
| 0x15 | Steuergeraete Fehler |
| 0x18 | Falsches Zahnrad |
| 0x19 | Bremslichtschalter Leitungsunterbrechung |
| 0x1E | Drehzahlfuehler hinten links |
| 0x1F | Drehzahlfuehler hinten rechts |
| 0x20 | Drehzahlfuehler vorne rechts |
| 0x21 | Drehzahlfuehler vorne links |
| 0x22 | ASC Umschaltventil Vorderachse |
| 0x25 | Steuergeraete Fehler ADS-Teil |
| 0x26 | Positions-Regler ADS-Teil |
| 0x27 | Stellmotor ADS-Teil |
| 0x28 | Drosselklappen-Potentiometer ADS-Teil |
| 0x29 | Lenkwinkel |
| 0x2F | Ventil Auslass hinten links |
| 0x30 | Ventil Auslass hinten rechts |
| 0x31 | Ventil Auslass vorne rechts |
| 0x32 | Ventil Auslass vorne links |
| 0x33 | Ventil Einlass hinten links |
| 0x34 | Ventil Einlass hinten rechts |
| 0x35 | Ventil Einlass vorne rechts |
| 0x36 | Ventil Einlass vorne links |
| 0x37 | Vorlade Ventil Vorderachse |
| 0x38 | CAN Fehler |
| 0x3A | Getriebesteuerung Botschaftsfehler |
| 0x3B | DMER1 Botschaftsfehler |
| 0x3F | V-Vergleich |
| 0x40 | Dauerregelung |
| 0x42 | Spannungsfehler aktive DF |
| 0x45 | DMER2 Botschaftsfehler |
| 0x47 | Lebensdauerueberwachung Motorrelais |
| 0x51 | Druck Sensor Leitung |
| 0x52 | Drehraten Sensor Leitung |
| 0x53 | Querbeschleunigung Sensor Leitung |
| 0x54 | Drehraten Sensor Plausibilitaet |
| 0x55 | Ladekolbeneinheit |
| 0x56 | ASC Umschaltventil Hinterachse |
| 0x57 | Vorlade Ventil Hinterachse |
| 0x58 | Vorlade Pumpe |
| 0x59 | Unterspannung |
| 0x5A | Passivschaltung |
| 0x5B | Lenkwinkel Botschaftsfehler |
| 0x5C | Druck Sensor Plausibilitaet |
| 0x5E | Drehraten Sensor  |
| 0x5F | Einstreuung |
| 0x60 | Aktuatorik |
| 0x61 | Lenkwinkelabgleich notwendig |
| 0x62 | Notbremse drucklos |
| 0x63 | Regler Dauereingriff |
| 0x64 | Querbeschleunigung Sensor |
| 0x67 | Lenkwinkel Berechnung |
| 0x68 | Fehler Lenkwinkel Steuergeraet  |
| 0x69 | Bremslichtschalter Plausibilitaet |
| 0x6A | Querbeschleunigung Sensor |
| 0x6B | Drehraten Sensor |
| 0x6C | SN-Ueberwachung |
| 0x6D | Bandendetest |
| 0x6E | Ueberspannung |
| 0xXY | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 9 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | ASC nicht passiv geschaltet |
| 0x01 | ASC passiv geschaltet |
| 0x02 | ABS-Regelung aktiv |
| 0x03 | ABS-Regelung passiv |
| 0x04 | BLS betaetigt |
| 0x05 | BLS nicht betaetigt |
| 0x06 | ASC-Regelung aktiv |
| 0x07 | ASC-Regelung passiv |
| 0xFF | nicht belegt |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 34 rows × 9 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x04 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x05 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x06 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x07 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x2F | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x30 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x31 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x32 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x33 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x34 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x35 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x36 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x0E | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x0F | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x15 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x18 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x1E | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x1F | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x20 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x21 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x03 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x14 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x16 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x1B | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x22 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x23 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x24 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x25 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x26 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x27 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x28 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x39 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x37 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |
| 0x17 | 0x01 | 0x00 | 0x03 | 0x02 | 0x05 | 0x04 | 0x07 | 0x06 |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 34 rows × 5 columns

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
| 0x1E | 0x01 | 0x00 | 256 | 1 |
| 0x1F | 0x01 | 0x00 | 256 | 1 |
| 0x20 | 0x01 | 0x00 | 256 | 1 |
| 0x21 | 0x01 | 0x00 | 256 | 1 |
| 0x03 | 0x01 | 0x00 | 256 | 1 |
| 0x14 | 0x01 | 0x00 | 256 | 1 |
| 0x16 | 0x01 | 0x00 | 256 | 1 |
| 0x1B | 0x01 | 0x00 | 256 | 1 |
| 0x22 | 0x01 | 0x00 | 256 | 1 |
| 0x23 | 0x01 | 0x00 | 256 | 1 |
| 0x24 | 0x01 | 0x00 | 256 | 1 |
| 0x25 | 0x01 | 0x00 | 256 | 1 |
| 0x26 | 0x01 | 0x00 | 256 | 1 |
| 0x27 | 0x01 | 0x00 | 256 | 1 |
| 0x28 | 0x01 | 0x00 | 256 | 1 |
| 0x39 | 0x01 | 0x00 | 256 | 1 |
| 0x37 | 0x01 | 0x00 | 256 | 1 |
| 0x17 | 0x01 | 0x00 | 256 | 1 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 2 rows × 3 columns

| UWNR | UWTEXT | UW_EINH |
| --- | --- | --- |
| 0x00 | Fahrzeuggeschwindigkeit | km/h |
| 0xXY | unbekannte Umweltnummer | XY |

<a id="table-stg-tabelle"></a>
### STG_TABELLE

Dimensions: 17 rows × 2 columns

| SIGNAL | BYTE |
| --- | --- |
| MRA | 0x22 |
| VLP1 | 0x24 |
| EVVL | 0x30 |
| AVVL | 0x32 |
| EVVR | 0x34 |
| AVVR | 0x36 |
| EVHR | 0x38 |
| AVHR | 0x3A |
| EVHL | 0x3C |
| AVHL | 0x3E |
| USV1 | 0x4E |
| USV2 | 0x50 |
| VLV1 | 0x52 |
| VLV2 | 0x54 |
| VLP2 | 0x84 |
| SILGK | 0x64 |
| NF-ASC | 0x78 |

<a id="table-a-ventil-tabelle"></a>
### A_VENTIL_TABELLE

Dimensions: 4 rows × 2 columns

| SIGNAL | BYTE |
| --- | --- |
| AVVL | 0x32 |
| AVVR | 0x36 |
| AVHR | 0x3A |
| AVHL | 0x3E |

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
