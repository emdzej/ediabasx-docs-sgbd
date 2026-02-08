# AHK.prg

- Jobs: [16](#jobs)
- Tables: [4](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Aktive Hinterachskinematik E31 |
| ORIGIN | BMW TP-421 Hirsch |
| REVISION | 1.64 |
| AUTHOR | BMW TP-421 Hirsch |
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
- [STATUS_LESEN](#job-status-lesen) - Status Eingaenge AHK
- [STATUS_FUNKTIONSAUSFUEHRUNG](#job-status-funktionsausfuehrung) - Auslesen des Status einer Funktionsausfuehrung
- [AKTIVE_DIAGNOSE](#job-aktive-diagnose) - Aktive Diagnose einschalten
- [K_ZAHL_SPEICHERN](#job-k-zahl-speichern) - Speichern der K-Zahl
- [O_STELLUNG_LENKRADW_SPEICHERN](#job-o-stellung-lenkradw-speichern) - Aktuelle Stellwegistposition als 0-Lenkradwinkel speichern
- [O_STELLUNG_HINTERRADLENKW_SPEICHERN](#job-o-stellung-hinterradlenkw-speichern) - Aktuelle Stellwegistposition als 0-Hinterradlenkwinkel speichern
- [DIGITALE_FKT_SCHALTEN](#job-digitale-fkt-schalten) - Schalten digitaler Funktionen (einzelne Ventile und Fehlerlampe)
- [POSITION_ANFAHREN](#job-position-anfahren) - Anfahren einer vorgegebenen Ist-Position
- [MECHANISCHE_MITTE_STELLEN](#job-mechanische-mitte-stellen) - Stellgied in die mechanische Mitte stellen
- [SYSTEM_DEAKTIVIEREN](#job-system-deaktivieren) - System dauerhaft deaktivieren (absolute Hochlaufsperre setzen)

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
| JOB_STATUS | string |  |
| ID_GEN_NR | int | Generationsnummer |
| ID_HW_NR | int | Hardwarenummer |
| ID_SW_NR | int | Softwarenummer |
| ID_PP_NR | int | Pruefplannummer |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_SG_NR | long | Steuergeraetenummer |

<a id="job-fs-lesen"></a>
### FS_LESEN

Auslesen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ORT_NR | int | Nr des Fehlers |
| F_ORT_TEXT | string | Fehlertext |
| F_HFK | int | Haeufigkeit eines Fehlers |
| F_ART_ANZ | int | Anzahl der Fehlerarten |
| F_ART1_NR | int | Textindex fuer Fehlerart 1 |
| F_ART1_TEXT | string | Text fuer Fehlerart 1 |
| F_ART2_NR | int | Textindex fuer Fehlerart 2 |
| F_ART2_TEXT | string | Text fuer Fehlerart 2 |
| F_ART3_NR | int | Textindex fuer Fehlerart 3 |
| F_ART3_TEXT | string | Text fuer Fehlerart 3 |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen |
| F_UW1_NR | int | Textindex der Umweltbedingung 1 |
| F_UW1_TEXT | string | Bedeutung der Umweltbedingung 1 |
| F_UW1_WERT | int | Integerwert der Umweltbedingung 1 |
| F_UW1_EINH | string | Einheit |
| F_UW2_NR | int | Textindex der Umweltbedingung 2 |
| F_UW2_TEXT | string | Bedeutung der Umweltbedingung 2 |
| F_UW2_WERT | int | Integerwert der Umweltbedingung 2 |
| F_UW2_EINH | string | Einheit |
| F_UW3_NR | int | Textindex der Umweltbedingung 3 |
| F_UW3_TEXT | string | Bedeutung der Umweltbedingung 3 |
| F_UW3_WERT | real | Realwert der Umweltbedingung 3 |
| F_UW3_EINH | string | Einheit |
| F_UW4_NR | int | Textindex der Umweltbedingung 4 |
| F_UW4_TEXT | string | Bedeutung der Umweltbedingung 4 |
| F_UW4_WERT | real | Realwert der Umweltbedingung 4 |
| F_UW4_EINH | string | Einheit |
| F_UW5_NR | int | Textindex der Umweltbedingung 5 |
| F_UW5_TEXT | string | Bedeutung der Umweltbedingung 5 |
| F_UW5_WERT | int | Integerwert der Umweltbedingung 5 |
| F_UW5_EINH | string | Einheit |
| F_UW6_NR | int | Textindex der Umweltbedingung 6 |
| F_UW6_TEXT | string | Bedeutung der Umweltbedingung 6 |
| F_UW6_WERT | int | Integerwert der Umweltbedingung 6 |
| F_UW6_EINH | string | Einheit |
| F_UW7_NR | int | Textindex der Umweltbedingung 7 |
| F_UW7_TEXT | string | Bedeutung der Umweltbedingung 7 |
| F_UW7_WERT | real | Realwert der Umweltbedingung 7 |
| F_UW7_EINH | string | Einheit |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| BUSY_ZEIT | unsigned int | Zeit bis zum Ende der Funktionsausfuehrung in Millisekunden |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Beenden der Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Status Eingaenge AHK

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_ECU_NACK |
| STAT_LENKRADW_1_WERT | long | Lenkradwinkel 1 in Grad |
| STAT_LENKRADW_BERECHNET_WERT | long | Lenkradwinkel berechnet in Grad |
| STAT_LENKRADW_EINH | string | Einheit aller Lenkradwinkel = Grad |
| STAT_STELLW_IST_POS_1_WERT | long | Stellwegistposition 1 in Millimeter |
| STAT_STELLW_IST_POS_2_WERT | long | Stellwegistposition 2 in Millimeter |
| STAT_STELLW_IST_POS_BERECHNET_WERT | long | Stellwegistposition berechnet in Millimeter |
| STAT_STELLW_SOLL_POS_WERT | long | Stellwegsollposition in Millimeter |
| STAT_STELLW_POS_EINH | string | Einheit aller Stellwegpositionen = mm |
| STAT_GESCHW_ABS_LINKS_WERT | long | Geschwindigkeit ABS links in km/h |
| STAT_GESCHW_ABS_RECHTS_WERT | long | Geschwindigkeit ABS rechts in km/h |
| STAT_GESCHW_EINH | string | Einheit fuer alle Geschwindigkeiten = km/h |
| STAT_TACHOSIGNAL_WERT | long | Tachosignal |
| STAT_TACHOSIGNAL_EINH | string | Einheit = 1 |
| STAT_GESCHW_BERECHNET_WERT | long | Geschwindigkeit berechnet |
| STAT_HYDRAULIK_DRUCK_WERT | long | Hydraulikdruck in bar |
| STAT_HYDRAULIK_DRUCK_EINH | string | Einheit = bar |
| STAT_BETRIEBSSPANNUNG_WERT | long | Betriebsspannung in Volt |
| STAT_BETRIEBSSPANNUNG_EINH | string | Einheit = Volt |
| STAT_AUSSEN_TEMPERATUR_WERT | long | Aussentemperatur in C |
| STAT_TEMPERATUR_EINH | string | Einheit fuer alle Temperaturen = C |
| STAT_SOFTWAREZUSTAND_WERT | int | Softwarezustand mit Werten zwischen XXXX0000 (X1XX0000) und XXXX1111 (X1XX1111) |
| STAT_SOFTWAREZUSTAND_TEXT | string | Softwarezustandtexte zu den Werten table SoftwareZustand WERT TEXT |
| STAT_EING_ABS_VL_EIN | int | 0 oder 1 |
| STAT_EING_ABS_VR_EIN | int | 0 oder 1 |
| STAT_EING_TACHO_EIN | int | 0 oder 1 |
| STAT_SPEICHERLADEVENTIL_AKTIV | int | 0 oder 1 |
| STAT_VENTIL_HYDR_KLEMMUNG_1_AKTIV | int | 0 oder 1 |
| STAT_VENTIL_HYDR_KLEMMUNG_2_AKTIV | int | 0 oder 1 |
| STAT_VENTIL_MECH_KLEMMUNG_AKTIV | int | 0 oder 1 |
| STAT_FEHLERLAMPE_KOMBI_EIN | int | 0 oder 1 |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| TELEGRAMM_ANT | binary | Antworttelegramm |

<a id="job-status-funktionsausfuehrung"></a>
### STATUS_FUNKTIONSAUSFUEHRUNG

Auslesen des Status einer Funktionsausfuehrung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY oder ERROR_ECU_NACK |

<a id="job-aktive-diagnose"></a>
### AKTIVE_DIAGNOSE

Aktive Diagnose einschalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY oder ERROR_ECU_NACK |

<a id="job-k-zahl-speichern"></a>
### K_ZAHL_SPEICHERN

Speichern der K-Zahl

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY oder ERROR_ECU_NACK |
| BUSY_ZEIT | unsigned int | Zeit bis zum Ende der Funktionsausfuehrung in Millisekunden |

<a id="job-o-stellung-lenkradw-speichern"></a>
### O_STELLUNG_LENKRADW_SPEICHERN

Aktuelle Stellwegistposition als 0-Lenkradwinkel speichern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY oder ERROR_ECU_NACK |
| BUSY_ZEIT | unsigned int | Zeit bis zum Ende der Funktionsausfuehrung in Millisekunden |

<a id="job-o-stellung-hinterradlenkw-speichern"></a>
### O_STELLUNG_HINTERRADLENKW_SPEICHERN

Aktuelle Stellwegistposition als 0-Hinterradlenkwinkel speichern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY oder ERROR_ECU_NACK |
| BUSY_ZEIT | unsigned int | Zeit bis zum Ende der Funktionsausfuehrung in Millisekunden |

<a id="job-digitale-fkt-schalten"></a>
### DIGITALE_FKT_SCHALTEN

Schalten digitaler Funktionen (einzelne Ventile und Fehlerlampe)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STATUS | string | EIN (Einschalten), AUS (Ausschalten) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY oder ERROR_ECU_NACK |
| BUSY_ZEIT | unsigned int | Zeit bis zum Ende der Funktionsausfuehrung in Millisekunden |

<a id="job-position-anfahren"></a>
### POSITION_ANFAHREN

Anfahren einer vorgegebenen Ist-Position

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| POSITION | int | Anzufahrende Position in 0.001 mm Gueltige Werte: -10 mm bis 10 mm |
| GESCHW | int | Verstellgeschwindigkeit in 0.01 mm/s Gueltige Werte: 1 mm/s bis 200 mm/s |
| ANZAHL | int | Anzahl der einfachen Wege Gueltige Werte: 1 bis 127 |
| FEHLERPRF | string | Fehlerpruefung Gueltige Werte: EIN, AUS |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY oder ERROR_ECU_NACK |
| BUSY_ZEIT | unsigned int | Zeit bis zum Ende der Funktionsausfuehrung in Millisekunden |

<a id="job-mechanische-mitte-stellen"></a>
### MECHANISCHE_MITTE_STELLEN

Stellgied in die mechanische Mitte stellen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY oder ERROR_ECU_NACK |
| BUSY_ZEIT | unsigned int | Zeit bis zum Ende der Funktionsausfuehrung in Millisekunden |

<a id="job-system-deaktivieren"></a>
### SYSTEM_DEAKTIVIEREN

System dauerhaft deaktivieren (absolute Hochlaufsperre setzen)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY oder ERROR_ECU_NACK |
| BUSY_ZEIT | unsigned int | Zeit bis zum Ende der Funktionsausfuehrung in Millisekunden |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (92 × 2)
- [FARTTEXTE](#table-farttexte) (7 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (7 × 2)
- [SOFTWAREZUSTAND](#table-softwarezustand) (17 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 92 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | Steuergeraetefehler |
| 0x06 | Stack Ueberlauf |
| 0x07 | Zykluszeitueberlauf |
| 0x10 | Kommunikationsfehler Zeitlimit |
| 0x11 | Synchronisationsfehler Zeitlimit |
| 0x1D | Feinpotentiometer Abgleich negative Referenzspannung |
| 0x1E | Feinpotentiometer ( 1 ) Fehler 90 Grad |
| 0x21 | Spannung Schleifer 1 Feinpotentiometer ( 1 ) |
| 0x22 | Spannung Schleifer 2 Feinpotentiometer ( 2 ) |
| 0x23 | Lenkradwinkelstatistik 0-Punkt |
| 0x25 | Lenkradwinkel &gt; Maximum |
| 0x27 | Lenkradwinkel Vergleichsfehler P1 zu P2 |
| 0x28 | Lenkradwinkel Abgleich Daten |
| 0x29 | Feinpotentiometer - Abgleich 90 Grad |
| 0x2A | Negative Referenzspannung Feinpotentiometer &gt; Maximum |
| 0x2B | Negative Referenzspannung Feinpotentiometer &lt; Minimum |
| 0x2C | LRW Abgleich Fehlerfehler |
| 0x2D | Klassierung nicht eindeutig |
| 0x2F | Aenderung Lenkradwinkel &gt; Maximum |
| 0x30 | Feinpotentiometer Abgleich unvollstaendig |
| 0x31 | Feinpotentiometer Abgleich Einbaulage |
| 0x32 | Radsensor vorne links VLV low Fehler |
| 0x33 | Radsensor vorne links VLV high Fehler |
| 0x34 | Radsensor vorne rechts VRV low Fehler |
| 0x35 | Radsensor vorne rechts VRV high Fehler |
| 0x36 | (Tacho 'A' Signal) VTACHO  low Fehler |
| 0x37 | (Tacho 'A' Signal) VTACHO  high Fehler |
| 0x39 | V - Abgleich Grenzen |
| 0x3A | V - Abgleich Daten |
| 0x3B | Vref - Vergleichsfehler P1 zu P2 |
| 0x3C | Stellweg Soll - Ist Toleranzfehler |
| 0x3E | Stellwegsensor 1 Schleiferspannung |
| 0x3F | Stellwegsensor 1 negative Referenzspannung &gt; Maximum |
| 0x40 | Stellwegsensor 2 Schleiferspannung |
| 0x41 | Stellwegsensor 1 negative Referenzspannung &lt; Minimum |
| 0x43 | Stellwegsensor 1 Abgleich Einbaulage |
| 0x44 | Stellwegsensor 2 Abgleich Einbaulage |
| 0x45 | Stellweg - Soll Vergleichsfehler P1 zu P2 |
| 0x46 | Abgleichfehler Differenz zw. Sensor 1 und Sensor 2 |
| 0x47 | Stellweg - Ist Abgleich Daten |
| 0x48 | Stellweg - Ist - Sensor 1 / 2 Vergleichsfehler |
| 0x49 | Stellweg - Ist - Differenz bei Klemm - Test |
| 0x4A | Stellwegsensor 2 positive Referenzspannung &gt; Maximum |
| 0x4B | Stellwegsensor 2 positive Referenzspannung &lt; Minimum |
| 0x4F | Stellweg - Ist Differenz |
| 0x50 | Fehlerlampe defekt |
| 0x64 | I - Bus defekt |
| 0x65 | EKM antwortet nicht |
| 0x69 | VLV - Vergleichsfehler P1 zu P2 |
| 0x6A | VRV - Vergleichsfehler P1 zu P2 |
| 0x6B | VTacho - Vergleichsfehler P1 zu P2 |
| 0x6E | EEProm Speicherfehler |
| 0x6F | EEProm dauernd busy |
| 0x73 | Oeldruck - Sensor - Spannung &lt; Minimum |
| 0x74 | Oeldruck - Sensor positive Referenzspannung &lt; Minimum |
| 0x75 | Oeldruck - Sensor positive Referenzspannung &gt; Maximum |
| 0x77 | Oeldruck - Sensor - Spannung &gt; Maximum |
| 0x78 | Aktivierungsdruck verloren |
| 0x79 | Keine Druckaenderung in 60 Sekunden |
| 0x7A | Mittler Speicherladezeit zu lang |
| 0x7B | Oeldruckwert kleiner Klemmschwelle |
| 0x7C | Oeldruckwert kleiner Aktivierungsschwelle |
| 0x7D | Oeldruckwert kleiner Notsteuerschwelle |
| 0x7E | Mittler Speicherentladezeit zu kurz |
| 0x7F | Oeldruck groesser Speicherabschaltschwelle |
| 0x80 | Einschaltdauer Speicherladeventil zu lang |
| 0x81 | Oeldruckvergleichsfehler P1 zu P2 |
| 0x82 | Stromregelfehler fuer Proportionalventilspule 1 |
| 0x83 | Stromregelfehler fuer Proportionalventilspule 2 |
| 0x84 | MSV-Fehler bei Klemmleitungstest |
| 0x85 | HSV1-Fehler bei Klemmleitungstest |
| 0x86 | HSV2-Fehler bei Klemmleitungstest |
| 0x87 | DV-Fehler bei Klemmleitungstest |
| 0x88 | PV1-Fehler bei Klemmleitungstest |
| 0x89 | PV2-Fehler bei Klemmleitungstest |
| 0x8A | PV1 + PV2 - Strom im Betrieb &gt; Maximum |
| 0x8B | PV - Strom Abgleich Grenzen |
| 0x8C | PV - Strom Abgleich Daten |
| 0x96 | Batteriespannng &lt; 9 V |
| 0x97 | Batteriespannng &lt; 10 V |
| 0x98 | Batteriespannng &lt; 11 V |
| 0x99 | Batteriespannng &gt; 16 V |
| 0x9A | Batteriespannng &gt; 18 V |
| 0x9D | Batteriespannng Abgleich Grenzen |
| 0x9E | Batteriespannng Abgleich Daten |
| 0x9F | Batteriespannng Vergleichsfehler P1 zu P2 |
| 0xA0 | Proportionalventil 1 Fehler |
| 0xB0 | Proportionalventil 2 Fehler |
| 0xC0 | Mechanisches Sperrventil |
| 0xD0 | Hydraulisches Sperrventil 1 |
| 0xE0 | Hydraulisches Sperrventil 2 |
| 0xF0 | Speicherladeventil |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 7 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | Fehler momentan nicht vorhanden |
| 0x02 | Fehler momentan vorhanden |
| 0x03 | Fehler trat bei ausgeschaltetem Ventil auf |
| 0x04 | Fehler trat bei eingeschaltetem Ventil auf |
| 0x05 | Letzter Fehler der die Klemmung ausloeste |
| 0x06 | Fehler aus Fehlerspeicherblock |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 7 rows × 2 columns

| UWNR | UWTEXT |
| --- | --- |
| 0x01 | Softwarezustand |
| 0x02 | Lenkradwinkel |
| 0x03 | Stellweg-Ist |
| 0x04 | Stellweg-Soll |
| 0x05 | Fahrgeschwindigkeit |
| 0x06 | Hydraulikdruck |
| 0x07 | Betriebsspannung |

<a id="table-softwarezustand"></a>
### SOFTWAREZUSTAND

Dimensions: 17 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Reset |
| 0x01 | Minimalzyklus |
| 0x02 | Test Minimalsystem |
| 0x03 | Power-Up-Check |
| 0x04 | Fehlerspeicherauswertung |
| 0x05 | Passivzyklus |
| 0x06 | Warten auf Kl. 15 |
| 0x07 | Stellgliedpruefungen |
| 0x08 | Uebergang Power-Up-Fahrzyklus |
| 0x09 | Fahrzyklus |
| 0x0A | Notsteuerung |
| 0x0B | Aktive Diagnose |
| 0x0C | Klemminterrupt |
| 0x0D | elektrische Ventilpruefung |
| 0x0E | Warten auf Pruefbedingungen |
| 0x0F | nicht belegt |
| 0xXX | EE-Prom oder Abgleichwerte defekt |
