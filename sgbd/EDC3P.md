# EDC3P.prg

- Jobs: [14](#jobs)
- Tables: [2](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Elektronische Daempfer Regelung III plus |
| ORIGIN | BMW TP-421 Gerd Huber |
| REVISION | 3.00 |
| AUTHOR | Softing SAG Mw, BMW TP-421 Gerd Huber |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Info fuer Anwender
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung
- [IDENT](#job-ident) - Auslesen der Identifikationsdaten
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Beenden der Diagnose
- [STEUERN_DIGITAL](#job-steuern-digital) - Ansteuern der Ventilendstufen
- [STEUERN_VF](#job-steuern-vf) - Abspeichern der aktuellen Geschwindigkeit VF
- [STATUS_VF](#job-status-vf) - Auslesen der Raddrehzahl
- [STATUS_DIGITAL](#job-status-digital) - Auslesen der Statusbytes
- [STATUS_ANALOG](#job-status-analog) - Analogwerte auslesen
- [STATUS_ONLINE](#job-status-online) - Online-Lesen
- [CODIERUNG_LESEN](#job-codierung-lesen) - Fahrzeugcodierung auslesen
- [EEPROM_LESEN](#job-eeprom-lesen) - Lesen des EEPROM-Speichers

<a id="job-info"></a>
### INFO

Info fuer Anwender

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
| JOB_STATUS | string |  |
| ID_GEN_NR | int | Generationsnummer |
| ID_HW_NR | int | Hardwarenummer |
| ID_SW_NR | int | Softwarenummer |
| ID_PP_NR | int | Pruefplannummer |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_RES_0 | int | Reserve 0 |
| ID_RES_1 | int | Reserve 1 |
| ID_MASKEN_NR | int | Maskennummer |
| ID_STRUKTUR_NR | int | Strukturdatennummer |

<a id="job-fs-lesen"></a>
### FS_LESEN

Auslesen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, falls IO |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | int | Nr des Fehlers |
| F_ORT_TEXT | string | Fehlertext |
| F_HFK | int | Haeufigkeit eines Fehlers |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Beenden der Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

Ansteuern der Ventilendstufen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FUNKTION | string | Ansteuerfunktion auswaehlen |
| EIN | int | "1", wenn einschalten / "0", wenn ausschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY" "ERROR_NACK" |
| _TEL_AN_SG | binary |  |

<a id="job-steuern-vf"></a>
### STEUERN_VF

Abspeichern der aktuellen Geschwindigkeit VF

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY" "ERROR_NACK" |

<a id="job-status-vf"></a>
### STATUS_VF

Auslesen der Raddrehzahl

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY" "ERROR_NACK" |
| STAT_VF | int | Raddrehzahl Bereich: 0 bis +255 |
| _TEL_AUFTRAG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

Auslesen der Statusbytes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY" "ERROR_NACK" |
| STAT_VENTILE_VORNE_WEICH | int | Ventilstellung Bit0 - Vorne weich |
| STAT_VENTILE_VORNE_MITTEL | int | Ventilstellung Bit1 - Vorne mittel |
| STAT_VENTILE_HINTEN_WEICH | int | Ventilstellung Bit2 - Hinten weich |
| STAT_VENTILE_HINTEN_MITTEL | int | Ventilstellung Bit3 - Hinten mittel |
| STAT_KL15_DOWN_BIT_AKTIV | int | Ventilstellung Bit4 - Port1.0 KL15_Down Bit |
| STAT_PROGRAMM_SPORT | int | SYS_STAT_low - Sport_Programm (Programmauswahl) |
| STAT_DIMMUNG_AN | int | SYS_STAT_low - Dimmung (KL58) |
| STAT_WARN_FLAG_AKTIV | int | SYS_STAT_low - Warn_flag (Fehler aufgetreten) |
| STAT_OUT_EN_AKTIV | int | SYS_STAT_low - Out-en |
| STAT_DIAGNOSE_MODE_AKTIV | int | SYS_STAT_low - Diagnose_Mode |
| STAT_WATCH_TEST_AKTIV | int | SYS_STAT_low - Watch_TEST |
| STAT_PLAUSI_EN_AKTIV | int | SYS_STAT_low - Plausi_en |
| STAT_EEPROM_PARAM_ERKANNT | int | SYS_STAT_low - EEPROM_Parametersatz_erkannnt |
| STAT_DUMP_MODE_AKTIV | int | SYS_STAT_high - DUMP_Modus (realtime Datenuebertragung) |
| STAT_PL_SEKUNDE_AKTIV | int | SYS_STAT_high - pl_sekunde |
| STAT_PL_MINUTE_AKTIV | int | SYS_STAT_high - pl_minute |
| STAT_LAMPENFLAG_AKTIV | int | SYS_STAT_high - Lampenflag |
| STAT_LEW_OKAY | int | SYS_STAT_high - LEW imm EEPROM okay |
| STAT_DIS_VENT_TEST_AKTIV | int | SYS_STAT_high - dis_vent_test |
| STAT_SHUT_DOWN_AKTIV | int | SYS_STAT_high - SHUT_DOWN |
| _TEL_ANTWORT | binary |  |

<a id="job-status-analog"></a>
### STATUS_ANALOG

Analogwerte auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY" "ERROR_NACK" |
| STAT_LENKWINKEL_G_WERT | int | Zahlenwert des Lenkwinkels |
| STAT_LENKWINKEL_G_EINH | string | Lenkwinkel in Winkelgraden |
| STAT_LENKWINKEL_R_WERT | int | Zahlenwert des Lenkwinkels |
| STAT_LENKWINKEL_R_EINH | string | Lenkwinkel in Winkelgraden |
| STAT_B_SENSOR_LAENGS_WERT | int | Spannung am B-Senson laengs |
| STAT_B_SENSOR_LAENGS_EINH | string | Spannung in Volt [V] |
| STAT_B_SENSOR_HINTEN_WERT | int | spannung am B-Sensor hinten |
| STAT_B_SENSOR_HINTEN_EINH | string | Spannung in Volt [V] |
| STAT_B_SENSOR_VORNE_WERT | int | Spannung am B-Sensor vorne |
| STAT_B_SENSOR_VORNE_EINH | string | Spannung in Volt [V] |
| STAT_U_VENT_H_M_WERT | int | Zahlenwert Spannung am Normal-Ventil hinten |
| STAT_U_VENT_H_M_EINH | string | Spannung in Volt [V] |
| STAT_U_VENT_H_W_WERT | int | Zahlenwert Spannung am Komfort-Ventil hinten |
| STAT_U_VENT_H_W_EINH | string | Spannung in Volt [V] |
| STAT_U_VENT_V_M_WERT | int | Zahlenwert Spannung am Normal-Ventil vorne |
| STAT_U_VENT_V_M_EINH | string | Spannung in Volt [V] |
| STAT_U_VENT_V_W_WERT | int | Zahlenwert Spannung am Komfort-Ventil vorne |
| STAT_U_VENT_V_W_EINH | string | Spannung in Volt [V] |
| STAT_I_VENT_V_WERT | int | Zahlenwert Ventilstrom vorne |
| STAT_I_VENT_V_EINH | string | Ventilstrom in Apmere [I] |
| STAT_I_VENT_H_WERT | int | Zahlenwert Ventilstrom hinten |
| STAT_I_VENT_H_EINH | string | Ventilstrom in Ampere [I] |
| STAT_U_COIL_WERT | int | Zahlenwert Spannung |
| STAT_U_COIL_EINH | string | Spannung in Volt [V] |
| STAT_U_KL15_WERT | int | Zahlenwert der Spannung an Klemme 15 |
| STAT_U_KL15_EINH | string | Spannung in Volt [V] |
| _TEL_ANTWORT | binary |  |

<a id="job-status-online"></a>
### STATUS_ONLINE

Online-Lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY" "ERROR_NACK" |
| STAT_BESCHL_VERT_VORNE_WERT | int | vertikale Beschleunigung der Karosse vorne |
| STAT_BESCHL_VERT_VORNE_EINH | string | Einheit der vertikalen Beschleunigung vorne |
| STAT_BESCHL_VERT_HINTEN_WERT | int | vertikale Beschleunigung der Karosse hinten |
| STAT_BESCHL_VERT_HINTEN_EINH | string | Einheit der vertikalen Beschleunigung hinten |
| STAT_BESCHL_QUER_WERT | int | Querbeschleunigung der Karosse |
| STAT_BESCHL_QUER_EINH | string | Einheit der Querbeschleunigung |
| STAT_BESCHL_LAENGS_WERT | int | Laengsbeschleunigung der Karosse |
| STAT_BESCHL_LAENGS_EINH | string | Einheit der Laengsbeschleunigung |
| STAT_GESCHWINDIGKEIT_WERT | int | Geschwindigkeit der Karosse |
| STAT_GESCHWINDIGKEIT_EINH | string | Einheit der Geschwindigkeit |
| STAT_LENKWINKEL_WERT | int | Lenkwinkel |
| STAT_LENKWINKEL_EINH | string | Einheit des Lenkwinkels |
| STAT_LENKWINKEL_DIFF_WERT | int | Lenkwinkel-Differenz |
| STAT_LENKWINKEL_DIFF_EINH | string | Einheit der Lenkwinkel-Differenz |
| STAT_VENTILSTELLUNG_WERT | int | Ventilstellung (Kontrollwert) |
| STAT_VENTILSTELLUNG_EINH | string | Einheit der Ventilstellung |
| _TEL_ANTWORT | binary |  |

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Fahrzeugcodierung auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int | Low-Byte der Startadresse |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY" "ERROR_NACK" |
| CODIERDATEN | binary | Datenbytes 0..15 |
| _TEL_SENDE | binary |  |

<a id="job-eeprom-lesen"></a>
### EEPROM_LESEN

Lesen des EEPROM-Speichers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | long | 2 Byte (high / low) |
| ANZAHL | int | normal 16 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AN_SG | binary | Auftragstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (26 × 2)
- [STEUERN_DIGITAL](#table-steuern-digital) (11 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 26 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | Lenkwinkelfehler: Differenz der Sensorwinkel zu gross |
| 0x01 | Lenkwinkelfehler: Ableitung Analogsignal zu gross |
| 0x02 | Lenkwinkelfehler: Aktivitaet zu gering |
| 0x03 | Lenkwinkelfehler: 5 Vref extern Masse-Schluss |
| 0x10 | Fehler im VF-Signal |
| 0x20 | B-Sensor vorne: ausgefallen |
| 0x21 | B-Sensor vorne: Pegelfehler |
| 0x30 | B-Sensor hinten: ausgefallen |
| 0x31 | B-Sensor hinten: Pegelfehler |
| 0x40 | B-Sensor laengs: ausgefallen |
| 0x41 | B-Sensor laengs: Pegelfehler |
| 0x50 | Ucoil: Schluss nach Masse |
| 0x51 | Ucoil: Schluss nach Klemme 15 |
| 0x52 | Ucoil: Ventilleitung an Klemme 15 |
| 0x53 | Ucoil: Ucoil ungleich PWM -&gt; Steuergeraet defekt |
| 0x60 | Ventilfehler vorne: Unterbrechung Ucoil an Ventile |
| 0x61 | Ventilfehler vorne: Unterbrechung beider Ventilleitungen Mittel |
| 0x62 | Ventilfehler vorne: Unterbrechung einer Ventilleitung Mittel |
| 0x63 | Ventilfehler vorne: Unterbrechung beider Ventilleitungen Weich |
| 0x64 | Ventilfehler vorne: Unterbrechung einer Ventilleitung Weich |
| 0x80 | Ventilfehler hinten: Unterbrechung Ucoil an Ventile |
| 0x81 | Ventilfehler hinten: Unterbrechung beider Ventilleitungen Mittel |
| 0x82 | Ventilfehler hinten: Unterbrechung einer Ventilleitung Mittel |
| 0x83 | Ventilfehler hinten: Unterbrechung beider Ventilleitungen Weich |
| 0x84 | Ventilfehler hinten: Unterbrechung einer Ventilleitung Weich |
| 0xXY | unbekannter Fehlerort |

<a id="table-steuern-digital"></a>
### STEUERN_DIGITAL

Dimensions: 11 rows × 2 columns

| FUNCT | BYTE |
| --- | --- |
| VW | 0x01 |
| VM | 0x02 |
| VH | 0x03 |
| HW | 0x04 |
| HM | 0x08 |
| HH | 0x0C |
| LENKW | 0x01 |
| TBEL | 0x02 |
| DIMM | 0x04 |
| CC | 0x08 |
| XY | 0xFF |
