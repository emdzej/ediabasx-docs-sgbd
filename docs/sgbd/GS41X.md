# GS41X.prg

- Jobs: [19](#jobs)
- Tables: [5](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Getriebesteuerung 4.1x |
| ORIGIN | BMW TP-421 Mellersh |
| REVISION | 1.43 |
| AUTHOR | Softing SAG Ta, BMW TP-421 Mellersh |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Info fuer Anwender
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung
- [ENDE](#job-ende) - Abbruch der Kommunikation
- [IDENT](#job-ident) - Auslesen der Identifikationsdaten
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Beenden der Diagnose
- [RAM_LESEN](#job-ram-lesen) - RAM lesen
- [ROM_LESEN](#job-rom-lesen) - ROM lesen
- [RESET_ADAPTION](#job-reset-adaption) - Alle Adaptionswerte loeschen
- [STATUS_MOTORDREHZAHL](#job-status-motordrehzahl) - Auslesen der Motordrehzahl
- [STATUS_ABTRIEBSDREHZ](#job-status-abtriebsdrehz) - Auslesen der Abtriebsdrehzahl
- [STATUS_LASTSIGNAL_DKG](#job-status-lastsignal-dkg) - Auslesen des Lastsignals DKG
- [STATUS_UBATT](#job-status-ubatt) - Auslesen der Batteriespannung
- [STATUS_GETRIEBETEMP](#job-status-getriebetemp) - Auslesen der Getriebetemperatur
- [STATUS_EINSPRITZMENGE](#job-status-einspritzmenge) - Auslesen der Einspritzmenge
- [STATUS_DIGITAL_LESEN](#job-status-digital-lesen) - Auslesen der digitalen Eingangsstati
- [STEUERN_STELLGLIED_GETAKTET](#job-steuern-stellglied-getaktet) - Getaktetes Ansteuern der Stellglieder mit variablen Tastverhaeltnis und variabler Periodendauer
- [STATUS_KICKDOWN_SCHALTER](#job-status-kickdown-schalter) - Auslesen der digitalen Eingangsstati

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

<a id="job-ende"></a>
### ENDE

Abbruch der Kommunikation

_No arguments._

_No results._

<a id="job-ident"></a>
### IDENT

Auslesen der Identifikationsdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| ID_HW_ZULIEFERER | string | Zulieferer-Hardwarenummer |
| ID_SW_ZULIEFERER | string | Zulieferer-Softwarenummer |
| ID_GEN_NR | string | BMW Generationsnummer |
| ID_SW_NR | string | BMW-Softwarenummer (Laufende Nummer) |
| ID_DATUM | string | Herstelldatum |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_AIF_VORHANDEN | int | Ist ein AIF vorhanden (0 (nein)/ 1 (ja)) |

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
| F_UW2_NR | int | Umweltbedingung 2 des einzelnen Fehlers als Index |
| F_UW1_EINH | string | Umweltbedingung 2 des einzelnen Fehlers Einheit |
| F_UW2_TEXT | string | Umweltbedingung 2 des einzelnen Fehlers als Text |
| F_UW2_WERT | real | Umweltbedingung 2 des einzelnen Fehlers als Wert |
| F_UW2_EINH | string | Umweltbedingung 2 des einzelnen Fehlers  Einheit |
| F_CODEHEX | binary | 5 Fehlerbyte |

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
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |

<a id="job-ram-lesen"></a>
### RAM_LESEN

RAM lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int | Startadresse |
| ANZAHL | int | Anzahl zu lesender Bytes |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | Inhalt der Speicherzellen |
| JOB_STATUS | string | OKAY, ERROR_NACK |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| TELEGRAMM_ANT | binary | Antworttelegramm |

<a id="job-rom-lesen"></a>
### ROM_LESEN

ROM lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | int | Startadresse |
| ANZAHL | int | Anzahl zu lesender Bytes |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | Inhalt der Speicherzellen |
| JOB_STATUS | string | OKAY, ERROR_NACK |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| TELEGRAMM_ANT | binary | Antworttelegramm |

<a id="job-reset-adaption"></a>
### RESET_ADAPTION

Alle Adaptionswerte loeschen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADR_HI | int | Startadresse high |
| ADR_LO | int | Startadresse low |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_NACK |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| TELEGRAMM_ANT | binary | Antworttelegramm |

<a id="job-status-motordrehzahl"></a>
### STATUS_MOTORDREHZAHL

Auslesen der Motordrehzahl

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOTORDREHZAHL_WERT | int | Motordrehzahl Wert |
| STAT_MOTORDREHZAHL_EINH | string | Motordrehzahl Einheit [1/min] |
| JOB_STATUS | string | OKAY, ERROR_NACK |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| TELEGRAMM_ANT | binary | Antworttelegramm |

<a id="job-status-abtriebsdrehz"></a>
### STATUS_ABTRIEBSDREHZ

Auslesen der Abtriebsdrehzahl

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ABTRIEBSDREHZ_WERT | int | Abtriebsdrehzahl Wert |
| STAT_ABTRIEBSDREHZ_EINH | string | Abtriebsdrehzahl Einheit [1/min] |
| JOB_STATUS | string | OKAY, ERROR_NACK |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| TELEGRAMM_ANT | binary | Antworttelegramm |

<a id="job-status-lastsignal-dkg"></a>
### STATUS_LASTSIGNAL_DKG

Auslesen des Lastsignals DKG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LASTSIGNAL_DKG_WERT | real | Lastsignal DKG Wert |
| STAT_LASTSIGNAL_DKG_EINH | string | Lastsignal DKG Einheit [%] |
| JOB_STATUS | string | OKAY, ERROR_NACK |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| TELEGRAMM_ANT | binary | Antworttelegramm |

<a id="job-status-ubatt"></a>
### STATUS_UBATT

Auslesen der Batteriespannung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_UBATT_WERT | real | UBatt Wert |
| STAT_UBATT_EINH | string | UBatt Einheit [Volt] |
| JOB_STATUS | string | OKAY, ERROR_NACK |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| TELEGRAMM_ANT | binary | Antworttelegramm |

<a id="job-status-getriebetemp"></a>
### STATUS_GETRIEBETEMP

Auslesen der Getriebetemperatur

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GETRIEBETEMP_WERT | int | Getriebetemperatur Wert |
| STAT_GETRIEBETEMP_EINH | string | Getriebetemperatur Einheit [Grad C] |
| JOB_STATUS | string | OKAY, ERROR_NACK |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| TELEGRAMM_ANT | binary | Antworttelegramm |

<a id="job-status-einspritzmenge"></a>
### STATUS_EINSPRITZMENGE

Auslesen der Einspritzmenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EINSPRITZMENGE_WERT | real | Einspritzmenge Wert |
| STAT_EINSPRITZMENGE_EINH | string | Einspritzmenge Einheit [ms] |
| JOB_STATUS | string | OKAY, ERROR_NACK |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| TELEGRAMM_ANT | binary | Antworttelegramm |

<a id="job-status-digital-lesen"></a>
### STATUS_DIGITAL_LESEN

Auslesen der digitalen Eingangsstati

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_POSITIONSHEBEL | string | Stellung des Positionshebels (D,3,N,2,R,1,P,unplaus.) |
| STAT_STUFE_L1_EIN | int | Zustand der Codierschalter L1 |
| STAT_STUFE_L2_EIN | int | Zustand der Codierschalter L2 |
| STAT_STUFE_L3_EIN | int | Zustand der Codierschalter L3 |
| STAT_STUFE_L4_EIN | int | Zustand der Codierschalter L4 |
| STAT_KLIMAKOMPRESSOR_EIN | int | Status des Klimakompressors |
| STAT_PROGRAMMTASTER | string | Programmtasterauswertung (AUS,M,E,S,unplaus.) |
| STAT_MOTOREINGRIFF_EIN | int | Motoreingriff aktiv |
| STAT_KICKDOWN_EIN | int | Kickdownschalter ein |
| STAT_BREMSLICHT_EIN | int | Bremslicht ein |
| JOB_STATUS | string | OKAY, ERROR_NACK |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| TELEGRAMM_ANT | binary | Antworttelegramm |

<a id="job-steuern-stellglied-getaktet"></a>
### STEUERN_STELLGLIED_GETAKTET

Getaktetes Ansteuern der Stellglieder mit variablen Tastverhaeltnis und variabler Periodendauer

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STELLGL | string | Anzusteuerndes Stellglied MV_1_2 MV_2_3 MV_BAND MV_WK MOTOREINGRIFF PN_SPERRE DRUCKREGLER S_ANZEIGE E_ANZEIGE M_ANZEIGE STOERANZEIGE GETRIEBEREL |
| EINSCHZ | long | Einschaltzeit in Prozent (0 bis 100 %) |
| PERIODE | long | Periodendauer in Millisekunden (0 bis 25500 ms) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_ANSTEUERUNG | int | Ansteuerergebnis 0: Stellglied kann angesteuert werden 1: PIN-Nummer ist unbekannt 2: Positionshebel ist nicht in N oder P 3: Abtriebsdrehzahl ist zu hoch 4: Relais ist abgefallen, ein Fehler ist vorhanden |

<a id="job-status-kickdown-schalter"></a>
### STATUS_KICKDOWN_SCHALTER

Auslesen der digitalen Eingangsstati

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KICKDOWN_EIN | int | Kickdownschalter ein |
| JOB_STATUS | string | OKAY, ERROR_NACK |
| TELEGRAMM_ANF | binary | Anforderungstelegramm |
| TELEGRAMM_ANT | binary | Antworttelegramm |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (28 × 4)
- [FARTTEXTE](#table-farttexte) (19 × 2)
- [FARTMATRIX](#table-fartmatrix) (28 × 17)
- [FUMWELTTEXTE](#table-fumwelttexte) (10 × 5)
- [STELLGLIEDER](#table-stellglieder) (12 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 28 rows × 4 columns

| ORT | ORTTEXT | UW_1 | UW_2 |
| --- | --- | --- | --- |
| 0x01 | Magnet-Ventil Shift-Lock | 0x02 | 0x08 |
| 0x02 | Programmschalter | 0x07 | 0x04 |
| 0x04 | Motoreingriff | 0x02 | 0x08 |
| 0x09 | KVA-Signal | 0x03 | 0x01 |
| 0x0b | Drehzahlsignal n-mot | 0x03 | 0x02 |
| 0x14 | Drehzahlsignal n-ab | 0x01 | 0x08 |
| 0x16 | Oelsumpftemperatursensor | 0x05 | 0x02 |
| 0x17 | Waehlhebelposition | 0x01 | 0x02 |
| 0x1c | Ubatt Versorgung (perm.) | 0x04 | 0x05 |
| 0x1e | Kick-Down Schalter | 0x03 | 0x08 |
| 0x25 | Ubatt Versorgung | 0x04 | 0x02 |
| 0x26 | Magnetventil MV-WK | 0x02 | 0x08 |
| 0x28 | Druckregler | 0x06 | 0x08 |
| 0x2b | Magnetventil MV 2-3 | 0x02 | 0x08 |
| 0x2d | Magnetventil Band | 0x02 | 0x08 |
| 0x30 | Magnetventil MV 1-2/3-4 | 0x02 | 0x08 |
| 0x36 | Masse Magnetventile | 0x02 | 0x08 |
| 0x37 | Drosselklappensignal | 0x01 | 0x04 |
| 0x39 | Bremslichtschalter | 0x07 | 0x08 |
| 0x64 | Gangueberwachung | 0x01 | 0x02 |
| 0x65 | Rueckschaltsicherung | 0x01 | 0x02 |
| 0x66 | Ueberdrehsicherung | 0x01 | 0x08 |
| 0x67 | Checksumme EPROM | 0x07 | 0x08 |
| 0x68 | DKT Temperaturinfo | 0x01 | 0x05 |
| 0x69 | DKT Drosselklapppeninfo | 0x01 | 0x06 |
| 0x6a | DKT Einspritzmenge | 0x00 | 0x00 |
| 0x6b | Umschaltg. N-&gt;D b. hoher Abtriebsd. | 0x02 | 0x01 |
| 0xXY | unbekannte Fehlerart | 0x00 | 0x00 |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 19 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | Kurzschluss gegen U-Batt |
| 0x02 | Kurzschluss gegen Masse |
| 0x03 | Leitungsunterbrechung |
| 0x04 | Keine Plausibilitaet |
| 0x05 | Plausibilitaet |
| 0x06 | Bei letzter Abfrage nicht vorhanden |
| 0x07 | Bei letzter Abfrage vorhanden |
| 0x08 | Pruefbedingung nicht erreicht |
| 0x09 | Pruefbedingung erreicht |
| 0x0a | Fehler momentan nicht vorhanden |
| 0x0b | Fehler momentan vorhanden |
| 0x0c | statischer Fehler |
| 0x0d | sporadischer Fehler |
| 0x0e | Getriebetemperatur zu hoch (&gt; 165 Grad C) |
| 0x0f | Spg. ausserhalb d. gueltigen Bereichs |
| 0x10 | DME erkennt falsches Drosselklappensignal |
| 0x11 | DME sendet fehlerh. Motortemperatursignal |
| 0x12 | DME sendet fehlerh. Drosselklappensignal |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 28 rows × 17 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 | A6_0 | A6_1 | A7_0 | A7_1 | A8_0 | A8_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x01 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x02 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x04 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x09 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x0b | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x14 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x0e | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x16 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x17 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x1c | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x1e | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x25 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x0f | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x26 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x28 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x2b | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x2d | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x30 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x36 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x37 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x10 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x39 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x64 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x65 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x66 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x67 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x68 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x11 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x69 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x12 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x6a | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x6b | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 10 rows × 5 columns

| UWNR | UWTEXT | UW_EINH | UWF_A | UWF_B |
| --- | --- | --- | --- | --- |
| 0x00 | -- | -- | 1.0 | 0.0 |
| 0x01 | Motordrehzahl | [1/min] | 32.0 | 0.0 |
| 0x02 | Abbtriebsdrehzahl | [1/min] | 32.0 | 0.0 |
| 0x03 | Drosselklappe | [%] | 0.392 | 0.0 |
| 0x04 | Batteriespannng | [Volt] | 0.068 | 0.0 |
| 0x05 | Getriebeoeltemperatur | [Grad C] | 1.0 | -40.0 |
| 0x06 | Druckreglerstrom | [mA] | 1.0 | 0.0 |
| 0x07 | Statusbyte 1 | -- | 1.0 | 0.0 |
| 0x08 | Statusbyte 2 | -- | 1.0 | 0.0 |
| 0xXY | unbekannte Umweltbedingung | -- | 1.0 | 0.0 |

<a id="table-stellglieder"></a>
### STELLGLIEDER

Dimensions: 12 rows × 2 columns

| STELLGLIED | PIN |
| --- | --- |
| MV_1_2 | 48 |
| MV_2_3 | 43 |
| MV_BAND | 45 |
| MV_WK | 38 |
| MOTOREINGRIFF | 4 |
| PN_SPERRE | 1 |
| DRUCKREGLER | 40 |
| S_ANZEIGE | 7 |
| E_ANZEIGE | 10 |
| M_ANZEIGE | 12 |
| STOERANZEIGE | 29 |
| GETRIEBEREL | 54 |
