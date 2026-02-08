# mrradio.prg

- Jobs: [40](#jobs)
- Tables: [2](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Radio |
| ORIGIN | I+ME Actia GmbH, Keck |
| REVISION | 1.021 |
| AUTHOR | I+ME Actia GmbH, Keck und BMW Motorrad, Kufer |
| COMMENT | N/A |
| PACKAGE | 1.52 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung
- [IDENT](#job-ident) - Lesen der Teilenummer Byte 4-7
- [STATUS_TEILENUMMER](#job-status-teilenummer) - Lesen der Teilenummer Byte 4-7 BCD
- [STATUS_HARDWARESTAND](#job-status-hardwarestand) - Lesen Hardwarestand Byte 8 BCD
- [STATUS_CODIERINDEX](#job-status-codierindex) - Lesen der Codierbarkeit Byte 9
- [STATUS_DIAGNOSEINDEX](#job-status-diagnoseindex) - Lesen Diagnoseindex Byte 10 BCD
- [STATUS_BUSINDEX](#job-status-busindex) - Lesen BusIndex Byte 11 BCD
- [STATUS_HERSTELLUNGSKALENDERWOCHE](#job-status-herstellungskalenderwoche) - Lesen der Kalenderwoche Byte 12 BCD
- [STATUS_HERSTELLUNGSKALENDERJAHR](#job-status-herstellungskalenderjahr) - Lesen Kalenderjahr Byte 13 BCD
- [STATUS_ZULIEFERER](#job-status-zulieferer) - Lesen Zulieferer Byte 14 BCD
- [STATUS_SOFTWARESTAND](#job-status-softwarestand) - Lesen Softwarestand Byte 15 BCD
- [STATUS_AENDERUNGSINDEX](#job-status-aenderungsindex) - Lesen Änderungsindex Byte 16-17 in ASCII
- [STATUS_GAL_EINSTELLUNG](#job-status-gal-einstellung) - Einstellung Geschwindigkeits abhängige Lautstärke lesen
- [STATUS_VF_MINDESTLAUTSTAERKE](#job-status-vf-mindestlautstaerke) - Mindestlautstärke Verkehrsfunk lesen
- [STATUS_GAL_SIGNAL_EINHEIT](#job-status-gal-signal-einheit) - Einheit Geschwindigkeits abhängige Lautstärke
- [STATUS_GAL_SIGNAL_WERT](#job-status-gal-signal-wert) - Wert Geschwindigkeits abhängige Lautstärke
- [STATUS_FELDSTAERKE_WERT](#job-status-feldstaerke-wert) - Feldstärke Wert
- [STATUS_QUALITAET_WERT](#job-status-qualitaet-wert) - Qualität Wert
- [STEUERN_LAUTSPRECHER_ALLE](#job-steuern-lautsprecher-alle) - alle Lautsprecher Kanäle ansteuern
- [STEUERN_LAUTSPRECHER_VL](#job-steuern-lautsprecher-vl) - Lautsprecher vorn links ansteuern
- [STEUERN_LAUTSPRECHER_VR](#job-steuern-lautsprecher-vr) - Lautsprecher vorn rechts ansteuern
- [STEUERN_LAUTSPRECHER_HR](#job-steuern-lautsprecher-hr) - Lautsprecher hinten rechts ansteuern
- [STEUERN_LAUTSPRECHER_HL](#job-steuern-lautsprecher-hl) - Lautsprecher hinten links ansteuern
- [STEUERN_LAUTSTARKE_ERHOEHEN](#job-steuern-lautstarke-erhoehen) - Lautstärke um 1 Schritt erhöhen
- [STEUERN_LAUTSTARKE_ERNIEDRIGEN](#job-steuern-lautstarke-erniedrigen) - Lautstärke um 1 Schritt verringern
- [STEUERN_SUCHLAUF_TASTENDRUCK_VOR](#job-steuern-suchlauf-tastendruck-vor) - Tastendruck auf Suchlauftaste &gt; nachbilden
- [STEUERN_SUCHLAUF_TASTENDRUCK_ZURUECK](#job-steuern-suchlauf-tastendruck-zurueck) - Tastendruck auf Suchlauftaste &lt; nachbilden
- [STEUERN_MODE_WEITERSCHALTUNG](#job-steuern-mode-weiterschaltung) - Mode weiterschalten (Tuner-&gt;Tape-&gt;CD)
- [STEUERN_FREQUENZ_EINSTELLEN](#job-steuern-frequenz-einstellen) - Empfangsfrequenz einstellen
- [STEUERN_RADIO_EINSCHALTEN](#job-steuern-radio-einschalten) - Radio einschalten
- [STEUERN_RADIO_AUSSCHALTEN](#job-steuern-radio-ausschalten) - Radio ausschalten
- [STEUERN_AUTOSTORE_AUSFUEHREN](#job-steuern-autostore-ausfuehren) - Autostore ausführen
- [STEUERN_LAUSTAERKE_EINSTELLEN](#job-steuern-laustaerke-einstellen) - Lautstärke einstellen
- [STEUERN_GAL_KURVE_VERRINGERN](#job-steuern-gal-kurve-verringern) - nächste niedrige Geschwindigkeits abhängige Laustärke Kurve wählen
- [STEUERN_GAL_KURVE_ERHOEHEN](#job-steuern-gal-kurve-erhoehen) - nächste höhere Geschwindigkeits abhängige Lautstärke Kurve wählen
- [STEUERN_VF_MINDESTLAUTSTAERKE_VERRINGERN](#job-steuern-vf-mindestlautstaerke-verringern) - Verkehrsfunk Mindestlautstärke um einen Schritt verringern
- [STEUERN_VF_MINDESTLAUTSTAERKE_ERHOEHEN](#job-steuern-vf-mindestlautstaerke-erhoehen) - Verkehrsfunk Mindestlautstärke um einen Schritt erhöhen
- [STATUS_SERIENNUMMER](#job-status-seriennummer) - Lesen der Seriennummer
- [STEUERN_SELBSTTEST_AKTIVIEREN](#job-steuern-selbsttest-aktivieren) - Steuergeräte Test starten

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

Lesen der Teilenummer Byte 4-7

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | BMW-Teilenummer, BCD |
| VARIANTE_IND | string | Name der SGBD, immer MRRADIO |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-status-teilenummer"></a>
### STATUS_TEILENUMMER

Lesen der Teilenummer Byte 4-7 BCD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | BMW-Teilenummer, BCD |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-status-hardwarestand"></a>
### STATUS_HARDWARESTAND

Lesen Hardwarestand Byte 8 BCD

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

Lesen der Codierbarkeit Byte 9

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | Wert Codierindex |
| STAT_WERT_TEXT | string | Wert Codierindex |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-status-diagnoseindex"></a>
### STATUS_DIAGNOSEINDEX

Lesen Diagnoseindex Byte 10 BCD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | Wert Diagnoseindex |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-status-busindex"></a>
### STATUS_BUSINDEX

Lesen BusIndex Byte 11 BCD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | Wert Busindex |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-status-herstellungskalenderwoche"></a>
### STATUS_HERSTELLUNGSKALENDERWOCHE

Lesen der Kalenderwoche Byte 12 BCD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | Wert Kalenderwoche |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-status-herstellungskalenderjahr"></a>
### STATUS_HERSTELLUNGSKALENDERJAHR

Lesen Kalenderjahr Byte 13 BCD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | Wert Kalenderjahr |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-status-zulieferer"></a>
### STATUS_ZULIEFERER

Lesen Zulieferer Byte 14 BCD

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

Lesen Softwarestand Byte 15 BCD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | Softwarestand Wert BCD |
| STAT_WERT_TEXT | string | Softwarestand Text |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-status-aenderungsindex"></a>
### STATUS_AENDERUNGSINDEX

Lesen Änderungsindex Byte 16-17 in ASCII

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | Änderungsindex Wert Ascii |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-status-gal-einstellung"></a>
### STATUS_GAL_EINSTELLUNG

Einstellung Geschwindigkeits abhängige Lautstärke lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_WERT | int | Wert als Zahl |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-vf-mindestlautstaerke"></a>
### STATUS_VF_MINDESTLAUTSTAERKE

Mindestlautstärke Verkehrsfunk lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_WERT | int | Wert als Zahl |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-gal-signal-einheit"></a>
### STATUS_GAL_SIGNAL_EINHEIT

Einheit Geschwindigkeits abhängige Lautstärke

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_WERT_TEXT | string | Einheit: km/h oder Hz |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-gal-signal-wert"></a>
### STATUS_GAL_SIGNAL_WERT

Wert Geschwindigkeits abhängige Lautstärke

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_WERT_TEXT | string | Geschwindigkeits abhängige Lautstärke als String |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-feldstaerke-wert"></a>
### STATUS_FELDSTAERKE_WERT

Feldstärke Wert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_WERT_TEXT | string | Feldstärke Wert |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-qualitaet-wert"></a>
### STATUS_QUALITAET_WERT

Qualität Wert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| STAT_WERT_TEXT | string | Qualität Wert |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-lautsprecher-alle"></a>
### STEUERN_LAUTSPRECHER_ALLE

alle Lautsprecher Kanäle ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-lautsprecher-vl"></a>
### STEUERN_LAUTSPRECHER_VL

Lautsprecher vorn links ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-lautsprecher-vr"></a>
### STEUERN_LAUTSPRECHER_VR

Lautsprecher vorn rechts ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-lautsprecher-hr"></a>
### STEUERN_LAUTSPRECHER_HR

Lautsprecher hinten rechts ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-lautsprecher-hl"></a>
### STEUERN_LAUTSPRECHER_HL

Lautsprecher hinten links ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-lautstarke-erhoehen"></a>
### STEUERN_LAUTSTARKE_ERHOEHEN

Lautstärke um 1 Schritt erhöhen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-lautstarke-erniedrigen"></a>
### STEUERN_LAUTSTARKE_ERNIEDRIGEN

Lautstärke um 1 Schritt verringern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-suchlauf-tastendruck-vor"></a>
### STEUERN_SUCHLAUF_TASTENDRUCK_VOR

Tastendruck auf Suchlauftaste &gt; nachbilden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-suchlauf-tastendruck-zurueck"></a>
### STEUERN_SUCHLAUF_TASTENDRUCK_ZURUECK

Tastendruck auf Suchlauftaste &lt; nachbilden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-mode-weiterschaltung"></a>
### STEUERN_MODE_WEITERSCHALTUNG

Mode weiterschalten (Tuner-&gt;Tape-&gt;CD)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-frequenz-einstellen"></a>
### STEUERN_FREQUENZ_EINSTELLEN

Empfangsfrequenz einstellen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FREQUENZ | string | Frequenz in kHz als String 89,3MHz -&gt; Eingabe 89300 als String |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-radio-einschalten"></a>
### STEUERN_RADIO_EINSCHALTEN

Radio einschalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-radio-ausschalten"></a>
### STEUERN_RADIO_AUSSCHALTEN

Radio ausschalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-autostore-ausfuehren"></a>
### STEUERN_AUTOSTORE_AUSFUEHREN

Autostore ausführen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-laustaerke-einstellen"></a>
### STEUERN_LAUSTAERKE_EINSTELLEN

Lautstärke einstellen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LAUTSTAERKE | string | Lautstärke 0..99 Eingabe als String |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-gal-kurve-verringern"></a>
### STEUERN_GAL_KURVE_VERRINGERN

nächste niedrige Geschwindigkeits abhängige Laustärke Kurve wählen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-gal-kurve-erhoehen"></a>
### STEUERN_GAL_KURVE_ERHOEHEN

nächste höhere Geschwindigkeits abhängige Lautstärke Kurve wählen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-vf-mindestlautstaerke-verringern"></a>
### STEUERN_VF_MINDESTLAUTSTAERKE_VERRINGERN

Verkehrsfunk Mindestlautstärke um einen Schritt verringern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-steuern-vf-mindestlautstaerke-erhoehen"></a>
### STEUERN_VF_MINDESTLAUTSTAERKE_ERHOEHEN

Verkehrsfunk Mindestlautstärke um einen Schritt erhöhen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |
| _TEL_ANFRAGE | binary | Hex Anfrage zum SG |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |

<a id="job-status-seriennummer"></a>
### STATUS_SERIENNUMMER

Lesen der Seriennummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex Antwort vom SG |
| STAT_WERT | string | Seriennummer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS TEXT |

<a id="job-steuern-selbsttest-aktivieren"></a>
### STEUERN_SELBSTTEST_AKTIVIEREN

Steuergeräte Test starten

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

- [JOBRESULT](#table-jobresult) (12 × 2)
- [LIEFERANTEN](#table-lieferanten) (81 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 12 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | OKAY |
| 0x01 | FEHLER |
| 0x02 | FEHLER: ARGUMENTE |
| 0x03 | FEHLER: AUSSERHALB BEREICH |
| 0x04 | FEHLER: ZUGRIFF VERWEIGERT |
| 0x05 | FEHLER: FORMATFEHLER DATEN (NICHT HEX) |
| 0x08 | FEHLER: ZUGRIFF VERWEIGERT |
| 0xA0 | OKAY |
| 0xB0 | FEHLER: AUSFUEHRUNG NICHT MOEGLICH |
| 0xB1 | FEHLER: FUNKTION |
| 0xF1 | FEHLER: NO_RESPONE_FROM_CONTROL_UNIT |
| 0x00 | FEHLER: UNBEKANNT |

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
