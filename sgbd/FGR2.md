# FGR2.prg

- Jobs: [26](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Fahrgeschwindigkeitsregler II |
| ORIGIN | BMW TP-421 Winkler |
| REVISION | 1.10 |
| AUTHOR | BMW TP-421 Baumgartner, BMW TP-421 Winkler |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer FGRII
- [IDENT](#job-ident) - Ident-Daten fuer FGRII
- [FS_QUICK_LESEN](#job-fs-quick-lesen) - Quicktest High-Konzept nach Lastenheft (mit Abwandlungen)
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [DIAGNOSE_ERHALTEN](#job-diagnose-erhalten) - Diagnose aufrechterhalten
- [HARDWARETEST](#job-hardwaretest) - Hardwaretest GRII
- [SPEICHER_LESEN](#job-speicher-lesen) - Speicher lesen GRII
- [CODIERDATEN_LESEN](#job-codierdaten-lesen) - Codierdaten lesen GRII
- [STATUS_LESEN](#job-status-lesen) - Statusfeld lesen GRII
- [STATUS_FGRMOT_PLUS](#job-status-fgrmot-plus) - Ausgangsspannung Motorendstufe Plus
- [STATUS_FGRPOT_PLUS](#job-status-fgrpot-plus) - Referenzspannung Stellglied PLUS
- [STATUS_FGRMOT_MINUS](#job-status-fgrmot-minus) - Ausgangsspannung Motorendstufe Minus
- [STATUS_KU_PLUS](#job-status-ku-plus) - Ausgangsspannung Kupplungsendstufe PLUS
- [STATUS_SPANNUNG](#job-status-spannung) - Versorgungsspannung
- [STATUS_LEITUNG_MFL](#job-status-leitung-mfl) - Status Datenleitung MFL
- [STATUS_INKREMENTE](#job-status-inkremente) - Statusfeld INKREMENTE lesen bei GRII
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [STEUERN_FGRMOT_PLUS_AKTIV](#job-steuern-fgrmot-plus-aktiv) - Ausgang Motorendstufe Plus aktivieren
- [STEUERN_FGRMOT_MINUS_AKTIV](#job-steuern-fgrmot-minus-aktiv) - Ausgang Motorendstufe Minus aktivieren
- [STEUERN_FGRMOT_PASSIV](#job-steuern-fgrmot-passiv) - Ausgang Motorendstufe passiv schalten
- [STEUERN_KUPPLUNG_AKTIV](#job-steuern-kupplung-aktiv) - Ausgang Kupplung aktiv schalten
- [STEUERN_KUPPLUNG_PASSIV](#job-steuern-kupplung-passiv) - Ausgang Kupplung passiv schalten

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

Init-Job fuer FGRII

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer FGRII

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
| ID_LIEF_TEXT | string | Lieferant |
| ID_SW_NR | int | Softwarenummer |

<a id="job-fs-quick-lesen"></a>
### FS_QUICK_LESEN

Quicktest High-Konzept nach Lastenheft (mit Abwandlungen)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | normalerweise OKAY |
| F_ANZ | int | Anzahl Fehler |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

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
| JOB_STATUS | string |  |
| F_ZAEHLER | int | Anzehl der gespeicherten Fehler |
| F_ORT_NR | int | Fehlercode des SG als Index |
| F_ORT_TEXT | string | Fehlercode des SG als Text |
| F_HFK | int | Haeufigkeit des einzelnen Fehlers |
| F_ART_ANZ | int | Anzahl der Fehlerarten, hier immer 0 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen, hier immer 0 |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-diagnose-erhalten"></a>
### DIAGNOSE_ERHALTEN

Diagnose aufrechterhalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-hardwaretest"></a>
### HARDWARETEST

Hardwaretest GRII

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| HARDWARE_OK | string | "OKAY", wenn Hardware in Ordnung |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Speicher lesen GRII

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| H_ADR | string | High- Byte Adresse des Speicherbereichs |
| L_ADR | string | LOW- Byte Adresse des Speicherbereichs |
| ANZ_BYTE | int | Anzahl auszulesender Bytes |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| DATEN | binary | Codierdaten |

<a id="job-codierdaten-lesen"></a>
### CODIERDATEN_LESEN

Codierdaten lesen GRII

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| HIGH_SCHLUESS | int | High Byte Schluessel |
| LOW_SCHLUESS | int | Low Byte Schluessel |
| F_ZAEHLER | int | Fehlerzugriffszaehler |
| ZYLINDER | int | 4, 6, oder 8 moeglich |
| GETRIEBE | string | AUTOMATIK oder HANDSCHALTUNG |
| K_ZAHL | long | Wert = 225 EXP+6/K |
| SOLL_MAX | int | Maximale Sollgeschwindigkeit |
| KOEF_B0 | int | Koeffizient der Reglergleichung |
| KOEF_B1 | int | Koeffizient der Reglergleichung |
| KOEF_A1 | int | Koeffizient der Reglergleichung |
| M_VORSTEU | int | Steigung Vorsteuerkennlinie |
| OFF_VORSTEU | int | Offset Vorsteuerkennlinie |
| SBANF_FAKTOR | int | Faktor d. Reduzierung Vorsteuerwert bei Betaetigen SB |
| SBENDE_FAKTOR | int | Faktor d. Stellgroessenkorr. nach Beendigen DAUER SB |
| WAANF_FAKTOR | int | Faktor Reduzierung Vorsteuerwert bei Betaetigen WA |
| WAENDE_FAKTOR | int | Faktor Stellgroessenkorr. nach Beendigen WA |
| V_DIFF_WA | int | Differenzgeschw. bei Uebergang Konstantfahrt |
| DATEN | binary | Ergebnistelegramm |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Statusfeld lesen GRII

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_FGRMOT_MINUS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_KUPPL_SCHALTER_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_INKREMENTE | int | Wertebereich 0 - 100 % |
| STAT_WAHLHEBEL_FAHRSTUFE_AKTIV | int | 0, wenn Stellung P oder N 1, wenn Stellung Fahrstufe |
| STAT_KF_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_WA_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_SB_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_SV_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_DREHZAHL_INKREMENTE | int | 1 Inkrement 2 usec |
| STAT_WA_BETAETIGT | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_GESCHWINDIGKEIT_WERT | int | Geschwindigkeit in Km/h |
| STAT_GESCHWINDIGKEIT_EINH | string | Einheit der Geschwindigkeit |
| STAT_FGRMOT_PLUS_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_SCHLUPF_AKTIV | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_SB_BETAETIGT | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_SV_BETAETIGT | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_AUS_BETAETIGT | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_BREMSPEDAL_BETAETIGT_EL | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_BREMSPEDAL_BETAETIGT_MECH | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_MAIN_BETAETIGT | int | 0, wenn FALSE / 1, wenn TRUE |
| STAT_KUPPL_AKTIV | int | Stellgliegkupplung 0, wenn FALSE / 1, wenn TRUE |
| DATEN | binary | Ergebnistelegramm |

<a id="job-status-fgrmot-plus"></a>
### STATUS_FGRMOT_PLUS

Ausgangsspannung Motorendstufe Plus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| FGRMOT_PLUS_WERT | long | Ausgangsspannung in V |
| FGRMOT_PLUS_EINH | string | Einheit V |

<a id="job-status-fgrpot-plus"></a>
### STATUS_FGRPOT_PLUS

Referenzspannung Stellglied PLUS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| FGRPOT_PLUS_WERT | long | Ausgangsspannung in V |
| FGRPOT_PLUS_EINH | string | Einheit V |

<a id="job-status-fgrmot-minus"></a>
### STATUS_FGRMOT_MINUS

Ausgangsspannung Motorendstufe Minus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| FGRMOT_MINUS_WERT | long | Ausgangsspannung in V |
| FGRMOT_MINUS_EINH | string | Einheit V |

<a id="job-status-ku-plus"></a>
### STATUS_KU_PLUS

Ausgangsspannung Kupplungsendstufe PLUS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| KU_PLUS_WERT | long | Ausgangsspannung in V |
| KU_PLUS_EINH | string | Einheit V |

<a id="job-status-spannung"></a>
### STATUS_SPANNUNG

Versorgungsspannung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| SPANNUNG_WERT | long | Versorgungsspannung in V |
| SPANNUNG_EINH | string | Einheit V |

<a id="job-status-leitung-mfl"></a>
### STATUS_LEITUNG_MFL

Status Datenleitung MFL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_SV | string | "okay" oder "gestoert" |

<a id="job-status-inkremente"></a>
### STATUS_INKREMENTE

Statusfeld INKREMENTE lesen bei GRII

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_INKREMENTE | int | Wertebereich 0 - 100 % |
| SPANNUNG_WERT | long | Versorgungsspannung in V |
| SPANNUNG_EINH | string | Einheit V |

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

<a id="job-steuern-fgrmot-plus-aktiv"></a>
### STEUERN_FGRMOT_PLUS_AKTIV

Ausgang Motorendstufe Plus aktivieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABSCHALTWERT | string | Abschaltwert 0 - 5000 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-steuern-fgrmot-minus-aktiv"></a>
### STEUERN_FGRMOT_MINUS_AKTIV

Ausgang Motorendstufe Minus aktivieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-steuern-fgrmot-passiv"></a>
### STEUERN_FGRMOT_PASSIV

Ausgang Motorendstufe passiv schalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-steuern-kupplung-aktiv"></a>
### STEUERN_KUPPLUNG_AKTIV

Ausgang Kupplung aktiv schalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-steuern-kupplung-passiv"></a>
### STEUERN_KUPPLUNG_PASSIV

Ausgang Kupplung passiv schalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (8 × 2)
- [FORTTEXTE](#table-forttexte) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (31 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 8 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xB2 | ERROR_ECU_NUMBER |
| 0xFF | ERROR_ECU_NACK |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 13 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Watchdog-Error, Fehlerhaftes WD-System |
| 0x02 | Fehler im RAM bei Initialisierung |
| 0x03 | Fehlerhafte Checksumme im BMW Codierdatenbereich |
| 0x04 | Fehlerhafte Checksumme im VDO Codierdatenbereich |
| 0x05 | Unplausible Eingangssignalerkennung ( Main- Switch)  |
| 0x06 | Vmin- Fehler, Unplausibilitaet zwischen Hard-/Software- Vmin  |
| 0x07 | Unplaus. zwischen Hard- und Software Abschaltspeicher |
| 0x10 | Fehler Kupplungszustand zu ku_plus Plausibilitaet |
| 0x11 | Stellglied hat max. Abschaltzeit ueberschritten |
| 0x12 | Fehler bei Reglerueberwachung |
| 0x13 | P+ - Spannung im ungueltigen Spannungsbereich |
| 0x21 | Fehler Togglebit |
| 0xFF | unbekannter Fehlerort |

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
| 0x30 | NEC |
| 0xFF | unbekannter Hersteller |
