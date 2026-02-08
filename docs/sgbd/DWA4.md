# DWA4.prg

- Jobs: [10](#jobs)
- Tables: [2](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Diebstahlwarnanlage DWA4 E31 / E32 / E34 / E36 |
| ORIGIN | BMW TP-422 Teepe |
| REVISION | 1.09 |
| AUTHOR | BMW TP-422 Teepe, BMW TP-421 Drexel |
| COMMENT | diese Version ist erforderlich fuer EDIABAS 4.0 |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Default init job
- [IDENT](#job-ident) - Default ident job
- [FS_LESEN](#job-fs-lesen) - Default FS_LESEN job
- [FS_LOESCHEN](#job-fs-loeschen) - Default FS_LOESCHEN job
- [SPEICHER_LESEN](#job-speicher-lesen) - Default SPEICHER_LESEN job
- [STATUS_EINGAENGE_LESEN](#job-status-eingaenge-lesen) - Default Status_eingaenge lesen job
- [CODIERUNG_LESEN](#job-codierung-lesen) - Default Codierunglesen job
- [STATUS_SCHAERFEN_LESEN](#job-status-schaerfen-lesen) - Default Status_schaerfen_lesen job
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Default Diagnose_ende job

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

Default init job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 if done |

<a id="job-ident"></a>
### IDENT

Default ident job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| ID_GEN_NR | int | Generationsnummer |
| ID_HW_NR | int | Hardware-Nummer |
| ID_VERSION | string | High/low-Version |
| ID_SW_NR | int | Software-Nummer |
| ID_PP_NR | int | Pruefplannummer |
| ID_DATUM_KW | int |  |
| ID_DATUM_JAHR | int |  |

<a id="job-fs-lesen"></a>
### FS_LESEN

Default FS_LESEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_HFK | int | Fehlerhaefigkeit |
| F_ORT_NR | int | Fehlercode |
| F_ORT_TEXT | string | Fehlertext |
| F_ART_ANZ | int | Anzahl Fehlerarten (immer 0) |
| F_UW_ANZ | int | Anzahl Umweltbedingungen (immer 0) |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Default FS_LOESCHEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Default SPEICHER_LESEN job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANZAHL | int |  |
| ADRESSE_HIGH | int |  |
| ADRESSE_LOW | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| DATENFELD | binary | angeforderter Datenblock |

<a id="job-status-eingaenge-lesen"></a>
### STATUS_EINGAENGE_LESEN

Default Status_eingaenge lesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_KL_R_EIN | int |  |
| STAT_KL_30_EIN | int |  |
| STAT_KL_61_EIN | int |  |
| STAT_DIAGNOSE_HORN_EIN | int |  |
| STAT_KL_15_EIN | int |  |
| STAT_DIAGNOSE_WFS_EIN | int |  |
| STAT_ZS22_EIN | int |  |
| STAT_ZS2_EIN | int |  |
| STAT_ZS21_EIN | int |  |
| STAT_ZS1_EIN | int |  |
| STAT_ZS11_EIN | int |  |
| STAT_HKS_EIN | int |  |
| STAT_HKE_EIN | int |  |
| STAT_HECKKLAPPE_OFFEN | int |  |
| STAT_TUEREN_HINTEN_OFFEN | int |  |
| STAT_HANDSCHUHFACH_OFFEN | int |  |
| STAT_FAHRERTUER_OFFEN | int |  |
| STAT_QZV_EIN | int |  |
| STAT_MOTORHAUBE_RADIO_OFFEN | int |  |
| STAT_WEGSIGNAL_EIN | int |  |
| STAT_BEIFAHRERTUER_OFFEN | int |  |
| STAT_SCHEIBE_GH_RECHTS_EIN | int |  |
| STAT_SCHEIBE_GH_LINKS_EIN | int |  |
| STAT_HECKSCHEIBE_EIN | int |  |
| STAT_SCHEIBE_FAHRERTUER_EIN | int |  |
| STAT_SCHEIBE_BEIFAHRERTUER_EIN | int |  |
| STAT_SCHEIBE_TUER_HINTEN_LINKS_EIN | int |  |
| STAT_SCHEIBE_TUER_HINTEN_RECHTS_EIN | int |  |
| STAT_NEIGUNGSGEBER_EIN | int |  |

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Default Codierunglesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| FAHRZEUG_TYP | string | E31,E32,E34,E36 |
| FAHRZEUG_VARIANTE | int | /2,/4,/7 |
| TYP_SCHLOSS_SIGNALE | string |  |
| NEIGUNGSGEBER_VERBAUT | int |  |
| IRS_VERBAUT | int |  |
| TYP_HECKKLAPPEN_SIGNALE | string | E32 oder E36 |
| HECKKLAPPE_WIE_FAHRERTUER | int | wie Fahrertuer oder seperat |
| ALARMVARIANTE | string | ECE oder Schweiz |
| OPTISCHER_ALARM_CODIERT | int | j/n |
| LED_BLITZT | int | Blitz oder leuchtet |
| NUR_MIT_FERNBEDIENUNG | int |  |
| PANICMODUS_MOEGLICH | int |  |
| ULTRASCHALLINNENRAUMSCHUTZ_VERBAUT | int |  |
| OPTISCHE_QUITTIERUNG_BEIM_SCHAERFEN | int |  |
| TYP_E31 | int |  |
| OPTISCHE_QUITTIERUNG_BEIM_ENTSCHAERFEN | int |  |
| ZEITDAUER_AKUSTISCHE_QUITTIERUNG_WERT | int | 0 bis 140 ms |
| ZEITDAUER_AKUSTISCHE_QUITTIERUNG_EINH | string | ms |
| AKUSTISCHE_QUITTIERUNG_BEIM_ENTSCHAERFEN | int |  |
| PIN_C8_IST_EINGANG_NG | int |  |
| FENSTER_HINTEN_RECHTS_UEBERWACHEN | int |  |
| FENSTER_HINTEN_LINKS_UEBERWACHEN | int |  |
| FENSTER_VORNE_RECHTS_UEBERWACHEN | int |  |
| FENSTER_VORNE_LINKS_UEBERWACHEN | int |  |
| HECKSCHEIBE_UEBERWACHEN | int |  |
| FRONTSCHEIBE_UEBERWACHEN | int |  |
| SCHEIBE_HINTEN_RECHTS_WIRD_UEBERWACHT | int |  |
| NEIGUNGSGEBER_IST_AKTIV_LOW | int |  |
| SCHEIBE_TUER_HINTEN_RECHTS_IST_AKTIV_LOW | int |  |
| SCHEIBE_TUER_HINTEN_LINKS_IST_AKTIV_LOW | int |  |
| SCHEIBE_BEIFAHRERTUER_IST_AKTIV_LOW | int |  |
| SCHEIBE_FAHRERTUER_IST_AKTIV_LOW | int |  |
| HECKSCHEIBE_IST_AKTIV_LOW | int |  |
| SCHEIBE_HINTEN_LINKS_IST_AKTIV_LOW | int |  |
| SCHEIBE_HINTEN_RECHTS_IST_AKTIV_LOW | int |  |
| PIN_C14_WIRD_UEBERWACHT | int |  |
| PIN_C1_WIRD_UEBERWACHT | int |  |
| PIN_C15_WIRD_UEBERWACHT | int |  |
| PIN_C2_WIRD_UEBERWACHT | int |  |
| PIN_C16_WIRD_UEBERWACHT | int |  |
| PIN_C3_WIRD_UEBERWACHT | int |  |
| PIN_C17_WIRD_UEBERWACHT | int |  |
| PIN_C4_WIRD_UEBERWACHT | int |  |
| PIN_C14_IST_AKTIV_LOW | int |  |
| PIN_C1_IST_AKTIV_LOW | int |  |
| PIN_C15_IST_AKTIV_LOW | int |  |
| PIN_C2_IST_AKTIV_LOW | int |  |
| PIN_C16_IST_AKTIV_LOW | int |  |
| PIN_C3_IST_AKTIV_LOW | int |  |
| PIN_C17_IST_AKTIV_LOW | int |  |
| PIN_C4_IST_AKTIV_LOW | int |  |
| PIN_D3_WIRD_UEBERWACHT | int |  |
| PIN_D4_WIRD_UEBERWACHT | int |  |
| PIN_D18_WIRD_UEBERWACHT | int |  |
| PIN_D3_IST_AKTIV_OFFEN | int |  |
| PIN_D4_IST_AKTIV_OFFEN | int |  |
| PIN_D18_IST_AKTIV_OFFEN | int |  |
| PRUEFSTROM_PIN_C14_WERT | int | 1 oder 10 mA |
| PRUEFSTROM_PIN_C14_EINH | string | mA |
| PRUEFSTROM_PIN_C1_WERT | int | 1 oder 10 mA |
| PRUEFSTROM_PIN_C1_EINH | string | mA |
| PRUEFSTROM_PIN_C15_WERT | int | 1 oder 10 mA |
| PRUEFSTROM_PIN_C15_EINH | string | mA |
| PRUEFSTROM_PIN_C2_WERT | int | 1 oder 10 mA |
| PRUEFSTROM_PIN_C2_EINH | string | mA |
| PRUEFSTROM_PIN_C16_WERT | int | 1 oder 10 mA |
| PRUEFSTROM_PIN_C16_EINH | string | mA |
| PRUEFSTROM_PIN_C3_WERT | int | 1 oder 10 mA |
| PRUEFSTROM_PIN_C3_EINH | string | mA |
| PRUEFSTROM_PIN_C17_WERT | int | 1 oder 10 mA |
| PRUEFSTROM_PIN_C17_EINH | string | mA |
| PRUEFSTROM_PIN_C4_WERT | int | 1 oder 10 mA |
| PRUEFSTROM_PIN_C4_EINH | string | mA |
| PRUEFSTROM_NEIGUNGSGEBER_WERT | int | 1 oder 10 mA |
| PRUEFSTROM_NEIGUNGSGEBER_EINH | string | mA |
| PRUEFSTROM_SCHEIBE_TUER_HINTEN_RECHTS_WERT | int | 1 oder 10 mA |
| PRUEFSTROM_SCHEIBE_TUER_HINTEN_RECHTS_EINH | string | mA |
| PRUEFSTROM_SCHEIBE_TUER_HINTEN_LINKS_WERT | int | 1 oder 10 mA |
| PRUEFSTROM_SCHEIBE_TUER_HINTEN_LINKS_EINH | string | mA |
| PRUEFSTROM_SCHEIBE_BEIFAHRERTUER_WERT | int | 1 oder 10 mA |
| PRUEFSTROM_SCHEIBE_BEIFAHRERTUER_EINH | string | mA |
| PRUEFSTROM_SCHEIBE_FAHRERTUER_WERT | int | 1 oder 10 mA |
| PRUEFSTROM_SCHEIBE_FAHRERTUER_EINH | string | mA |
| PRUEFSTROM_HECKSCHEIBE_WERT | int | 1 oder 10 mA |
| PRUEFSTROM_HECKSCHEIBE_EINH | string | mA |
| PRUEFSTROM_SCHEIBE_HINTEN_LINKS_WERT | int | 1 oder 10 mA |
| PRUEFSTROM_SCHEIBE_HINTEN_LINKS_EINH | string | mA |
| PRUEFSTROM_SCHEIBE_HINTEN_RECHTS_WERT | int | 1 oder 10 mA |
| PRUEFSTROM_SCHEIBE_HINTEN_RECHTS_EINH | string | mA |

<a id="job-status-schaerfen-lesen"></a>
### STATUS_SCHAERFEN_LESEN

Default Status_schaerfen_lesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_SCHAERFZUSTAND | string |  |
| STAT_WEGFAHRSICHERUNG_EIN | int |  |
| STAT_NEIGUNGSGEBER_EIN | int |  |
| STAT_ULTRASCHALLSCHUTZ_EIN | int |  |
| STAT_CRASH_ALARMGEBER_EIN | int |  |
| STAT_HORN_EIN | int |  |
| STAT_LED_EIN | int |  |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Default Diagnose_ende job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (40 × 3)
- [JOBRESULT](#table-jobresult) (12 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 40 rows × 3 columns

| ORT | INDEX | ORTTEXT |
| --- | --- | --- |
| 0x01 | 0x01 | EEPROM nach Power-on-Reset defekt, Kodierung verloren |
| 0x02 | 0x02 | EEPROM nach WD-Reset defekt, Kodierung verloren |
| 0x03 | 0x03 | RAM nach WD-Reset defekt |
| 0x04 | 0x04 | Reset |
| 0x05 | 0x05 | Schaerftabelle nicht beschreibbar |
| 0x06 | 0x06 | Alarmtabelle nicht beschreibbar |
| 0x07 | 0x07 | Schloss-Signale Fahrertuer ungueltig |
| 0x08 | 0x08 | Schloss-Signale Beifahrertuer ungueltig |
| 0x09 | 0x09 | Signale Infrarot ungueltig |
| 0x0A | 0x0A | Schloss-Signale Heckklappe ungueltig |
| 0x0B | 0x0B | ZS wurde 1, ohne das ein Schloss auf VR stand |
| 0x0C | 0x0C | Neigungsgeber gibt kein Quittungssignal beim Einschalten |
| 0x0D | 0x0D | Quittungsimpuls Neigungsgeber, falsche Laenge |
| 0x0E | 0x0E | Leitung NG aktiviert, obwohl Neigungsgeber nicht eingeschaltet |
| 0x0F | 0x0F | Diagnose Horn ist 0, obwohl Horn ein |
| 0x10 | 0x10 | Diagnose Horn ist 1, obwohl Horn aus (gesetzt durch BC-Alarm) |
| 0x11 | 0x11 | Diagnose Horn wird nicht 1 |
| 0x12 | 0x12 | Diagnose Horn wird nicht 0 (gesetzt durch BC-Alarm) |
| 0x13 | 0x13 | Diagnose Wegfahrsicherung ist 0, obwohl WFS ein |
| 0x14 | 0x14 | Diagnose Wegfahrsicherung ist 1, obwohl WFS aus |
| 0x15 | 0x15 | Diagnose Wegfahrsicherung wird nicht 1 |
| 0x16 | 0x16 | Diagnose Wegfahrsicherung wird nicht 0 |
| 0x17 | 0x17 | Fehler auf der Leitung Wegfahrsicherung |
| 0x18 | 0x18 | Fehler auf der Leitung ST |
| 0x19 | 0x19 | Fehler auf der Leitung CAG |
| 0x1A | 0x1A | Fehler auf der Leitung Horn |
| 0x1B | 0x1B | Fehler auf der Leitung LED |
| 0x1C | 0x1C | Watchdog Reset |
| 0x1D | 0x1D | DWA sollte schaerfen, Kl.15/R/61 war aktiv |
| 0x1E | 0x1E | Fehler auf ER1, Schloss unbekannt |
| 0x1F | 0x1F | Erstprogrammierung 1.Kopie falsch |
| 0x20 | 0x20 | Erstprogrammierung 2.Kopie falsch |
| 0x21 | 0x21 | Variantenprogrammierung 1.Kopie falsch |
| 0x22 | 0x22 | Variantenprogrammierung 2.Kopie falsch |
| 0x23 | 0x23 | Ultraschall keine Quittierung |
| 0x24 | 0x24 | Ultraschall Quittierung falsch |
| 0x25 | 0x25 | Ultraschall defekt |
| 0x26 | 0x26 | Ultraschallsensor links defekt |
| 0x27 | 0x27 | Ultraschallsensor rechts defekt |
| 0xFF | 0xFF | unbekannter Fehlerort |

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 12 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | OKAY |
| 0x01 | OKAY |
| 0x02 | OKAY |
| 0x05 | OKAY |
| 0x07 | OKAY |
| 0x0C | OKAY |
| 0x0D | OKAY |
| 0x0C | ERROR_ECU_FUNCTION |
| 0xAA | ERROR_ECU_REJECTED |
| 0x0A | ERROR_ECU_NACK |
| xxxx | OKAY |
| 0xFF | ERROR_ECU_UNKNOWN_STATUSBYTE |
