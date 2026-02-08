# SMG.prg

- Jobs: [14](#jobs)
- Tables: [35](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Getriebesteuerung SMG |
| ORIGIN | BMW TP-421 Mellersh |
| REVISION | 2.04 |
| AUTHOR | BMW TP-421 Mellersh, BMW-M ZS-E-53 J.Weber, BMW TP-421 Teepe |
| COMMENT | Originalfile GS834.src geaendert fuer SMG |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Init-Job fuer EGS
- [INFO](#job-info) - Information SGBD
- [IDENT](#job-ident) - Ident-Daten fuer EGS
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender-Info-Feldes
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen fuer EGS
- [CODIER_CS_PRUEFEN](#job-codier-cs-pruefen) - Ueberpruefen der Codier-Checksumme fuer EGS
- [STATUS_IO_LESEN](#job-status-io-lesen) - Status Eingaenge SMG
- [SPEICHER_LESEN](#job-speicher-lesen) - Speicher Lesen
- [STEUERN_STELLGLIED](#job-steuern-stellglied) - Ansteuern der Stellglieder
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [TESTPRG_STARTEN](#job-testprg-starten) - Testprogramm starten
- [TEST_PRG_STOP](#job-test-prg-stop) - Beenden eines laufenden Testprogrammes
- [COD_ADAPT_LESEN](#job-cod-adapt-lesen) - Codierdaten oder Adaptionswerte Lesen

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Init-Job fuer EGS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

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

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer EGS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | string | Codier-Index |
| ID_DIAG_INDEX | string | Diagnose-Index |
| ID_BUS_INDEX | string | Bus-Index |
| ID_DATUM_KW | string | Herstelldatum KW |
| ID_DATUM_JAHR | string | Herstelldatum Jahr |
| ID_LIEF_NR | string | Lieferanten-Nummer |
| ID_SW_NR | string | Softwarenummer |
| ID_SN_NR | string | Seriennummer |
| _TEL_ANTWORT | binary |  |

<a id="job-aif-lesen"></a>
### AIF_LESEN

Auslesen des Anwender-Info-Feldes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| AIF_ADRESSE | long | AIF Basisadresse |
| AIF_FG_NR | string | Fahrgestellnummer |
| AIF_DATUM | string | Fertigungsdatum |
| AIF_AENDERUNGS_INDEX | string | Aenderungsindex |
| AIF_SW_NR | long | Softwarenummer |
| AIF_BEHOERDEN_NR | long | Behoerdennummer |
| AIF_ZB_NR | long | Zusbaunummer |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| F_ANZ_NR | int | Anzahl aller gespeicherter Fehler (max. 5) |
| F_ORT_NR | int | momentan identisch Fehlerbyte |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_HFK | int | Wertebereich 0 - 31 |
| F_ART_ANZ | int | immer 1 |
| F_ART1_NR | int | Index der Fehlernummer |
| F_ART1_TEXT | string | Fehlerart als Text |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen bei SMG immer 2 |
| F_UW1_NR | int | Index der 1. Umweltbedingung, 1.Satz |
| F_UW1_TEXT | string | Text der 1. Umweltbedingung, 1.Satz |
| F_UW1_WERT | int | Wert der 1. Umweltbedingung, 1.Satz |
| F_UW1_EINH | string | Einheit |
| F_UW2_NR | int |  |
| F_UW2_TEXT | string |  |
| F_UW2_WERT | int |  |
| F_UW2_EINH | string | Einheit |
| _TEL_ANTWORT | binary |  |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen fuer EGS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| TELEGRAMM_ANT | binary | Antworttelegramm |

<a id="job-codier-cs-pruefen"></a>
### CODIER_CS_PRUEFEN

Ueberpruefen der Codier-Checksumme fuer EGS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| CS_STATUS_DATEN | string | Datenbereich OKAY, FEHLER |
| CS_STATUS_POINTER | string | Pointerbereich OKAY, FEHLER |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-status-io-lesen"></a>
### STATUS_IO_LESEN

Status Eingaenge SMG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_MOTORDREHZAHL_WERT | int |  |
| STAT_MOTORDREHZAHL_EINH | string |  |
| STAT_EINGANGSDREHZAHL_WERT | int | Getriebeeingangsdrehzahl |
| STAT_EINGANGSDREHZAHL_EINH | string | Getriebeeingangsdrehzahl |
| STAT_AUSGANGSDREHZAHL_WERT | int | Getriebeausgangsdrehzahl |
| STAT_AUSGANGSDREHZAHL_EINH | string | Getriebeausgangsdrehzahl |
| STAT_GESCHWINDIGKEIT_WERT | int | Fahrzeuggeschwindigkeit |
| STAT_GESCHWINDIGKEIT_EINH | int | Fahrzeuggeschwindigkeit |
| STAT_RADDREHZAHL_VL_WERT | int |  |
| STAT_RADDREHZAHL_VL_EINH | string |  |
| STAT_RADDREHZAHL_VR_WERT | int |  |
| STAT_RADDREHZAHL_VR_EINH | string |  |
| STAT_RADDREHZAHL_HL_WERT | int |  |
| STAT_RADDREHZAHL_HL_EINH | string |  |
| STAT_RADDREHZAHL_HR_WERT | int |  |
| STAT_RADDREHZAHL_HR_EINH | string |  |
| STAT_PWG_WERT | int | PWG adaptiert |
| STAT_PWG_EINH | string | PWG adaptiert |
| STAT_WDK_WERT | int | WDK adaptiert |
| STAT_WDK_EINH | string | WDK adaptiert |
| STAT_MOTORMOMENT_WERT | int | Motormoment |
| STAT_MOTORMOMENT_EINH | string | Motormoment |
| STAT_MOTORTEMPERATUR_WERT | int | MOTORTEMPERATUR |
| STAT_MOTORTEMPERATUR_EINH | string | MOTORTEMPERATUR |
| STAT_GETRIEBETEMPERATUR_WERT | int | Getriebeoeltemperatur |
| STAT_GETRIEBETEMPERATUR_EINH | string | Getriebeoeltemperatur |
| STAT_LUFTTEMPERATUR_WERT | int | Ansauglufttemperatur |
| STAT_LUFTTEMPERATUR_EINH | string | Ansauglufttemperatur |
| STAT_POS_KUP_WERT | int | Position Kupplung |
| STAT_POS_KUP_EINH | string | Position Kupplung |
| STAT_POS_GANG_WERT | int | Position Gang |
| STAT_POS_GANG_EINH | string | Position Gang |
| STAT_POS_GASSE_WERT | int | Position Gasse |
| STAT_POS_GASSE_EINH | string | Position Gasse |
| STAT_GANG_WERT | int | 0.1.2.3.4.5.6.7., 7 = R-Gang, 0=Neutral |
| STAT_GANG_TEXT | string | 0.1.2.3.4.5.6.R. Gang |
| STAT_POS_WH_WERT | int | Position Waehlhebel |
| STAT_POS_WH_EINH | string | Position Waehlhebel |
| STAT_STROM_KUP_WERT | int | Strom Kupplung |
| STAT_STROM_KUP_EINH | string | Strom Kupplung |
| STAT_STROM_GASSE_WERT | int | Strom Gasse |
| STAT_STROM_GASSE_EINH | string | Strom Gasse |
| STAT_STROM_GANG_V_WERT | int | Strom Gang vor |
| STAT_STROM_GANG_V_EINH | string | Strom Gang vor |
| STAT_STROM_GANG_R_WERT | int | Strom Gang rueck |
| STAT_STROM_GANG_R_EINH | string | Strom Gang rueck |
| STAT_UBAT_WERT | long | UBat |
| STAT_UBAT_EINH | string | UBat |
| STAT_USENS_WERT | int | Sensorversorgungsspannung |
| STAT_USENS_EINH | string | Sensorversorgungsspannung |
| STAT_PHYD_WERT | int | Hydraulikdruck |
| STAT_PHYD_EINH | string | Hydraulikdruck |
| STAT_AQUER_WERT | int | Querbeschleunigung |
| STAT_AQUER_EINH | string | Querbeschleunigung |
| STAT_WHS1_EIN | int | Waehlhebel Schalter1 0 oder 1 |
| STAT_WHS2_EIN | int | Waehlhebel Schalter2 0 oder 1 |
| STAT_WH_MANUELL_EIN | int | Waehlhebel Schalter Manuell 0 oder 1 |
| STAT_SHIFT_UP_EIN | int | Schrittschalter Gang hoch 0 oder 1 |
| STAT_SHIFT_DOWN_EIN | int | Schrittschalter Gang rueck 0 oder 1 |
| STAT_PROG_TASTER_W_EIN | int | Programmtaster * Winter ein |
| STAT_BREMSSIGNAL1_EIN | int | 0 oder 1 |
| STAT_BREMSSIGNAL2_EIN | int | 0 oder 1 |
| STAT_HANDBREMSE_EIN | int | 0 oder 1 |
| STAT_LL_EIN | int | Leerlaufschalter 0 oder 1 |
| STAT_KICK_DOWN_EIN | int | 0 oder 1 |
| STAT_KLR_EIN | int | Zuendung Klemme R 0 oder 1 |
| STAT_KL15_EIN | int | Zuendung Klemme 15 0 oder 1 |
| STAT_KL50_EIN | int | Zuendung Klemme 50 0 oder 1 |
| STAT_MOTORHAUBE1_EIN | int | Motorhaubenkontakt1 0 oder 1 |
| STAT_MOTORHAUBE2_EIN | int | Motorhaubenkontakt2 0 oder 1 |
| STAT_FGR_AKTIV_EIN | int | FGR aktiv 0 oder 1 |
| STAT_ABS_REGELT_EIN | int | 0 oder 1, passiv oder aktiv |
| STAT_TUERE_EIN | int | Tuerkontakt 0 oder 1 |
| STAT_KUPPLUNG | string | Kupplungsstatus 0,1,2 oder 3 |
| STAT_GETRIEBE | string | Getriebestatus 0,1,2,3,4,5 oder 9 |
| STAT_ALAENGS_WERT | int | Querbeschleunigung |
| STAT_ALAENGS_EINH | string | Querbeschleunigung |
| STAT_PRG_ECON_EIN | int | Programmwahlschalter Economy 0 oder 1 |
| STAT_PRG_SPORT_EIN | int | Programmwahlschalter Sport 0 oder 1 |
| STAT_LAENGS_G_WERT | int | Laengsbeschleunigung |
| STAT_LAENGS_G_EINH | string | Laengsbeschleunigung |
| STAT_KONST_FAHRT_EIN | int | Tempomat-Konstantfahrt |
| STAT_WIEDER_EIN | int | Tempomat-Wiederaufnahme |
| STAT_BESCHL_EIN | int | Tempomat-Setzen Beschleunigung |
| STAT_VERZOEG_EIN | int | Tempomat-Setzen Verzoegern |
| STAT_FEHLER_EIN | int | Tempomat-Fehler |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Speicher Lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPEICHERART | string | Speicherart: FLASH, RAM, ROM, E2PROM |
| ADRESSE | long | Startadresse |
| ANZAHL | int | Anzahl zu lesender Bytes |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| DATEN | binary | Inhalt der Speicherzellen |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| TELEGRAMM_ANT | binary | Antworttelegramm |

<a id="job-steuern-stellglied"></a>
### STEUERN_STELLGLIED

Ansteuern der Stellglieder

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STELLGL | string | Anzusteuerndes Stellglied table Stellglieder STELLGLIED PIN |
| STEUERART1 | string | Steuerungsart: POSITIONSVORGABE STROMVORGABE INAKTIV AKTIV |
| STEUERART2 | int | Steuerungsart: abhaengig von Stellglied - siehe Lastenheft |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_ANSTEUERUNG | int | Ansteuerergebnis 0 : Stellglied wird ordnungsgemaess angesteuert 1 : Pin-Nr ist unbekannt 2 : nicht gueltig 3 : nicht gueltig 4 : Stellglied nicht ansteuerbar |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| TELEGRAMM_ANT | binary | Antworttelegramm |

<a id="job-testprg-starten"></a>
### TESTPRG_STARTEN

Testprogramm starten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TESTPRG_NR | int | Nummer des Testprogrammes |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| TEST_STATUS | string | 2, wenn beendet |
| TEST_STATUS_BYTE | int | kann Wert 0,2 oder 3 annehmen, Wert 1 (BUSY) wird im Job abgefangen |
| INFO_STATUS_BYTE | int | Inhalt Byte 3 |
| INFO_STATUS | string | Nur bei Getriebeadaption, wird auf alle erweitert |
| TELEGRAMM_ANT | binary | Antworttelegramm |

<a id="job-test-prg-stop"></a>
### TEST_PRG_STOP

Beenden eines laufenden Testprogrammes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-cod-adapt-lesen"></a>
### COD_ADAPT_LESEN

Codierdaten oder Adaptionswerte Lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| COD_ADAPT | int | Auswahl Codierdaten oder Adaptionswerte Lesen (00 oder 01) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| DATEN | binary | Inhalt der Speicherzellen |
| OSSWW_WERT | int | Adaptionswert |
| OSSWW_EINH | string | Adaptionswert |
| WWG1_WERT | int | Adaptionswert |
| WWG1_EINH | string | Adaptionswert |
| WWG2_WERT | int | Adaptionswert |
| WWG2_EINH | string | Adaptionswert |
| WWG3_WERT | int | Adaptionswert |
| WWG3_EINH | string | Adaptionswert |
| WWG4_WERT | int | Adaptionswert |
| WWG4_EINH | string | Adaptionswert |
| WWG5_WERT | int | Adaptionswert |
| WWG5_EINH | string | Adaptionswert |
| WWG6_WERT | int | Adaptionswert |
| WWG6_EINH | string | Adaptionswert |
| WWGR_WERT | int | Adaptionswert |
| WWGR_EINH | string | Adaptionswert |
| SWN_WERT | int | Adaptionswert |
| SWN_EINH | string | Adaptionswert |
| SWAGG_WERT | int | Adaptionswert |
| SWAGG_EINH | string | Adaptionswert |
| SWAUG_WERT | int | Adaptionswert |
| SWAUG_EINH | string | Adaptionswert |
| WW1D3_WERT | int | Adaptionswert-Differenz |
| WW1D3_EINH | string | Adaptionswert-Differenz |
| WW3D5_WERT | int | Adaptionswert-Differenz |
| WW3D5_EINH | string | Adaptionswert-Differenz |
| WWRD1_WERT | int | Adaptionswert-Differenz |
| WWRD1_EINH | string | Adaptionswert-Differenz |
| SWAGUD_WERT | int | Adaptionswert-Differenz |
| SWAGUD_EINH | string | Adaptionswert-Differenz |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| TELEGRAMM_ANT | binary | Antworttelegramm |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (8 × 2)
- [FORTTEXTE](#table-forttexte) (48 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (24 × 6)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [SPEICHER](#table-speicher) (4 × 2)
- [STELLGLIEDER](#table-stellglieder) (11 × 2)
- [STATTESTTEXTE](#table-stattesttexte) (5 × 2)
- [INFOTEXTE1A](#table-infotexte1a) (2 × 2)
- [INFOTEXTE2A](#table-infotexte2a) (2 × 2)
- [INFOTEXTE3A](#table-infotexte3a) (2 × 2)
- [INFOTEXTE4A](#table-infotexte4a) (11 × 2)
- [INFOTEXTE5A](#table-infotexte5a) (22 × 2)
- [INFOTEXTE6A](#table-infotexte6a) (8 × 2)
- [INFOTEXTE7A](#table-infotexte7a) (5 × 2)
- [INFOTEXTE8A](#table-infotexte8a) (19 × 2)
- [INFOTEXTE9A](#table-infotexte9a) (4 × 2)
- [INFOTEXTE10A](#table-infotexte10a) (3 × 2)
- [INFOTEXTE11A](#table-infotexte11a) (2 × 2)
- [INFOTEXTE12A](#table-infotexte12a) (2 × 2)
- [INFOTEXTE13A](#table-infotexte13a) (6 × 2)
- [INFOTEXTE14A](#table-infotexte14a) (3 × 2)
- [INFOTEXTE1F](#table-infotexte1f) (4 × 2)
- [INFOTEXTE2F](#table-infotexte2f) (3 × 2)
- [INFOTEXTE3F](#table-infotexte3f) (7 × 2)
- [INFOTEXTE4F](#table-infotexte4f) (16 × 2)
- [INFOTEXTE5F](#table-infotexte5f) (10 × 2)
- [INFOTEXTE6F](#table-infotexte6f) (6 × 2)
- [INFOTEXTE7F](#table-infotexte7f) (10 × 2)
- [INFOTEXTE8F](#table-infotexte8f) (46 × 2)
- [INFOTEXTE9F](#table-infotexte9f) (5 × 2)
- [INFOTEXTE10F](#table-infotexte10f) (3 × 2)
- [INFOTEXTE11F](#table-infotexte11f) (4 × 2)
- [INFOTEXTE12F](#table-infotexte12f) (4 × 2)
- [INFOTEXTE13F](#table-infotexte13f) (5 × 2)
- [INFOTEXTE14F](#table-infotexte14f) (6 × 2)

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

Dimensions: 48 rows × 5 columns

| ORT | ORTTEXT | UW_1 | UW_2 | UW_3 |
| --- | --- | --- | --- | --- |
| 0x01 | CAN fehlerhafter Wert | 0x06 | 0x01 | 0x00 |
| 0x03 | Getriebeoeltemperatur | 0x08 | 0x07 | 0x00 |
| 0x05 | Hydropumpe dauernd angesteuert | 0x0B | 0x0C | 0x00 |
| 0x07 | Raddrehzahl hinten links | 0x04 | 0x0D | 0x00 |
| 0x08 | Anlasserfreigabe | 0x09 | 0x0D | 0x00 |
| 0x0A | Magnetventil Kupplung | 0x0C | 0x09 | 0x00 |
| 0x0D | Motorhaubenkontakt bei Fahrt | 0x04 | 0x10 | 0x00 |
| 0x12 | Waehlhebel Schalter M | 0x0F | 0x0E | 0x00 |
| 0x13 | Tuerkontakt | 0x09 | 0x0D | 0x00 |
| 0x1A | Positionsgeber Gasse (Waehlwinkel) | 0x11 | 0x12 | 0x00 |
| 0x1B | Batteriespannung | 0x09 | 0x06 | 0x00 |
| 0x1D | Sensor Laengsbeschleunigung | 0x12 | 0x04 | 0x00 |
| 0x1E | Waehlhebel Positionsgeber Gasse A | 0x0F | 0x12 | 0x00 |
| 0x22 | Raddrehzahl vorne links | 0x04 | 0x0D | 0x00 |
| 0x28 | Magnetventil Gasse | 0x0C | 0x09 | 0x00 |
| 0x33 | Sensor Spannungsversorgung | 0x12 | 0x09 | 0x00 |
| 0x34 | Handbremse immer aktiv | 0x04 | 0x0D | 0x00 |
| 0x36 | Positionsgeber Gang (Schaltweg) | 0x11 | 0x12 | 0x00 |
| 0x37 | Positionsgeber Kupplung | 0x0C | 0x12 | 0x00 |
| 0x38 | Hydraulikdruck | 0x12 | 0x09 | 0x00 |
| 0x39 | Sensor Querbeschleunigung | 0x12 | 0x04 | 0x00 |
| 0x3A | Fahrpedal | 0x02 | 0x12 | 0x00 |
| 0x3E | Funktionsanzeige / Summer | 0x09 | 0x04 | 0x00 |
| 0x3F | Getriebeeingangsdrehzahl | 0x05 | 0x06 | 0x00 |
| 0x40 | Raddrehzahl vorne rechts | 0x04 | 0x0D | 0x00 |
| 0x41 | Raddrehzahl hinten rechts | 0x04 | 0x0D | 0x00 |
| 0x42 | Ganganzeige Protokollfehler | 0x15 | 0x15 | 0x00 |
| 0x46 | Kick Down Schalter | 0x13 | 0x12 | 0x00 |
| 0x48 | Magnetventil Gang vor | 0x0C | 0x09 | 0x00 |
| 0x49 | Waehlhebel Schalter Automatikgasse | 0x0F | 0x0E | 0x00 |
| 0x4C | Magnetventil Gang rueck | 0x0C | 0x09 | 0x00 |
| 0x4E | Signal Betriebsbremse | 0x0A | 0x09 | 0x00 |
| 0x4F | Schnittstelle FGR | 0x04 | 0x06 | 0x00 |
| 0x57 | Leerlauf-Schalter | 0x13 | 0x12 | 0x00 |
| 0x58 | Motordrehzahl | 0x06 | 0x03 | 0x00 |
| 0x64 | Steuergeraetefehler | 0x09 | 0x0D | 0x00 |
| 0x65 | CAN Bus Fehler | 0x06 | 0x01 | 0x00 |
| 0x69 | Hydropumpe Ausfall | 0x0B | 0x0C | 0x00 |
| 0x6B | Raddrehzahlen alle | 0x04 | 0x0D | 0x00 |
| 0x71 | Motorhaubenkontakt im Stehen | 0x04 | 0x10 | 0x00 |
| 0x82 | Waehlhebel Automatikgasse | 0x0F | 0x0E | 0x00 |
| 0x9C | Druckverlust im System | 0x0D | 0x06 | 0x00 |
| 0x9E | Fahrpedal und DK-Poti defekt | 0x06 | 0x12 | 0x00 |
| 0xBC | Motordrehzahl DME fehlerhaft | 0x06 | 0x05 | 0x00 |
| 0xC8 | Adaption unvollstaendig | 0x14 | 0x14 | 0x00 |
| 0xC9 | Getriebefehler | 0x15 | 0x16 | 0x00 |
| 0xCA | Anfahrgaenge | 0x15 | 0x16 | 0x00 |
| 0xFF | unbekannter Fehlerort | 0x06 | 0x08 | 0x00 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 24 rows × 6 columns

| LABEL | UWTEXT | UW_EINH | UW_MULT | UW_DIV | UW_ADD |
| --- | --- | --- | --- | --- | --- |
| 0x01 | Fehlerinfo CAN | - | 1 | 1 | 0 |
| 0x02 | Drosselklappenwinkel | % | 100 | 255 | 0 |
| 0x03 | Motordrehzahl ueber CAN | % | 100 | 255 | 0 |
| 0x04 | Fahrzeuggeschwindigkeit | km/h | 2 | 1 | 0 |
| 0x05 | Getriebeeingangsdrehzahl | 1/min | 40 | 1 | 0 |
| 0x06 | Motordrehzahl | 1/min | 40 | 1 | 0 |
| 0x07 | Motortemperatur | Grad C | 1 | 1 | -48 |
| 0x08 | Getriebeoeltemperatur | Grad C | 1 | 1 | -55 |
| 0x09 | Batteriespannung | mV | 16 | 198 | 0 |
| 0x0A | Status Betriebsbremse | - | 1 | 1 | 0 |
| 0x0B | Hydraulikstatus | - | 1 | 1 | 0 |
| 0x0C | Hydraulikdruck | bar | 255 | 128 | -26 |
| 0x0D | Ansauglufttemperatur | Grad C | 1 | 1 | -48 |
| 0x0E | Potispannung Waehlhebel | mV | 255 | 13 | 0 |
| 0x0F | Status Waehlhebel | - | 1 | 1 | 0 |
| 0x10 | Status Haubenkontakt | - | 1 | 1 | 0 |
| 0x11 | Gang Getriebeuebersetzung | - | 1 | 1 | 0 |
| 0x12 | Spannungsversorgung Sensor | mv | 235 | 6 | 0 |
| 0x13 | Analogwert Fahrpedal | mV | 255 | 13 | 0 |
| 0x14 | Testprogramm  | - | 1 | 1 | 0 |
| 0x15 | Zielgang/Gang | - | 1 | 1 | 0 |
| 0x16 | Gang Fehlerart | - | 1 | 1 | 0 |
| 0x17 | Keine Umweltbedingung | - | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | XY | 1 | 1 | 0 |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | sporadischer Fehler |
| 0x01 | Fehler momentan vorhanden |
| 0xFF | unbekannte Fehlerart |

<a id="table-speicher"></a>
### SPEICHER

Dimensions: 4 rows × 2 columns

| SPEICHER | WERT |
| --- | --- |
| FLASH | 0x00 |
| RAM | 0x01 |
| ROM | 0x02 |
| E2PROM | 0x12 |

<a id="table-stellglieder"></a>
### STELLGLIEDER

Dimensions: 11 rows × 2 columns

| STELLGLIED | PIN |
| --- | --- |
| MAGNETVENTIL_KUPPLUNG | 0x0A |
| MAGNETVENTIL_GASSE | 0x28 |
| MAGNETVENTIL_GANG_VOR | 0x48 |
| MAGNETVENTIL_GANG_R | 0x4C |
| ANLASSER_FREIGABE | 0x08 |
| HYDROPUMPE | 0x05 |
| TEMPOMAT_AUS | 0x3B |
| GONG | 0x3D |
| WARNLAMPE | 0x3E |
| SHIFTLOCK | 0x21 |
| KOMBI | 0x42 |

<a id="table-stattesttexte"></a>
### STATTESTTEXTE

Dimensions: 5 rows × 2 columns

| STB | TEST_STATUS_TEXT |
| --- | --- |
| 0x00 | Testbedingung nicht erfuellt |
| 0x01 | Testprogramm laeuft |
| 0x02 | Testprogramm beendet |
| 0x03 | Testprogramm nicht ordnungsgemaess beendet |
| 0xFF | Unbekannter Status |

<a id="table-infotexte1a"></a>
### INFOTEXTE1A

Dimensions: 2 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Adaption laeuft |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte2a"></a>
### INFOTEXTE2A

Dimensions: 2 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Adaption laeuft |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte3a"></a>
### INFOTEXTE3A

Dimensions: 2 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Adaption laeuft |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte4a"></a>
### INFOTEXTE4A

Dimensions: 11 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Warten auf Waehlhebel A, Start der Pruefung mit Bremse |
| 0x01 | Hydroanschluss SWV 1. mal pruefen |
| 0x02 | Hydroanschluss SWR 1. mal pruefen |
| 0x03 | Hydroanschluss WW  1. mal pruefen |
| 0x04 | Hydroanschluss KU  1. mal pruefen |
| 0x05 | Hydroanschluss SWV 2. mal pruefen |
| 0x06 | Hydroanschluss SWR 2. mal pruefen |
| 0x07 | Hydroanschluss WW  2. mal pruefen |
| 0x08 | Hydroanschluss KU  2. mal pruefen |
| 0x09 | Ende der Anschlussplausibilitaet |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte5a"></a>
### INFOTEXTE5A

Dimensions: 22 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Warten auf Waehlhebel A, Start des Entlueftens mit Bremse |
| 0x01 | Warten auf Betriebsdruck fuer 1. WW-Entlueftung |
| 0x02 | WW 1. mal entlueften |
| 0x03 | Warten auf Betriebsdruck fuer 1. SW-Entlueftung |
| 0x04 | SW 1. mal entlueften |
| 0x05 | Warten auf 2. Entlueftungszyklus |
| 0x06 | Warten auf Betriebsdruck fuer 2. WW-Entlueftung |
| 0x07 | WW 2. mal entlueften |
| 0x08 | Warten auf Betriebsdruck fuer 2. SW-Entlueftung |
| 0x09 | SW 2. mal entlueften |
| 0x0A | Warten auf 3. Entlueftungszyklus |
| 0x0B | Warten auf Betriebsdruck fuer 3. WW-Entlueftung |
| 0x0C | WW 3. mal entlueften |
| 0x0D | Warten auf Betriebsdruck fuer 3. SW-Entlueftung |
| 0x0E | SW 3. mal entlueften |
| 0x0F | Warten auf Entlueftungsventilpruefung |
| 0x10 | Warten auf Betriebsdruck fuer WW-Entlueftungsventilpruefung |
| 0x11 | WW-Entlueftungsventil pruefen |
| 0x12 | Warten auf Betriebsdruck fuer SW-Entlueftungsventilpruefung |
| 0x13 | SW-Entlueftungsventil pruefen |
| 0x14 | Ende der Aktuatorentlueftung |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte6a"></a>
### INFOTEXTE6A

Dimensions: 8 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Adaption laeuft |
| 0x01 | Kupplung oeffnen |
| 0x02 | Mittellage positionieren |
| 0x03 | Waehlhebelposition R einlernen, Start mit Bremse |
| 0x04 | Waehlhebelposition N einlernen, Start mit Bremse |
| 0x05 | Waehlhebelposition E einlernen, Start mit Bremse |
| 0x06 | in NV RAM schreiben |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte7a"></a>
### INFOTEXTE7A

Dimensions: 5 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x01 | Kupplung oeffnen |
| 0x02 | Mittellage positionieren |
| 0x06 | in NV RAM schreiben |
| 0x07 | Waehlwinkeloffsetstromadaption |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte8a"></a>
### INFOTEXTE8A

Dimensions: 19 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Adaption laeuft |
| 0x01 | Kupplung oeffnen |
| 0x02 | Mittellage positionieren |
| 0x06 | in NV RAM schreiben |
| 0x07 | Waehlwinkeloffsetstromadaption |
| 0x08 | Waehlwinkel Verfahrweg testen |
| 0x09 | Vorwaertsgang E ist eingelegt- Start der Adaption mit Bremse |
| 0x0A | Waehlwinkel R einlegen - Start der Adaption mit Bremse |
| 0x0B | Gang 1 ausmessen |
| 0x0C | Gang 2 ausmessen |
| 0x0D | Gang 3 ausmessen |
| 0x0E | Gang 4 ausmessen |
| 0x0F | Gang 5 ausmessen |
| 0x10 | Gang 6 ausmessen |
| 0x11 | Gang R ausmessen |
| 0x12 | Neutralstellung einnehmen |
| 0x14 | Waehlwinkel N einlegen - Start mit Bremse |
| 0x15 | Bowdenzug testen |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte9a"></a>
### INFOTEXTE9A

Dimensions: 4 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Adaption laeuft |
| 0x28 | Kupplung ist geschlossen, wird geoeffnet |
| 0x29 | Kupplung ist offen, wird geschlossen |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte10a"></a>
### INFOTEXTE10A

Dimensions: 3 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Adaption laeuft |
| 0x20 | Fahrpedal durchtreten |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte11a"></a>
### INFOTEXTE11A

Dimensions: 2 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Adaption laeuft |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte12a"></a>
### INFOTEXTE12A

Dimensions: 2 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Adaption laeuft |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte13a"></a>
### INFOTEXTE13A

Dimensions: 6 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Adaption laeuft |
| 0x01 | Initialisierung |
| 0x02 | Initialisierung |
| 0x03 | Maximale Ueberdeckung einlernen |
| 0x04 | Minimale Ueberdeckung einlernen |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte14a"></a>
### INFOTEXTE14A

Dimensions: 3 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x01 | SW auf Mittellage positionieren |
| 0x02 | Ende der Schaltwegmittellagepositionierung |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte1f"></a>
### INFOTEXTE1F

Dimensions: 4 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x22 | Fahrpedalnullstellung groesser 240 Bit (1,17V) |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft, oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte2f"></a>
### INFOTEXTE2F

Dimensions: 3 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0xA0 | Testbedingung nicht erfuellt (Motor oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte3f"></a>
### INFOTEXTE3F

Dimensions: 7 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x24 | Schleifpunkt zu klein |
| 0x25 | Schleifpunkt zu gross |
| 0x26 | keine Getriebedrehzahl |
| 0x27 | Schleifpunkt konnte nicht eingelernt werden |
| 0xA0 | Testbedingung nicht erfuellt (Motor ist aus, Gang eingelegt oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte4f"></a>
### INFOTEXTE4F

Dimensions: 16 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x0B | SWV hat keine Funktion |
| 0x0C | SWV ist an SWR angeschlossen |
| 0x0D | SWV ist an WW angeschlossen |
| 0x0F | SWR hat keine Funktion |
| 0x10 | SWR ist an SWV angeschlossen |
| 0x11 | SWR ist an WW angeschlossen |
| 0x13 | WW hat keine Funktion |
| 0x14 | WW ist an SWV angeschlossen |
| 0x15 | WW ist an SWR angeschlossen |
| 0x17 | KU ist an SWV angeschlossen |
| 0x18 | KU ist an SWR angeschlossen |
| 0x19 | KU ist an WW angeschlossen |
| 0x1B | Hydraulikanschluesse sind i.O. |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte5f"></a>
### INFOTEXTE5F

Dimensions: 10 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x1C | Betriebsdruck fuer WW-Entlueftung nicht erreicht |
| 0x1D | WW-Entlueftung n.i.O. / Entlueftungsventil oeffnet nicht richtig |
| 0x1E | WW-Entlueftungsventil schliesst nicht richtig |
| 0x1F | Betriebsdruck fuer SW-Entlueftung nicht erreicht |
| 0x20 | SW-Entlueftung n.i.O. / Entlueftungsventil oeffnet nicht richtig |
| 0x21 | SW-Entlueftungsventil schliesst nicht richtig |
| 0x22 | Aktuator ist entlueftet, Entlueftung i.O. |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte6f"></a>
### INFOTEXTE6F

Dimensions: 6 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x1E | Schaltwegposition nicht auf Mittellage positionierbar |
| 0x1F | Keine gueltige Mittellage gefunden |
| 0x28 | Die Bestaetigung der Waehlhebelposition geschah bei nicht aktiviertem Schalter |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte7f"></a>
### INFOTEXTE7F

Dimensions: 10 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x0A | Wert WW-offsetstrom zu gross |
| 0x14 | Speichern in NV-RAM nicht moeglich |
| 0x1E | Schaltwegposition nicht auf Mittellage positionierbar |
| 0x1F | Keine gueltige Mittellage gefunden |
| 0x20 | Kein gueltiger Waehlwinkeloffsetstrom |
| 0x28 | Die Bestaetigung der Waehlhebelposition geschah bei nicht aktiviertem Schalter |
| 0x3C | Waehlwinkelregler nicht adaptiert |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte8f"></a>
### INFOTEXTE8F

Dimensions: 46 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Minimaler Abstand li/re zu gering |
| 0x02 | Endstellung gerade Gaenge zu unterschiedlich |
| 0x03 | Endstellung ungerade Gaenge zu unterschiedlich |
| 0x04 | Endstellung R-Gang zu ungerade Gaenge zu unterschiedlich |
| 0x05 | Minimale Waehlwinkel-Fenstergroesse zu gering |
| 0x06 | mimimale Fenstergroesse fuer R unterschritten |
| 0x0A | Waehlwinkelstromoffset zu gross |
| 0x0B | Schaltwegendstellung gerade Gaenge zu gross |
| 0x0C | Schaltwegendstellung ungerade Gaenge zu gross |
| 0x0D | Schaltwegendstellung Neutral zu gross |
| 0x0E | Waehlwinkel Neutral zu gross |
| 0x0F | Waehlwinkel Gang 1 und 2 zu gross |
| 0x10 | Waehlwinkel Gang 3 und 4 zu gross |
| 0x11 | Waehlwinkel Gang 5 und 6 zu gross |
| 0x12 | Waehlwinkel Gang R zu gross |
| 0x14 | NVRAM Waehlwinkeloffsetstrom nicht gespeichert |
| 0x15 | NVRAM Schaltwegende gerade Gaenge nicht gespeichert |
| 0x16 | NVRAM Schaltwegende ungerade Gaenge nicht gespeichert |
| 0x17 | NVRAM Schaltweg Neutral nicht gespeichert |
| 0x18 | NVRAM Waehlwinkel Neutral nicht gespeichert |
| 0x19 | NVRAM Waehlwinkel Gasse 1-2 nicht gespeichert |
| 0x1A | NVRAM Waehlwinkel Gasse 3-4 nicht gespeichert |
| 0x1B | NVRAM Waehlwinkel Gasse 5-6 nicht gespeichert |
| 0x1C | NVRAM Waehlwinkel Gasse R nicht gespeichert |
| 0x1E | Schaltwegposition nicht auf Mittellage positionierbar |
| 0x1F | keine gueltige Mittellage gefunden |
| 0x20 | kein gueltiger Waehlwinkeloffsetstrom |
| 0x21 | Zeitueberschreitung Einregeln Waehlwinkelmitte |
| 0x22 | Zeitueberschreitung Einregeln Schaltwegmitte |
| 0x23 | Minimaler Abstand Schaltwegmitte Schaltwegende zu gering |
| 0x24 | Linke WW-Anschlag kleiner als der erlaubte elektrische Bereich |
| 0x25 | Rechte WW-Anschlag groesser als der erlaubte elektrische Bereich |
| 0x28 | Nicht aktivierte Schalter bei Bestaetigung der Waehlhebelposition |
| 0x32 | Gang 1 wurde substituiert |
| 0x33 | Gang 2 wurde substituiert |
| 0x34 | Gang 3 wurde substituiert |
| 0x35 | Gang 4 wurde substituiert |
| 0x36 | Gang 5 wurde substituiert |
| 0x37 | Gang 6 wurde substituiert |
| 0x38 | Gang R wurde substituiert |
| 0x3A | Verriegelung der Vorwaertsgaenge unwirksam |
| 0x3B | Verriegelung der Rueckwaertsgaenge unwirksam |
| 0x3C | Waehlwinkelregler nicht adaptierbar |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft, oder Zuendung ist aus) |
| 0xFF | unbekannter Infotext |

<a id="table-infotexte9f"></a>
### INFOTEXTE9F

Dimensions: 5 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x28 | Platzhalter Error 0x28 (40) |
| 0x29 | Platzhalter Error 0x29 (41) |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft, oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte10f"></a>
### INFOTEXTE10F

Dimensions: 3 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte11f"></a>
### INFOTEXTE11F

Dimensions: 4 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x2A | Offset kleiner 1,6V oder groesser 2,0 V |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte12f"></a>
### INFOTEXTE12F

Dimensions: 4 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x2C | Offset kleiner 1,6V oder groesser 2,0 V |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte13f"></a>
### INFOTEXTE13F

Dimensions: 5 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x2F | EK oder AK Position der Kupplung ausserhalb der Toleranz |
| 0x31 | Ueberdeckung des Kupplungsventils ausserhalb der Toleranz |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |

<a id="table-infotexte14f"></a>
### INFOTEXTE14F

Dimensions: 6 rows × 2 columns

| IB | INFO_TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x23 | Schaltweg laesst sich nicht positionieren |
| 0x24 | keine SW Mitte gefunden |
| 0x25 | SW-Mittellage erreicht |
| 0xA0 | Testbedingung nicht erfuellt (Motor laeuft oder Zuendung ist aus) |
| 0xFF | Unbekannter Infotext |
