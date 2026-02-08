# GS7X_K.prg

- Jobs: [26](#jobs)
- Tables: [7](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Getriebesteuerung 7.x Kennfeld |
| ORIGIN | BMW TP-421 Mellersh |
| REVISION | 1.65 |
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
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender-Info-Feldes
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Beenden der Diagnose
- [RAM_LESEN](#job-ram-lesen) - RAM lesen
- [ROM_LESEN](#job-rom-lesen) - ROM lesen
- [STATUS_MOTORDREHZAHL](#job-status-motordrehzahl) - Auslesen der Motordrehzahl
- [STATUS_ABTRIEBSDREHZAHL](#job-status-abtriebsdrehzahl) - Auslesen der Abtriebsdrehzahl
- [STATUS_LASTSIGNAL](#job-status-lastsignal) - Auslesen des Lastsignals
- [STATUS_DROSSELKLAPPE](#job-status-drosselklappe) - Auslesen der Drosselklappenstellung (7.11 und hoeher)
- [STATUS_STEGDREHZAHL](#job-status-stegdrehzahl) - Auslesen der Stegdrehzahl
- [STATUS_GETR_OELTEMPERATUR](#job-status-getr-oeltemperatur) - Auslesen der Getriebeoeltemperatur (7.11 und hoeher)
- [STATUS_BATTERIESPANNUNG](#job-status-batteriespannung) - Auslesen der Batteriespannung
- [STATUS_STATUSBYTE1](#job-status-statusbyte1) - Auslesen des 1. Statusbytes
- [STATUS_STATUSBYTE2](#job-status-statusbyte2) - Auslesen des 2. Statusbytes
- [STATUS_STATUSBYTE3](#job-status-statusbyte3) - Auslesen des 3. Statusbytes
- [STATUS_STATUSBYTE4](#job-status-statusbyte4) - Auslesen des 4. Statusbytes
- [STATUS_STATUSBYTE5](#job-status-statusbyte5) - Auslesen des 5. Statusbytes
- [STATUS_WAEHLHEBELSTELLUNG](#job-status-waehlhebelstellung) - Auslesen der Waehlhebelstellung
- [STATUS_GANG](#job-status-gang) - Anzeige des eingelegten Gangs
- [STEUERN_STELLGLIED_GETAKTET](#job-steuern-stellglied-getaktet) - Getaktetes Ansteuern der Stellglieder
- [STATUS_KICKDOWN_SCHALTER](#job-status-kickdown-schalter) - Auslesen des Kickdown-Schalters

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
| ID_ZF_NR | string | Getriebeteilenummer |
| ID_AIF_VORHANDEN | int | Ist ein AIF vorhanden (0 (nein)/ 1 (ja)) |

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

<a id="job-status-motordrehzahl"></a>
### STATUS_MOTORDREHZAHL

Auslesen der Motordrehzahl

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_MOTORDREHZAHL_WERT | long | Motordrehzahl als Wert |
| STAT_MOTORDREHZAHL_EINH | string | Einheit der Motordrehzahl [1/min] |

<a id="job-status-abtriebsdrehzahl"></a>
### STATUS_ABTRIEBSDREHZAHL

Auslesen der Abtriebsdrehzahl

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_ABTRIEBSDREHZAHL_WERT | long | Abtriebsdrehzahl als Wert |
| STAT_ABTRIEBSDREHZAHL_EINH | string | Einheit der Abtriebsdrehzahl [1/min] |

<a id="job-status-lastsignal"></a>
### STATUS_LASTSIGNAL

Auslesen des Lastsignals

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_LASTSIGNAL_WERT | long | Lastsignal als Wert |
| STAT_LASTSIGNAL_EINH | string | Einheit des Lastsignal [ms] |

<a id="job-status-drosselklappe"></a>
### STATUS_DROSSELKLAPPE

Auslesen der Drosselklappenstellung (7.11 und hoeher)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_DROSSELKLAPPE_WERT | long | Drosselklappenimpuls als Wert |
| STAT_DROSSELKLAPPE_EINH | string | Einheit der Drosselklappenstellung [%] |

<a id="job-status-stegdrehzahl"></a>
### STATUS_STEGDREHZAHL

Auslesen der Stegdrehzahl

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_STEGDREHZAHL_WERT | long | Stegdrehzahl als Wert |
| STAT_STEGDREHZAHL_EINH | string | Einheit der Stegdrehzahl [1/min] |

<a id="job-status-getr-oeltemperatur"></a>
### STATUS_GETR_OELTEMPERATUR

Auslesen der Getriebeoeltemperatur (7.11 und hoeher)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_GETR_OELTEMPERATUR_WERT | long | Getriebeoeltemperatur als Wert |
| STAT_GETR_OELTEMPERATUR_EINH | string | Einheit der Getriebeoeltemperatur [Grad C] |

<a id="job-status-batteriespannung"></a>
### STATUS_BATTERIESPANNUNG

Auslesen der Batteriespannung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_BATTERIESPANNUNG_WERT | long | Batteriespannung als Wert |
| STAT_BATTERIESPANNUNG_EINH | string | Einheit der Batteriespannung [Volt] |

<a id="job-status-statusbyte1"></a>
### STATUS_STATUSBYTE1

Auslesen des 1. Statusbytes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_AUSG_MAGNETVENTIL_1_EIN | int |  |
| STAT_AUSG_MAGNETVENTIL_2_EIN | int |  |
| STAT_AUSG_MAGNETVENTIL_3_EIN | int |  |
| STAT_AUSG_MAGNETVENTIL_4_EIN | int |  |
| STAT_AUSG_MAGNETVENTIL_5_EIN | int |  |
| STAT_AUSG_MAGNETVENTIL_WK_EIN | int |  |
| STAT_AUSG_HUBMAGNET_PN_SPERRE_EIN | int |  |
| STAT_AUSG_ABLAUFENDE_HS_RS_EIN | int |  |

<a id="job-status-statusbyte2"></a>
### STATUS_STATUSBYTE2

Auslesen des 2. Statusbytes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_EING_PROGRAMM_S_EIN | int |  |
| STAT_EING_PROGRAMM_E_EIN | int |  |
| STAT_EING_PROGRAMM_M_EIN | int |  |
| STAT_EING_PROGRAMM_W_EIN | int |  |
| STAT_AUSG_PROGRAMM_S_EIN | int |  |
| STAT_AUSG_PROGRAMM_E_EIN | int |  |
| STAT_AUSG_PROGRAMM_M_EIN | int |  |
| STAT_AUSG_PROGRAMM_W_EIN | int |  |

<a id="job-status-statusbyte3"></a>
### STATUS_STATUSBYTE3

Auslesen des 3. Statusbytes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_EING_OVERDRIVE_EIN | int |  |
| STAT_EING_ASC_EIN | int |  |
| STAT_EING_KICK_DOWN_EIN | int |  |
| STAT_EING_BREMSLICHTSCHALTER_EIN | int |  |
| STAT_EING_BREMSTESTSCHALTER_EIN | int |  |
| STAT_EING_POSITIONSHEBEL | string | Stellung des Positionshebels (D,3,N,2,R,P,4,unplaus.) |
| STAT_EING_LEITERBAHN_1_EIN | int |  |
| STAT_EING_LEITERBAHN_2_EIN | int |  |
| STAT_EING_LEITERBAHN_3_EIN | int |  |
| STAT_EING_LEITERBAHN_4_EIN | int |  |

<a id="job-status-statusbyte4"></a>
### STATUS_STATUSBYTE4

Auslesen des 4. Statusbytes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_AUSG_MOTOREINGRIFF_EIN | int |  |
| STAT_AUSG_STOERANZEIGE_EIN | int |  |
| STAT_EING_REIZLEITUNG_DIAGNOSE_EIN | int |  |

<a id="job-status-statusbyte5"></a>
### STATUS_STATUSBYTE5

Auslesen des 5. Statusbytes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_RUECKMELDUNG_MV3_EIN | int |  |
| STAT_RUECKMELDUNG_MV5_EIN | int |  |
| STAT_RUECKMELDUNG_MV2_EIN | int |  |
| STAT_AUSG_KS_VON_MJ44_EIN | int |  |
| STAT_AUSG_LL_VON_MJ44_EIN | int |  |
| STAT_RUECKFUEHRUNG_MOTOREINGRIFF_EIN | int |  |
| STAT_RUECKFUEHRUNG_DRUCKREGLER_EIN | int |  |

<a id="job-status-waehlhebelstellung"></a>
### STATUS_WAEHLHEBELSTELLUNG

Auslesen der Waehlhebelstellung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_WAEHLHEBELSTELLUNG | string | Waehlhebelstellung (D,3,N,2,R,P,4,unplaus.) |

<a id="job-status-gang"></a>
### STATUS_GANG

Anzeige des eingelegten Gangs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_GANG | string | Gang |

<a id="job-steuern-stellglied-getaktet"></a>
### STEUERN_STELLGLIED_GETAKTET

Getaktetes Ansteuern der Stellglieder

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STELLGL | string | Anzusteuerndes Stellglied MAGNETVENTIL_1 MAGNETVENTIL_2 MAGNETVENTIL_3 MAGNETVENTIL_4 MAGNETVENTIL_5 MAGNETVENTIL_WK HUBM_PN_SPERRE MV_DRUCKREGLER SPG_VERS_MV_DR ZUENDWINKELEINGR S_ANZEIGE E_ANZEIGE W_ANZEIGE STOERANZEIGE |
| EINSCHZ | long | Einschaltzeit in Prozent (0 bis 100 %) |
| PERIODE | long | Periodendauer in Millisekunden (0 bis 25500 ms) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_ANSTEUERUNG | int | Ansteuerergebnis 0: Stellglied kann angesteuert werden 1: PIN-Nummer ist unbekannt 2: Positionshebel ist nicht in N oder P 3: Abtriebsdrehzahl ist zu hoch 4: Relais ist abgefallen, ein Fehler ist vorhanden |

<a id="job-status-kickdown-schalter"></a>
### STATUS_KICKDOWN_SCHALTER

Auslesen des Kickdown-Schalters

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| STAT_EING_KICK_DOWN_EIN | int |  |

## Tables

### Index

- [FORTTEXTE](#table-forttexte) (41 × 4)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [FARTMATRIX](#table-fartmatrix) (40 × 17)
- [FUMWELTTEXTE](#table-fumwelttexte) (12 × 5)
- [STATUSAMATRIX](#table-statusamatrix) (7 × 5)
- [GANGTABELLE](#table-gangtabelle) (7 × 2)
- [STELLGLIEDER](#table-stellglieder) (14 × 2)

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 41 rows × 4 columns

| ORT | ORTTEXT | UW_1 | UW_2 |
| --- | --- | --- | --- |
| 0x02 | HubMagnet P/N-Sperre | 0x08 | 0x0a |
| 0x03 | Magnetventil MV5 | 0x08 | 0x02 |
| 0x04 | Magnetventil MV-WK | 0x08 | 0x02 |
| 0x05 | Druckregler | 0x08 | 0x02 |
| 0x08 | Waehlhebelposition L2 | 0x0a | 0x02 |
| 0x09 | Waehlhebelposition L3 L4 | 0x0a | 0x02 |
| 0x0c | Programmschalter | 0x09 | 0x0a |
| 0x10 | Drehzahlgeber Turbine | 0x03 | 0x08 |
| 0x12 | Kick-Down Schalter | 0x05 | 0x0a |
| 0x13 | ASC-Ueberwachung | 0x05 | 0x04 |
| 0x16 | Oelsumpftemperatursensor | 0x04 | 0x08 |
| 0x1a | Ubatt Versorgung (perm.) | 0x06 | 0x07 |
| 0x1e | Magnetventil MV1 | 0x08 | 0x0a |
| 0x1f | Magnetventil MV4 | 0x08 | 0x0a |
| 0x20 | Magnetventil MV3 | 0x08 | 0x04 |
| 0x21 | Magnetventil MV2 | 0x08 | 0x0a |
| 0x23 | Drosselklappensignal (DKT) | 0x04 | 0x08 |
| 0x24 | Waehlhebelposition L1 | 0x0a | 0x02 |
| 0x28 | Motoreingriff | 0x08 | 0x0a |
| 0x29 | KVA-Signal | 0x04 | 0x08 |
| 0x2a | Drehzahlsignal n-ab | 0x02 | 0x01 |
| 0x2b | Drehzahlsignal n-mot | 0x05 | 0x04 |
| 0x35 | Spannungsversorgung MV | 0x04 | 0x09 |
| 0x36 | Ubatt Versorgung | 0x08 | 0x04 |
| 0x64 | Gangueberwachung | 0x03 | 0x08 |
| 0x65 | Checksumme EPROM | 0x08 | 0x0a |
| 0x66 | Checksumme Programminsel | 0x08 | 0x0a |
| 0x67 | Getrieberelais | 0x04 | 0x09 |
| 0x68 | DKT Temperaturinfo | 0x02 | 0x07 |
| 0x69 | DKT Drosselklapppeninfo | 0x02 | 0x05 |
| 0x6A | MUX Einspritzmenge | 0x04 | 0x09 |
| 0x6e | Grunddatensatz | 0x06 | 0x0a |
| 0x96 | Timeout in Initialisierung | 0x06 | 0x0a |
| 0x97 | Timeout im Betrieb | 0x04 | 0x0a |
| 0x98 | CAN-Busueberwachung | 0x06 | 0x02 |
| 0x99 | CAN-Stand Fehler | 0x06 | 0x0a |
| 0x9a | DK-Info ueber CAN | 0x05 | 0x00 |
| 0x9b | T_L-Info ueber CAN | 0x00 | 0x02 |
| 0x9c | Momentenreduzierung | 0x00 | 0x00 |
| 0x9d | Temperatur-Info von CAN | 0x00 | 0x00 |
| 0xXY | unbekannter Fehlerort | 0x00 | 0x00 |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 14 rows × 2 columns

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

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 40 rows × 17 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 | A6_0 | A6_1 | A7_0 | A7_1 | A8_0 | A8_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x02 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x03 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x04 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x05 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x08 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x09 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x0c | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x10 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x12 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x13 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x16 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x1a | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x1e | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x1f | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x20 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x21 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x23 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x24 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x28 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x29 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x2a | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x2b | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x35 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x36 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x64 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x65 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x66 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x67 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x68 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x69 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x6e | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x96 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x97 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x98 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x99 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x9a | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x9b | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x9c | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |
| 0x9d | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 12 rows × 5 columns

| UWNR | UWTEXT | UW_EINH | UWF_A | UWF_B |
| --- | --- | --- | --- | --- |
| 0x00 | ---- | ---- | 1.0 | 0.0 |
| 0x01 | Gang | . Gang | 1.0 | 0.0 |
| 0x02 | Motordrehzahl | [1/min] | 32.0 | 0.0 |
| 0x03 | Turbinendrehzahl | [1/min] | 32.0 | 0.0 |
| 0x04 | Abbtriebsdrehzahl | [1/min] | 32.0 | 0.0 |
| 0x05 | Fahrpedalstellung | [%] | 0.392 | 0.0 |
| 0x06 | Batteriespannng | [Volt] | 0.082 | 0.0 |
| 0x07 | Getriebeoeltemperatur | [Grad C] | 1.0 | -55.0 |
| 0x08 | Statusbyte 1 | -- | 1.0 | 0.0 |
| 0x09 | Statusbyte 2 | -- | 1.0 | 0.0 |
| 0x0a | Statusbyte 3 | -- | 1.0 | 0.0 |
| 0xXY | unbekannte Umweltbedingung | -- | 1.0 | 0.0 |

<a id="table-statusamatrix"></a>
### STATUSAMATRIX

Dimensions: 7 rows × 5 columns

| SNAME | TYP | FAKT_A | FAKT_B | EINH |
| --- | --- | --- | --- | --- |
| Motordrehz | 1 | 32000 | 0 | 1/min |
| Abtrdrehz | 1 | 32000 | 0 | 1/min |
| KVA | 1 | 80 | 0 | ms |
| DKI | 1 | 392 | 0 | % |
| Stegdrehz | 1 | 32000 | 0 | 1/min |
| Getroelt | 1 | 1000 | -55000 | Grad C |
| Ubatt | 1 | 82 | 0 | Volt |

<a id="table-gangtabelle"></a>
### GANGTABELLE

Dimensions: 7 rows × 2 columns

| GNR | GTEXT |
| --- | --- |
| 0x00 | Gang 4 |
| 0x20 | Gang 3 |
| 0x60 | Gang 2 |
| 0x80 | Gang 5 |
| 0xc0 | Gang 1/R |
| 0xe0 | Gang P/N/1 |
| xxxx | Gang ? |

<a id="table-stellglieder"></a>
### STELLGLIEDER

Dimensions: 14 rows × 2 columns

| STELLGLIED | PIN |
| --- | --- |
| MAGNETVENTIL_1 | 0x1e |
| MAGNETVENTIL_2 | 0x21 |
| MAGNETVENTIL_3 | 0x20 |
| MAGNETVENTIL_4 | 0x1f |
| MAGNETVENTIL_5 | 0x03 |
| MAGNETVENTIL_WK | 0x04 |
| HUBM_PN_SPERRE | 0x02 |
| MV_DRUCKREGLER | 0x05 |
| SPG_VERS_MV_DR | 0x35 |
| ZUENDWINKELEINGR | 0x28 |
| S_ANZEIGE | 0x11 |
| E_ANZEIGE | 0x27 |
| W_ANZEIGE | 0x0C |
| STOERANZEIGE | 0x19 |
