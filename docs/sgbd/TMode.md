# TMode.prg

- Jobs: [25](#jobs)
- Tables: [0](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | TMODE |
| ORIGIN | BMW VS-43 Leipold |
| REVISION | 1.40 |
| AUTHOR | Softing Ta, Softing WT |
| COMMENT | Erstellung aus TMODE.B1V, Version 1.3 |
| PACKAGE | 1.29 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Es wird nur der Interfacetyp festgestellt
- [SETZE_INTERFACE_ZURUECK](#job-setze-interface-zurueck) - Versetzt das Interface in den Initialisierungszustand
- [SETZE_SG_PARAM_ZURUECK](#job-setze-sg-param-zurueck) - Ruecksetzen der im Interface gespeicherten SG-Parameter Abbruch einer gerade laufenden SG-Kommunikation
- [SETZE_SG_PARAMETER_ALLG](#job-setze-sg-parameter-allg) - Es werden die fuer die Kommunikation notwendigen Parameter festgelegt
- [SETZE_SG_PARAMETER_EIDBSS](#job-setze-sg-parameter-eidbss) - Einstellen der Kommunikationsparameter nur fuer das EIDBSS und IDBSS
- [SETZE_ANTWORTLAENGE](#job-setze-antwortlaenge) - Setzen der Antwortlaenge
- [HOLE_KEYBYTES](#job-hole-keybytes) - Dieser Job liest die Keybytes aus einem Konzept 2,3,4 SG aus. Laeuft die Kommunikation mit dem SG noch nicht, wird automatisch mit einem ACK-Telegramm gereizt.
- [SENDE_TELEGRAMM](#job-sende-telegramm) - Mit diesem Job wird ein Telegramm an ein SG geschickt und die Antwort empfangen
- [SENDE_TELEGR_WIEDERHOLT](#job-sende-telegr-wiederholt) - Mit diesem Job wird ein Telegramm im frequent Mode an ein SG geschickt
- [HOLE_ANTWORT_TELEGR](#job-hole-antwort-telegr) - Mit diesem Job werden SG-Antworttelegramme vom Interface abgeholt, nachdem die Anforderung mit dem Job SENDE_TELEGR_WIEDERHOLT gestartet wurde
- [STOPPE_WIEDERH_ANFORDERUNG](#job-stoppe-wiederh-anforderung) - Diese Job stoppt die wiederholte SG-Abfrage
- [LESE_INTERFACE_TYP](#job-lese-interface-typ) - Dieser Job stellt den Interfacetyp fest
- [LESE_INTERFACE_VERSION](#job-lese-interface-version) - Dieser Job liest die Versionsnummer des Interface
- [LESE_SPANNUNG_KL30](#job-lese-spannung-kl30) - Dieser Job stellt die Batteriespannung fest
- [LESE_SPANNUNG_KL15](#job-lese-spannung-kl15) - Dieser Job stellt die Spannung an der Zuendung fest
- [LESE_PORT](#job-lese-port) - Dieser Job liest das angegebene Port aus
- [SETZE_PORT](#job-setze-port) - Dieser Job setzt das angegebene Port mit dem uebergebenen Wert
- [SETZE_PROGRAMMIERSPANNUNG](#job-setze-programmierspannung) - Mit diesem Job wird die Programmierspannung auf einen bestimmten Wert eingestellt
- [SETZE_SIA_RELAIS](#job-setze-sia-relais) - Schliesst das SIA Relais fuer die angegebene Zeit
- [TESTE_DIAGNOSELEITUNG](#job-teste-diagnoseleitung) - Dieser Job testet die Diagnoseleitung
- [HOLE_INTERFACE_STATUS](#job-hole-interface-status) - Dieser Job liest den Interfacestatus aus
- [REICHE_AN_INTERFACE_DURCH](#job-reiche-an-interface-durch) - Mit diesem Job werden Daten uninterpretiert an das Interface geschickt. Auch die Antwort wird nicht interpretiert. Wird das BMW-Std-Interface erkannt, dann wird jedem Kommando wird als Kennung fuer das Interface das Byte 0x99 vorangestellt
- [SETZE_TRAP_MASK_REGISTER](#job-setze-trap-mask-register) - Mit diesem Job wird das Trapmaskregister entsprechend dem uebergebenen Parameter gesetzt
- [LIES_TRAP_MASK_REGISTER](#job-lies-trap-mask-register) - Mit diesem Job wird der aktuelle Wert des TMR ausgelesen

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

Es wird nur der Interfacetyp festgestellt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-setze-interface-zurueck"></a>
### SETZE_INTERFACE_ZURUECK

Versetzt das Interface in den Initialisierungszustand

_No arguments._

_No results._

<a id="job-setze-sg-param-zurueck"></a>
### SETZE_SG_PARAM_ZURUECK

Ruecksetzen der im Interface gespeicherten SG-Parameter Abbruch einer gerade laufenden SG-Kommunikation

_No arguments._

_No results._

<a id="job-setze-sg-parameter-allg"></a>
### SETZE_SG_PARAMETER_ALLG

Es werden die fuer die Kommunikation notwendigen Parameter festgelegt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PARAMETER | binary | Steuergeraete Parameter Inhalt: Konzept BMW-Konzept 1      1 BMW-Konzept 2      2 BMW-Konzept IHK    3 BMW-Konzept DDE    4 BMW-Konzept DS1    5 BMW-Konzept DS2    6 BMW-Konzept ISO 9141 CARB/OBD II 7 Baudrate Reizadresse Wakeup-Zeit in ms 0, wenn kein Wakeup Idle-Zeit in ms Timeout-Zeit In dieser Zeit muss SG antworten Regenerations-Zeit Zeit zwischen den Telegrammen Telegrammende-Zeit Wartezeit nach dem letzte Byte, nach der auf Telegrammende entschieden wird Bytezwischenzeit Checksumme |

_No results._

<a id="job-setze-sg-parameter-eidbss"></a>
### SETZE_SG_PARAMETER_EIDBSS

Einstellen der Kommunikationsparameter nur fuer das EIDBSS und IDBSS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PARAMETER | binary | Steuergeraete Parameter |

_No results._

<a id="job-setze-antwortlaenge"></a>
### SETZE_ANTWORTLAENGE

Setzen der Antwortlaenge

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANTWORTLAENGE | binary | Antwortlaenge |

_No results._

<a id="job-hole-keybytes"></a>
### HOLE_KEYBYTES

Dieser Job liest die Keybytes aus einem Konzept 2,3,4 SG aus. Laeuft die Kommunikation mit dem SG noch nicht, wird automatisch mit einem ACK-Telegramm gereizt.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| KEYBYTES | binary | SG-Keybytes |

<a id="job-sende-telegramm"></a>
### SENDE_TELEGRAMM

Mit diesem Job wird ein Telegramm an ein SG geschickt und die Antwort empfangen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TELEGRAMM | binary | SG-Anforderungstelegramm |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SG_ANTWORT | binary | SG-Antworttelegramm |

<a id="job-sende-telegr-wiederholt"></a>
### SENDE_TELEGR_WIEDERHOLT

Mit diesem Job wird ein Telegramm im frequent Mode an ein SG geschickt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TELEGRAMM | binary | SG-Anforderungstelegramm |

_No results._

<a id="job-hole-antwort-telegr"></a>
### HOLE_ANTWORT_TELEGR

Mit diesem Job werden SG-Antworttelegramme vom Interface abgeholt, nachdem die Anforderung mit dem Job SENDE_TELEGR_WIEDERHOLT gestartet wurde

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SG_ANTWORT | binary | SG-Antworttelegramm |

<a id="job-stoppe-wiederh-anforderung"></a>
### STOPPE_WIEDERH_ANFORDERUNG

Diese Job stoppt die wiederholte SG-Abfrage

_No arguments._

_No results._

<a id="job-lese-interface-typ"></a>
### LESE_INTERFACE_TYP

Dieser Job stellt den Interfacetyp fest

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| TYP | binary | SG-Interfacetyp Wertebereich: "EDIC", "STD", "ADS", ... |

<a id="job-lese-interface-version"></a>
### LESE_INTERFACE_VERSION

Dieser Job liest die Versionsnummer des Interface

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| VERSION | binary | Versionsnummer |

<a id="job-lese-spannung-kl30"></a>
### LESE_SPANNUNG_KL30

Dieser Job stellt die Batteriespannung fest

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SPANNUNG | binary | Batteriespannung in mV |

<a id="job-lese-spannung-kl15"></a>
### LESE_SPANNUNG_KL15

Dieser Job stellt die Spannung an der Zuendung fest

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SPANNUNG | binary | Spannung an der Zuendung in mV |

<a id="job-lese-port"></a>
### LESE_PORT

Dieser Job liest das angegebene Port aus

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PORT | binary | Nummer des Ports EIDBSS: Port  0-5 Analog0 bis Analog5 6 Klemme15 7 Klemme30 8 Jumperfeld |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| PORTWERT | binary | Analogwerte in mV |

<a id="job-setze-port"></a>
### SETZE_PORT

Dieser Job setzt das angegebene Port mit dem uebergebenen Wert

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PORT_WERT | binary | Portnummer und Wert |

_No results._

<a id="job-setze-programmierspannung"></a>
### SETZE_PROGRAMMIERSPANNUNG

Mit diesem Job wird die Programmierspannung auf einen bestimmten Wert eingestellt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PROGRAMMIERSPANNUNG | binary | Programmierspannung in mV |

_No results._

<a id="job-setze-sia-relais"></a>
### SETZE_SIA_RELAIS

Schliesst das SIA Relais fuer die angegebene Zeit

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEIT | binary | Zeit in ms |

_No results._

<a id="job-teste-diagnoseleitung"></a>
### TESTE_DIAGNOSELEITUNG

Dieser Job testet die Diagnoseleitung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ERGEBNIS | binary | Testergebnis i.O/n.i.O = 1/0 |

<a id="job-hole-interface-status"></a>
### HOLE_INTERFACE_STATUS

Dieser Job liest den Interfacestatus aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| IF_STATUS | binary | Interfacestatus |

<a id="job-reiche-an-interface-durch"></a>
### REICHE_AN_INTERFACE_DURCH

Mit diesem Job werden Daten uninterpretiert an das Interface geschickt. Auch die Antwort wird nicht interpretiert. Wird das BMW-Std-Interface erkannt, dann wird jedem Kommando wird als Kennung fuer das Interface das Byte 0x99 vorangestellt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTEFOLGE | binary | Bytefolge |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| IF_ANTWORT | binary | Interfaceantwort auf die Bytefolge |

<a id="job-setze-trap-mask-register"></a>
### SETZE_TRAP_MASK_REGISTER

Mit diesem Job wird das Trapmaskregister entsprechend dem uebergebenen Parameter gesetzt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TMR_WERT | long | Trapmaskregisterwert |

_No results._

<a id="job-lies-trap-mask-register"></a>
### LIES_TRAP_MASK_REGISTER

Mit diesem Job wird der aktuelle Wert des TMR ausgelesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| TMR | long | Trapmaskregisterwert |

## Tables

No tables found.
