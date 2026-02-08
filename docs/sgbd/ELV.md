# ELV.prg

- Jobs: [14](#jobs)
- Tables: [12](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Elektrische Lenkungsverriegelung ELV |
| ORIGIN | BMW TI-430 Stefan Bendel |
| REVISION | 1.0 |
| AUTHOR | BMW TI-433 Gerd Huber, Valeo ESE Hagen Friedrich |
| COMMENT | N/A |
| PACKAGE | 0.02 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung / Kommunikationsparameter fuer ELV automatischer Aufruf beim ersten Zugriff auf die SGBD
- [IDENT](#job-ident) - Ident-Daten der Elektrischen Lenkungsverriegelung ELV auslesen
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose Sonderfall: Loeschdatum (KW/Jahr) integriert !
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen Sonderfall: Loeschdatum (KW/Jahr) integriert !
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen Info-Speicher ist im Aufbau analog zum Fehlerspeicher Low-Konzept nach Lastenheft Codierung/Diagnose
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen des internen Speichers der ELV Als Argumente werden die Anzahl und die Adresse der Datenbytes uebergeben.
- [STATUS_LESEN](#job-status-lesen) - Status der ELV auslesen
- [STEUERN_STAT_VORG_GESCH](#job-steuern-stat-vorg-gesch) - Status auf geschaerft setzen
- [STEUERN_STAT_VORG_NI_GESCH](#job-steuern-stat-vorg-ni-gesch) - Status auf nicht geschaerft setzen
- [STEUERN](#job-steuern) - Ansteuern der ELV ! erlaubte Namen des Arguments 'ORT' ueber Tool XTRACT.exe ! Aufruf 'XTRACT [-F] ELV.prg'
- [CODIERDATEN_LESEN](#job-codierdaten-lesen) - Auslesen der Codierdaten der ELV
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden

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

Initialisierung / Kommunikationsparameter fuer ELV automatischer Aufruf beim ersten Zugriff auf die SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten der Elektrischen Lenkungsverriegelung ELV auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | string | BMW-Hardwarenummer |
| ID_COD_INDEX | string | Codier-Index |
| ID_DIAG_INDEX | string | Diagnose-Index |
| ID_BUS_INDEX | string | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Text table Lieferanten LIEF_TEXT |
| ID_SW_NR | string | Softwarenummer |
| ID_AEND_NR | string | Aenderungsindex |
| ID_SERIEN_NR | string | Seriennummer |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose Sonderfall: Loeschdatum (KW/Jahr) integriert !

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | int | Index fuer Fehlerort momentan identisch Fehlerbyte |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_HFK | int | Fehlerhaeufigkeit Bereich: 0 - 31 |
| F_ART_ANZ | int | Anzahl der Fehlerarten Bereich: immer 1 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Bereich: immer 0 |
| F_ART1_NR | int | 1. (einzige) Fehlerart Bereich: 0, 1 |
| F_ART1_TEXT | string | 1. (einzige) Fehlerart als Text table FArtTexte ARTTEXT |
| F_LOESCHDATUM_KW | int | Loeschdatum des Fehlerspeichers (KW) |
| F_LOESCHDATUM_JAHR | int | Loeschdatum des Fehlerspeichers (Jahr) |
| _TEL_ANTWORT | binary | Hex-Antwort(en) von SG |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen Sonderfall: Loeschdatum (KW/Jahr) integriert !

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-lesen"></a>
### IS_LESEN

Infospeicher lesen Info-Speicher ist im Aufbau analog zum Fehlerspeicher Low-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_HEX_CODE | binary | Infodaten pro Fehler als Hexcode |
| F_ORT_NR | int | Index fuer Infoort momentan identisch Infobyte |
| F_ORT_TEXT | string | Infoort als Text table IOrtTexte ORTTEXT |
| F_HFK | int | Infohaeufigkeit Bereich: 0 - 31 |
| F_ART_ANZ | int | Anzahl der Infoarten Bereich: immer 1 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Bereich: immer 0 |
| F_ART1_NR | int | 1. (einzige) Infoart Bereich: 0, 1 |
| F_ART1_TEXT | string | 1. (einzige) Infoart als Text table IArtTexte ARTTEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Lesen des internen Speichers der ELV Als Argumente werden die Anzahl und die Adresse der Datenbytes uebergeben.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANZAHL | int | Bereich 1 - 32 |
| ADRESSE | int | Bereich 0x0000 - 0xFFFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | ausgelesene Daten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Status der ELV auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_IEIN_ENDLAGE_VER | string | Status Hallsensor 1 (Endlage Verriegelt) Interner Eingang keine Stoerung, Stoerung, 0 (nicht erregt), 1 (erregt) |
| STAT_IEIN_ENDLAGE_VER_int | int | Fehlerfreier Status Hallsensor 1 (Endlage Verriegelt) Interner Eingang Bereich: 0 (nicht erregt), 1 (erregt) |
| STAT_IEIN_ENDLAGE_ENT | string | gestoerter Status Hallsensor 2 (Endlage Entriegelt) Interner Eingang keine Stoerung, Stoerung, 0 (nicht erregt), 1 (erregt) |
| STAT_IEIN_ENDLAGE_ENT_int | int | Status Hallsensor 2 (Endlage Entriegelt) Interner Eingang Bereich: 0 (nicht erregt), 1 (erregt) |
| STAT_IEIN_SPERRP_GES | string | Status Hallsensor 3 (Sperrplattenstatus) Interner Eingang keine Stoerung, Stoerung, 0 (nicht erregt), 1 (erregt) |
| STAT_IEIN_SPERRP_GES_int | int | Status Hallsensor 3 (Sperrplattenstatus) Interner Eingang Bereich: 0 (nicht erregt), 1 (erregt) |
| STAT_IEIN_SPERRP_PN | string | Status Hallsensor 4 (Sperrplattenstatus fuer P/N) Interner Eingang keine Stoerung, Stoerung, 0 (nicht erregt), 1 (erregt) |
| STAT_IEIN_SPERRP_PN_int | int | Status Hallsensor 4 (Sperrplattenstatus fuer P/N) Interner Eingang Bereich: 0 (nicht erregt), 1 (erregt) |
| STAT_IEIN_R_PN_EWS | int | Rueckgelesener P/N-EWS-Ausgang Interner Eingang Bereich: ein, aus |
| STAT_IEIN_R_DRSP | int | Rueckgelesener Drehsperren-Treiberausgang Interner Eingang Bereich: ein, aus |
| STAT_IEIN_R_SMAG | int | Rueckgelesener SI-Magnettreiberausgang Interner Eingang Bereich: ein, aus |
| STAT_IEIN_R_MSP_ENT | int | Rueckgelesener Status 'Sperrplattenmotor Entriegeln' Interner Eingang Bereich: 0 (nicht angezogen), 1 (angezogen) |
| STAT_IEIN_D_DRSP | int | Diagnose (Status) Treiber Drehsperre Interner Eingang Bereich: 0 (nicht aktiv), 1 (aktiv) |
| STAT_IEIN_D_SMAG | int | Diagnose (Status) Treiber Sicherungsmagnet Interner Eingang Bereich: 0 (nicht aktiv), 1 (aktiv) |
| STAT_IEIN_D_SPERR | int | Diagnose (Status) Vollbruecke Sperrplatte Interner Eingang Bereich: 0 (nicht aktiv), 1 (aktiv) |
| STAT_EEIN_DREHK | string | Status Hallsensor 5 (Dreherkennung SZE) Externer Eingang Bereich: 0 (nicht erregt, nicht erkannt), 1 (erregt, erkannt), Stoerung |
| STAT_EEIN_DREHK_int | int | Status Hallsensor 5 (Dreherkennung SZE) Externer Eingang Bereich: 0 (nicht erregt, nicht erkannt), 1 (erregt, erkannt) |
| STAT_EEIN_P_N | int | Getriebewaehlhebel P/N-Eingang Externer Eingang Bereich: ein, aus |
| STAT_EEIN_KL15 | int | Lokal ueber Hardware vorliegende Klemme 15 Externer Eingang Bereich: ein, aus |
| STAT_EEIN_KLR | int | Lokal ueber Hardware vorliegende Klemme R Externer Eingang Bereich: ein, aus |
| STAT_EEIN_DFA_HL | int | Raddrehzahlfuehler hinten links Externer Eingang (Frequenz) Bereich: f &lt; 18Hz bedeutet "Fahrzeug steht" (&lt;3km/h) |
| STAT_EEIN_DFA_PLAU | int | Plausibilitaet Geschwindigkeitssignal Externer Eingang Bereich: 1 = 'Fahrzeug faehrt' ist unplausibel, 0 = 'Fahrzeug faehrt' ist plausibel |
| STAT_AUSG_12V_INT | int | 12V getaktet intern Ausgang Bereich: ein, aus |
| STAT_AUSG_PN_EWS | int | P/N-Ausgang zur EWS3 (Freigabeleitung) Ausgang Bereich: ein, aus |
| STAT_AUSG_DRSP | int | Drehsperren-Ansteuerung Ausgang Bereich: ein, aus |
| STAT_AUSG_SMAG_TR | int | Sicherungsmagnet-Ansteuerung Ausgang Bereich: ein, aus |
| STAT_AUSG_UNTREL | int | Unterbrechungsrelais-Ansteuerung Ausgang Bereich: ein, aus |
| STAT_AUSG_SP_ENT | int | 'Sperrplatte entriegeln'-Ansteuerung Ausgang Bereich: ein, aus |
| STAT_AUSG_SP_VER | int | 'Sperrplatte verriegeln'-Ansteuerung Ausgang Bereich: ein, aus |
| STAT_AUSG_SP_BRK | int | 'Sperrplatte bremsen'-Motoransteuerung Ausgang Bereich: ein, aus |
| STAT_AUSG_UDREK | int | 12V getaktet extern Ausgang Bereich: ein, aus |
| STAT_KBUS_KLR | string | 'Klemme R'-Information ueber K-Bus K-Bus Bereich: "definiert" / "undefiniert" |
| STAT_KBUS_KLR_int | int | 'Klemme R'-Information ueber K-Bus K-Bus Bereich: 0 (aus), 1 (ein) |
| STAT_KBUS_KL15 | string | 'Klemme 15'-Information ueber K-Bus K-Bus Bereich: "definiert" / "undefiniert" |
| STAT_KBUS_KL15_int | int | 'Klemme 15'-Information ueber K-Bus K-Bus Bereich: 0 (aus), 1 (ein) |
| STAT_KBUS_EWS_KEY | string | 'Gueltiger Schluessel im Schloss'-Information ueber K-Bus K-Bus Bereich: "nein" / "ja" |
| STAT_KBUS_EWS_KEY_int | int | 'Gueltiger Schluessel im Schloss'-Information ueber K-Bus K-Bus Bereich: "nein" / "ja" |
| STAT_KBUS_EWS_FREE | string | 'EWS freigeschaltet ueber Schluessel'-Information ueber K-Bus K-Bus Bereich: "nein" / "ja" |
| STAT_KBUS_EWS_FREE_int | int | 'EWS freigeschaltet ueber Schluessel'-Information ueber K-Bus K-Bus Bereich: "nein" / "ja" |
| STAT_KBUS_AIRBAG_CRASH | string | 'Grundmodul ZV oeffnen'-Information ueber K-Bus K-Bus Bereich: "nein" / "ja" |
| STAT_KBUS_AIRBAG_CRASH_int | int | 'Grundmodul ZV oeffnen'-Information ueber K-Bus K-Bus Bereich: "nein" / "ja" |
| STAT_KBUS_KL_UNDEF | string | 'Klemmenstatus undefiniert'-Information ueber K-Bus K-Bus Bereich: "nein" / "ja" |
| STAT_KBUS_KL_UNDEF_int | int | 'Klemmenstatus undefiniert'-Information ueber K-Bus K-Bus Bereich: "nein" / "ja" |
| STAT_KBUS_EWS_UNDEF | string | 'EWS-Status undefiniert'-Information ueber K-Bus K-Bus Bereich: "nein" / "ja" |
| STAT_KBUS_EWS_UNDEF_int | int | 'EWS-Status undefiniert'-Information ueber K-Bus K-Bus Bereich: "nein" / "ja" |
| STAT_ER_SICH | int | ELV ist entriegelt und gesichert Bereich: 0 (nein), 1 (ja) interner ELV-Status |
| STAT_VR | int | ELV ist verriegelt Bereich: 0 (nein), 1 (ja) interner ELV-Status |
| STAT_ER_MOV | int | ELV wird momentan entriegelt Bereich: 0 (nein), 1 (ja) interner ELV-Status |
| STAT_VR_MOV | int | ELV wird momentan verriegelt Bereich: 0 (nein), 1 (ja) interner ELV-Status |
| STAT_ER | int | ELV ist entriegelt Bereich: 0 (nein), 1 (ja) interner ELV-Status |
| STAT_GESCH | int | ELV geschaerft Bereich: 0 (nein), 1 (ja) interner ELV-Status |
| STAT_STATE_Ebene0 | string | ELV Zustand interner ELV-Status |
| STAT_STATE_Ebene1 | string | ELV Zustand interner ELV-Status |
| STAT_ALOG_U_KL30 | string | A/D-Wert von KL30 Analog-Werte Bereich: 0 .. 255 Digits Einheit: Volt |
| STAT_ALOG_U_EINH | string | Einheit der gemessenen A/D-Werte der Versorgungsspannung Analog-Werte |
| STAT_ALOG_I_DREK | string | A/D-Stromwert des Hallsensors 'Dreherkennung' Analog-Werte Bereich: 0 .. 255 Digits Einheit: mA |
| STAT_ALOG_I_SMAG_HALL | string | A/D-Stromwert des Hallsensors 'Sperrplatte gesichert' Analog-Werte Bereich: 0 .. 255 Digits Einheit: mA |
| STAT_ALOG_I_PN_HALL | string | A/D-Stromwert des Hallsensors 'P/N-Eingang' Analog-Werte Bereich: 0 .. 255 Digits Einheit: mA |
| STAT_ALOG_I_ELEK_ENT | string | A/D-Stromwert des Hallsensors 'Endlage entriegelt' Analog-Werte Bereich: 0 .. 255 Digits Einheit: mA |
| STAT_ALOG_I_ELEK_VER | string | A/D-Stromwert des Hallsensors 'Endlage verriegelt' Analog-Werte Bereich: 0 .. 255 Digits Einheit: mA |
| STAT_ALOG_I_EINH | string | Einheit der gemessenen A/D-Werte der Hallsensorstroeme Analog-Werte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-stat-vorg-gesch"></a>
### STEUERN_STAT_VORG_GESCH

Status auf geschaerft setzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-stat-vorg-ni-gesch"></a>
### STEUERN_STAT_VORG_NI_GESCH

Status auf nicht geschaerft setzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern"></a>
### STEUERN

Ansteuern der ELV ! erlaubte Namen des Arguments 'ORT' ueber Tool XTRACT.exe ! Aufruf 'XTRACT [-F] ELV.prg'

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ORT | string | gewuenschte Komponente table BITS NAME TEXT |
| EIN | int | '1' zum Einschalten / '0' zum Ausschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-lesen"></a>
### CODIERDATEN_LESEN

Auslesen der Codierdaten der ELV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| CODE_PN_EINGANG | string | Auswertung des P/N-Einganges Codierdaten Bereich: 1 = ja, 0 = nein |
| CODE_DSC_SIGNAL | string | Auswertung des DSC-Signales Codierdaten Bereich: 1 = Fahrzeug faehrt, 0 = Fahrzeug steht |
| CODE_SCHL_NR_GESCH | int | Schluesselnummer fuer Wechsel zu 'geschaerft' Codierdaten Bereich: 1...3 (aktuell) |
| CODE_CODIERUNG | string | Codierung Codierdaten Bereich: AAh = EEPROM, &lt;&gt;AAh = ROM |
| _TEL_ANTWORT | binary |  |

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Sleep-Mode versetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (8 × 2)
- [LIEFERANTEN](#table-lieferanten) (33 × 2)
- [FORTTEXTE](#table-forttexte) (35 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [CODETEXTE](#table-codetexte) (4 × 2)
- [IORTTEXTE](#table-iorttexte) (8 × 2)
- [IARTTEXTE](#table-iarttexte) (3 × 2)
- [STTEXTE_EBENE0](#table-sttexte-ebene0) (13 × 2)
- [STTEXTE_EBENE1](#table-sttexte-ebene1) (33 × 2)
- [HALLTEXTE](#table-halltexte) (4 × 2)
- [KBUSTEXTE](#table-kbustexte) (8 × 2)
- [BITS](#table-bits) (48 × 4)

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

Dimensions: 33 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
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
| 0x31 | DASA |
| 0x32 | Pioneer |
| 0xXY | unbekannter Hersteller |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 35 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | ELV Watchdog uC intern |
| 0x01 | ELV Prozessor ROM |
| 0x02 | ELV Taktgeber |
| 0x03 | ELV EEPROM |
| 0x04 | Fehler bei RAM-Check |
| 0x05 | Fehler bei ROM-Check |
| 0x07 | ELV noch nie kodiert oder Kodierdaten verloren |
| 0x10 | Treiber SI-Magnet defekt (Ub-Kurzschluss) |
| 0x11 | Treiber SI-Magnet defekt (Gnd-Kurzschluss oder Unterbrechung) |
| 0x12 | Beide Endlagenerkennungen gleichzeitig aktiv |
| 0x13 | Hallsensor 'Sicherungsmagnet' Unterbrechung oder Kurzschluss |
| 0x14 | Hallsensor 'P/N-Freigabe' Unterbrechung oder Kurzschluss |
| 0x15 | Hallsensor 'Endlage verriegelt' Unterbrechung oder Kurzschluss |
| 0x16 | Hallsensor 'Endlage entriegelt' Unterbrechung oder Kurzschluss |
| 0x17 | Fehler bei Verriegelungsvorgang (Anzahl Versuche ueberschritten) |
| 0x18 | Unterbrechungsrelais defekt |
| 0x19 | Spannungsueberwachung defekt |
| 0x1A | Sperrplattenmotor Kurz./Unterbr./Uebertemp. des Treibers in Richtung 'Ent' |
| 0x1B | Sicherungsmagnet defekt |
| 0x1C | Fehler bei Entriegelungsvorgang |
| 0x1D | Treiber Sicherungsmagnet Kurzschluss |
| 0x1E | Fehler bei Verriegelungsvorgang (Endlage 'Entr' nicht verlassen) |
| 0x1F | Interne Sensor-Spannungsversorgung defekt |
| 0x2A | Sperrplattenmotor Kurz./Unterbr./Uebertemp. des Treibers in Richtung 'Ver' |
| 0x2B | Verriegelung des SI-Magnettreibers ueber KL15 defekt |
| 0x40 | K-Bus oder EWS |
| 0x41 | Treiber DRSP defekt (DRSP oder Leitung DRSP mit Ub-Kurzschluss) |
| 0x42 | Treiber DRSP defekt (DRSP oder Leitung DRSP mit Gnd-Kurzschluss) |
| 0x43 | P/N-EWS 'low' (Leitung P/N-EWS mit Gnd-Kurzschluss) |
| 0x44 | P/N-EWS 'high' (Leitung P/N-EWS mit Ub-Kurzschluss) |
| 0x45 | Dreherkennung defekt oder KLR/KL15 mit Ub-Kurzschluss |
| 0x46 | Hallsensor 'Dreherkennung' hat Unterbrechung oder Kurzschluss |
| 0x47 | KLR mit Gnd-Kurzschluss/Unterbrechung oder KL15 mit Ub-Kurzschluss |
| 0x48 | Geschwindigkeitssignal unplausibel |
| 0xFF | unbekannter Fehler |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ART | ARTTEXT |
| --- | --- |
| 0x00 | sporadischer Fehler          |
| 0x01 | aktiver Fehler               |
| 0xFF | unbekannte Fehlerart         |

<a id="table-codetexte"></a>
### CODETEXTE

Dimensions: 4 rows × 2 columns

| CODE_NR | CODE_TEXTE |
| --- | --- |
| 0x00 | nein           |
| 0x01 | ja             |
| 0x10 | ROM            |
| 0xAA | EEPROM         |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 8 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x80 | Fehler bei Verriegelvorgang |
| 0x81 | Fehler bei Entriegelvorgang |
| 0x83 | Ueberlastsicherung aktiviert |
| 0x85 | Unterspannung bei Entriegelungsvorgang |
| 0x86 | Crash wurde ausgeloest |
| 0x87 | Verriegelungssperre Unterspannung aktiv |
| 0x88 | KLR- oder KL15- Abfall nicht ueber K-Bus bestaetigt |
| 0xXY | unbekannter Info-Ort |

<a id="table-iarttexte"></a>
### IARTTEXTE

Dimensions: 3 rows × 2 columns

| ART | ARTTEXT |
| --- | --- |
| 0x00 | sporadischer Fehler          |
| 0x01 | aktiver Fehler               |
| 0xFF | unbekannte Fehlerart         |

<a id="table-sttexte-ebene0"></a>
### STTEXTE_EBENE0

Dimensions: 13 rows × 2 columns

| ST_ART0 | ST_TEXTE0 |
| --- | --- |
| 0x00 | CHECK_ACTIVE_ERRORS |
| 0x01 | RESET_INIT |
| 0x02 | CHECK_RAM_ROM_EEPROM |
| 0x03 | RAM_ROM_EEPROM_ERROR |
| 0x04 | RESET_INIT_DONE |
| 0x05 | GET_SYSTEM_STAT |
| 0x06 | VERRIEGELT |
| 0x07 | ENTRIEGELT_UND_GES |
| 0x08 | ENTRIEGELN |
| 0x09 | ENTRIEGELN_FERTIG |
| 0x0A | VERRIEGELN |
| 0x0B | VERRIEGELN_FERTIG |
| 0xFF | unbekannter Zustand |

<a id="table-sttexte-ebene1"></a>
### STTEXTE_EBENE1

Dimensions: 33 rows × 2 columns

| ST_ART1 | ST_TEXTE1 |
| --- | --- |
| 0x00 | - |
| 0x10 | - |
| 0x20 | - |
| 0x30 | - |
| 0x40 | - |
| 0x50 | - |
| 0x60 | - |
| 0x61 | WARTE_DREH_SET |
| 0x62 | WARTE_KBUS_MESSAGE |
| 0x63 | WARTE_KBUS_RESPONSE |
| 0x70 | START_NICHT_FREIGEBEN |
| 0x71 | MOT_ZULEITUNG_UNTERBRECHEN |
| 0x72 | DAUERFEHLER_PRUEFEN |
| 0x73 | DREHSPERRE_VOR_START |
| 0x74 | MOT_ZULEITUNG_UNTERBRECHEN_R |
| 0x75 | DREHSPERRE_VOR_FAHRT1 |
| 0x76 | SICHERUNGSMAGNET_UEBERPRUEFEN |
| 0x77 | FAHREN_MOEGLICH |
| 0x78 | DREHSPERRE_NACH_START |
| 0x79 | DREHSPERRE_VOR_FAHRT2 |
| 0x80 | DEFAULT |
| 0x81 | WARTE_DREH_SCHL |
| 0x82 | AUSFUEHREN |
| 0x83 | ENTRIEGELN_MOVING |
| 0x84 | CHECK_SIMGNT |
| 0x90 | - |
| 0xA0 | AUSFUEHREN |
| 0xA1 | CHECK_SENSORS |
| 0xA2 | VERRIEGELN_MOVING |
| 0xA3 | VERRIEGELN_FERTIG |
| 0xA4 | CHECK_SIMGNT |
| 0xB0 | - |
| 0xFF | unbekannter Zustand |

<a id="table-halltexte"></a>
### HALLTEXTE

Dimensions: 4 rows × 2 columns

| HALL_NUMMER | HALL_TEXT |
| --- | --- |
| 0x00 | nicht erregt                    |
| 0x01 | erregt                          |
| 0x02 | Stoerung                        |
| 0xXY | unbekannter Hallsensor-Status   |

<a id="table-kbustexte"></a>
### KBUSTEXTE

Dimensions: 8 rows × 2 columns

| KBUS_NUMMER | KBUS_TEXT |
| --- | --- |
| 0x00 | aus                                     |
| 0x01 | ein                                     |
| 0x02 | undefiniert                             |
| 0x03 | gueltig                                 |
| 0x04 | ungueltig                               |
| 0x05 | ja                                      |
| 0x06 | nein                                    |
| 0xXY | unbekannter K-Bus Status                |

<a id="table-bits"></a>
### BITS

Dimensions: 48 rows × 4 columns

| ZELLE | BYTE | NAME | TEXT |
| --- | --- | --- | --- |
| 0 | 1 | STAT_EEIN_DREK | Dreherkennung ist aktiviert (von SZE) |
| 1 | 1 | STAT_EEIN_DREK_GEST | Signal Dreherkennung gestoert |
| 2 | 1 | STAT_EEIN_P_N | Getriebewaehlhebel P/N-Eingang 0: D , 1: P/N |
| 3 | 1 | STAT_EEIN_KLR | Klemme R ein |
| 4 | 1 | STAT_EEIN_KL15 | Klemme 15 ein |
| 5 | 1 | STAT_EEIN_DFA_HL | Fahrzeug faehrt (Raddrehzahlfuehler-Ausgang hinten links) |
| 6 | 1 | STAT_EEIN_DFA_PLAU | Geschwindigkeitssignal unplausibel |
| 8 | 2 | STAT_IEIN_ENDLAGE_VER | Hallsensor 'Endlagenerkennung verriegelt' |
| 10 | 2 | STAT_IEIN_ENDLAGE_ENT | Hallsensor 'Endlagenerkennung entriegelt' |
| 12 | 2 | STAT_IEIN_SPERRP_GES | Hallsensor 'Sicherungsmagnet gesichert', Anker angez./liegt auf Sperrplatte |
| 14 | 2 | STAT_IEIN_SPERRP_PN | Hallsensor 'Sicherungsmagnet P/N-Freigabe gesichert', Anker angez./liegt auf Sperrplatte |
| 16 | 3 | STAT_IEIN_R_PN_EWS | Ausgang 'P/N-EWS' rueckgelesen |
| 17 | 3 | STAT_IEIN_R_DRSP | Ausgang 'Drehsperre' rueckgelesen |
| 18 | 3 | STAT_IEIN_R_SMAG | Ausgang 'Sicherungsmagnet' rueckgelesen  |
| 19 | 3 | STAT_IEIN_R_MSP_ENT | Relais 'Motor Sperrplatte entriegeln' rueckgelesen |
| 20 | 3 | STAT_IEIN_D_DRSP | Diagnose (Status) 'Treiber Drehsperre'  |
| 21 | 3 | STAT_IEIN_D_SMAG | Diagnose (Status) 'Treiber Sicherungsmagnet'  |
| 22 | 3 | STAT_IEIN_D_SPERR | Diagnose (Status) 'Vollbruecke Sperrplatte'  |
| 24 | 4 | STAT_AUSG_12V_INT | 12V getaktet intern |
| 25 | 4 | STAT_AUSG_PN_EWS | P/N-Ausgang zur EWS3 (Freigabeleitung) |
| 26 | 4 | STAT_AUSG_DRSP | Drehsperre angesteuert |
| 27 | 4 | STAT_AUSG_SMAG_TR | Sicherungsmagnet angesteuert |
| 28 | 4 | STAT_AUSG_UNTREL | Unterbrechungsrelais |
| 29 | 4 | STAT_AUSG_SP_ENT | Sperrplatte entriegeln |
| 30 | 4 | STAT_AUSG_SP_VER | Sperrplatte verriegeln |
| 31 | 4 | STAT_AUSG_SP_BRK | Motor Sperrplatte bremsen |
| 32 | 5 | STAT_AUSG_UDREK | 12V getaktet extern |
| 40 | 6 | STAT_KBUS_KLR | 'Klemme R'-Information ueber K-Bus |
| 41 | 6 | STAT_KBUS_KL15 | 'Klemme 15'-Information ueber K-Bus |
| 42 | 6 | STAT_KBUS_EWS_Key | 'Gueltiger Schluessel im Schloss'-Information ueber K-Bus |
| 43 | 6 | STAT_KBUS_ESW_free | 'EWS freigeschaltet ueber Schluessel'-Information ueber K-Bus |
| 44 | 6 | STAT_KBUS_Airbag_Crash | 'Grundmodul ZV oeffnen'-Information ueber K-Bus |
| 45 | 6 | STAT_KBUS_KL_undef | Klemmenstatus ueber K-Bus ist undefiniert |
| 46 | 6 | STAT_KBUS_EWS_undef | Schluesselstatus ueber K-Bus ist undefiniert |
| 48 | 7 | STAT_ER_SICH | ELV ist entriegelt und gesichert |
| 49 | 7 | STAT_VR | ELV ist verriegelt |
| 50 | 7 | STAT_ER_MOV | ELV wird momentan entriegelt |
| 51 | 7 | STAT_VR_MOV | ELV wird momentan verriegelt |
| 52 | 7 | STAT_ER | ELV ist entriegelt |
| 56 | 8 | STAT_GESCH | ELV geschaerft |
| 64 | 9 | STAT_STATE | Momentan aktiver Zustand (nur fuer Entwickler) |
| XY | 10 | ALOG_U_KL30 | Spannung Klemme 30 |
| XY | 14 | ALOG_I_DREK | Strom ueber Hallsensor 'Dreherkennung'  |
| XY | 15 | ALOG_I_SMAG_HALL | Strom ueber Hallsensor 'Sicherungsmagnet'  |
| XY | 16 | ALOG_I_PN_HALL | Strom ueber Hallsensor 'P/N-Freigabe'  |
| XY | 17 | ALOG_I_ELEK_ENT | Strom ueber Hallsensor 'Endlagenerkennung entriegelt'  |
| XY | 18 | ALOG_I_ELEK_VER | Strom ueber Hallsensor 'Endlagenerkennung verriegelt'  |
| XY | XY | XY | nicht definiertes Signal |
