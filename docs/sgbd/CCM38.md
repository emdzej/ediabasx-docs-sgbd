# CCM38.prg

- Jobs: [17](#jobs)
- Tables: [3](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Check-Control Modul E38 |
| ORIGIN | BMW TP-422 Teepe |
| REVISION | 1.55 |
| AUTHOR | BMW TP-422 Teepe |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Default init job
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Default pruefstempel_lesen job
- [PRUEFSTEMPEL_SETZEN](#job-pruefstempel-setzen) - Default pruefstempel_setzen job
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Speicherinhaltes
- [IDENT](#job-ident) - Default IDENTIFIKATION job
- [FS_ZAEHLER](#job-fs-zaehler) - fs_zaehler job
- [FS_LESEN](#job-fs-lesen) - fs_lesen job
- [FS_LOESCHEN](#job-fs-loeschen) - Default fs_loeschen job
- [STATUS_LESEN](#job-status-lesen) - Default status job
- [SELBSTTEST](#job-selbsttest) - selbsttest job
- [CODIERUNG_LESEN](#job-codierung-lesen) - codierung_lesen job
- [LERN_BEREICH_LESEN](#job-lern-bereich-lesen) - lern_bereich_lesen job
- [MOTORKENNFELD_LESEN](#job-motorkennfeld-lesen) - MOTORKENNFELD_LESEN job
- [OELWARNSCHWELLEN_LESEN](#job-oelwarnschwellen-lesen) - auslesen Oelwarnschwellen_LESEN job
- [POWER_DOWN](#job-power-down) - POWER_DOWN job
- [DIAGNOSE_ENDE](#job-diagnose-ende) - diagnose_ende job

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

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Default pruefstempel_lesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| PRUEFSTEMPEL1 | int |  |
| PRUEFSTEMPEL2 | int |  |
| PRUEFSTEMPEL3 | int |  |

<a id="job-pruefstempel-setzen"></a>
### PRUEFSTEMPEL_SETZEN

Default pruefstempel_setzen job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WELCHER_PRUEFSTEMPEL | int | 1 bis 3 |
| WELCHES_BIT | int | 0 bis 7 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| PRUEFSTEMPEL_ALT | binary | Alter Pruefstempel |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Auslesen des Speicherinhaltes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HIGH | int | gewuenschte Startadresse high als Hexwert! |
| LOW | int | gewuenschte Startadresse low als Hexwert! |
| ANZAHL | int | gewuenschte Anzahl Datenbytes, max. 24! |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| DATEN | binary | angeforderter Datenblock (bis zu 24 Bytes!) |

<a id="job-ident"></a>
### IDENT

Default IDENTIFIKATION job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | Hardwarenummer |
| ID_COD_INDEX | int | Codierindex |
| ID_DIAG_INDEX | int | Diagnoseindex |
| ID_BUS_INDEX | int | Busindex |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferantennummer |
| ID_LIEF_TEXT | string | Lieferantenname |
| ID_SW_NR | int | Softwarenummer |

<a id="job-fs-zaehler"></a>
### FS_ZAEHLER

fs_zaehler job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ZAHL | int |  |

<a id="job-fs-lesen"></a>
### FS_LESEN

fs_lesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ZAHL | int |  |
| F_ORT_TEXT | string |  |
| F_ORT_NR | int |  |
| F_ART_ANZ | int |  |
| F_ART1_NR | int |  |
| F_UW_ANZ | int |  |
| F_ART1_TEXT | string |  |
| F_HFK | int |  |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Default fs_loeschen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Default status job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| LOW_ZEIT_OELSTAND_THERMISCH_WERT | int | 0 bis 1024 ms |
| LOW_ZEIT_OELSTAND_THERMISCH_EINH | string | ms |
| OELSTAND_DYNAMISCH_AD_WERT | int | 0 bis 5 (0-1 zu wenig Oel, 4 bis 5.0 Leitung defekt) |
| OELSTAND_DYNAMISCH_AD_EINH | string | Volt [V] |
| DATENBUS_D0_HIGH | int |  |
| DATENBUS_D1_HIGH | int |  |
| DATENBUS_D2_HIGH | int |  |
| DATENBUS_D3_HIGH | int |  |
| DATENBUS_D4_HIGH | int |  |
| DATENBUS_D5_HIGH | int |  |
| DATENBUS_D6_HIGH | int |  |
| DATENBUS_D7_HIGH | int |  |
| STAT_SICHERHEITSGURT_OFFEN | int | IC A0, aktiv low |
| STAT_ZUENDSCHLUESSEL_STECKT | int | IC A1, aktiv low |
| STAT_BREMSFLUESSIGKEITSSCHALTER_EIN | int | IC A2, aktiv low |
| STAT_PANZERTUER_OFFEN | int | IC A3, aktiv high |
| STAT_KUEHLWASSERSTAND_LOW_EIN | int | IC A4, aktiv high |
| STAT_OELSTAND_STATISCH_LOW_EIN | int | IC A6, aktiv high |
| STAT_WASCHWASSERSTAND_LOW_EIN | int | IC A7, aktiv low |
| STAT_MOTORNOTPROGRAMM_EIN | int | IC B0 |
| STAT_KAT_ZU_HEISS_EIN | int | IC B1 |
| STAT_VORGLUEHEN_EINSPRITZUNG_EIN | int | IC B3 |
| STAT_LOESCHANLAGE_DEFEKT_EIN | int | IC B4 |
| STAT_LUFTANLAGE_DEFEKT_EIN | int | IC B5 |

<a id="job-selbsttest"></a>
### SELBSTTEST

selbsttest job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| RAM_NIO | int |  |
| ROM_NIO | int |  |
| COD_DATEN_NIO | int |  |

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

codierung_lesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| PROGRAMMIERT | string | programmiert j/n |
| MOTOR_TYP | string | motorvariante |
| UEBERTEMPERATUR_CC_WERT | int |  |
| UEBERTEMPERATUR_CC_EINH | string |  |
| MELDUNG_PARKBREMSE_LOESEN_AKTIV | int | j/n |
| MELDUNG_TUER_OFFEN_AKTIV | int | j/n |
| MELDUNG_KOFFERRAUM_OFFEN_AKTIV | int | j/n |
| MELDUNG_VORGLUEHEN_AKTIV | int | j/n |
| MELDUNG_EINSPRITZANLAGE_AKTIV | int | j/n |
| MELDUNG_BREMSFLUESSIGKEIT_PRUEFEN_AKTIV | int | j/n |
| MELDUNG_STOP_OELDRUCK_MOTOR_AKTIV | int | j/n |
| MELDUNG_NIVEAUREGULIERUNG_INAKTIV_AKTIV | int | j/n |
| MELDUNG_EEPROM_CCM_AKTIV | int | j/n |
| MELDUNG_KUEHLWASSERTEMPERATUR_AKTIV | int | j/n |
| MELDUNG_BREMSLICHT_PRUEFEN_AKTIV | int | j/n |
| MELDUNG_MOTORNOTPROGRAMM_AKTIV | int | j/n |
| MELDUNG_I_BUS_CCM_OK_AKTIV | int | j/n |
| MELDUNG_ABBLENDLICHT_PRUEFEN_AKTIV | int | j/n |
| MELDUNG_STANDLICHT_PRUEFEN_AKTIV | int | j/n |
| MELDUNG_RUECKLICHT_PRUEFEN_AKTIV | int | j/n |
| MELDUNG_NEBELLICHT_VORN_PRUEFEN_AKTIV | int | j/n |
| MELDUNG_NEBELLICHT_HINTEN_PRUEFEN_AKTIV | int | j/n |
| MELDUNG_KENNZEICHENLICHT_PRUEFEN_AKTIV | int | j/n |
| MELDUNG_ANHAENGERLICHT_PRUEFEN_AKTIV | int | j/n |
| MELDUNG_GETRIEBENOTPROGRAMM_AKTIV | int | j/n |
| MELDUNG_BREMSBELAG_PRUEFEN_AKTIV | int | j/n |
| MELDUNG_OELSTAND_MOTOR_PRUEFEN_AKTIV | int | j/n |
| MELDUNG_KUEHLWASSERSTAND_PRUEFEN_AKTIV | int | j/n |
| MELDUNG_WASCHWASSER_FUELLEN_AKTIV | int | j/n |
| MELDUNG_LICHT_AN_AKTIV | int | j/n |
| MELDUNG_ZUENDSCHLUESSEL_STECKT_AKTIV | int | j/n |
| MELDUNG_BITTE_GURT_ANLEGEN_AKTIV | int | j/n |
| MELDUNG_LANGSAM_KAT_ZU_HEISS_AKTIV | int | j/n |
| MELDUNG_LIMIT_AKTIV | int | j/n |
| MELDUNG_CHECK_CONTROL_OK_AKTIV | int | j/n |
| MELDUNG_FUNKSCHLUESSEL_BATTERIE_AKTIV | int | j/n |
| MELDUNG_LANGSAM_KAT_ZU_HEISS_PREDRIVE_CHECK_AKTIV | int | j/n |
| MELDUNG_PANZERTUER_OFFEN_AKTIV | int | j/n |
| MELDUNG_LUFTANLAGE_PRUEFEN_AKTIV | int | j/n |
| MELDUNG_FEUERLOESCHANLAGE_PRUEFEN_AKTIV | int | j/n |
| MELDUNG_FERNLICHT_PRUEFEN_AKTIV | int | j/n |
| MELDUNG_RUECKFAHRLICHT_PRUEFEN_AKTIV | int | j/n |
| MELDUNG_MAX_170_KMH_AKTIV | int | j/n |
| MELDUNG_TEILNEHMER_TEXTMELDUNG_AKTIV | int | j/n |
| INTERMITTIERENDER_GONG_FUER_GURT_AKTIV | int | j/n |
| FEHLERSPEICHER_OENS_AKTIV | int | j/n |
| FEHLERSPEICHER_TOG_AKTIV | int | j/n |
| TEL_CC_SENSOR_ZUENDSCHLUESSEL_AKTIV | int | j/n |
| TEL_CC_SENSOR_GURT_ANLEGEN_AKTIV | int | j/n |
| TEL_CC_SENSOR_BREMSFLUESSIGKEIT_AKTIV | int | j/n |
| V_LIMIT_WERT | int | gesetzter Limit-Wert |
| V_LIMIT_EINH | string | km/h |
| SA_3_IC_VERBAUT | int | 3. Eingangs-IC verbaut j/n |
| SA_SICHERHEITSFAHRZEUG | int | j/n |
| OELSTANDSSENSOR | string | thermisch oder statisch/dynamisch |
| SA_ASP_VERBAUT | int | j/n |
| CC_MELDUNG_KATALYSATOR_AKTIV | int | j/n |
| CC_MELDUNG_IGONG_GURT_AKTIV | int | j/n |
| CC_MELDUNG_TEXT_GURT_AKTIV | int | j/n |
| CC_MELDUNG_ZUENDSCHLUESSEL_AKTIV | int | j/n |

<a id="job-lern-bereich-lesen"></a>
### LERN_BEREICH_LESEN

lern_bereich_lesen job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| CC_SPRACHE | string | gelernte CC-sprache |
| OELSTAND_MOTOR | int | flag OELSTAND Motor |
| GESCHWINDIGKEIT_EINH | string | km/h oder mph |

<a id="job-motorkennfeld-lesen"></a>
### MOTORKENNFELD_LESEN

MOTORKENNFELD_LESEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| MOTORKENNFELD | binary | komplettes Motorkennfeld Bytes 1 bis 17 |

<a id="job-oelwarnschwellen-lesen"></a>
### OELWARNSCHWELLEN_LESEN

auslesen Oelwarnschwellen_LESEN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| WARNSCHWELLE_OELKALT | int | Warnschwelle Oelkalt |
| WARNSCHWELLE_OELVOR | int | Warnschwelle Oelvor |
| WARNSCHWELLE_OELWARM | int | Warnschwelle Oelwarm |

<a id="job-power-down"></a>
### POWER_DOWN

POWER_DOWN job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

diagnose_ende job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (69 × 2)
- [JOBRESULT](#table-jobresult) (8 × 2)
- [LIEFERANTEN](#table-lieferanten) (27 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 69 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Parkbremse loesen |
| 0x02 | Tuer offen |
| 0x03 | Kofferraum offen |
| 0x04 | Vorgluehen |
| 0x05 | Einspritzanlage |
| 0x06 | Bremsfluessigkeit pruefen |
| 0x07 | Stop! Oeldruck Motor |
| 0x08 | Niveauregulierung inaktiv |
| 0x09 | EEPROM CCM |
| 0x0A | Kuehlwassertemperatur |
| 0x0B | Bremslicht pruefen |
| 0x0C | Motornotprogramm |
| 0x0D | I-Bus CCME38 OK |
| 0x0E | Abblendlicht pruefen |
| 0x0F | Standlicht pruefen |
| 0x10 | Ruecklicht pruefen |
| 0x11 | Nebellicht vorn pruefen |
| 0x12 | Nebellicht hinten pruefen |
| 0x13 | Kennzeichenlicht pruefen |
| 0x14 | Anhaengerlicht pruefen |
| 0x15 | Getriebenotprogramm |
| 0x16 | Bremsbelag pruefen |
| 0x17 | Oelstand Motor pruefen |
| 0x18 | Kuehlwasserstand pruefen |
| 0x19 | Motornotprogramm |
| 0x1A | Waschwasser fuellen |
| 0x1B | Licht an ? |
| 0x1C | Zuendschluessel steckt |
| 0x1D | Gurt anlegen |
| 0x1E | Langsam! Kat zu heiss |
| 0x1F | LIMIT |
| 0x20 | EDC inaktiv |
| 0x21 | Servotronic inaktiv |
| 0x22 | CHECK CONTROL OK |
| 0x23 | Funkschluessel Batterie |
| 0x24 | Langsam! Kat zu heiss |
| 0x25 | Panzertuer Gepaeckraum |
| 0x26 | Luftanlage pruefen |
| 0x27 | Feuerloeschanlage pruefen |
| 0x28 | Fernlicht pruefen |
| 0x29 | Rueckfahrlicht pruefen |
| 0x2A | CC Text 42 |
| 0x2B | CC Text 43 |
| 0x2C | CC Text 44 |
| 0x2D | CC Text 45 |
| 0x2E | CC Text 46 |
| 0x2F | CC Text 47 |
| 0x30 | CC Text 48 |
| 0x31 | CC Text 49 |
| 0x32 | CC Text 50 |
| 0x33 | CC Text 51 |
| 0x34 | CC Text 52 |
| 0x35 | CC Text 53 |
| 0x36 | CC Text 54 |
| 0x37 | CC Text 55 |
| 0x38 | CC Text 56 |
| 0x39 | CC Text 57 |
| 0x3A | CC Text 58 |
| 0x3B | CC Text 59 |
| 0x3C | Schwimmerschalter statisch/dynamisch |
| 0x3D | thermischer Oelstandssensor |
| 0x3E | F3 Oelstand Sensor thermisch |
| 0x46 | Checksumme Codierdaten |
| 0x47 | COP Monitor Reset / Quarzausfall |
| 0x49 | Fehler EEPROM schreiben |
| 0x4A | Fehler EEPROM loeschen |
| 0x4B | Fehler Watchdog |
| 0x4C | Fehler illegal Opcode |
| 0xFF | unbekannter Fehlerort |

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
