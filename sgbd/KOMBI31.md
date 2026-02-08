# KOMBI31.prg

- Jobs: [10](#jobs)
- Tables: [1](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Kombi E31 |
| ORIGIN | BMW TI-433 Dennert |
| REVISION | 2.02 |
| AUTHOR | Softing Taubert, BMW TI-433 Dennert |
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
- [FG_NR_LESEN](#job-fg-nr-lesen) - Auslesen der Fahrgestellnummer
- [SELBST_TEST](#job-selbst-test) - Anstoss des KOMBI-Selbsttests
- [STEUERN_SELBSTTEST](#job-steuern-selbsttest) - Anstoss des KOMBI-Selbsttests
- [STATUS_EMPFANGSPUFFER_LESEN](#job-status-empfangspuffer-lesen) - Auslesen des Empfangspuffers Adresse 0x00 bis 0x0B

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
| ID_GEN_NR | string | Generationsnummer |
| ID_HW_NR | string | Hardwarenummer |
| ID_SW_NR | string | Softwarenummer |
| ID_PP_NR | string | Pruefplannummer |
| ID_DATUM_KW | string | Herstelldatum KW |
| ID_DATUM_JAHR | string | Herstelldatum Jahr |

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
| F_UW_ANZ | int | Anzahl der Umweltbedingungen |
| F_HFK | int | Haeufigkeit eines Fehlers |

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
| JOB_STATUS | string | Liefert: OKAY |

<a id="job-fg-nr-lesen"></a>
### FG_NR_LESEN

Auslesen der Fahrgestellnummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| FG_NR | string | Fahrgestellnummer |

<a id="job-selbst-test"></a>
### SELBST_TEST

Anstoss des KOMBI-Selbsttests

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-steuern-selbsttest"></a>
### STEUERN_SELBSTTEST

Anstoss des KOMBI-Selbsttests

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-status-empfangspuffer-lesen"></a>
### STATUS_EMPFANGSPUFFER_LESEN

Auslesen des Empfangspuffers Adresse 0x00 bis 0x0B

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_MODUS | int | Modus des Empfangspuffers |
| STAT_TESTPHASE_EIN | int |  |
| STAT_TELEGRAMMFEHLER_EIN | int |  |
| STAT_ANZEIGE_IN_KM_EIN | int | 0=miles, 1=km |
| STAT_TAGESKMZAEHLER_2_EIN | int | 0=zaehler 1, 1=zaehler 2 |
| STAT_ANZEIGEN_AUF_NULL_EIN | int |  |
| STAT_VERBRAUCHSANZEIGE_WERT | long |  |
| STAT_VERBRAUCHSANZEIGE_EINH | string |  |
| STAT_TACHOANZEIGE_WERT | long |  |
| STAT_TACHOANZEIGE_EINH | string |  |
| STAT_TEMPERATURANZEIGE_WERT | long |  |
| STAT_TEMPERATURANZEIGE_EINH | string |  |
| STAT_TANKANZEIGE_WERT | long |  |
| STAT_TANKANZEIGE_EINH | string |  |
| STAT_LAMPE_OELDRUCK_EIN | int |  |
| STAT_LAMPE_TANKRESERVE_EIN | int |  |
| STAT_LAMPE_KUEHLMITTEL_ZU_HOCH_EIN | int |  |
| STAT_LAMPE_KUEHLMITTEL_ZU_NIEDRIG_EIN | int |  |
| STAT_LAMPE_CHECK_CONTROL_EIN | int |  |
| STAT_LAMPE_GURTWARNUNG_EIN | int |  |
| STAT_LAMPE_BREMSWARNUNG_EIN | int |  |
| STAT_LAMPE_HANDBREMSE_EIN | int |  |
| STAT_GWSZ_WERT | long | Gesamtkilometerstand |
| STAT_GWSZ_EINH | string | km |
| STAT_TRIP_COUNTER_WERT | long | aktueller Tageskilometerzaehlerstand |
| STAT_TRIP_COUNTER_EINH | string | km |
| STAT_PROGRAMMANZEIGE | string | Programmanzeige Automatikgetriebe |
| _TEL_ANTWORT | binary | Antwort-Telegramm |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (4 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 4 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | unbekannter Fehler |
| 0x01 | Datenleitung zum EKM |
| 0x02 | interner Fehlerspeicher |
| 0x03 | interner Hardware-Fehler |
