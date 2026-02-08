# mrehks.prg

- Jobs: [44](#jobs)
- Tables: [5](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Elektrohydraulischer Kippständer EHKS |
| ORIGIN | I+ME Actia GmbH, Keck |
| REVISION | 1.030 |
| AUTHOR | I+ME Actia GmbH, Keck und BMW Motorrad, Kufer |
| COMMENT | N/A |
| PACKAGE | 1.52 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung
- [IDENT](#job-ident) - Modus  : Default
- [STATUS_TEILENUMMER](#job-status-teilenummer) - Teilenummer lesen Byte 4-7, BCD
- [STATUS_HARDWARESTAND](#job-status-hardwarestand) - Hardwarestand lesen Byte 8, BCD
- [STATUS_CODIERINDEX](#job-status-codierindex) - Codierindex lesen Byte 9
- [STATUS_DIAGNOSEINDEX](#job-status-diagnoseindex) - Diagnoseindex lesen Byte 10
- [STATUS_BUSINDEX](#job-status-busindex) - BusIndex lesen Byte 11
- [STATUS_HERSTELLUNGSKALENDERWOCHE](#job-status-herstellungskalenderwoche) - Kalenderwoche lesen Byte 12
- [STATUS_HERSTELLUNGSKALENDERJAHR](#job-status-herstellungskalenderjahr) - Kalenderjahr lesen Byte 13
- [STATUS_ZULIEFERER](#job-status-zulieferer) - Zulieferer lesen Byte 14
- [STATUS_SOFTWARESTAND](#job-status-softwarestand) - Softwarestand lesen Byte 15
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Rücksetzen des Steuergerätes in den normalen Betrieb
- [STATUS_SERIENNUMMER](#job-status-seriennummer) - Seriennummer lesen
- [STATUS_DAUER_MOTORLAUF](#job-status-dauer-motorlauf) - maximale Einschaltdauer Motor Byte 5-6 lesen
- [STATUS_EHKS_TASTER_ENTPRELLZEIT](#job-status-ehks-taster-entprellzeit) - Entprellzeit EHKS-Taster Byte 7 lesen
- [STATUS_ENDPOSITIONSSCHALTER_ENTPRELLZEIT](#job-status-endpositionsschalter-entprellzeit) - Entprellzeit Endpositionsschalter Byte 8 lesen
- [STATUS_SEITENSTUETZE_ENTPRELLZEIT](#job-status-seitenstuetze-entprellzeit) - Entprellzeit Seitenstütze Byte 9
- [STATUS_BREMSLICHT_ENTPRELLZEIT](#job-status-bremslicht-entprellzeit) - Entprellzeit Bremslicht Byte 10
- [STATUS_LEERLAUF_SIGNAL_ENTRELLZEIT](#job-status-leerlauf-signal-entrellzeit) - Entprellzeit Leerlaufsignal Byte 11
- [STATUS_KLEMME15_ENTRPELLZEIT](#job-status-klemme15-entrpellzeit) - Klemme 15 Entprellzeit Byte 12
- [STATUS_KLEMME30_ENTPRELLZEIT](#job-status-klemme30-entprellzeit) - Klemme 30 Entprellzeit Byte 13
- [STATUS_BETAETIGUNG_MIN_PAUSE](#job-status-betaetigung-min-pause) - Minimale Pause zwischen 2 Aktivierungen Byte 16-17
- [STATUS_SYSTEMUEBERLAST_DAUER](#job-status-systemueberlast-dauer) - Dauer der Systemüberlast lesen Byte 18-19
- [STATUS_UEBERLAST_MIN_PAUSE](#job-status-ueberlast-min-pause) - Minimale Pause nach Systemüberlast Byte 20-21
- [STATUS_RESET_DURCH_KL15_EIN](#job-status-reset-durch-kl15-ein) - System Reset wenn die Zündung eingeschaltet wird lesen (Ja/Nein) Byte 22
- [STATUS_LED_FREQUENZ](#job-status-led-frequenz) - Lesen der Led Frequenz bei Betrieb und Überlast (4 oder 2 Hz) Byte 23
- [STATUS_KLEMME30](#job-status-klemme30) - Batteriespannung lesen Byte 4-5
- [STATUS_KLEMME15](#job-status-klemme15) - Spannung Klemme 15 (Zündung) lesen Byte 8-9
- [STATUS_SCHALTER_ENDPOSITION](#job-status-schalter-endposition) - Status Schalter Endposition lesen Byte 16
- [STATUS_EHKS_TASTER](#job-status-ehks-taster) - Status EHKS-Taster lesen Byte 17
- [STATUS_BREMSLICHTSIGNAL](#job-status-bremslichtsignal) - Status Bremslichtsignal lesen Byte 18
- [STATUS_GESCHWINDIGKEIT](#job-status-geschwindigkeit) - Geschwindigkeit lesen Byte 19
- [STATUS_SEITENSTUETZSCHALTER](#job-status-seitenstuetzschalter) - Schalter Seitenstütze lesen Byte 20
- [STATUS_LEERLAUF_SIGNAL](#job-status-leerlauf-signal) - Leerlaufsignal lesen Byte 21
- [STATUS_WARNLAMPE](#job-status-warnlampe) - Status EHKS-Kontrollleuchte lesen Byte 22
- [STATUS_RELAIS](#job-status-relais) - Status EHKS-Relais lesen Byte 23
- [FS_ANZAHL](#job-fs-anzahl) - Fehlerspeicher lesen (alle Fehler) Security Access Level 1 notwendig
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen (alle Fehler)
- [FS_LESEN_FELD](#job-fs-lesen-feld) - Fehlerspeicher lesen (ein Fehlerfeld)
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher Löschen
- [STEUERN_LED](#job-steuern-led) - Led ansteuern
- [STEUERN_RELAIS](#job-steuern-relais) - EHKS Relais ansteuern
- [STEUERN_SELBSTTEST](#job-steuern-selbsttest) - Selbsttest EHKS starten

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

Initialisierung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn i.O. |

<a id="job-ident"></a>
### IDENT

Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| VARIANTE_IND | string | Name der SGBD, immer MREHKS |
| STAT_WERT | string | BMW-Teilenummer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-teilenummer"></a>
### STATUS_TEILENUMMER

Teilenummer lesen Byte 4-7, BCD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | BMW-Teilenummer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-status-hardwarestand"></a>
### STATUS_HARDWARESTAND

Hardwarestand lesen Byte 8, BCD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | Hardwarestand Wert BCD |
| STAT_WERT_TEXT | string | Hardwarestand Text |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-status-codierindex"></a>
### STATUS_CODIERINDEX

Codierindex lesen Byte 9

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | Wert Codierindex als Hex |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-status-diagnoseindex"></a>
### STATUS_DIAGNOSEINDEX

Diagnoseindex lesen Byte 10

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | Wert Diagnoseindex |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-status-busindex"></a>
### STATUS_BUSINDEX

BusIndex lesen Byte 11

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | Wert Busindex |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-status-herstellungskalenderwoche"></a>
### STATUS_HERSTELLUNGSKALENDERWOCHE

Kalenderwoche lesen Byte 12

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | Wert Kalenderwoche |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-status-herstellungskalenderjahr"></a>
### STATUS_HERSTELLUNGSKALENDERJAHR

Kalenderjahr lesen Byte 13

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | Wert Kalenderjahr |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-status-zulieferer"></a>
### STATUS_ZULIEFERER

Zulieferer lesen Byte 14

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | Wert Zulieferer |
| STAT_WERT_TEXT | string | Text Zulieferer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-status-softwarestand"></a>
### STATUS_SOFTWARESTAND

Softwarestand lesen Byte 15

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | Softwarestand Wert BCD |
| STAT_WERT_TEXT | string | Softwarestand Text |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Rücksetzen des Steuergerätes in den normalen Betrieb

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Liefert: OKAY od. ERROR_NACK |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-seriennummer"></a>
### STATUS_SERIENNUMMER

Seriennummer lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | int | Seriennummer |

<a id="job-status-dauer-motorlauf"></a>
### STATUS_DAUER_MOTORLAUF

maximale Einschaltdauer Motor Byte 5-6 lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| DAUER_MOTORLAUF_WERT | real |  |
| DAUER_MOTORLAUF_EINH | string |  |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-ehks-taster-entprellzeit"></a>
### STATUS_EHKS_TASTER_ENTPRELLZEIT

Entprellzeit EHKS-Taster Byte 7 lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| EHKS_TASTER_ENTPRELLZEIT_WERT | real | Entprellzeit |
| EHKS_TASTER_ENTPRELLZEIT_EINH | string | Wert in Millisekunden |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-endpositionsschalter-entprellzeit"></a>
### STATUS_ENDPOSITIONSSCHALTER_ENTPRELLZEIT

Entprellzeit Endpositionsschalter Byte 8 lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| ENDPOSITIONSSCHALTER_ENTPRELLZEIT_WERT | real | Entprellzeit |
| ENDPOSITIONSSCHALTER_ENTPRELLZEIT_EINH | string | Wert in Millisekunden |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-seitenstuetze-entprellzeit"></a>
### STATUS_SEITENSTUETZE_ENTPRELLZEIT

Entprellzeit Seitenstütze Byte 9

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| SEITENSTUETZE_ENTPRELLZEIT_WERT | real | Entprellzeit |
| SEITENSTUETZE_ENTPRELLZEIT_EINH | string | Wert in Millisekunden |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-bremslicht-entprellzeit"></a>
### STATUS_BREMSLICHT_ENTPRELLZEIT

Entprellzeit Bremslicht Byte 10

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| BREMSLICHT_ENTPRELLZEIT_WERT | real | Entprellzeit |
| BREMSLICHT_ENTRELLZEIT_EINH | string | Wert in Millisekunden |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-leerlauf-signal-entrellzeit"></a>
### STATUS_LEERLAUF_SIGNAL_ENTRELLZEIT

Entprellzeit Leerlaufsignal Byte 11

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| LEERLAUF_ENTPRELLZEIT_WERT | real | Entprellzeit |
| LEERLAUF_ENTPRELLZEIT_EINH | string | Wert in Millisekunden |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-klemme15-entrpellzeit"></a>
### STATUS_KLEMME15_ENTRPELLZEIT

Klemme 15 Entprellzeit Byte 12

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| KLEMME15_ENTPRELLZEIT_WERT | real | Entprellzeit |
| KLEMME15_ENTPRELLZEIT_EINH | string | Wert in Millisekunden |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-klemme30-entprellzeit"></a>
### STATUS_KLEMME30_ENTPRELLZEIT

Klemme 30 Entprellzeit Byte 13

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| KLEMME30_ENTPRELLZEIT_WERT | real | Entprellzeit |
| KLEMME30_ENTPRELLZEIT_EINH | string | Wert in Millisekunden |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-betaetigung-min-pause"></a>
### STATUS_BETAETIGUNG_MIN_PAUSE

Minimale Pause zwischen 2 Aktivierungen Byte 16-17

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| PAUSE_AKTIVIERUNG_WERT | real | Pause zwischen zwei Betätigungen |
| PAUSE_AKTIVIERUNG_EINH | string | Wert in Sekunden |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-systemueberlast-dauer"></a>
### STATUS_SYSTEMUEBERLAST_DAUER

Dauer der Systemüberlast lesen Byte 18-19

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| DAUER_SYSTEMUEBERLAST_WERT | real | Pause zwischen zwei Betätigungen |
| DAUER_SYSTEMUEBERLAST_EINH | string | Wert in Sekunden |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-ueberlast-min-pause"></a>
### STATUS_UEBERLAST_MIN_PAUSE

Minimale Pause nach Systemüberlast Byte 20-21

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| PAUSE_UEBERLAST_WERT | real | Pause nach einer Überlast |
| PAUSE_UEBERLAST_EINH | string | Wert in Sekunden |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-reset-durch-kl15-ein"></a>
### STATUS_RESET_DURCH_KL15_EIN

System Reset wenn die Zündung eingeschaltet wird lesen (Ja/Nein) Byte 22

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| RESET_DURCH_KL15_EIN_WERT | string | Wert als bcd Zahl |
| RESET_DURCH_KL15_EIN_TEXT | string | Werte: EIN/AUS |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-led-frequenz"></a>
### STATUS_LED_FREQUENZ

Lesen der Led Frequenz bei Betrieb und Überlast (4 oder 2 Hz) Byte 23

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| LED_FREQUENZ_WERT | string | Wert als bcd zahl |
| LED_FREQUENZ_TEXT | string |  |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-klemme30"></a>
### STATUS_KLEMME30

Batteriespannung lesen Byte 4-5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_KL30_WERT | real | Batterispannung |
| STAT_KL30_EINH | string | Einheit Volt |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-klemme15"></a>
### STATUS_KLEMME15

Spannung Klemme 15 (Zündung) lesen Byte 8-9

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_KL15_WERT | real | Spannung Klemme 15 |
| STAT_KL15_EINH | string | Einheit Volt |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-schalter-endposition"></a>
### STATUS_SCHALTER_ENDPOSITION

Status Schalter Endposition lesen Byte 16

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_ENDPOSITION_SCHALTER_WERT | int |  |
| STAT_ENDPOSITION_SCHALTER_TEXT | string | Ein/Aus |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-ehks-taster"></a>
### STATUS_EHKS_TASTER

Status EHKS-Taster lesen Byte 17

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_EHKS_TASTER_WERT | int |  |
| STAT_EHKS_TASTER_TEXT | string | Ein/Aus |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-bremslichtsignal"></a>
### STATUS_BREMSLICHTSIGNAL

Status Bremslichtsignal lesen Byte 18

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_BREMSLICHTSIGNAL_WERT | int |  |
| STAT_BREMSLICHTSIGNAL_TEXT | string | Ein/Aus |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-geschwindigkeit"></a>
### STATUS_GESCHWINDIGKEIT

Geschwindigkeit lesen Byte 19

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_GESCHWINDIGKEIT_WERT | int |  |
| STAT_GESCHWINDIGKEIT_EINH | string |  |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-seitenstuetzschalter"></a>
### STATUS_SEITENSTUETZSCHALTER

Schalter Seitenstütze lesen Byte 20

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_SEITENSTUETZENSCHALTER_WERT | int |  |
| STAT_SEITENSTUETZENSCHALTER_TEXT | string | Ein/Aus |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-leerlauf-signal"></a>
### STATUS_LEERLAUF_SIGNAL

Leerlaufsignal lesen Byte 21

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_LEERLAUFSIGNAL_WERT | int |  |
| STAT_LEERLAUFSIGNAL_TEXT | string | Ein/Aus |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-warnlampe"></a>
### STATUS_WARNLAMPE

Status EHKS-Kontrollleuchte lesen Byte 22

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_WARNLAMPE_WERT | int |  |
| STAT_WARNLAMPE_TEXT | string | Ein/Aus |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-relais"></a>
### STATUS_RELAIS

Status EHKS-Relais lesen Byte 23

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_RELAIS_WERT | int |  |
| STAT_RELAIS_TEXT | string | Ein/Aus |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-fs-anzahl"></a>
### FS_ANZAHL

Fehlerspeicher lesen (alle Fehler) Security Access Level 1 notwendig

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_ANZAHL | int | Anzahl der Fehler im Speicher |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen (alle Fehler)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers |
| F_ANZAHL | int | Anzahl der Fehler im Speicher |
| F_ORT_NR | long | Index für den Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text Table FOrteTexte als ORTTEXT |
| F_SYMPTOM_NR | int | Index für die Fehlerart |
| F_SYMPTOM_TEXT | string | Fehlerart als Text Table FArtTexte als ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard Fehlerart) als Text Fehlerart table ArtTexte als Text |
| F_HFK | int | Haeufigkeitszaehler |
| F_UW_KM | long | Umweltbedingung Kilometerstand |
| F_UW_KM_EINH | string | Einheit Kilometerstand km |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hex Code |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| _TEL_ANTWORT2 | binary | Hex Antwort vom SG |
| _TEL_ANTWORT3 | binary | Hex Antwort vom SG |

<a id="job-fs-lesen-feld"></a>
### FS_LESEN_FELD

Fehlerspeicher lesen (ein Fehlerfeld)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NUMMER | int | Eingabe Fehler Feld 1..3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers |
| F_ANZAHL | int | Anzahl der Fehler im Speicher |
| F_ORT_NR | long | Index für den Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text Table FOrteTexte als ORTTEXT |
| F_SYMPTOM_NR | int | Index für die Fehlerart |
| F_SYMPTOM_TEXT | string | Fehlerart als Text Table FArtTexte als ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard Fehlerart) als Text Fehlerart table ArtTexte als Text |
| F_HFK | int | Haeufigkeitszaehler |
| F_UW_KM | long | Umweltbedingung Kilometerstand |
| F_UW_KM_EINH | string | Einheit Kilometerstand km |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hex Code |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher Löschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-led"></a>
### STEUERN_LED

Led ansteuern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PARAMETER | int | 1 - Led ein, 0 - Led aus |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-relais"></a>
### STEUERN_RELAIS

EHKS Relais ansteuern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PARAMETER | int | 1 - Relais ein, 0 - Relais aus Relais wird nach 16 sekunden automatisch abgeschaltet Wiedereinschalten erst nach einer bestimmten Zeit möglich |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-selbsttest"></a>
### STEUERN_SELBSTTEST

Selbsttest EHKS starten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| ERGEBNIS_WERT | string |  |
| ERGEBNIS_TEXT | string |  |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (11 × 2)
- [FORTTEXTE](#table-forttexte) (12 × 2)
- [FARTTEXTE](#table-farttexte) (13 × 2)
- [FEHLERSTATUS](#table-fehlerstatus) (5 × 2)
- [LIEFERANTEN](#table-lieferanten) (81 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 11 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | OKAY |
| 0x01 | FEHLER |
| 0x02 | FEHLER: ARGUMENTE |
| 0x03 | FEHLER: AUSSERHALB BEREICH |
| 0x04 | FEHLER: ZUGRIFF VERWEIGERT |
| 0x05 | FEHLER: FORMATFEHLER DATEN (NICHT HEX) |
| 0xA0 | OKAY |
| 0xB0 | FEHLER: PARAMETER |
| 0xB1 | FEHLER: FUNKTION |
| 0xFF | FEHLER: FUNKTION NICHT DEFINIERT |
| 0x00 | FEHLER: UNBEKANNT |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 12 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x01 | Fehler Endpositionsschalter |
| 0x02 | Fehler EHKS-Taster |
| 0x03 | Fehler Bremssignal |
| 0x04 | Fehler Geschwindigkeitssignal |
| 0x05 | Fehler Signal Seitenstützenschalter |
| 0x06 | Fehler EHKS-Kontrollleuchte |
| 0x07 | Fehler Ansteuerung EHKS-Relais |
| 0x08 | Fehler Leerlaufsignal |
| 0x09 | Interner Fehler |
| 0x0A | IBUS Fehler |
| 0x0B | Unterspannung |
| 0xFF | UNBEKANNT |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 13 rows × 2 columns

| WERT | ARTTEXT |
| --- | --- |
| 0x00 |  |
| 0x01 | Kurzschluss nach Plus |
| 0x02 | Kurzschluss nach Masse |
| 0x04 | Unterbrechung |
| 0x05 | Unterbrechung oder Kurzschluss nach Plus |
| 0x06 | Unterbrechung oder Kurzschluss nach Masse |
| 0x08 | Unplausibel |
| 0x10 | Speicherfehler |
| 0x20 | Tasterfehler |
| 0xFF | unbekannte Fehlerart |
| 0x21 | Fehler vorhanden |
| 0x22 | Fehler sporadisch |
| 0x23 | Fehler vorhanden und sporadisch |

<a id="table-fehlerstatus"></a>
### FEHLERSTATUS

Dimensions: 5 rows × 2 columns

| WERT | STATUS_TEXT |
| --- | --- |
| 0x00 | Fehler nicht vorhanden |
| 0x01 | Fehler vorhanden |
| 0x02 | Fehler sporadisch |
| 0x03 | Fehler vorhanden und sporadisch |
| 0xFF | Status: unbekannt |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 81 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x01 | Reinshagen =&gt; Delphi |
| 0x02 | Kostal |
| 0x03 | Hella |
| 0x04 | Siemens |
| 0x05 | Eaton |
| 0x06 | UTA |
| 0x07 | Helbako |
| 0x08 | Bosch |
| 0x09 | Loewe =&gt; Lear |
| 0x10 | VDO |
| 0x11 | Valeo |
| 0x12 | MBB |
| 0x13 | Kammerer |
| 0x14 | SWF |
| 0x15 | Blaupunkt |
| 0x16 | Philips |
| 0x17 | Alpine |
| 0x18 | Continental Teves |
| 0x19 | Elektromatik Suedafrika |
| 0x20 | Becker |
| 0x21 | Preh |
| 0x22 | Alps |
| 0x23 | Motorola |
| 0x24 | Temic |
| 0x25 | Webasto |
| 0x26 | MotoMeter |
| 0x27 | Delphi PHI |
| 0x28 | DODUCO =&gt; BERU |
| 0x29 | DENSO |
| 0x30 | NEC |
| 0x31 | DASA |
| 0x32 | Pioneer |
| 0x33 | Jatco |
| 0x34 | Fuba |
| 0x35 | UK-NSI |
| 0x36 | AABG |
| 0x37 | Dunlop |
| 0x38 | Sachs |
| 0x39 | ITT |
| 0x40 | FTE |
| 0x41 | Megamos |
| 0x42 | TRW |
| 0x43 | Wabco |
| 0x44 | ISAD Electronic Systems |
| 0x45 | HEC (Hella Electronics Corporation) |
| 0x46 | Gemel |
| 0x47 | ZF |
| 0x48 | GMPT |
| 0x49 | Harman Kardon |
| 0x50 | Remes |
| 0x51 | ZF Lenksysteme |
| 0x52 | Magneti Marelli |
| 0x53 | Borg Instruments |
| 0x54 | GETRAG |
| 0x55 | BHTC (Behr Hella Thermocontrol) |
| 0x56 | Siemens VDO Automotive |
| 0x57 | Visteon |
| 0x58 | Autoliv |
| 0x59 | Haberl |
| 0x60 | Magna Steyr |
| 0x61 | Marquardt |
| 0x62 | AB-Elektronik |
| 0x63 | Siemens VDO Borg |
| 0x64 | Hirschmann Electronics |
| 0x65 | Hoerbiger Electronics |
| 0x66 | Thyssen Krupp Automotive Mechatronics |
| 0x67 | Gentex GmbH |
| 0x68 | Atena GmbH |
| 0x69 | Magna-Donelly |
| 0x70 | Koyo Steering Europe |
| 0x71 | NSI B.V |
| 0x72 | ASIN AWCO.LTD |
| 0x73 | Shorlock |
| 0x74 | Schrader |
| 0x75 | BERU Electronics GmbH |
| 0x76 | CEL |
| 0x77 | Audio Mobil |
| 0x78 | rd electronic |
| 0x79 | iSYS RTS GmbH |
| 0x80 | Westfalia Automotive GmbH |
| 0xFF | unbekannter Hersteller |
