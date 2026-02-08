# EDIC.PRG

- Jobs: [36](#jobs)
- Tables: [0](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | EDIC Interface |
| ORIGIN | BMW TI-430 Drexel |
| REVISION | 1.1 |
| AUTHOR | BMW ET-421 Weber, BMW TI-430 Drexel |
| COMMENT | N/A |
| PACKAGE | 0.06 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Default init job
- [EDIC_SPANNUNG_KL30](#job-edic-spannung-kl30) - Messung Klemme30
- [EDIC_SPANNUNG_KL15](#job-edic-spannung-kl15) - Default Messung Klemme15 job
- [EDIC_GET_PORT_0](#job-edic-get-port-0) - Messung Spannung Analogeingang 0
- [EDIC_GET_PORT_1](#job-edic-get-port-1) - Messung Spannung Analogeingang 1
- [EDIC_GET_PORT_2](#job-edic-get-port-2) - Messung Spannung Analogeingang 2
- [EDIC_GET_PORT_3](#job-edic-get-port-3) - Messung Spannung Analogeingang 3
- [EDIC_GET_PORT_4](#job-edic-get-port-4) - Messung Spannung Analogeingang 4
- [EDIC_GET_PORT_5](#job-edic-get-port-5) - Messung Spannung Analogeingang 5
- [EDIC_GET_PORT_6](#job-edic-get-port-6) - Messung Spannung Analogeingang 6
- [EDIC_GET_PORT_7](#job-edic-get-port-7) - Messung Spannung Analogeingang 7
- [EDIC_SET_U_PROG](#job-edic-set-u-prog) - Default set uprog job
- [EDIC_JUMPER_EINLESEN](#job-edic-jumper-einlesen) - Default jumper einlesen job
- [EDIC_SIA_RESET](#job-edic-sia-reset) - Default sia-reset job
- [EDIC_SIA_EIN](#job-edic-sia-ein) - Default sia-reset job
- [EDIC_SIA_AUS](#job-edic-sia-aus) - Default sia-reset job
- [EDIC_SET_PORT_0_EIN](#job-edic-set-port-0-ein) - Set Port 0 Ein
- [EDIC_SET_PORT_0_AUS](#job-edic-set-port-0-aus) - Set Port 0 Aus
- [EDIC_SET_PORT_1_EIN](#job-edic-set-port-1-ein) - Set Port 1 Ein
- [EDIC_SET_PORT_1_AUS](#job-edic-set-port-1-aus) - Set Port 1 Aus
- [EDIC_SET_PORT_2_EIN](#job-edic-set-port-2-ein) - Set Port 2 Ein
- [EDIC_SET_PORT_2_AUS](#job-edic-set-port-2-aus) - Set Port 2 Aus
- [EDIC_SET_PORT_3_EIN](#job-edic-set-port-3-ein) - Set Port 3 Ein
- [EDIC_SET_PORT_3_AUS](#job-edic-set-port-3-aus) - Set Port 3 Aus
- [EDIC_SET_PORT_4_EIN](#job-edic-set-port-4-ein) - Set Port 4 Ein
- [EDIC_SET_PORT_4_AUS](#job-edic-set-port-4-aus) - Set Port 4 Aus
- [EDIC_SET_PORT_5_EIN](#job-edic-set-port-5-ein) - Set Port 5 Ein
- [EDIC_SET_PORT_5_AUS](#job-edic-set-port-5-aus) - Set Port 5 Aus
- [EDIC_SET_PORT_6_EIN](#job-edic-set-port-6-ein) - Set Port 5 Ein
- [EDIC_SET_PORT_6_AUS](#job-edic-set-port-6-aus) - Set Port 5 Aus
- [EDIC_SET_PORT_7_EIN](#job-edic-set-port-7-ein) - Set Port 7 Ein
- [EDIC_SET_PORT_7_AUS](#job-edic-set-port-7-aus) - Set Port 7 Aus
- [EDIC_LEITUNGSTEST](#job-edic-leitungstest) - Testschleife
- [EDIC_RESET](#job-edic-reset) - EDIC-Reset
- [EDIC_VERSION](#job-edic-version) - EDIC-Version auslesen

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

Default init job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 if done |

<a id="job-edic-spannung-kl30"></a>
### EDIC_SPANNUNG_KL30

Messung Klemme30

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| KL30_WERT | real | Spannungswert KL30 in mVolt |
| KL30_EINH | string | Einheit von KL30_WERT (V) |

<a id="job-edic-spannung-kl15"></a>
### EDIC_SPANNUNG_KL15

Default Messung Klemme15 job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| KL15_WERT | real | Spannung an KL15 in V |
| KL15_EINH | string | Einheit KL15 (V) |

<a id="job-edic-get-port-0"></a>
### EDIC_GET_PORT_0

Messung Spannung Analogeingang 0

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| EDIC_GET_PORT_0_WERT | real | Wert des Eingangs in mV |
| EDIC_GET_PORT_0_EINH | string | Einheit der Spannung (V) |

<a id="job-edic-get-port-1"></a>
### EDIC_GET_PORT_1

Messung Spannung Analogeingang 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| EDIC_GET_PORT_1_WERT | real | Wert des Eingangs in mV |
| EDIC_GET_PORT_1_EINH | string | Einheit der Spannung (V) |

<a id="job-edic-get-port-2"></a>
### EDIC_GET_PORT_2

Messung Spannung Analogeingang 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| EDIC_GET_PORT_2_WERT | real | Wert des Eingangs in mV |
| EDIC_GET_PORT_2_EINH | string | Einheit der Spannung (V) |

<a id="job-edic-get-port-3"></a>
### EDIC_GET_PORT_3

Messung Spannung Analogeingang 3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| EDIC_GET_PORT_3_WERT | real | Wert des Eingangs in mV |
| EDIC_GET_PORT_3_EINH | string | Einheit der Spannung (V) |

<a id="job-edic-get-port-4"></a>
### EDIC_GET_PORT_4

Messung Spannung Analogeingang 4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| EDIC_GET_PORT_4_WERT | real | Wert des Eingangs in mV |
| EDIC_GET_PORT_4_EINH | string | Einheit der Spannung (V) |

<a id="job-edic-get-port-5"></a>
### EDIC_GET_PORT_5

Messung Spannung Analogeingang 5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| EDIC_GET_PORT_5_WERT | real | Wert des Eingangs in mV |
| EDIC_GET_PORT_5_EINH | string | Einheit der Spannung (V) |

<a id="job-edic-get-port-6"></a>
### EDIC_GET_PORT_6

Messung Spannung Analogeingang 6

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| EDIC_GET_PORT_6_WERT | real | Wert des Eingangs in mV |
| EDIC_GET_PORT_6_EINH | string | Einheit der Spannung (V) |

<a id="job-edic-get-port-7"></a>
### EDIC_GET_PORT_7

Messung Spannung Analogeingang 7

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| EDIC_GET_PORT_7_WERT | real | Wert des Eingangs in mV |
| EDIC_GET_PORT_7_EINH | string | Einheit der Spannung (V) |

<a id="job-edic-set-u-prog"></a>
### EDIC_SET_U_PROG

Default set uprog job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPANNUNG | string | Wert der Programmierspannung in mV |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-edic-jumper-einlesen"></a>
### EDIC_JUMPER_EINLESEN

Default jumper einlesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| JUMPERS | string | Jumperstellungen |

<a id="job-edic-sia-reset"></a>
### EDIC_SIA_RESET

Default sia-reset job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEIT | string | Zeit fuer das Schliessen des SI-Relais |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-edic-sia-ein"></a>
### EDIC_SIA_EIN

Default sia-reset job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-edic-sia-aus"></a>
### EDIC_SIA_AUS

Default sia-reset job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-edic-set-port-0-ein"></a>
### EDIC_SET_PORT_0_EIN

Set Port 0 Ein

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Jobstatus |

<a id="job-edic-set-port-0-aus"></a>
### EDIC_SET_PORT_0_AUS

Set Port 0 Aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Jobstatus |

<a id="job-edic-set-port-1-ein"></a>
### EDIC_SET_PORT_1_EIN

Set Port 1 Ein

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Jobstatus |

<a id="job-edic-set-port-1-aus"></a>
### EDIC_SET_PORT_1_AUS

Set Port 1 Aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Jobstatus |

<a id="job-edic-set-port-2-ein"></a>
### EDIC_SET_PORT_2_EIN

Set Port 2 Ein

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Jobstatus |

<a id="job-edic-set-port-2-aus"></a>
### EDIC_SET_PORT_2_AUS

Set Port 2 Aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Jobstatus |

<a id="job-edic-set-port-3-ein"></a>
### EDIC_SET_PORT_3_EIN

Set Port 3 Ein

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Jobstatus |

<a id="job-edic-set-port-3-aus"></a>
### EDIC_SET_PORT_3_AUS

Set Port 3 Aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Jobstatus |

<a id="job-edic-set-port-4-ein"></a>
### EDIC_SET_PORT_4_EIN

Set Port 4 Ein

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Jobstatus |

<a id="job-edic-set-port-4-aus"></a>
### EDIC_SET_PORT_4_AUS

Set Port 4 Aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Jobstatus |

<a id="job-edic-set-port-5-ein"></a>
### EDIC_SET_PORT_5_EIN

Set Port 5 Ein

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Jobstatus |

<a id="job-edic-set-port-5-aus"></a>
### EDIC_SET_PORT_5_AUS

Set Port 5 Aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Jobstatus |

<a id="job-edic-set-port-6-ein"></a>
### EDIC_SET_PORT_6_EIN

Set Port 5 Ein

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Jobstatus |

<a id="job-edic-set-port-6-aus"></a>
### EDIC_SET_PORT_6_AUS

Set Port 5 Aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Jobstatus |

<a id="job-edic-set-port-7-ein"></a>
### EDIC_SET_PORT_7_EIN

Set Port 7 Ein

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Jobstatus |

<a id="job-edic-set-port-7-aus"></a>
### EDIC_SET_PORT_7_AUS

Set Port 7 Aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Jobstatus |

<a id="job-edic-leitungstest"></a>
### EDIC_LEITUNGSTEST

Testschleife

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| CHECK | string | Ergebnis des Leitungstests: Leitungen OKAY |

<a id="job-edic-reset"></a>
### EDIC_RESET

EDIC-Reset

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-edic-version"></a>
### EDIC_VERSION

EDIC-Version auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| VERSION | long | EDIC-Versionsnummer |

## Tables

No tables found.
