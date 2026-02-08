# EML3.prg

- Jobs: [45](#jobs)
- Tables: [7](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | EML 3 Siemens |
| ORIGIN | BMW TI-433 Dennert |
| REVISION | 1.69 |
| AUTHOR | BMW TP-421 Weber, BMW TI-433 Dennert |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [EDIC_RESET](#job-edic-reset) - EDIC-Reset
- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Default Init-Job
- [RAM_MC1_LESEN](#job-ram-mc1-lesen) - Beliebige RAM - Zellen auslesen
- [RAM_MC2_LESEN](#job-ram-mc2-lesen) - Beliebige RAM - Zellen auslesen
- [EPROM_LESEN](#job-eprom-lesen) - Beliebige EPROM - Zellen auslesen
- [IDENT](#job-ident) - Ident-Daten fuer DME
- [FS_QUICK_LESEN](#job-fs-quick-lesen) - Auslesen des QUICK Fehlerspeichers
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [LOGIN](#job-login) - Schutzmechanismus LOGIN
- [SEED_KEY](#job-seed-key) - Schutzmechanismus SEED_KEY
- [STATUS_VARIANTE](#job-status-variante) - Programmierte Variante auslesen
- [PWG_ADAPTION_RESET](#job-pwg-adaption-reset) - Adaptionswert PWG Reset
- [STAT_PWG_LERN](#job-stat-pwg-lern) - Status fuer PWG Lernvorgang auslesen
- [CODIER_VAR_1_SCHREIBEN](#job-codier-var-1-schreiben) - Variante 1 E31 programmieren
- [CODIER_VAR_2_SCHREIBEN](#job-codier-var-2-schreiben) - Variante 2 E31 programmieren
- [CODIER_VAR_3_SCHREIBEN](#job-codier-var-3-schreiben) - Variante 3 E31 programmieren
- [CODIER_VAR_4_SCHREIBEN](#job-codier-var-4-schreiben) - Variante 4 E38 Programmieren
- [CODIER_VAR_5_SCHREIBEN](#job-codier-var-5-schreiben) - Variante 5 E38 programmieren
- [CODIER_VAR_6_SCHREIBEN](#job-codier-var-6-schreiben) - Variante 6 E38 programmieren
- [CODIER_VAR_7_SCHREIBEN](#job-codier-var-7-schreiben) - Variante 7 E38 programmieren
- [CODIER_VAR_8_SCHREIBEN](#job-codier-var-8-schreiben) - Variante 8 E38 programmieren
- [CODIER_VAR_9_SCHREIBEN](#job-codier-var-9-schreiben) - Variante 9 E38 programmieren
- [CODIER_VAR_A_SCHREIBEN](#job-codier-var-a-schreiben) - Variante A E38 programmieren
- [CODIER_VAR_B_SCHREIBEN](#job-codier-var-b-schreiben) - Variante 11 E38 programmieren
- [CODIER_VAR_C_SCHREIBEN](#job-codier-var-c-schreiben) - Variante 12 E38 programmieren
- [CODIER_VAR_D_SCHREIBEN](#job-codier-var-d-schreiben) - Variante 13 E38 programmieren
- [CODIER_VAR_E_SCHREIBEN](#job-codier-var-e-schreiben) - Variante 14 E38 programmieren
- [CODIER_VAR_F_SCHREIBEN](#job-codier-var-f-schreiben) - Variante 15 E38 programmieren
- [CODIER_VAR_10_SCHREIBEN](#job-codier-var-10-schreiben) - Variante 16 E38 programmieren
- [STATUS_PEDALWINKEL](#job-status-pedalwinkel) - Pedalwinkel
- [STATUS_PWG_LERN_RESTZEIT](#job-status-pwg-lern-restzeit) - Lern Restzeit
- [STATUS_PWG_OLERN](#job-status-pwg-olern) - PWG_OLERN
- [STATUS_PWG_ULERN](#job-status-pwg-ulern) - PWG_ULERN
- [STATUS_W_DK1](#job-status-w-dk1) - W_DK1
- [STATUS_W_DK2](#job-status-w-dk2) - W_DK2
- [STATUS_DK1_P1](#job-status-dk1-p1) - DK1_P1
- [STATUS_DK1_P2](#job-status-dk1-p2) - DK1_P1
- [STATUS_DK2_P1](#job-status-dk2-p1) - DK2_P1
- [STATUS_DK2_P2](#job-status-dk2-p2) - DK2_P2
- [STATUS_DIGITAL](#job-status-digital) - Status Schalteingaenge
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Loeschen des Fehlerspeichers
- [STATUS_DK1_FANGBETRIEB](#job-status-dk1-fangbetrieb) - DK1-Fangbetrieb
- [STATUS_DK2_FANGBETRIEB](#job-status-dk2-fangbetrieb) - DK1-Fangbetrieb

<a id="job-edic-reset"></a>
### EDIC_RESET

EDIC-Reset

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

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

Default Init-Job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn job erfolgreich 0 wenn job nicht erfolgreich |

<a id="job-ram-mc1-lesen"></a>
### RAM_MC1_LESEN

Beliebige RAM - Zellen auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RAM_LESEN_ADRESSE | long | Uebergabeparameter, Startadresse High-Middle-Low |
| RAM_LESEN_ANZAHL_BYTE | int | Uebergabeparameter, Anzahl der auszulesenden BYTES |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| RAM_LESEN_WERT | binary | nichts |
| RAM_LESEN_EINH | string | Einheit HEX |

<a id="job-ram-mc2-lesen"></a>
### RAM_MC2_LESEN

Beliebige RAM - Zellen auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RAM_LESEN_ADRESSE | long | Uebergabeparameter, Startadresse High-Middle-Low |
| RAM_LESEN_ANZAHL_BYTE | int | Uebergabeparameter, Anzahl der auszulesenden BYTES |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| RAM_LESEN_WERT | binary | nichts |
| RAM_LESEN_EINH | string | Einheit HEX |

<a id="job-eprom-lesen"></a>
### EPROM_LESEN

Beliebige EPROM - Zellen auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EPROM_LESEN_ADRESSE | long | Uebergabeparameter, Startadresse High-Middle-Low |
| EPROM_LESEN_ANZAHL_BYTE | int | Uebergabeparameter, Anzahl der auszulesenden BYTES |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| EPROM_LESEN_WERT | binary | nichts |
| EPROM_LESEN_EINH | string | Einheit HEX |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer DME

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | string | BMW-Hardwarenummer |
| ID_COD_INDEX | string | Codier-Index |
| ID_DIAG_INDEX | string | Diagnose-Index |
| ID_BUS_INDEX | string | Bus-Index |
| ID_DATUM_KW | string | Herstelldatum KW |
| ID_DATUM_JAHR | string | Herstelldatum Jahr |
| ID_LIEF_NR | string | Lieferanten-Nummer |
| ID_SW_NR | string | Softwarenummer |
| ID_AI_NR | string | Aenderungsindex |
| ID_PROD_NR | string | Produktionsnummer |

<a id="job-fs-quick-lesen"></a>
### FS_QUICK_LESEN

Auslesen des QUICK Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ANZ_NR | int | Anzahl der gespeicherten Fehler |
| F_BSZ_AKT | real | Betriebsstundenzahler aktuell |
| F_BSZ_ALT | real | Betriebsstundenzaehler beim letzten Loeschen |

<a id="job-fs-lesen"></a>
### FS_LESEN

Auslesen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ANZ_NR | int | Anzahl der gespeicherten Fehler |
| F_ORT_NR | int | Fehlercode des SG als Index |
| F_ORT_TEXT | string | Fehlercode des SG als Text |
| F_HFK | int | Haeufigkeit des einzelnen Fehlers |
| F_LOGISTIK | int | Fehlerlogistikzaehler |
| F_ART_ANZ | int | Anzahl der Fehlerarten des SG |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen des einzelnen Fehlers |
| F_ART1_NR | int | Fehlerart 1 des einzelnen Fehlers als Index |
| F_ART1_TEXT | string | Fehlerart 1 des einzelnen Fehlers als Text |
| F_ART2_NR | int | Fehlerart 2 des einzelnen Fehlers als Index |
| F_ART2_TEXT | string | Fehlerart 2 des einzelnen Fehlers als Text |
| F_ART3_NR | int | Fehlerart 3 des einzelnen Fehlers als Index |
| F_ART3_TEXT | string | Fehlerart 3 des einzelnen Fehlers als Text |
| F_ART4_NR | int | Fehlerart 4 des einzelnen Fehlers als Index |
| F_ART4_TEXT | string | Fehlerart 4 des einzelnen Fehlers als Text |
| F_ART5_NR | int | Fehlerart 5 des einzelnen Fehlers als Index |
| F_ART5_TEXT | string | Fehlerart 5 des einzelnen Fehlers als Text |
| F_ART6_NR | int | Fehlerart 6 des einzelnen Fehlers als Index |
| F_ART6_TEXT | string | Fehlerart 6 des einzelnen Fehlers als Text |
| F_ART7_NR | int | Fehlerart 7 des einzelnen Fehlers als Index |
| F_ART7_TEXT | string | Fehlerart 7 des einzelnen Fehlers als Text |
| F_ART8_NR | int | Fehlerart 8 des einzelnen Fehlers als Index |
| F_ART8_TEXT | string | Fehlerart 8 des einzelnen Fehlers als Text |
| F_UW1_NR | int | Umweltbedingung 1 des einzelnen Fehlers als Index |
| F_UW1_TEXT | string | Umweltbedingung 1 des einzelnen Fehlers als Text |
| F_UW1_WERT | real | Umweltbedingung 1 des einzelnen Fehlers als Wert |
| F_UW1_EINH | string | Umweltbedingung 1 des einzelnen Fehlers Einheit |
| F_UW2_NR | int | Umweltbedingung 2 des einzelnen Fehlers als Index |
| F_UW2_TEXT | string | Umweltbedingung 2 des einzelnen Fehlers als Text |
| F_UW2_WERT | real | Umweltbedingung 2 des einzelnen Fehlers als Wert |
| F_UW2_EINH | string | Umweltbedingung 2 des einzelnen Fehlers Einheit |
| F_UW3_NR | int | Umweltbedingung 3 des einzelnen Fehlers als Index |
| F_UW3_TEXT | string | Umweltbedingung 3 des einzelnen Fehlers als Text |
| F_UW3_WERT | real | Umweltbedingung 3 des einzelnen Fehlers als Wert |
| F_UW3_EINH | string | Umweltbedingung 3 des einzelnen Fehlers Einheit |
| F_UW4_NR | int | Umweltbedingung 4 des einzelnen Fehlers als Index |
| F_UW4_TEXT | string | Umweltbedingung 4 des einzelnen Fehlers als Text |
| F_UW4_WERT | real | Umweltbedingung 4 des einzelnen Fehlers als Wert |
| F_UW4_EINH | string | Umweltbedingung 4 des einzelnen Fehlers Einheit |
| F_HEX_CODE | binary | 18 Fehlerbyte in Hexformat |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-login"></a>
### LOGIN

Schutzmechanismus LOGIN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_LOGIN | binary | Rueckgabewert Status |

<a id="job-seed-key"></a>
### SEED_KEY

Schutzmechanismus SEED_KEY

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_SEED_KEY | binary | Rueckgabewert Status |

<a id="job-status-variante"></a>
### STATUS_VARIANTE

Programmierte Variante auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_VARIANTE_EEPROM1_WERT | long | Zahlenwert der programmierten Variante |
| STAT_VARIANTE_TEXT | string | Einheit HEX |
| STAT_VARIANTE_EEPROM2_WERT | long | Zahlenwert der programmierten Variante |

<a id="job-pwg-adaption-reset"></a>
### PWG_ADAPTION_RESET

Adaptionswert PWG Reset

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-stat-pwg-lern"></a>
### STAT_PWG_LERN

Status fuer PWG Lernvorgang auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_PWG_LERN_WERT | int | Status beim Lernvorgang des PWG |
| STAT_PWG_LERN_EINH | string | Einheit HEX |

<a id="job-codier-var-1-schreiben"></a>
### CODIER_VAR_1_SCHREIBEN

Variante 1 E31 programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-codier-var-2-schreiben"></a>
### CODIER_VAR_2_SCHREIBEN

Variante 2 E31 programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-codier-var-3-schreiben"></a>
### CODIER_VAR_3_SCHREIBEN

Variante 3 E31 programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-codier-var-4-schreiben"></a>
### CODIER_VAR_4_SCHREIBEN

Variante 4 E38 Programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-codier-var-5-schreiben"></a>
### CODIER_VAR_5_SCHREIBEN

Variante 5 E38 programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-codier-var-6-schreiben"></a>
### CODIER_VAR_6_SCHREIBEN

Variante 6 E38 programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-codier-var-7-schreiben"></a>
### CODIER_VAR_7_SCHREIBEN

Variante 7 E38 programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-codier-var-8-schreiben"></a>
### CODIER_VAR_8_SCHREIBEN

Variante 8 E38 programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-codier-var-9-schreiben"></a>
### CODIER_VAR_9_SCHREIBEN

Variante 9 E38 programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-codier-var-a-schreiben"></a>
### CODIER_VAR_A_SCHREIBEN

Variante A E38 programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-codier-var-b-schreiben"></a>
### CODIER_VAR_B_SCHREIBEN

Variante 11 E38 programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-codier-var-c-schreiben"></a>
### CODIER_VAR_C_SCHREIBEN

Variante 12 E38 programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-codier-var-d-schreiben"></a>
### CODIER_VAR_D_SCHREIBEN

Variante 13 E38 programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-codier-var-e-schreiben"></a>
### CODIER_VAR_E_SCHREIBEN

Variante 14 E38 programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-codier-var-f-schreiben"></a>
### CODIER_VAR_F_SCHREIBEN

Variante 15 E38 programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-codier-var-10-schreiben"></a>
### CODIER_VAR_10_SCHREIBEN

Variante 16 E38 programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-status-pedalwinkel"></a>
### STATUS_PEDALWINKEL

Pedalwinkel

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_PEDALWINKEL_WERT | real | Pedalwinkel Wert |
| STATUS_PEDALWINKEL_EINH | string | Einheit [%] |

<a id="job-status-pwg-lern-restzeit"></a>
### STATUS_PWG_LERN_RESTZEIT

Lern Restzeit

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_PWG_LERN_RESTZEIT_WERT | real | Pedalwinkel Lern Restzeit |
| STATUS_PWG_LERN_RESTZEIT_EINH | string | Einheit [s] |

<a id="job-status-pwg-olern"></a>
### STATUS_PWG_OLERN

PWG_OLERN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_PWG_OLERN_WERT | real | PWG_OLERN Wert |
| STATUS_PWG_OLERN_EINH | string | Einheit [%] |

<a id="job-status-pwg-ulern"></a>
### STATUS_PWG_ULERN

PWG_ULERN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_PWG_ULERN_WERT | real | PWG_ULERN Wert |
| STATUS_PWG_ULERN_EINH | string | Einheit [%] |

<a id="job-status-w-dk1"></a>
### STATUS_W_DK1

W_DK1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_W_DK1_WERT | real | W_DK1 Wert |
| STATUS_W_DK1_EINH | string | Einheit [%] |

<a id="job-status-w-dk2"></a>
### STATUS_W_DK2

W_DK2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_W_DK2_WERT | real | W_DK2 Wert |
| STATUS_W_DK2_EINH | string | Einheit [%] |

<a id="job-status-dk1-p1"></a>
### STATUS_DK1_P1

DK1_P1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_DK1_P1_WERT | real | DK1_P1 Wert |
| STATUS_DK1_P1_EINH | string | Einheit [V] |

<a id="job-status-dk1-p2"></a>
### STATUS_DK1_P2

DK1_P1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_DK1_P2_WERT | real | DK1_P1 Wert |
| STATUS_DK1_P2_EINH | string | Einheit [V] |

<a id="job-status-dk2-p1"></a>
### STATUS_DK2_P1

DK2_P1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_DK2_P1_WERT | real | DK2_P1 Wert |
| STATUS_DK2_P1_EINH | string | Einheit [V] |

<a id="job-status-dk2-p2"></a>
### STATUS_DK2_P2

DK2_P2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_DK2_P2_WERT | real | DK2_P2 Wert |
| STATUS_DK2_P2_EINH | string | Einheit [V] |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

Status Schalteingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_KD_EIN | int | Status Kickdownschalter 0=Aus / 1=Ein |
| STATUS_LL_EIN | int | Status Leerlaufschalter 0=Aus / 1=Ein |
| STATUS_S_PFAD1_EIN | int | Status Sicherheitspfad MC1 1=Aus / 0=Ein |
| STATUS_S_PFAD2_EIN | int | Status Sicherheitspfad MC2 0=Aus / 1=Ein |
| STATUS_BTS_EIN | int | Status Bremstestschalter 0=Aus / 1=Ein |
| STATUS_BLS_EIN | int | Status Bremslichtschalter 0=Aus / 1=Ein |
| STATUS_TEMPOMAT_HAUPTSCHALTER_EIN | int | Status Tempomat Hauptschalter  0=Aus / 1=Ein |
| STATUS_TEMPOMAT_EIN_EIN | int | Status Tempomat Ein  0=Aus / 1=Ein |
| STATUS_TEMPOMAT_AUS_EIN | int | Status Tempomat Aus  0=Aus / 1=Ein |
| STATUS_TEMPOMAT_VERZ_EIN | int | Status Tempomat Verzoegerung erkannt  0=Aus / 1=Ein |
| STATUS_TEMPOMAT_WIEDERAUF_EIN | int | Status Tempomat Wiederaufnahme  0=Aus / 1=Ein |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-status-dk1-fangbetrieb"></a>
### STATUS_DK1_FANGBETRIEB

DK1-Fangbetrieb

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_DK1_FANGBETRIEB_1_WERT | int | DK1 Fangbetrieb 1 Wert |
| STAT_DK1_FANGBETRIEB_2_WERT | int | DK1 Fangbetrieb 2 Wert |

<a id="job-status-dk2-fangbetrieb"></a>
### STATUS_DK2_FANGBETRIEB

DK1-Fangbetrieb

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_DK2_FANGBETRIEB_1_WERT | int | DK1 Fangbetrieb 1 Wert |
| STAT_DK2_FANGBETRIEB_2_WERT | int | DK1 Fangbetrieb 2 Wert |

## Tables

### Index

- [BETRIEBSWMATRIX](#table-betriebswmatrix) (18 × 8)
- [BITS](#table-bits) (11 × 4)
- [FORTTEXTE](#table-forttexte) (128 × 5)
- [FARTMATRIX](#table-fartmatrix) (2 × 17)
- [FARTTEXTE](#table-farttexte) (10 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (5 × 5)
- [JOBRESULT](#table-jobresult) (8 × 2)

<a id="table-betriebswmatrix"></a>
### BETRIEBSWMATRIX

Dimensions: 18 rows × 8 columns

| NAME | QUELLE | ZELLE | ORD | TYP | FAKT_A | FAKT_B | EINH |
| --- | --- | --- | --- | --- | --- | --- | --- |
| PEDALWINKEL | RAM2E | 0xF8F5 | -- | 1 | 0.39 | 0 | [%] |
| PWG_T_REST | RAM2E | 0xF965 | -- | 1 | 0.16 | 0 | [s] |
| DK1_P1 | RAM1E | 0xF8A5 | -- | 1 | 0.0196 | 0 | [V] |
| DK1_P2 | RAM2E | 0xF8A5 | -- | 1 | 0.0196 | 0 | [V] |
| DK2_P1 | RAM1E | 0xF8A6 | -- | 1 | 0.0196 | 0 | [V] |
| DK2_P2 | RAM2E | 0xF8A4 | -- | 1 | 0.0196 | 0 | [V] |
| PWG_OLERN | RAM2E | 0xF942 | HL | 1 | 0.1 | 0 | [Grad Phi] |
| PWG_ULERN | RAM2E | 0xF940 | HL | 1 | 0.1 | 0 | [Grad Phi] |
| W_DK1 | RAM1E | 0xF874 | -- | 1 | 1 | 0 | [%] |
| W_DK2 | RAM1E | 0xF875 | -- | 1 | 1 | 0 | [%] |
| STAT_PWG_LERN_MC1 | RAM1E | 0xF960 | -- | 1 | 1 | 0 | HEX |
| STAT_PWG_LERN_MC2 | RAM2E | 0xF960 | -- | 1 | 1 | 0 | HEX |
| VarEEPROM1 | EEPROM1 | 0x01c9 | HL | 1 | 1 | 0 | HEX |
| VarEEPROM2 | EEPROM2 | 0x01c9 | HL | 1 | 1 | 0 | HEX |
| FANG_DK1_1 | EEPROM1 | 0x010A | HL | 1 | 1 | 0 | HEX |
| FANG_DK1_2 | EEPROM1 | 0x010C | HL | 1 | 1 | 0 | HEX |
| FANG_DK2_1 | EEPROM2 | 0x010A | HL | 1 | 1 | 0 | HEX |
| FANG_DK2_2 | EEPROM2 | 0x010C | HL | 1 | 1 | 0 | HEX |

<a id="table-bits"></a>
### BITS

Dimensions: 11 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| MC2_S_KD | 2 | 0x02 | 0x02 |
| MC2_S_LL | 2 | 0x01 | 0x01 |
| MC1_SIPFAD | 0 | 0x80 | 0x80 |
| MC2_SIPFAD | 0 | 0x80 | 0x80 |
| MC1_BTS | 0 | 0x40 | 0x40 |
| MC2_BLS | 0 | 0x40 | 0x40 |
| S_T_SCHA | 0 | 0x20 | 0x20 |
| S_T_AUS | 3 | 0x10 | 0x10 |
| S_T_EINP | 3 | 0x04 | 0x04 |
| S_T_EINM | 3 | 0x08 | 0x08 |
| S_T_WA | 3 | 0x02 | 0x02 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 128 rows × 5 columns

| ORT | ORTTEXT | UW_1 | UW_2 | UW_3 |
| --- | --- | --- | --- | --- |
| 0x00 | -- | 0x00 | 0x00 | 0x00 |
| 0x01 | Minimalwertfehler bei DK 1, Poti 1 | 0x01 | 0x02 | 0x03 |
| 0x02 | Maximalwertfehler bei DK 1, Poti 1 | 0x01 | 0x02 | 0x03 |
| 0x03 | Minimalwertfehler bei DK 1, Poti 2 | 0x01 | 0x02 | 0x03 |
| 0x04 | Maximalwertfehler bei DK 1, Poti 2 | 0x01 | 0x02 | 0x03 |
| 0x05 | Minimalwertfehler bei DK 2, Poti 1 | 0x01 | 0x02 | 0x03 |
| 0x06 | Maximalwertfehler bei DK 2, Poti 1 | 0x01 | 0x02 | 0x03 |
| 0x07 | Minimalwertfehler bei DK 2, Poti 2 | 0x01 | 0x02 | 0x03 |
| 0x08 | Maximalwertfehler bei DK 2, Poti 2 | 0x01 | 0x02 | 0x03 |
| 0x09 | Differenz der DK-Poti Versorgungsspannung 1 | 0x01 | 0x02 | 0x03 |
| 0x0A | Differenz der DK-Poti Versorgungsspannung 2 | 0x01 | 0x02 | 0x03 |
| 0x0B | Vergleichsfehler Poti 1/2 bei DK 1, Minimalwert | 0x01 | 0x02 | 0x03 |
| 0x0C | Vergleichsfehler Poti 1/2 bei DK 1, Maximalwert | 0x01 | 0x02 | 0x03 |
| 0x0D | Vergleichsfehler Poti 1/2 bei DK 2, Minimalwert | 0x01 | 0x02 | 0x03 |
| 0x0E | Vergleichsfehler Poti 1/2 bei DK 2, Maximalwert | 0x01 | 0x02 | 0x03 |
| 0x14 | Fehler SG-Hardware bei PWG 1 | 0x01 | 0x02 | 0x03 |
| 0x15 | Fehler SG-Hardware bei PWG 2 | 0x01 | 0x02 | 0x03 |
| 0x16 | Fehler SG-Hardware bei PWG 3 | 0x01 | 0x02 | 0x03 |
| 0x17 | Fehler SG-Hardware bei PWG 1 | 0x01 | 0x02 | 0x03 |
| 0x18 | Fehler SG-Hardware bei PWG 2 | 0x01 | 0x02 | 0x03 |
| 0x19 | Fehler SG-Hardware bei PWG 3 | 0x01 | 0x02 | 0x03 |
| 0x1A | Fehler Komponente oder SG-Hardware bei PWG 1 | 0x01 | 0x02 | 0x03 |
| 0x1B | Fehler Komponente oder SG-Hardware bei PWG 2 | 0x01 | 0x02 | 0x03 |
| 0x1C | Fehler Komponente oder SG Hardware bei PWG 3 | 0x01 | 0x02 | 0x03 |
| 0x1D | Fehler Komponente oder SG-Hardware bei PWG 1 | 0x01 | 0x02 | 0x03 |
| 0x1E | Fehler Komponente oder SG-Hardware bei PWG 2 | 0x01 | 0x02 | 0x03 |
| 0x1F | Fehler Komponente oder SG-Hardware bei PWG 3 | 0x01 | 0x02 | 0x03 |
| 0x20 | Fehler Komponente od. SG-Hardware bei PWG 1 | 0x01 | 0x02 | 0x03 |
| 0x21 | Fehler Komponente od. SG-Hardware bei PWG 2 | 0x01 | 0x02 | 0x03 |
| 0x22 | Fehler Komponente od. SG-Hardware bei PWG 3 | 0x01 | 0x02 | 0x03 |
| 0x23 | Fehler Komponente od. SG-Hardware bei PWG 1 | 0x01 | 0x02 | 0x03 |
| 0x24 | Fehler Komponente od. SG-Hardware bei PWG 2 | 0x01 | 0x02 | 0x03 |
| 0x25 | Fehler Komponente od. SG-Hardware bei PWG 3 | 0x01 | 0x02 | 0x03 |
| 0x26 | Fehler lineare Unabhaengigkeit PWG 1, PWG 2 | 0x01 | 0x02 | 0x03 |
| 0x27 | Fehler lineare Unabhaengigkeit PWG 1, PWG 3 | 0x01 | 0x02 | 0x03 |
| 0x28 | Fehler lineare Unabhaengigkeit PWG 2, PWG 3 | 0x01 | 0x02 | 0x03 |
| 0x29 | Fehler lineare Unabhaengigkeit PWG 1, PWG 2 | 0x01 | 0x02 | 0x03 |
| 0x2A | Fehler lineare Unabhaengigkeit PWG 1, PWG 3 | 0x01 | 0x02 | 0x03 |
| 0x2B | Fehler lineare Unabhaengigkeit PWG 2, PWG 3 | 0x01 | 0x02 | 0x03 |
| 0x2C | Differenzfehler PWG 1/2 | 0x01 | 0x02 | 0x03 |
| 0x2D | Differenzfehler PWG 1/3 | 0x01 | 0x02 | 0x03 |
| 0x2E | Differenzfehler PWG 2/3 | 0x01 | 0x02 | 0x03 |
| 0x2F | Differenzfehler PWG 1/2 | 0x01 | 0x02 | 0x03 |
| 0x30 | Differenzfehler PWG 1/3 | 0x01 | 0x02 | 0x03 |
| 0x31 | Differenzfehler PWG 2/3 | 0x01 | 0x02 | 0x03 |
| 0x32 | ungueltige PWG Basisadaptionswerte im EEPROM 1 | 0x01 | 0x02 | 0x03 |
| 0x33 | ungueltige PWG Basisadaptionswerte im EEPROM 2 | 0x01 | 0x02 | 0x03 |
| 0x34 | Zuordnung PWG 3 fehlerhaft | 0x01 | 0x02 | 0x03 |
| 0x35 | Zuordnung PWG 3 fehlerhaft | 0x01 | 0x02 | 0x03 |
| 0x36 | unplausibler Spannungswert von PWG 1 | 0x01 | 0x02 | 0x03 |
| 0x37 | unplausibler Spannungswert von PWG 2 | 0x01 | 0x02 | 0x03 |
| 0x38 | unplausibler Spannungswert von PWG 3 | 0x01 | 0x02 | 0x03 |
| 0x39 | unplausibler Spannungswert von PWG 1 | 0x01 | 0x02 | 0x03 |
| 0x3A | unplausibler Spannungswert von PWG 2 | 0x01 | 0x02 | 0x03 |
| 0x3B | unplausibler Spannungswert von PWG 3 | 0x01 | 0x02 | 0x03 |
| 0x3C | unplausibles Oszillator-Signal von PWG 1 | 0x01 | 0x02 | 0x03 |
| 0x3D | unplausibles Oszillator-Signal von PWG 2 | 0x01 | 0x02 | 0x03 |
| 0x3E | unplausibles Oszillator-Signal von PWG 3 | 0x01 | 0x02 | 0x03 |
| 0x3F | unplausibles Oszillator-Signal von PWG 1 | 0x01 | 0x02 | 0x03 |
| 0x40 | unplausibles Oszillator-Signal von PWG 2 | 0x01 | 0x02 | 0x03 |
| 0x41 | unplausibles Oszillator-Signal von PWG 3 | 0x01 | 0x02 | 0x03 |
| 0x42 | Fehler redundante Oszillatorabschaltung (im SG)  PWG 1 | 0x01 | 0x02 | 0x03 |
| 0x43 | Fehler redundante Oszillatorabschaltung (im SG)  PWG 2 | 0x01 | 0x02 | 0x03 |
| 0x44 | Fehler redundante Oszillatorabschaltung (im SG)  PWG 3 | 0x01 | 0x02 | 0x03 |
| 0x45 | Fehler redundante Oszillatorabschaltung (im SG)  PWG 3 | 0x01 | 0x02 | 0x03 |
| 0x50 | EML - CAN Sendefehler | 0x01 | 0x02 | 0x03 |
| 0x51 | DME_R2, DME_L2, EGS, ASC   CAN - Empfangsfehler | 0x01 | 0x02 | 0x03 |
| 0x52 | DME_R1, DME_L1, CAN Empfangsfehler od. fal. CAN Stand | 0x01 | 0x02 | 0x03 |
| 0x53 | CAN nicht betriebsbereit | 0x01 | 0x02 | 0x03 |
| 0x56 | Fehler beim DK1 Soll- Istvergleich | 0x01 | 0x02 | 0x03 |
| 0x57 | Fehler beim DK2 Soll- Istvergleich | 0x01 | 0x02 | 0x03 |
| 0x58 | Fehler beim DK2 Soll- Istvergleich | 0x01 | 0x02 | 0x03 |
| 0x59 | Fehler beim DK1 Soll- Istvergleich | 0x01 | 0x02 | 0x03 |
| 0x5A | Unplausible DK-Lernwerte | 0x01 | 0x02 | 0x03 |
| 0x5B | Unplausible DK-Lernwerte | 0x01 | 0x02 | 0x03 |
| 0x5C | Fehler beim Sollwertvrgleich | 0x01 | 0x02 | 0x03 |
| 0x5D | Fehler beim Sollwertvrgleich | 0x01 | 0x02 | 0x03 |
| 0x64 | Steuergeraetefehler Rechner 1 | 0x01 | 0x02 | 0x03 |
| 0x65 | Steuergeraetefehler Rechner 2 | 0x01 | 0x02 | 0x03 |
| 0x66 | MC1 EEPROM Fehler | 0x01 | 0x02 | 0x03 |
| 0x67 | MC2 EEPROM Fehler | 0x01 | 0x02 | 0x03 |
| 0x68 | Checksummenfehler im EEPROM - Fehlerspeicher | 0x01 | 0x02 | 0x03 |
| 0x69 | Datenaustauschfehler in der Initialisierung | 0x01 | 0x02 | 0x03 |
| 0x6A | Datenaustauschfehler im Normalbetrieb | 0x01 | 0x02 | 0x03 |
| 0x6B | Datenaustauschfehler in der Initialisierung | 0x01 | 0x02 | 0x03 |
| 0x6C | Datenaustauschfehler im Normalbetrieb | 0x01 | 0x02 | 0x03 |
| 0x70 | Fehler FGR-Bedienhebel oder Multifunktionslenkrad | 0x01 | 0x02 | 0x03 |
| 0x71 | Fehler FGR Geschwindigkeitswertvom ASC unplausibel | 0x01 | 0x02 | 0x03 |
| 0x72 | Kickdown Schalterzustand unplausibel | 0x01 | 0x02 | 0x03 |
| 0x73 | Fehler Bremsschalter (BLS d. BTS) | 0x01 | 0x02 | 0x03 |
| 0x74 | Fehler Bremsschalter (BTS d. BLS) | 0x01 | 0x02 | 0x03 |
| 0x75 | Fehler ext. Sicherheitspfad zur DME rechts | 0x01 | 0x02 | 0x03 |
| 0x76 | Fehler ext. Sicherheitspfad zur DME links | 0x01 | 0x02 | 0x03 |
| 0x77 | Fehler bei Leerlauf-Quittierung durch DME_R ueber CAN | 0x01 | 0x02 | 0x03 |
| 0x78 | Fehler bei Leerlauf-Quittierung durch DME_L ueber CAN | 0x01 | 0x02 | 0x03 |
| 0x79 | Fehler bei Sicherheitspfad-Quittierung durch DME_R ueber CAN | 0x01 | 0x02 | 0x03 |
| 0x7A | Fehler bei Sicherheitspfad-Quittierung durch DME_L ueber CAN | 0x01 | 0x02 | 0x03 |
| 0x7B | Fehler bei Quittierung Status Notabschaltung durch DME_R ueber CAN | 0x01 | 0x02 | 0x03 |
| 0x7C | Fehler bei Quittierung Status Notabschaltung durch DME_L ueber CAN | 0x01 | 0x02 | 0x03 |
| 0x7D | Umschaltung Leerlaufregelung oder Ersatzwert | 0x01 | 0x02 | 0x03 |
| 0x7E | Verknuepfung ASC-MSR unpausibel (ASC-SG Fehler | 0x01 | 0x02 | 0x03 |
| 0x80 | Poti-Offsetfehler DK 1 | 0x01 | 0x02 | 0x03 |
| 0x81 | Poti-Offsetfehler DK 2 | 0x01 | 0x02 | 0x03 |
| 0x82 | DK1-Sprungfehler (Sonderinitialisierung) | 0x01 | 0x02 | 0x03 |
| 0x83 | DK2-Sprungfehler (SM Notinitialisierung) | 0x01 | 0x02 | 0x03 |
| 0x84 | DK1-Federtestfehler (SM Sonderinitialisierung) | 0x01 | 0x02 | 0x03 |
| 0x85 | DK2-Federtestfehler (SM Notinitialisierung) | 0x01 | 0x02 | 0x03 |
| 0x86 | Freigabenfehler ueber Voterlogik (SG-Fehler)   | 0x01 | 0x02 | 0x03 |
| 0x87 | Ueberwacherfehler in der INI | 0x01 | 0x02 | 0x03 |
| 0x88 | Poti-Offsetfehler DK 2 | 0x01 | 0x02 | 0x03 |
| 0x89 | Poti-Offsetfehler DK 1 | 0x01 | 0x02 | 0x03 |
| 0x8A | DK1-Sprungfehler (Sonderinitialisierung) | 0x01 | 0x02 | 0x03 |
| 0x8B | DK2-Sprungfehler (SM Notinitialisierung) | 0x01 | 0x02 | 0x03 |
| 0x8C | DK1-Federtestfehler (SM Sonderinitialisierung) | 0x01 | 0x02 | 0x03 |
| 0x8D | DK2-Federtestfehler (SM Notinitialisierung) | 0x01 | 0x02 | 0x03 |
| 0x8E | Freigabenfehler ueber Voterlogik (SG-Fehler)   | 0x01 | 0x02 | 0x03 |
| 0x8F | Ueberwacherfehler in der INI | 0x01 | 0x02 | 0x03 |
| 0x90 | Fehler Variante bei MC 1 | 0x01 | 0x02 | 0x03 |
| 0x91 | Fehler Variante bei MC 2 | 0x01 | 0x02 | 0x03 |
| 0x98 | Fehler Diagnose Schrittmotor-IC | 0x01 | 0x02 | 0x03 |
| 0x99 | Fehler Diagnose Schrittmotor-IC | 0x01 | 0x02 | 0x03 |
| 0x9A | Fehler Diagnose Schrittmotor-IC | 0x01 | 0x02 | 0x03 |
| 0x9B | Fehler Diagnose Schrittmotor-IC | 0x01 | 0x02 | 0x03 |
| 0x9C | Fehler Diagnose Schrittmotor-IC | 0x01 | 0x02 | 0x03 |
| 0x9D | Fehler Diagnose Schrittmotor-IC | 0x01 | 0x02 | 0x03 |
| 0x9E | Fehler Diagnose Schrittmotor-IC | 0x01 | 0x02 | 0x03 |
| 0x9F | Fehler Diagnose Schrittmotor-IC | 0x01 | 0x02 | 0x03 |
| 0xXY | unbekannter Fehlerort | 0x00 | 0x00 | 0x00 |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 2 rows × 17 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 | A6_0 | A6_1 | A7_0 | A7_1 | A8_0 | A8_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x06 | 0x07 | 0x00 | 0x00 | 0x09 | 0x08 |
| 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 10 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | Kurzschluss gegen U-Batt |
| 0x02 | Kurzschluss gegen Masse |
| 0x03 | Unterbrechung |
| 0x04 | Plausibilitaetsfehler |
| 0x05 | OBDII - relevant |
| 0x06 | Rohsignalueberwachung |
| 0x07 | Messamplitudenueberwachung |
| 0x08 | Fehler sporadisch |
| 0x09 | Fehler statisch |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 5 rows × 5 columns

| UWNR | UWTEXT | UW_EINH | UWF_A | UWF_B |
| --- | --- | --- | --- | --- |
| 0x00 | -- | ---- | 0 | 0 |
| 0x01 | UM1 | [1] | 1 | 0 |
| 0x02 | UW2 | [1] | 1 | 0 |
| 0x03 | UW3 | [1] | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | -- | 1 | 99 |

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
