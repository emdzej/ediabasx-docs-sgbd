# dia_dose.prg

- Jobs: [9](#jobs)
- Tables: [9](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Sonderfunktionen an der Diagnosesteckdose |
| ORIGIN | BMW VK-22 Siefermann |
| REVISION | 1.01 |
| AUTHOR | BMW VK-22 Siefermann, BMW TP-421 Drexel,  Fa. Softing R.Marziw |
| COMMENT | Einstellung der U_Prog |
| PACKAGE | 1.15 |
| SPRACHE | deutsch |

## Jobs

### Index

- [SPANNUNG_KL30_ABFRAGEN](#job-spannung-kl30-abfragen) - Abfragen des Hardwareinterface-Typs (ADS, EDIC usw.) Ermittlung der HW-Board-Kennung bei HW-Interface EDIC oder EDICC Ermittlung des Status der Klemmenspannung gemäß dem erkannten HW-Interface Abfragen der Spannung an Klemme 30 (Versorgungsspannung - UBatt), wenn Status der Klemmenspannung != -1
- [SPANNUNG_KL15_ABFRAGEN](#job-spannung-kl15-abfragen) - Abfragen des Hardwareinterface-Typs (ADS, EDIC usw.) Ermittlung der HW-Board-Kennung bei HW-Interface EDIC oder EDICC Ermittlung des Status der Klemmenspannung gemäß dem erkannten HW-Interface Abfragen der Spannung an Klemme 15 (Zündung), wenn Status der Klemmenspannung != -1
- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung
- [ENDE](#job-ende) - Stoppen des wiederholten Senden und Empfangen
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Beenden der Diagnose
- [U_PROG](#job-u-prog) - Einstellung der U_Prog
- [GET_VOLTAGE](#job-get-voltage) - KL30 oder KL 15 analog einlesen
- [SIA_RESET](#job-sia-reset) - Ruecksetzen der Service-Intervall-Anzeige

<a id="job-spannung-kl30-abfragen"></a>
### SPANNUNG_KL30_ABFRAGEN

Abfragen des Hardwareinterface-Typs (ADS, EDIC usw.) Ermittlung der HW-Board-Kennung bei HW-Interface EDIC oder EDICC Ermittlung des Status der Klemmenspannung gemäß dem erkannten HW-Interface Abfragen der Spannung an Klemme 30 (Versorgungsspannung - UBatt), wenn Status der Klemmenspannung != -1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, Der Auftrag wurde fehlerfrei bearbeitet Alle Ergebnisse enthalten gültige Werte  ERROR_EDIC_TYP_UNBEKANNT, Kommt nur vor, wenn bei HW-Interace EDIC oder EDICC die HW-Board-Kennung (wird mit Fkt. ifrawmode ermittelt) unbekannt ist Ansonsten liefert der Job immer OKAY |
| HW_INTERFACE_TYP | string | Typ des Hardware-Interfaces Rückgabewert der EDIABAS-Funktion "iftype()", für das in EDIABAS.INI eingestellte HW-Interface (EDIC, ADS usw.) |
| SPANNUNG_KL30 | long | Spannung an der Klemme 30 - UBatt der Spannungswert ist abhängig vom HW-Interface: AUS/EIN-Erkennung der Spannung am Diagnosestecker bei Spannung_Kl30_Status = 0 Wertebereich: AUS = 0 mV, EIN = 12000 mV  AD konvertierte Spannung am Diagnosestecker bei Spannung_Kl30_Status = 1 Wertebereich: 0x0000 - 0xXXXX mV |
| SPANNUNG_KL30_STATUS | int | Status des Spannungswertes Spannung_Kl30, der Status ist abhängig vom HW-Interface Wertebereich: -1 = Messwert nicht verfügbar 0 = ungültig -&gt;  Wert Spannung_Kl30 ist nicht plausibel, nur AUS/EIN Überprüfung möglich Der Wert von Spannung_Kl30 darf nicht als Entscheidungskriterium (z.B. bei Unterspannung) für Programmverzweigungen in einer Applikation verwendet werden 1 = gültig -&gt; Wert Spannung_Kl30 ist plausibel |
| SPANNUNG_KL30_EINH | string | Einheit des Spannungswertes -&gt; z.Z. immer mV |

<a id="job-spannung-kl15-abfragen"></a>
### SPANNUNG_KL15_ABFRAGEN

Abfragen des Hardwareinterface-Typs (ADS, EDIC usw.) Ermittlung der HW-Board-Kennung bei HW-Interface EDIC oder EDICC Ermittlung des Status der Klemmenspannung gemäß dem erkannten HW-Interface Abfragen der Spannung an Klemme 15 (Zündung), wenn Status der Klemmenspannung != -1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, Der Auftrag wurde fehlerfrei bearbeitet Alle Ergebnisse enthalten gültige Werte  ERROR_EDIC_TYP_UNBEKANNT, Kommt nur vor, wenn bei HW-Interace EDIC oder EDICC die HW-Board-Kennung (wird mit Fkt. ifrawmode ermittelt) unbekannt ist Ansonsten liefert der Job immer OKAY |
| HW_INTERFACE_TYP | string | Typ des Hardware-Interfaces Rückgabewert der EDIABAS-Funktion "iftype()", für das in EDIABAS.INI eingestellte HW-Interface (EDIC, ADS usw.) |
| SPANNUNG_KL15 | long | Spannung an der Klemme 15 - Zuendung, der Spannungswert ist abhängig vom HW-Interface: AUS/EIN-Erkennung der Spannung am Diagnosestecker bei Spannung_Kl15_Status = 0 Wertebereich: AUS = 0 mV, EIN = 12000 mV  AD konvertierte Spannung am Diagnosestecker bei Spannung_Kl15_Status = 1 Wertebereich: 0x0000 - 0xXXXX mV |
| SPANNUNG_KL15_STATUS | int | Status des Spannungswertes Spannung_Kl15, der Status ist abhängig vom HW-Interface Wertebereich: -1 = Messwert nicht verfügbar 0 = ungültig -&gt;  Wert Spannung_Kl15 ist nicht plausibel, nur AUS/EIN Überprüfung möglich Der Wert von Spannung_Kl15 darf nicht als Entscheidungskriterium (z.B. bei Unterspannung) für Programmverzweigungen in einer Applikation verwendet werden 1 = gültig -&gt; Wert Spannung_Kl15 ist plausibel |
| SPANNUNG_KL15_EINH | string | Einheit des Spannungswertes -&gt; z.Z. immer mV |

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

Initialisierung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn i.O. |

<a id="job-ende"></a>
### ENDE

Stoppen des wiederholten Senden und Empfangen

_No arguments._

_No results._

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Beenden der Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY |

<a id="job-u-prog"></a>
### U_PROG

Einstellung der U_Prog

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG1 | string | Der einzustellende Spannungswert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY, ERROR_NACK od. ERROR_PARAMETER |

<a id="job-get-voltage"></a>
### GET_VOLTAGE

KL30 oder KL 15 analog einlesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG1 | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SPANNUNG | string | Spannung in Millivolt |
| SPANNUNG_V | int | Spannung in Millivolt |
| JOB_STATUS | string | Liefert: OKAY, ERROR_PARAMETER |

<a id="job-sia-reset"></a>
### SIA_RESET

Ruecksetzen der Service-Intervall-Anzeige

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG1 | string | OEL_RESET, WEG/ZEIT_RESET |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert OKAY, ERROR_NACK, ERROR_PARAMETER |

## Tables

### Index

- [U_PRG](#table-u-prg) (10 × 2)
- [KL_SPG](#table-kl-spg) (6 × 2)
- [SIARESET](#table-siareset) (2 × 2)
- [IF_KL30_STAT_TAB](#table-if-kl30-stat-tab) (7 × 2)
- [IF_KL15_STAT_TAB](#table-if-kl15-stat-tab) (7 × 2)
- [EDICBOARDNR_KL30STAT](#table-edicboardnr-kl30stat) (8 × 2)
- [EDICBOARDNR_KL15STAT](#table-edicboardnr-kl15stat) (8 × 2)
- [ANDERE_KL30STAT](#table-andere-kl30stat) (5 × 2)
- [ANDERE_KL15STAT](#table-andere-kl15stat) (5 × 2)

<a id="table-u-prg"></a>
### U_PRG

Dimensions: 10 rows × 2 columns

| SELECTOR | FAKT |
| --- | --- |
| 0 | 0x01 |
| 5 | 0x02 |
| 10 | 0x03 |
| 12 | 0x04 |
| 15 | 0x05 |
| 18 | 0x06 |
| 10 | 0x07 |
| 25 | 0x08 |
| 33 | 0x09 |
| 33 | 0x0A |

<a id="table-kl-spg"></a>
### KL_SPG

Dimensions: 6 rows × 2 columns

| KL_BEZ | BED |
| --- | --- |
| KL15 | Kl15 |
| KL30 | Kl30 |
| KL61 | KL61 |
| KL50 | KL50 |
| KLR | KLR |
| CARB | CARB |

<a id="table-siareset"></a>
### SIARESET

Dimensions: 2 rows × 2 columns

| SELECTOR | RESET |
| --- | --- |
| OEL_RESET | 0x01 |
| WEG/ZEIT_RESET | 0x02 |

<a id="table-if-kl30-stat-tab"></a>
### IF_KL30_STAT_TAB

Dimensions: 7 rows × 2 columns

| INTERFACE | STAT_TAB |
| --- | --- |
| EDIC | EDICBoardNr_Kl30Stat |
| EDICC | EDICBoardNr_Kl30Stat |
| FUNK | Andere_Kl30Stat |
| ADS | Andere_Kl30Stat |
| EADS | Andere_Kl30Stat |
| OPPS | Andere_Kl30Stat |
| OBD | Andere_Kl30Stat |

<a id="table-if-kl15-stat-tab"></a>
### IF_KL15_STAT_TAB

Dimensions: 7 rows × 2 columns

| INTERFACE | STAT_TAB |
| --- | --- |
| EDIC | EDICBoardNr_Kl15Stat |
| EDICC | EDICBoardNr_Kl15Stat |
| FUNK | Andere_Kl15Stat |
| ADS | Andere_Kl15Stat |
| EADS | Andere_Kl15Stat |
| OPPS | Andere_Kl15Stat |
| OBD | Andere_Kl15Stat |

<a id="table-edicboardnr-kl30stat"></a>
### EDICBOARDNR_KL30STAT

Dimensions: 8 rows × 2 columns

| INTERFACE_TYP | KL30_STATUS |
| --- | --- |
| 0101 | -1 |
| 0102 | -1 |
| 0104 | -1 |
| 0105 | -1 |
| 0120 | 1 |
| 0200 | 1 |
| 0130 | 1 |
| 0131 | 1 |

<a id="table-edicboardnr-kl15stat"></a>
### EDICBOARDNR_KL15STAT

Dimensions: 8 rows × 2 columns

| INTERFACE_TYP | KL15_STATUS |
| --- | --- |
| 0101 | 0 |
| 0102 | 0 |
| 0104 | 0 |
| 0105 | 0 |
| 0120 | 1 |
| 0200 | 1 |
| 0130 | 1 |
| 0131 | 1 |

<a id="table-andere-kl30stat"></a>
### ANDERE_KL30STAT

Dimensions: 5 rows × 2 columns

| INTERFACE_TYP | KL30_STATUS |
| --- | --- |
| FUNK | 0 |
| ADS | 0 |
| EADS | 0 |
| OPPS | 0 |
| OBD | 0 |

<a id="table-andere-kl15stat"></a>
### ANDERE_KL15STAT

Dimensions: 5 rows × 2 columns

| INTERFACE_TYP | KL15_STATUS |
| --- | --- |
| FUNK | 0 |
| ADS | 0 |
| EADS | 0 |
| OPPS | 0 |
| OBD | 0 |
