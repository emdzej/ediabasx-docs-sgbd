# RDC.prg

- Jobs: [21](#jobs)
- Tables: [6](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Reifendruckkontrolle |
| ORIGIN | BMW TI-431 Stadlhofer |
| REVISION | 1.2 |
| AUTHOR | BMW TI-431 Krueger, BMW TI-433 Gerd Huber, BMW TI-433 Winkler, GTI Peter Gross-Grueber, BMW Ti-430 Gall, BMW TI-430 Mueller |
| COMMENT | N/A |
| PACKAGE | 0.06 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung / Kommunikationsparameter fuer Reifendruck-Control automatischer Aufruf beim ersten Zugriff auf die SGBD
- [IDENT](#job-ident) - Ident-Daten fuer RDC
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode aufrechterhalten
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [SPEICHER_LESEN](#job-speicher-lesen) - Lesen des internen Speichers
- [STATUS_RAD_IO](#job-status-rad-io) - Auslesen der Raddaten wenn alle Raeder zugeordnet
- [STATUS_IO](#job-status-io) - Auslesen der Statusbytes
- [STEUERN_DIGITAL](#job-steuern-digital) - Ansteuern einiger Signale
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [HERSTELLDATEN_LESEN](#job-herstelldaten-lesen) - Auslesen der Herstelldaten
- [CODIERUNG_LESEN](#job-codierung-lesen) - Auslesen der Codierdaten
- [ABGLEICHWERT_LESEN](#job-abgleichwert-lesen) - Auslesen der Rad-Daten
- [ABGLEICHWERT_SCHREIBEN](#job-abgleichwert-schreiben) - Beschreiben der Rad-Kennung
- [RE_TELEGRAMM_LESEN](#job-re-telegramm-lesen) - Auslesen des letzten Rad-Telegramms
- [RE_TELEGRAMM_CLEAR](#job-re-telegramm-clear) - Loeschen des RE-Telegramm-Zwischenspeichers
- [SETZE_TEL_ANZ_BIS_ER](#job-setze-tel-anz-bis-er) - Anzahl der RE-Telegramme bis Eigenradstatus auf den Wert ANZ_TEL setzen. Die neuen Daten werden gegenge- lesen und bei Nichtuebereinstimmung erneut geschreiben
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen

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

Initialisierung / Kommunikationsparameter fuer Reifendruck-Control automatischer Aufruf beim ersten Zugriff auf die SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer RDC

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_FREQUENZ | string | Frequenzvariante 433, 315 oder ??? (falls ID_BMW_NR unbekannt) |
| ID_HW_NR | int | BMW-Hardwarenummer |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_BUS_INDEX | int | Bus-Index |
| ID_DATUM_KW | int | Herstelldatum KW |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Text table Lieferanten LIEF_TEXT |
| ID_SW_NR | int | Softwarenummer |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen Low-Konzept nach Lastenheft Codierung/Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FEHLER_ANZAHL | int | Anzahl der Fehler im Fehlerspeicher |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | int | Index fuer Fehlerort momentan identisch Fehlerbyte |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_HFK | int | Fehlerhaeufigkeit Bereich: 0 - 31 |
| F_ART_ANZ | int | Anzahl der Fehlerarten Bereich: immer 1 |
| F_ART1_NR | int | Index der 1. (einzigen) Fehlerart Bereich: 0, 1 |
| F_ART1_TEXT | string | 1. (einzige) Fehlerart als Text table FArtTexte ARTTEXT |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Bereich: immer 1 |
| F_UW_SATZ | int | Anzahl der Umweltsaetze Bereich: immer 1 |
| F_UW1_NR | int | Index der 1. (einzigen) Umweltbedingung Bereich: 0, 1 |
| F_UW1_TEXT | string | 1. (einzige) Umweltbedingung als Text |
| F_UW1_WERT | int | Wert der 1. (einzigen) Umweltbedingung |
| F_UW1_EINH | string | Einheit der 1. (einzigen) Umweltbedingung |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Diagnosemode aufrechterhalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Lesen des internen Speichers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT | int | Speichersegment Bereich: 0x00-0xFF |
| ADRESSE | long | Speicheradresse Bereich: 0x0000-0xFFFF |
| ANZAHL | int | Anzahl der Daten Bereich: 1 bis 16 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_argumentname, wenn argument nicht uebergeben oder ausser Bereich table JobResult STATUS_TEXT |
| DATEN | binary | ausgelesene Hex-Daten |

<a id="job-status-rad-io"></a>
### STATUS_RAD_IO

Auslesen der Raddaten wenn alle Raeder zugeordnet

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RADPOS | int | Radposition {1,..,5} == {vl,vr,hl,hr,rr} |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SENSDEF | int | Anzahl 'Sensor-defekt'-Ereignisse |
| STAT_SENSDEF_ACT | int | 'Sensor-defekt' aktiv |
| STAT_NOSEND | int | Anzahl 'RE-sendet-nicht'-Ereignisse |
| STAT_NOSEND_ACT | int | 'RE-sendet-nicht' aktiv |
| STAT_UEBERH | int | Anzahl 'RE-ueberhitzt'-Ereignisse |
| STAT_UEBERH_ACT | int | 'RE-ueberhitzt' aktiv |
| STAT_PANNE | int | Anzahl 'Reifenpannen'-Ereignisse |
| STAT_PANNE_ACT | int | 'Reifenpanne' aktiv |
| STAT_DRUCK | int | Anzahl 'Reifendruck-pruefen'-Ereignisse |
| STAT_DRUCK_ACT | int | 'Reifendruck-pruefen' aktiv Folgende Werte werden bei Ereichen von 'bestaetigt' aller Raeder rueckgesetzt, wenn aktuell keine Panne bzw. Pruefbedingung vorliegt |
| STAT_PANNENMLDG | int | Anzahl 'Reifenpannen'-Meldungen |
| STAT_PRUEFMLDG | int | Anzahl 'Druck-pruefen'-Meldungen Folgender Wert wird bei 'Fehlerspeicher-loeschen' rueckgesetzt |
| STAT_TMPINAKTIV | int | Anzahl temporaerer Inaktiv-Zustaende |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-io"></a>
### STATUS_IO

Auslesen der Statusbytes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_RAD_BST_RR | int | RR-RE zugeordnet+bestaetigt |
| STAT_RAD_BST_HR | int | HR-RE zugeordnet+bestaetigt |
| STAT_RAD_BST_HL | int | HL-RE zugeordnet+bestaetigt |
| STAT_RAD_BST_VR | int | VR-RE zugeordnet+bestaetigt |
| STAT_RAD_BST_VL | int | VL-RE zugeordnet+bestaetigt |
| STAT_RE_TRIG | int | Retrigger des Zuordnung-TimeOut |
| STAT_CALABBR | int | Kalibrierung abgebrochen |
| STAT_CALREQ | int | SP hat Kalibrierung angenommen |
| STAT_ER_RUN | int | Eigenraderkennung laeuft |
| STAT_AUTO_ER | int | Status autom. Eigenraderkennung wenn kmh&gt;40 und Bandmode |
| STAT_ZO_BST | int | Alle REs bestaetigt |
| STAT_DWA | int | DWA-Ausgang interner Zustand |
| STAT_ZO | int | Alle REs zugeordnet |
| STAT_ZO_EIGN | int | Alle Eigenraeder erkannt |
| STAT_KALIB | int | System ist kalibriert |
| STAT_AKTIV | int | System-Controler meldet aktiv |
| STAT_DRUCK_VL | int | aktueller VL-Reifendruck |
| STAT_DRUCK_VR | int | aktueller VR-Reifendruck |
| STAT_DRUCK_HL | int | aktueller HL-Reifendruck |
| STAT_DRUCK_HR | int | aktueller HR-Reifendruck |
| STAT_DRUCK_RR | int | aktueller RR-Reifendruck |
| STAT_PRF_HL | int | KBUS-Msg: HL-Reifendruck pruefen |
| STAT_PRF_HR | int | KBUS-Msg: HR-Reifendruck pruefen |
| STAT_PRF_VL | int | KBUS-Msg: VL-Reifendruck pruefen |
| STAT_PRF_VR | int | KBUS-Msg: VR-Reifendruck pruefen |
| STAT_PAN_HL | int | KBUS-Msg: HL-Reifenpanne |
| STAT_PAN_HR | int | KBUS-Msg: HR-Reifenpanne |
| STAT_PAN_VL | int | KBUS-Msg: VL-Reifenpanne |
| STAT_PAN_VR | int | KBUS-Msg: VR-Reifenpanne |
| STAT_HF_UEBD | int | KBUS-Msg: HF-Ueberdeckung aktiv |
| STAT_PRF_RR | int | KBUS-Msg: RR-Reifendruck pruefen |
| STAT_INAKTIV | int | KBUS-Msg: RDC ist inaktiv |
| STAT_DRK_SET | int | KBUS-Msg: Reifendruck set |
| STAT_DIA_CON | int | Diagnose aktiv |
| STAT_KL_15 | int | interner KL15-Status (Kbus && Hardware) |
| STAT_FAEHRT | int | Status Fzg.-Faehrt |
| STAT_BANDMODE | int | RDC im Bandmode |
| STAT_ER_ERK | int | Eigenraderkennung laeuft |
| STAT_RE_1 | int | Je 1 Telegramm jeder RE empfangen |
| STAT_RE_OVLF | int | zu viele Telegramme bei Eigenraderkennung |
| STAT_ER_TO | int | TimeOut der Eigenraderkennung |
| STAT_P_HART | int | intern: |
| STAT_P_H_RR | int | intern: |
| STAT_P_H_HR | int | intern: schneller Druckverlust |
| STAT_P_H_HL | int | intern:   -"-         -"- |
| STAT_P_H_VR | int | intern:   -"-         -"- |
| STAT_P_H_VL | int | intern:   -"-         -"- |
| STAT_P_W_RR | int | intern: RR-Reifendruck pruefen |
| STAT_P_W_HR | int | intern: HR-Reifendruck pruefen =&gt; Pruefmeldung |
| STAT_P_W_HL | int | intern: HL-Reifendruck pruefen =&gt; Pruefmeldung |
| STAT_P_W_VR | int | intern: VR-Reifendruck pruefen =&gt; Pruefmeldung |
| STAT_P_W_VL | int | intern: VL-Reifendruck pruefen =&gt; Pruefmeldung |
| STAT_P_M_RR | int | intern: RR-Unterdruck |
| STAT_P_M_HR | int | intern: HR-Unterdruck =&gt; Panne |
| STAT_P_M_HL | int | intern: HL-Unterdruck =&gt; Panne |
| STAT_P_M_VR | int | intern: VR-Unterdruck =&gt; Panne |
| STAT_P_M_VL | int | intern: VL-Unterdruck =&gt; Panne |
| STAT_BAT_RR | int | intern: RR-Batterie leer |
| STAT_BAT_HR | int | intern: HR-Batterie leer |
| STAT_BAT_HL | int | intern: HL-Batterie leer |
| STAT_BAT_VR | int | intern: VR-Batterie leer |
| STAT_BAT_VL | int | intern: VL-Batterie leer |
| STAT_CPLAUS | int | intern: unplausible Kalibrierdruecke |
| STAT_PHERBST | int | intern: Herbstfilter aktiv |
| STAT_P_MIN | int | intern: unspez. Unterdruck =&gt; Panne |
| STAT_FOLGAUS | int | intern: Stoersender Folgeausfall |
| STAT_HFUEB | int | intern: HF-Ueberdeckung aktiv |
| STAT_UHZ_RR | int | RR-RE-Ueberhitzung |
| STAT_UHZ_HR | int | HR-RE-Ueberhitzung |
| STAT_UHZ_HL | int | HL-RE-Ueberhitzung |
| STAT_UHZ_VR | int | VR-RE-Ueberhitzung |
| STAT_UHZ_VL | int | VL-RE-Ueberhitzung |
| STAT_DWA_ST | int | Status DWA-Ausgang |
| STAT_UNT_SPNG | int | Unterspannung erkannt |
| STAT_HW_KL15 | int | Status Hardware-KL15 |
| STAT_HW_RDC_TST | int | Status RDC-Taster-Eingang |
| STAT_KB_KL15 | int | Status KBus-KL15 |
| STAT_DWA_READ | int | DWA-Ausgangs-Flanke neg-slope=='1' |
| STAT_MOTOR | int | Status Motor laeuft |
| STAT_ZO_TIMEOUT | int | Zuordnungstimeout abgelaufen |
| STAT_PRFLA_HL | int | Reifendruck-Prueflatch (1=&gt;Pruefmeldung) |
| STAT_PRFLA_HR | int | Reifendruck-Prueflatch (1=&gt;Pruefmeldung) |
| STAT_PRFLA_VL | int | Reifendruck-Prueflatch (1=&gt;Pruefmeldung) |
| STAT_PRFLA_VR | int | Reifendruck-Prueflatch (1=&gt;Pruefmeldung) |
| STAT_PRFLA_RR | int | Reifendruck-Prueflatch (1=&gt;Pruefmeldung) |
| STAT_PRFLA_UN | int | Reifendruck-Prueflatch (1=&gt;Pruefmeldung) |
| STAT_ZO_TIME | int | Restzeit fuer Zuordnung |
| STAT_RADDRUCK_EINH | string | Einheit Raddruck |
| STAT_TIMER_EINH | string | Einheit Timer |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

Ansteuern einiger Signale

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TST_REQ | int | Vorgeben Kalibriertaster |
| TST_VAL | int | Wert |
| DWA_REQ | int | Vorgeben DWA-Ausgang |
| DWA_VAL | int | Wert |
| BM_REQ | int | Vorgeben BandMode |
| BM_VAL | int | Wert |
| AER_REQ | int | Vorgeben Automatische Eigenrad. |
| AER_VAL | int | Wert |
| ERK_REQ | int | Vorgeben Eigenraderkennung |
| ERK_VAL | int | Wert |
| CAL_REQ | int | Vorgeben Kalibrieren |
| CAL_VAL | int | Wert |
| ANT_REQ | int | Vorgeben Antennentest |
| ANT_VAL | int | Wert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| FG_ZIFFERN | string | die letzten vier Stellen der Fahrgestellnummer |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-herstelldaten-lesen"></a>
### HERSTELLDATEN_LESEN

Auslesen der Herstelldaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE4 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierung-lesen"></a>
### CODIERUNG_LESEN

Auslesen der Codierdaten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ANZANT | int | Anzahl angeschlossener Antennen |
| ANZRADVB | int | Anzahl verbauter Raeder |
| ANZRADUE | int | Anzahl ueberwachter Raeder |
| ANZTELER | int | Anzahl Telegramme fuer Eigenradstatus |
| MDOFFSET | int | Offset fuer Mindestdruck |
| MDOFFSET_EINH | string | Einheit fuer Offset des Mindestdruck |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abgleichwert-lesen"></a>
### ABGLEICHWERT_LESEN

Auslesen der Rad-Daten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RADNR | int | laufende Nummer des Rades |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_RADPOS | unsigned int | Radposition |
| STAT_RADID | unsigned long | RE-Kennung |
| STAT_RADDRUCK | unsigned int | Raddruck in mbar |
| STAT_RADTEMP | int | Radtemperatur in Grad Celsius |
| STAT_RADBATTLOW | unsigned int | Radbatterie-LOW-Signalisierung |
| STAT_RADBATT | unsigned int | Radbatterie Restleben in Monaten |
| STAT_RADRSSI | unsigned int | analoger RSSI Summenpegel |
| STAT_RADSOLL | unsigned int | Radsolldruck in mbar |
| STAT_EMPFZAHL | unsigned int | Anzahl empfangener RE-Telegramme |
| STAT_EMPFGUETE | unsigned int | Guete der Empfaenge in Prozent |
| STAT_RADDRUCK_EINH | string | Einheit Raddruck |
| STAT_RADTEMP_EINH | string | Einheit Radtemperatur |
| STAT_RADSOLL_EINH | string | Einheit Raddruck |
| STAT_RADBATT_EINH | string | Einheit Radbatterie-LOW |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abgleichwert-schreiben"></a>
### ABGLEICHWERT_SCHREIBEN

Beschreiben der Rad-Kennung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RADPOS | int | Radposition |
| RADID | string | RE-Kennung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-re-telegramm-lesen"></a>
### RE_TELEGRAMM_LESEN

Auslesen des letzten Rad-Telegramms

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RADNR | int | laufende Nummer des Rades |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_RADID | unsigned long | RE-Kennung |
| STAT_RADDRUCK | int | Raddruck in mbar |
| STAT_RADTEMP | int | Radtemperatur in Grad Celsius |
| STAT_RADBATTLOW | int | Radbatterie-LOW-Signalisierung |
| STAT_RADBATT | int | Radbatterie Restleben in Monaten |
| STAT_RADSTAT | int | Status |
| STAT_RADPOS | int | Radposition |
| STAT_RADRSSI | int | RSSI-Empfangspegel |
| STAT_RADCNT | int | Anzahl Telegramme |
| STAT_RADDRUCK_EINH | string | Einheit Raddruck |
| STAT_RADTEMP_EINH | string | Einheit Radtemperatur |
| STAT_RADBATT_EINH | string | Einheit Batt-Restlebensdauer |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-re-telegramm-clear"></a>
### RE_TELEGRAMM_CLEAR

Loeschen des RE-Telegramm-Zwischenspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AN_SG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-setze-tel-anz-bis-er"></a>
### SETZE_TEL_ANZ_BIS_ER

Anzahl der RE-Telegramme bis Eigenradstatus auf den Wert ANZ_TEL setzen. Die neuen Daten werden gegenge- lesen und bei Nichtuebereinstimmung erneut geschreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANZ_TEL | int | Bereich: 2-255 bzw. 0x02-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Sleep-Mode versetzen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEIT | real | a) Zeit nach der das Steuergerät einschläft Bereich   : 0.5 bis 20.0 [Sekunden] Auflösung : 0.5 [Sekunden] =&gt; zeitgesteuerter Power-Down (0x9B) wird aktiviert b) Default: (Es wird kein Argument übergeben!) =&gt; normaler Power-Down (0x9D) wird aktiviert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (13 × 2)
- [LIEFERANTEN](#table-lieferanten) (33 × 2)
- [FORTTEXTE](#table-forttexte) (47 × 2)
- [FARTTEXTE](#table-farttexte) (3 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 4)
- [FUMWELTTEXTE](#table-fumwelttexte) (2 × 3)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 13 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xB2 | ERROR_ECU_NUMBER |
| 0xFF | ERROR_ECU_NACK |
| ?10? | ERROR_ARGUMENT |
| ?20? | ERROR_FEHLERANZAHL |
| ?70? | ERROR_NUMBER_ARGUMENT |
| ?71? | ERROR_RANGE_ARGUMENT |
| ?72? | ERROR_VERIFY |
| 0x?? | ERROR_ECU_UNKNOWN_STATUSBYTE |

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

Dimensions: 47 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x00 | Hardware: Betriebsspannung defekt |
| 0x04 | Hardware: Eigenraderkennung nicht moeglich |
| 0x05 | Hardware: EEPROM-Fehler Systemprozessor |
| 0x06 | Hardware: EEPROM-Fehler Kommunikationsprozessor |
| 0x07 | Hardware: RAM-Fehler Systemprozessor |
| 0x08 | Hardware: RAM-Fehler Kommunikationsprozessor |
| 0x09 | Hardware: RAM-Fehler Timerprozessor |
| 0x0b | Hardware: ROM-Fehler Systemprozessor |
| 0x0c | Hardware: ROM-Fehler Kommunikationsprozessor |
| 0x0d | Hardware: ROM-Fehler Timerprozessor |
| 0x10 | Hardware: Betriebsspannung Empfaenger defekt |
| 0x11 | Hardware: Betriebsstrom Empfaenger defekt |
| 0x12 | Hardware: Schnittstellenfehler System- mit Komm.-Prozessor |
| 0x13 | Hardware: Schnittstellenfehler System- mit Timer-Prozessor |
| 0x14 | Fremdraeder: Zuviele Radsensoren |
| 0x19 | Hardware: DWA-Ausgang defekt |
| 0x1a | Hardware: RDC-Taster Schluss nach Masse |
| 0x1b | Hardware: RDC-Taster Schluss nach Ub |
| 0x29 | Hardware: kein KBUS Empfang |
| 0x68 | Antenne vorne links: falsche Variante, defekt oder nicht gesteckt |
| 0x69 | Antenne vorne rechts: falsche Variante, defekt oder nicht gesteckt |
| 0x6a | Antenne hinten links: falsche Variante, defekt oder nicht gesteckt |
| 0x6b | Antenne hinten rechts: falsche Variante, defekt oder nicht gesteckt |
| 0x73 | Kalibrierung nicht moeglich |
| 0x80 | KL30 defekt |
| 0x81 | KL15 unterschiedlich: Hardware = AUS &lt;&gt; KBUS-Klemme = EIN |
| 0x82 | KL15 unterschiedlich: Hardware = EIN &lt;&gt; KBUS-Klemme = AUS |
| 0x2c | Radsensor: Batterie low vorne links |
| 0x2d | Radsensor: Sensorfehler vorne links |
| 0x2e | Uebertragungskanal: vorne links defekt |
| 0x2f | Radsensor: Batterie low vorne rechts |
| 0x30 | Radsensor: Sensorfehler vorne rechts |
| 0x31 | Uebertragungskanal: vorne rechts defekt |
| 0x32 | Radsensor: Batterie low hinten links |
| 0x33 | Radsensor: Sensorfehler hinten links |
| 0x34 | Uebertragungskanal: hinten links defekt |
| 0x35 | Radsensor: Batterie low hinten rechts |
| 0x36 | Radsensor: Sensorfehler hinten rechts |
| 0x37 | Uebertragungskanal: hinten rechts defekt |
| 0x38 | Radsensor: Batterie low Reserverad |
| 0x39 | Radsensor: Sensorfehler Reserverad |
| 0x3a | Radsensor: Reserverad sendet nicht |
| 0x3b | Radsensor: Batterie low, Radposition unbekannt |
| 0x3c | Radsensor: Sensorfehler, Radposition unbekannt |
| 0x3d | Uebertragungskanal defekt, Position unbekannt |
| 0x0E | defektes 5-Radsystem |
| 0xXY | unbekannter Fehlerort |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 3 rows × 2 columns

| ART | ARTTEXT |
| --- | --- |
| 0x00 | sporadischer Fehler |
| 0x01 | statischer Fehler |
| 0xXY | unbekannte Fehlerart |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 1 rows × 4 columns

| ORT | UW_ANZ | UW_SATZ | UW1_NR |
| --- | --- | --- | --- |
| 0xFF | 0x01 | 0x01 | 0x01 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 2 rows × 3 columns

| UWNR | UWTEXT | UW_EINH |
| --- | --- | --- |
| 0x01 | Fahrzeuggeschwindigkeit | km/h |
| 0xXY | unbekannte Umweltbedingung | XY |
