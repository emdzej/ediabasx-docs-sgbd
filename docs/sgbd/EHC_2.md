# EHC_2.prg

- Jobs: [32](#jobs)
- Tables: [10](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | 2-Achs-Luftfederung EHC |
| ORIGIN | Stefan Reisinger, EE-230 |
| REVISION | 1.00 |
| AUTHOR | IDS Schmidt (BS), Stefan Reisinger (SR) |
| COMMENT | Kommentar |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung / Kommunikationsparameter fuer &lt;SG&gt; automatischer Aufruf beim ersten Zugriff auf SGBD
- [INFO](#job-info) - Information bzgl. SGBD
- [IDENTIFIKATION](#job-identifikation) - Ermittlung der SG-Variante
- [IDENT](#job-ident) - Ident-Daten fuer EHC
- [FS_QUICK_LESEN](#job-fs-quick-lesen) - Fehlerspeicher quick lesen
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [CODE_LESEN](#job-code-lesen) - gibt die Codierinformation als BYTE-STRING aus
- [STATUS_LESEN](#job-status-lesen) - I/O Status lesen
- [STATUS_SETZEN](#job-status-setzen) - Hardward Zugriff
- [SG_STATUS_LESEN](#job-sg-status-lesen) - Software-Status lesen
- [SG_STATUS_VORGEBEN](#job-sg-status-vorgeben) - Software Zugriff
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels
- [SPEICHER_LOESCHEN](#job-speicher-loeschen) - EEPROM loeschen bis auf SG-Identifikation
- [SG_RESET](#job-sg-reset) - Reset des Steuergeraetes
- [FS_SHADOW_LESEN](#job-fs-shadow-lesen) - auslesen des Fehlershadowspeichers
- [ABGLEICHWERT_LESEN](#job-abgleichwert-lesen) - Hoehenstand lesen
- [ABGLEICHWERT_PROGRAMMIEREN](#job-abgleichwert-programmieren) - Offset fuer Hoehenstaende eingeben
- [HERSTELLDATEN_LESEN](#job-herstelldaten-lesen) - Auslesen des Herstelldaten
- [HERSTELLDATEN_SCHREIBEN](#job-herstelldaten-schreiben) - Schreiben der Herstelldaten
- [DIAGNOSEMODE_ERHALTEN](#job-diagnosemode-erhalten) - Zaehler fuer Diagnosemode zuruecksetzen
- [DIAGNOSEMODE_BEENDEN](#job-diagnosemode-beenden) - beendet den Diagnosemode vorzeitig
- [SEED_HOLEN](#job-seed-holen) - meldet fuer eine Zugriffsebene an
- [KEY_SENDEN_NORMAL](#job-key-senden-normal) - Key an SG senden fuer Zugriffsebene 1
- [KEY_SENDEN_EXPERT](#job-key-senden-expert) - Key an SG senden fuer Zugriffsebene 2
- [FAHRZEUG_HOEHE_ABGLEICHEN](#job-fahrzeug-hoehe-abgleichen) - automatischer Hoehenabgleich
- [STATUS_VORGEBEN](#job-status-vorgeben) - Ansteuern eines digitalen Ein- Ausgaenge
- [SG_STATUS_SETZEN](#job-sg-status-setzen) - Ansteuern der SGs
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Speicherinhaltes
- [AKTOREN_VORGEBEN](#job-aktoren-vorgeben) - Ansteuern der Modi
- [HOEHE_SPEICHERN](#job-hoehe-speichern) - Hoehe in den leak-Bereich
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung / Kommunikationsparameter fuer &lt;SG&gt; automatischer Aufruf beim ersten Zugriff auf SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn Okay |

<a id="job-info"></a>
### INFO

Information bzgl. SGBD

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

<a id="job-identifikation"></a>
### IDENTIFIKATION

Ermittlung der SG-Variante

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| VARIANT | string | Programmname |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer EHC

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | string | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Variantenindex |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Text |
| ID_SW_NR | string | Software-Nummer |
| ID_AIF_VORHANDEN | int | 1, wenn Anwender-Info-Feld vorhanden |
| ID_BUS_ANZ | int | Anzahl Busse |
| ID_BUS1_TYP | int | Bustyp 1 |
| ID_BUS1_INDEX | int | Busindex 1 |
| ID_BUS2_TYP | int | Bustyp 2 |
| ID_BUS2_INDEX | int | Busindex 2 |
| _TEL_ANTWORT | binary |  |

<a id="job-fs-quick-lesen"></a>
### FS_QUICK_LESEN

Fehlerspeicher quick lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| F_ANZ | int | Anzahl der Fehler |
| FS_DATUM_KW | int | Loeschdatum KW [0-53] |
| FS_DATUM_JAHR | int | Loeschdatum Jahr [0-99] |
| _TEL_ANTWORT | binary |  |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-code-lesen"></a>
### CODE_LESEN

gibt die Codierinformation als BYTE-STRING aus

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODIERBLOCK | int | Codierblock Nr. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |
| _TEL_SEND | binary |  |

<a id="job-status-lesen"></a>
### STATUS_LESEN

I/O Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |
| STAT_ANALOG_H_FL_WERT | int | Hoehenstand vom Sensor vorne links [mm] |
| STAT_ANALOG_H_FR_WERT | int | Hoehenstand vom Sensor vorne rechts [mm] |
| STAT_ANALOG_H_RL_WERT | int | Hoehenstand vom Sensor hinten links [mm] |
| STAT_ANALOG_H_RR_WERT | int | Hoehenstand vom Sensor hinten rechts [mm] |
| STAT_ANALOG_H_EINH | string | [mm] |
| STAT_ANALOG_P_RES_WERT | real | Speicherdruck [Bar] |
| STAT_ANALOG_P_QUSP_F_WERT | real | Druck des Quersperrdrucksensors VA [Bar] |
| STAT_ANALOG_P_QUSP_R_WERT | real | Druck des Quersperrdrucksensors HA [Bar] |
| STAT_ANALOG_P_EINH | string | [Bar] |
| STAT_ANALOG_TE_COMP_WERT | int | Komoressortemperatur [Grad Celsius] |
| STAT_ANALOG_TE_COMP_EINH | string | [Grad Celsius] |
| STAT_ANALOG_U_KL_30_WERT | real | gemessene Versorgungsspannung [Volt] |
| STAT_ANALOG_U_KL_30_EINH | string | [Volt] |
| STAT_SWITCH_ACCESS_EIN | int | Access Taster [High Aktiv] |
| STAT_SWITCH_UP_EIN | int | Tasterwippe rauf [High Aktiv] |
| STAT_SWITCH_DOWN_EIN | int | Tasterwippe runter [High Aktiv] |
| STAT_SWITCH_HOLD_EIN | int | Hold Taster [High Aktiv] |
| STAT_VALVE_STAT_VORHANDEN | binary | Ventile ueberhitzt, Kompressor ueberhitzt |

<a id="job-status-setzen"></a>
### STATUS_SETZEN

Hardward Zugriff

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | (0)MV_FR (1)MV_FL (2)MV_RR (3)MV_RL (4)MV_RES (5)MV_EX (6)C_SW [alle High Aktiv] |
| BYTE2 | int | (0)MV_CFR (1)MV_CFL (2)MV_CRR (3)MV_CRL [alle High Aktiv] |
| BYTE3 | int | (1)Access Static (3)Motorway Static (5)Standard Static (7)Offroad Static [alle High Aktiv] |
| BYTE4 | int | (1)Hold Static [alle High Aktiv] |
| BYTE5 | int | reserviert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |
| _TEL_AN_SG | binary |  |

<a id="job-sg-status-lesen"></a>
### SG_STATUS_LESEN

Software-Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |
| STAT_DUMP_MODUS_EIN | int | Zusatzbotschaften fuer FESTUS [High Aktiv] |
| STAT_BAND_MODUS_EIN | int | Aktivierungs-Sperre [High Aktiv] |
| STAT_VERLADEMODUS_EIN | int | Einstellungen fuer den Transport [High Aktiv] |
| STAT_BYPASSMODUS_EIN | int | Daten ueber Fzg-CAN [High Aktiv] |
| STAT_EMV_KUNDENMODUS_EIN | int | fuer webaco EMV-Tests [High Aktiv] |
| STAT_HANDSTEUERMODUS_EIN | int | Freischaltung fuer I/O Status-Vorgabe [High Aktiv] |
| STAT_NOPLAUMODUS_EIN | int | fuer Laborauto Tests [High Aktiv] |

<a id="job-sg-status-vorgeben"></a>
### SG_STATUS_VORGEBEN

Software Zugriff

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | (0)Dump Modus (1)Badn Modus (2)Verlademodus (3)Bypassmodus (4)EMV Kundenmodus (5)Handsteuermodus (6)NoPlausibilitymodus[alle High Aktiv] |
| BYTE2 | int | reserviert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |
| _TEL_AN_SG | binary |  |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| BYTE1 | int | nach Codierung soll hier ein Teil der Fahrgestell-Nr. stehen |
| BYTE2 | int | nach Codierung soll hier ein Teil der Fahrgestell-Nr. stehen |
| BYTE3 | int | nach Codierung soll hier ein Teil der Fahrgestell-Nr. stehen |
| _TEL_ANTWORT | binary |  |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | nach Codierung soll hier ein Teil der Fahrgestell-Nr. stehenn |
| BYTE2 | int | nach Codierung soll hier ein Teil der Fahrgestell-Nr. stehen |
| BYTE3 | int | nach Codierung soll hier ein Teil der Fahrgestell-Nr. stehen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-speicher-loeschen"></a>
### SPEICHER_LOESCHEN

EEPROM loeschen bis auf SG-Identifikation

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-sg-reset"></a>
### SG_RESET

Reset des Steuergeraetes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-fs-shadow-lesen"></a>
### FS_SHADOW_LESEN

auslesen des Fehlershadowspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-abgleichwert-lesen"></a>
### ABGLEICHWERT_LESEN

Hoehenstand lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| EE_H_FL_ZERO | int | Nullabgleich fuer Hoehenstandssensor |
| EE_H_FR_ZERO | int | Nullabgleich fuer Hoehenstandssensor |
| EE_H_RL_ZERO | int | Nullabgleich fuer Hoehenstandssensor |
| EE_H_RR_ZERO | int | Nullabgleich fuer Hoehenstandssensor |
| EE_H_ZERO_EINH | string | Einheit fuer Nullabgleich [in AD-Counts] |
| EE_H_FR_LEAK | int | Eingeschriebender Hoehenstand zur Grobleckagepruefung |
| EE_H_FL_LEAK | int | Eingeschriebender Hoehenstand zur Grobleckagepruefung |
| EE_H_RR_LEAK | int | Eingeschriebender Hoehenstand zur Grobleckagepruefung |
| EE_H_RL_LEAK | int | Eingeschriebender Hoehenstand zur Grobleckagepruefung |
| EE_H_LEAK_EINH | int | Einheit fuer Hoehenstand zur Grobleckagepruefung [mm] |
| _TEL_ANTWORT | binary |  |

<a id="job-abgleichwert-programmieren"></a>
### ABGLEICHWERT_PROGRAMMIEREN

Offset fuer Hoehenstaende eingeben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| OFFSETBYTE_FL_A | int | Offset fuer Hoehenstandssensor |
| OFFSETBYTE_FL_B | int | Offset fuer Hoehenstandssensor |
| OFFSETBYTE_FR_A | int | Offset fuer Hoehenstandssensor |
| OFFSETBYTE_FR_B | int | Offset fuer Hoehenstandssensor |
| OFFSETBYTE_RL_A | int | Offset fuer Hoehenstandssensor |
| OFFSETBYTE_RL_B | int | Offset fuer Hoehenstandssensor |
| OFFSETBYTE_RR_A | int | Offset fuer Hoehenstandssensor |
| OFFSETBYTE_RR_B | int | Offset fuer Hoehenstandssensor |
| VOREINST_BYTE_FR_A | int | Im Bandablauf voreingestellter Offset fuer Hoehenstandssensor |
| VOREINST_BYTE_FR_B | int | Im Bandablauf voreingestellter Offset fuer Hoehenstandssensor |
| VOREINST_BYTE_FL_A | int | Im Bandablauf voreingestellter Offset fuer Hoehenstandssensor |
| VOREINST_BYTE_FL_B | int | Im Bandablauf voreingestellter Offset fuer Hoehenstandssensor |
| VOREINST_BYTE_RR_A | int | Im Bandablauf voreingestellter Offset fuer Hoehenstandssensor |
| VOREINST_BYTE_RR_B | int | Im Bandablauf voreingestellter Offset fuer Hoehenstandssensor |
| VOREINST_BYTE_RL_A | int | Im Bandablauf voreingestellter Offset fuer Hoehenstandssensor |
| VOREINST_BYTE_RL_B | int | Im Bandablauf voreingestellter Offset fuer Hoehenstandssensor |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-herstelldaten-lesen"></a>
### HERSTELLDATEN_LESEN

Auslesen des Herstelldaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| BYTE1 | int | 1. Herstelldatenbyte |
| BYTE2 | int | 2. Herstelldatenbyte |
| BYTE3 | int | 3. Herstelldatenbyte |
| BYTE4 | int | 4. Herstelldatenbyte |
| BYTE5 | int | 5. Herstelldatenbyte |
| BYTE6 | int | 6. Herstelldatenbyte |
| BYTE7 | int | 7. Herstelldatenbyte |
| BYTE8 | int | 8. Herstelldatenbyte |
| BYTE9 | int | 9. Herstelldatenbyte |
| BYTE10 | int | 10. Herstelldatenbyte |
| BYTE11 | int | 11. Herstelldatenbyte |
| BYTE12 | int | 12. Herstelldatenbyte |
| BYTE13 | int | 13. Herstelldatenbyte |
| BYTE14 | int | 14. Herstelldatenbyte |
| BYTE15 | int | 15. Herstelldatenbyte |
| BYTE16 | int | 16. Herstelldatenbyte |
| BYTE17 | int | 17. Herstelldatenbyte |
| BYTE18 | int | 18. Herstelldatenbyte |
| BYTE19 | int | 19. Herstelldatenbyte |
| BYTE20 | int | 20. Herstelldatenbyte |
| BYTE21 | int | 21. Herstelldatenbyte |
| BYTE22 | int | 22. Herstelldatenbyte |
| _TEL_ANTWORT | binary |  |

<a id="job-herstelldaten-schreiben"></a>
### HERSTELLDATEN_SCHREIBEN

Schreiben der Herstelldaten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | zur Dokumentierung |
| BYTE2 | int | zur Dokumentierung |
| BYTE3 | int | zur Dokumentierung |
| BYTE4 | int | zur Dokumentierung |
| BYTE5 | int | zur Dokumentierung |
| BYTE6 | int | zur Dokumentierung |
| BYTE7 | int | zur Dokumentierung |
| BYTE8 | int | zur Dokumentierung |
| BYTE9 | int | zur Dokumentierung |
| BYTE10 | int | zur Dokumentierung |
| BYTE11 | int | zur Dokumentierung |
| BYTE12 | int | zur Dokumentierung |
| BYTE13 | int | zur Dokumentierung |
| BYTE14 | int | zur Dokumentierung |
| BYTE15 | int | zur Dokumentierung |
| BYTE16 | int | zur Dokumentierung |
| BYTE17 | int | zur Dokumentierung |
| BYTE18 | int | zur Dokumentierung |
| BYTE19 | int | zur Dokumentierung |
| BYTE20 | int | zur Dokumentierung |
| BYTE21 | int | zur Dokumentierung |
| BYTE22 | int | zur Dokumentierung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-diagnosemode-erhalten"></a>
### DIAGNOSEMODE_ERHALTEN

Zaehler fuer Diagnosemode zuruecksetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-diagnosemode-beenden"></a>
### DIAGNOSEMODE_BEENDEN

beendet den Diagnosemode vorzeitig

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-seed-holen"></a>
### SEED_HOLEN

meldet fuer eine Zugriffsebene an

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Zugriffsebene |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |
| SEED_LSB | int | Seed LSB |
| SEED_MSB | int | Seed MSB |

<a id="job-key-senden-normal"></a>
### KEY_SENDEN_NORMAL

Key an SG senden fuer Zugriffsebene 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Key LSB |
| BYTE2 | int | Key MSB |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| send1 | int | Key LSB send |
| send2 | int | Key MSB send |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-key-senden-expert"></a>
### KEY_SENDEN_EXPERT

Key an SG senden fuer Zugriffsebene 2

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Key LSB |
| BYTE2 | int | Key MSB |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| send1 | int | Key LSB send |
| send2 | int | Key MSB send |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_AN_SG | binary |  |
| _TEL_ANTWORT | binary |  |

<a id="job-fahrzeug-hoehe-abgleichen"></a>
### FAHRZEUG_HOEHE_ABGLEICHEN

automatischer Hoehenabgleich

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DELTA_HOEHE_LINKS | int | mm |
| DELTA_HOEHE_RECHTS | int | mm |
| MINDEST_DELTA | int | mm |
| ACHSE | int | 1 Vorne und 2 Hinten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| OFFSET_LINKS_ALT | int | alter offset |
| OFFSET_RECHTS_ALT | int | alter offset |
| OFFSET_LINKS_NEU | int | alter offset |
| OFFSET_RECHTS_NEU | int | alter offset |
| SG_HOEHE_LINKS | int | aktuelle Fahrzeughoehe laut Fastfilter |
| SG_HOEHE_RECHTS | int | aktuelle Fahrzeughoehe laut Fastfilter |
| AUFLOESUNG_LINKS_WERT | real | Sensoraufloesung links laut Kodierdaten |
| AUFLOESUNG_RECHTS_WERT | real | Sensoraufloesung rechts laut Kodierdaten |
| ABWEICHUNG_LINKS_WERT | int | Abweichung links |
| ABWEICHUNG_RECHTS_WERT | int | Abweichung rechts |
| TEL_ABGLEICH | binary | gesendetes Abgleichtelegramm |

<a id="job-status-vorgeben"></a>
### STATUS_VORGEBEN

Ansteuern eines digitalen Ein- Ausgaenge

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT1 | string | gewuenschte Komponente 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-sg-status-setzen"></a>
### SG_STATUS_SETZEN

Ansteuern der SGs

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODUS | string | gewuenschte Komponente 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Auslesen des Speicherinhaltes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT | int | gewuenschtes Startsegment (0) |
| MIDDLE | int | gewuenschte Startadresse midle als Hexwert! |
| LOW | int | gewuenschte Startadresse low als Hexwert! |
| ANZAHL | int | gewuenschte Anzahl Bytes (2-28) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| _TEL_SENDE | binary |  |
| _TEL_ANTWORT | binary |  |
| DATEN | binary | angeforderter Datenblock (28 Bytes!) |

<a id="job-aktoren-vorgeben"></a>
### AKTOREN_VORGEBEN

Ansteuern der Modi

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODI | string | gewuenschte Komponente |
| VORG1 | int | VorgabeByte |
| VORG2 | int | VorgabeByte |
| VORG3 | int | VorgabeByte |
| VORG4 | int | VorgabeByte |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| BACK1 | int | Rueckgabewert |
| BACK2 | int | Rueckgabewert |
| BACK3 | int | Rueckgabewert |
| BACK4 | int | Rueckgabewert |

<a id="job-hoehe-speichern"></a>
### HOEHE_SPEICHERN

Hoehe in den leak-Bereich

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
| JOB_STATUS | string | OKAY, ERROR_.. |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | int | momentan identisch Fehlerbyte |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_HFK | int | Fehlerhaufigkeit |
| F_ART_ANZ | int | Anzahl der Fehlerarten (hier immer 8) |
| F_UW_GES_ANZ | int | Anzahl der Umweltbedingungen (alle) |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen (pro Fehler) |
| F_UW_SATZ | int | Anzahl der Umweltbedingungssaetze |
| F_ART1_NR | int | Fehlerartenbyte |
| F_ART1_TEXT | string | Fehlerart als Text |
| F_UW1_NR | int | Index der 1. Umweltbedingung |
| F_UW1_TEXT | string | Text zur 1. Umweltbedingung |
| F_UW1_WERT | real | Wert zur 1. Umweltbedingung |
| F_UW1_EINH | string | Einheit der 1. Umweltbedingung |
| F_UW2_NR | int | Index der 2. Umweltbedingung |
| F_UW2_TEXT | string | Text zur 2. Umweltbedingung |
| F_UW2_WERT | real | Wert zur 2. Umweltbedingung |
| F_UW2_EINH | string | Einheit der 2. Umweltbedingung |
| F_UW3_NR | int | Index der 3. Umweltbedingung |
| F_UW3_TEXT | string | Text zur 3. Umweltbedingung |
| F_UW3_WERT | real | Wert zur 3. Umweltbedingung |
| F_UW3_EINH | string | Einheit der 3. Umweltbedingung |
| F_UW4_NR | int | Index der 4. Umweltbedingung |
| F_UW4_TEXT | string | Text zur 4. Umweltbedingung |
| F_UW4_WERT | real | Wert zur 4. Umweltbedingung |
| F_UW4_EINH | string | Einheit der 4. Umweltbedingung |
| F_UW5_NR | int | Index der 5. Umweltbedingung |
| F_UW5_TEXT | string | Text zur 5. Umweltbedingung |
| F_UW5_WERT | real | Wert zur 5. Umweltbedingung |
| F_UW5_EINH | string | Einheit der 5. Umweltbedingung |
| F_UW6_NR | int | Index der 6. Umweltbedingung |
| F_UW6_TEXT | string | Text zur 6. Umweltbedingung |
| F_UW6_WERT | real | Wert zur 6. Umweltbedingung |
| F_UW6_EINH | string | Einheit der 6. Umweltbedingung |
| F_UW7_NR | int | Index der 6. Umweltbedingung |
| F_UW7_TEXT | string | Text zur 7. Umweltbedingung |
| F_UW7_WERT | real | Wert zur 7. Umweltbedingung |
| F_UW7_EINH | string | Einheit der 7. Umweltbedingung |
| F_UW8_NR | int | Index der 8. Umweltbedingung |
| F_UW8_TEXT | string | Text zur 8. Umweltbedingung |
| F_UW8_WERT | real | Wert zur 8. Umweltbedingung |
| F_UW8_EINH | string | Einheit der 8. Umweltbedingung |
| F_UW9_NR | int | Index der 9. Umweltbedingung |
| F_UW9_TEXT | string | Text zur 9. Umweltbedingung |
| F_UW9_WERT | real | Wert zur 9. Umweltbedingung |
| F_UW9_EINH | string | Einheit der 9. Umweltbedingung |
| F_UW10_NR | int | Index der 10. Umweltbedingung |
| F_UW10_TEXT | string | Text zur 10. Umweltbedingung |
| F_UW10_WERT | real | Wert zur 10. Umweltbedingung |
| F_UW10_EINH | string | Einheit der 10. Umweltbedingung |
| F_UW11_NR | int | Index der 11. Umweltbedingung |
| F_UW11_TEXT | string | Text zur 11. Umweltbedingung |
| F_UW11_WERT | real | Wert zur 11. Umweltbedingung |
| F_UW11_EINH | string | Einheit der 11. Umweltbedingung |
| F_UW12_NR | int | Index der 12. Umweltbedingung |
| F_UW12_TEXT | string | Text zur 12. Umweltbedingung |
| F_UW12_WERT | real | Wert zur 12. Umweltbedingung |
| F_UW12_EINH | string | Einheit der 12. Umweltbedingung |
| F_UW13_NR | int | Index der 13. Umweltbedingung |
| F_UW13_TEXT | string | Text zur 13. Umweltbedingung |
| F_UW13_WERT | real | Wert zur 13. Umweltbedingung |
| F_UW13_EINH | string | Einheit der 13. Umweltbedingung |
| F_UW14_NR | int | Index der 14. Umweltbedingung |
| F_UW14_TEXT | string | Text zur 14. Umweltbedingung |
| F_UW14_WERT | real | Wert zur 14. Umweltbedingung |
| F_UW14_EINH | string | Einheit der 14. Umweltbedingung |
| F_UW15_NR | int | Index der 15. Umweltbedingung |
| F_UW15_TEXT | string | Text zur 15. Umweltbedingung |
| F_UW15_WERT | real | Wert zur 15. Umweltbedingung |
| F_UW15_EINH | string | Einheit der 15. Umweltbedingung |
| F_UW16_NR | int | Index der 16. Umweltbedingung |
| F_UW16_TEXT | string | Text zur 16. Umweltbedingung |
| F_UW16_WERT | real | Wert zur 16. Umweltbedingung |
| F_UW16_EINH | string | Einheit der 16. Umweltbedingung |
| F_UW17_NR | int | Index der 17. Umweltbedingung |
| F_UW17_TEXT | string | Text zur 17. Umweltbedingung |
| F_UW17_WERT | real | Wert zur 17. Umweltbedingung |
| F_UW17_EINH | string | Einheit der 17. Umweltbedingung |
| F_UW18_NR | int | Index der 18. Umweltbedingung |
| F_UW18_TEXT | string | Text zur 18. Umweltbedingung |
| F_UW18_WERT | real | Wert zur 18. Umweltbedingung |
| F_UW18_EINH | string | Einheit der 18. Umweltbedingung |
| F_UW19_NR | int | Index der 19. Umweltbedingung |
| F_UW19_TEXT | string | Text zur 19. Umweltbedingung |
| F_UW19_WERT | real | Wert zur 19. Umweltbedingung |
| F_UW19_EINH | string | Einheit der 19. Umweltbedingung |
| F_UW20_NR | int | Index der 20. Umweltbedingung |
| F_UW20_TEXT | string | Text zur 20. Umweltbedingung |
| F_UW20_WERT | real | Wert zur 20. Umweltbedingung |
| F_UW20_EINH | string | Einheit der 20. Umweltbedingung |
| F_UW21_NR | int | Index der 21. Umweltbedingung |
| F_UW21_TEXT | string | Text zur 21. Umweltbedingung |
| F_UW21_WERT | real | Wert zur 21. Umweltbedingung |
| F_UW21_EINH | string | Einheit der 21. Umweltbedingung |
| F_UW22_NR | int | Index der 22. Umweltbedingung |
| F_UW22_TEXT | string | Text zur 22. Umweltbedingung |
| F_UW22_WERT | real | Wert zur 22. Umweltbedingung |
| F_UW22_EINH | string | Einheit der 22. Umweltbedingung |
| F_UW23_NR | int | Index der 23. Umweltbedingung |
| F_UW23_TEXT | string | Text zur 23. Umweltbedingung |
| F_UW23_WERT | real | Wert zur 23. Umweltbedingung |
| F_UW23_EINH | string | Einheit der 23. Umweltbedingung |
| F_UW24_NR | int | Index der 24. Umweltbedingung |
| F_UW24_TEXT | string | Text zur 24. Umweltbedingung |
| F_UW24_WERT | real | Wert zur 24. Umweltbedingung |
| F_UW24_EINH | string | Einheit der 24. Umweltbedingung |
| F_UW25_NR | int | Index der 25. Umweltbedingung |
| F_UW25_TEXT | string | Text zur 25. Umweltbedingung |
| F_UW25_WERT | real | Wert zur 25. Umweltbedingung |
| F_UW25_EINH | string | Einheit der 25. Umweltbedingung |
| F_UW26_NR | int | Index der 26. Umweltbedingung |
| F_UW26_TEXT | string | Text zur 26. Umweltbedingung |
| F_UW26_WERT | real | Wert zur 26. Umweltbedingung |
| F_UW26_EINH | string | Einheit der 26. Umweltbedingung |
| F_UW27_NR | int | Index der 27. Umweltbedingung |
| F_UW27_TEXT | string | Text zur 27. Umweltbedingung |
| F_UW27_WERT | real | Wert zur 27. Umweltbedingung |
| F_UW27_EINH | string | Einheit der 27. Umweltbedingung |
| F_UW28_NR | int | Index der 28. Umweltbedingung |
| F_UW28_TEXT | string | Text zur 28. Umweltbedingung |
| F_UW28_WERT | real | Wert zur 28. Umweltbedingung |
| F_UW28_EINH | string | Einheit der 28. Umweltbedingung |
| F_UW29_NR | int | Index der 29. Umweltbedingung |
| F_UW29_TEXT | string | Text zur 29. Umweltbedingung |
| F_UW29_WERT | real | Wert zur 29. Umweltbedingung |
| F_UW29_EINH | string | Einheit der 29. Umweltbedingung |
| F_UW30_NR | int | Index der 30. Umweltbedingung |
| F_UW30_TEXT | string | Text zur 30. Umweltbedingung |
| F_UW30_WERT | real | Wert zur 30. Umweltbedingung |
| F_UW30_EINH | string | Einheit der 30. Umweltbedingung |
| F_UW31_NR | int | Index der 31. Umweltbedingung |
| F_UW31_TEXT | string | Text zur 31. Umweltbedingung |
| F_UW31_WERT | real | Wert zur 31. Umweltbedingung |
| F_UW31_EINH | string | Einheit der 31. Umweltbedingung |
| F_UW32_NR | int | Index der 32. Umweltbedingung |
| F_UW32_TEXT | string | Text zur 32. Umweltbedingung |
| F_UW32_WERT | real | Wert zur 32. Umweltbedingung |
| F_UW32_EINH | string | Einheit der 32. Umweltbedingung |
| F_UW33_NR | int | Index der 33. Umweltbedingung |
| F_UW33_TEXT | string | Text zur 33. Umweltbedingung |
| F_UW33_WERT | real | Wert zur 33. Umweltbedingung |
| F_UW33_EINH | string | Einheit der 33. Umweltbedingung |
| F_UW34_NR | int | Index der 34. Umweltbedingung |
| F_UW34_TEXT | string | Text zur 34. Umweltbedingung |
| F_UW34_WERT | real | Wert zur 34. Umweltbedingung |
| F_UW34_EINH | string | Einheit der 34. Umweltbedingung |
| F_UW35_NR | int | Index der 35. Umweltbedingung |
| F_UW35_TEXT | string | Text zur 35. Umweltbedingung |
| F_UW35_WERT | real | Wert zur 35. Umweltbedingung |
| F_UW35_EINH | string | Einheit der 35. Umweltbedingung |
| F_UW36_NR | int | Index der 36. Umweltbedingung |
| F_UW36_TEXT | string | Text zur 36. Umweltbedingung |
| F_UW36_WERT | real | Wert zur 36. Umweltbedingung |
| F_UW36_EINH | string | Einheit der 36. Umweltbedingung |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (7 × 2)
- [LIEFERANTEN](#table-lieferanten) (31 × 2)
- [FORTTEXTE](#table-forttexte) (20 × 2)
- [FARTMATRIX](#table-fartmatrix) (20 × 15)
- [FARTTEXTE](#table-farttexte) (13 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (20 × 6)
- [FUMWELTTEXTE](#table-fumwelttexte) (6 × 8)
- [STEUERN](#table-steuern) (16 × 3)
- [AKTOREN](#table-aktoren) (22 × 3)
- [STEUERN_SG](#table-steuern-sg) (9 × 3)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 7 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_REJECTED |
| 0xB0 | ERROR_PARAMETER |
| 0xB1 | ERROR_FUNCTION |
| 0xFF | ERROR_NOT_ACKNOWLEDGE |
| 0xXY | ERROR_UNKNOWN_STATUSBYTE |

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
| 0x43 | WABCO |
| 0xFF | unbekannter Hersteller |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 20 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Ventil vorne links |
| 0x02 | Ventil vorne rechts |
| 0x03 | Ventil hinten links |
| 0x04 | Ventil hinten rechts |
| 0x05 | Quersperrventil vorne links |
| 0x06 | Quersperrventil vorne rechts |
| 0x07 | Quersperrventil hinten links |
| 0x08 | Quersperrventil hinten rechts |
| 0x0A | Ablassventil |
| 0x0B | Speicherventil |
| 0x0C | Kompressorrelais |
| 0x14 | Hoehenstandssensor vorne links |
| 0x15 | Hoehenstandssensor vorne rechts |
| 0x16 | Hoehenstandssensor hinten links |
| 0x17 | Hoehenstandssensor hinten rechts |
| 0x18 | Speicherdrucksensor |
| 0x19 | Quersperrdrucksensor Vorderachse |
| 0x1A | Quersperrdrucksensor Hinterachse |
| 0x1E | CAN-Bus |
| 0xFF | unbekannter Fehlerort |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 20 rows × 15 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 | A6_0 | A6_1 | A7_0 | A7_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 |
| 0x02 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 |
| 0x03 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 |
| 0x04 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 |
| 0x05 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 |
| 0x06 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 |
| 0x07 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 |
| 0x08 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 |
| 0x0A | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 |
| 0x0B | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 |
| 0x0C | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 |
| 0x14 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 |
| 0x15 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 |
| 0x16 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 |
| 0x17 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 |
| 0x18 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 |
| 0x19 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 |
| 0x1A | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 |
| 0x1E | 0x00 | 0x0B | 0x00 | 0x0C | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF | 0x00 | 0xFF |
| 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF | 0xFF |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 13 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | Kurzschluss gegen U-Batt |
| 0x02 | Kurzschluss gegen Masse |
| 0x03 | Leitungsunterbrechung |
| 0x04 | Plausibilitaet |
| 0x07 | Fehler momentan vorhanden |
| 0x08 | sporadischer Fehler |
| 0x0A | blockiert |
| 0x0B | Bus Off |
| 0x0C | mindestens eine Botschaft fehlt |
| 0x0D | Checksumme falsch |
| 0xFE | allg. Fehler |
| 0xFF | unbekannte Fehlerart |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 20 rows × 6 columns

| ORT | UW_ANZ | UW_SATZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- | --- | --- |
| 0x01 | 2 | 1 | 0x01 | 0x10 | 0x00 |
| 0x02 | 2 | 1 | 0x01 | 0x10 | 0x00 |
| 0x03 | 2 | 1 | 0x01 | 0x10 | 0x00 |
| 0x04 | 2 | 1 | 0x01 | 0x10 | 0x00 |
| 0x05 | 2 | 1 | 0x01 | 0x10 | 0x00 |
| 0x06 | 2 | 1 | 0x01 | 0x10 | 0x00 |
| 0x07 | 2 | 1 | 0x01 | 0x10 | 0x00 |
| 0x08 | 2 | 1 | 0x01 | 0x10 | 0x00 |
| 0x0A | 2 | 1 | 0x01 | 0x10 | 0x00 |
| 0x0B | 2 | 1 | 0x01 | 0x10 | 0x00 |
| 0x0C | 2 | 1 | 0x01 | 0x10 | 0x00 |
| 0x14 | 2 | 1 | 0x01 | 0x10 | 0x00 |
| 0x15 | 2 | 1 | 0x01 | 0x10 | 0x00 |
| 0x16 | 2 | 1 | 0x01 | 0x10 | 0x00 |
| 0x17 | 2 | 1 | 0x01 | 0x10 | 0x00 |
| 0x18 | 2 | 1 | 0x01 | 0x10 | 0x00 |
| 0x19 | 2 | 1 | 0x01 | 0x10 | 0x00 |
| 0x1A | 2 | 1 | 0x01 | 0x10 | 0x00 |
| 0x1E | 2 | 1 | 0x01 | 0x10 | 0x00 |
| 0xXY | 0 | 0 | 0xFF | 0xFF | 0xFF |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 6 rows × 8 columns

| UWNR | UWTEXT | UW_EINH | MASK | NAME | UW_MULT | UW_DIV | UW_ADD |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Kilometerstand | km | -- | -- | 10 | 1 | 0 |
| 0x10 | zusaetzliche UW Bedingungen | xxx | -- | -- | 1 | 1 | 0 |
| 0x11 | Motordrehzahl | 1/min | -- | -- | 32 | 1 | 0 |
| 0x12 | Fahrzeuggeschwindigkeit | km/h | -- | -- | 1 | 1 | 0 |
| 0x13 | Batteriespannung | Volt | -- | -- | 1 | 10 | 0 |
| 0xXY | unbekannte Umweltbedingung | XY | 1 | 1 | 1 | 1 | 0 |

<a id="table-steuern"></a>
### STEUERN

Dimensions: 16 rows × 3 columns

| STEUER_I_O | BYTE | BITWERT |
| --- | --- | --- |
| 1110 | 0 | 0x43 |
| 1101 | 0 | 0x44 |
| 1100 | 0 | 0x48 |
| 1011 | 0 | 0x47 |
| 1010 | 0 | 0x4B |
| 1001 | 0 | 0x4C |
| 1000 | 0 | 0x4F |
| 0111 | 0 | 0x23 |
| 0110 | 0 | 0x24 |
| 0101 | 0 | 0x28 |
| 0100 | 0 | 0x27 |
| 0011 | 0 | 0x2B |
| 0010 | 0 | 0x2C |
| 0001 | 0 | 0x2F |
| 0000 | 0 | 0x00 |
| XXX | Y | Z |

<a id="table-aktoren"></a>
### AKTOREN

Dimensions: 22 rows × 3 columns

| AKTOREN | BYTE | BITWERT |
| --- | --- | --- |
| MV_FR | 0 | 0x01 |
| MV_FL | 0 | 0x02 |
| MV_RR | 0 | 0x04 |
| MV_RL | 0 | 0x08 |
| MV_RES | 0 | 0x10 |
| MV_EX | 0 | 0x20 |
| C_SW | 0 | 0x40 |
| Vent+Komp_OFF | 0 | 0x00 |
| MV_CFR | 1 | 0x01 |
| MV_CFL | 1 | 0x02 |
| MV_CRR | 1 | 0x04 |
| MV_CRL | 1 | 0x08 |
| Crosslk_OFF | 1 | 0x00 |
| ACCESS_STATIC | 2 | 0x02 |
| MOTORWAY_STATIC | 2 | 0x08 |
| STANDARD_STATIC | 2 | 0x20 |
| OFFROAD_STATIC | 2 | 0x80 |
| LED_OFF | 2 | 0x00 |
| HOLD_STATIC | 3 | 0x02 |
| HOLD_LED_OFF | 3 | 0x00 |
| ALLE_AUS | 4 | 0x00 |
| XXX | Y | Z |

<a id="table-steuern-sg"></a>
### STEUERN_SG

Dimensions: 9 rows × 3 columns

| STEUER_SG | BYTE | BITWERT |
| --- | --- | --- |
| DUMP_MODUS | 0 | 0x01 |
| BAND_MODUS | 0 | 0x02 |
| VERLADEMODUS | 0 | 0x04 |
| BYPASSMODUS | 0 | 0x08 |
| EMV_KUNDENMODUS | 0 | 0x10 |
| HANDSTEUERMODUS | 0 | 0x20 |
| NOPLAUMODUS | 0 | 0x40 |
| ALLES_OFF | 0 | 0x00 |
| XXX | Y | Z |
