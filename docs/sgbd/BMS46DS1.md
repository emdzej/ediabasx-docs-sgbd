# BMS46DS1.prg

- Jobs: [106](#jobs)
- Tables: [8](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | BMS 46 fuer M43 EU3 |
| ORIGIN | BMW TI-433 Schiefer |
| REVISION | 1.09 |
| AUTHOR | BMW EE-30 Hecht , BMW TP-421 Weber, BMW TI-433 Schiefer |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [RAM_LESEN](#job-ram-lesen) - Beliebige RAM - Zellen auslesen
- [ROM_LESEN](#job-rom-lesen) - Beliebige EPROM - Zellen auslesen
- [ECU_CONFIG](#job-ecu-config) - Ident-Daten fuer DME
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Pruefcode-Daten in Hex auslesen
- [IDENT](#job-ident) - Ident-Daten fuer DME
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender-Info-Feldes
- [IDENT_AIF](#job-ident-aif) - Ident und AIF zusammen lesen
- [STATUS_DIGITAL_OBDII](#job-status-digital-obdii) - Status Schalteingaenge
- [initialisierung](#job-initialisierung) - Default Init-Job
- [INFO](#job-info) - Information SGBD
- [SEED_KEY](#job-seed-key) - Schutzmechanismus SEED_KEY
- [STATUS_CODIER_CHECKSUMME](#job-status-codier-checksumme) - Codier - Checksumme abfragen
- [STATUS_MOTORDREHZAHL](#job-status-motordrehzahl) - Motordrehzahl auslesen
- [STATUS_MOTORTEMPERATUR](#job-status-motortemperatur) - Motortemperatur auslesen
- [STATUS_KUEHLW_AUSL_TEMPERATUR](#job-status-kuehlw-ausl-temperatur) - Kuehlwasserauslasstemperatur auslesen
- [STATUS_AN_LUFTTEMPERATUR](#job-status-an-lufttemperatur) - Ansauglufttemperatur auslesen
- [STATUS_LAST](#job-status-last) - Lastsignal auslesen
- [STATUS_UBATT](#job-status-ubatt) - Batteriespannung auslesen
- [STATUS_VERSORGUNG_DKP](#job-status-versorgung-dkp) - Versorgungsspannung DKP auslesen
- [STATUS_VERSORGUNG_HFM_TAN_TMO_TKA](#job-status-versorgung-hfm-tan-tmo-tka) - Versorgungsspannung HFM_TAN_TMO_TKA auslesen
- [STATUS_GESCHWINDIGKEIT](#job-status-geschwindigkeit) - Geschwindigkeit auslesen
- [STATUS_DKP_SPANNUNG](#job-status-dkp-spannung) - Drosselklappenspannung auslesen
- [STATUS_DKP_WINKEL](#job-status-dkp-winkel) - Drosselklappenwinkel auslesen
- [STATUS_LMM_SPANNUNG](#job-status-lmm-spannung) - Lastsignal Spg auslesen
- [STATUS_KL15_SPANNUNG](#job-status-kl15-spannung) - Lastsignal Spg auslesen
- [STATUS_ZUENDWINKEL](#job-status-zuendwinkel) - Zuendwinkel auslesen
- [STATUS_LS_VKAT_SIGNAL_1](#job-status-ls-vkat-signal-1) - Lambdasondenspannung Sonde 1
- [STATUS_LS_NKAT_SIGNAL_1](#job-status-ls-nkat-signal-1) - Lambdasondenspannung Sonde 1 nach KAT
- [STATUS_LAMBDA_INTEGRATOR_1](#job-status-lambda-integrator-1) - Lambdaregelfaktor auslesen
- [STATUS_LAMBDA_MUL_1](#job-status-lambda-mul-1) - Adaption Gemisch multiplikativ auslesen
- [STATUS_LAMBDA_ADD_1](#job-status-lambda-add-1) - Adaption Gemisch additiv auslesen
- [STATUS_TE_TASTVERHAELTNIS](#job-status-te-tastverhaeltnis) - TE Tastverhaeltnis auslesen
- [STATUS_EINSPRITZZEIT](#job-status-einspritzzeit) - Auslesen der Einspritzzeit pro Umdrehung
- [STATUS_LMM_MASSE](#job-status-lmm-masse) - Luftmasse lesen
- [STATUS_LL_INTEGRATOR](#job-status-ll-integrator) - Auslesen des Leerlaufintegrators
- [STATUS_LL_SOLL_LUFTMASSE](#job-status-ll-soll-luftmasse) - LL Soll LM auslesen
- [STATUS_LL_ADAPTION](#job-status-ll-adaption) - LL Soll LM auslesen
- [STATUS_LL_SOLLDREHZAHL](#job-status-ll-solldrehzahl) - Solldrehzahl Leerlaufregler auslesen
- [STATUS_DK_ADAPTION](#job-status-dk-adaption) - Adaption Drosselklappenpotentiometer auslesen
- [STATUS_TE_ADAPTION](#job-status-te-adaption) - Adaption Tankentlueftung auslesen
- [STATUS_BSZ](#job-status-bsz) - Betriebsstundenzaehlers auslesen
- [STATUS_E_LUEFTER_TV](#job-status-e-luefter-tv) - Tastverhaeltnis E-Luefter Ansteuerung auslesen
- [STATUS_KFK_TV](#job-status-kfk-tv) - Tastverhaeltnis Ansteuerung Kennfeldkuehlung auslesen
- [STATUS_LS_VKAT_HEIZUNG_TV_1](#job-status-ls-vkat-heizung-tv-1) - Tastverhaeltnis  Lambdasondenheizung vor KAT
- [STATUS_LS_NKAT_HEIZUNG_TV_1](#job-status-ls-nkat-heizung-tv-1) - Tastverhaeltnis Ansteuerung Lambdasondenheizung nach KAT
- [STATUS_LL_STELLER_TV](#job-status-ll-steller-tv) - Tastverhaeltnis Ansteuerung  LL-Steller auslesen
- [STATUS_SYSTEMCHECK_LAUFUNRUHE](#job-status-systemcheck-laufunruhe) - Systemcheck Laufunruhe lesen
- [STATUS_DIGITAL](#job-status-digital) - Status Schalteingaenge
- [STATUS_UEBERDREH](#job-status-ueberdreh)
- [STEUERN_EV_1](#job-steuern-ev-1) - EV 1 ansteuern
- [STEUERN_EV_2](#job-steuern-ev-2) - EV 2 ansteuern
- [STEUERN_EV_3](#job-steuern-ev-3) - EV 3 ansteuern
- [STEUERN_EV_4](#job-steuern-ev-4) - EV 4 ansteuern
- [STEUERN_EV_1_AUS](#job-steuern-ev-1-aus) - EV 1 ausschalten
- [STEUERN_EV_2_AUS](#job-steuern-ev-2-aus) - EV 2 ausschalten
- [STEUERN_EV_3_AUS](#job-steuern-ev-3-aus) - EV 3 ausschalten
- [STEUERN_EV_4_AUS](#job-steuern-ev-4-aus) - EV 4 ausschalten
- [STEUERN_DISA](#job-steuern-disa) - Differenziertere Saugrohranlage ansteuern,0 oder 0xFF
- [STEUERN_SSP](#job-steuern-ssp) - Saugstrahlpumpenventil ansteuern, 0 oder 255
- [STEUERN_E_LUEFTER](#job-steuern-e-luefter) - Elektroluefter ansteuern, 0 oder 29 - 228
- [STEUERN_LS_HEIZUNG](#job-steuern-ls-heizung) - Lambdasondenheizungsrelais ansteuern, 0 - 255
- [STEUERN_LS_HEIZUNG_HK](#job-steuern-ls-heizung-hk) - Lambdasondenheizungsrelais ansteuern hinter KAT, 0-255
- [STEUERN_TEV](#job-steuern-tev) - Tankentlueftungsventil  ansteuern, 0 oder 255
- [STEUERN_KO](#job-steuern-ko) - Klimakompressor ansteuern, 0 oder 255
- [STEUERN_EKP](#job-steuern-ekp) - EKP ansteuern
- [STEUERN_LL_STELLER](#job-steuern-ll-steller) - Einwegdrehsteller ansteuern, 0 oder 255
- [STEUERN_KF_THERMOSTAT](#job-steuern-kf-thermostat) - KennfeldkuehlungHeizung  ansteuern, 0 oder 255
- [STEUERN_SLP](#job-steuern-slp) - Sekundaerluftpumpe ansteuern, 0 oder 255
- [START_SEK_LUFT](#job-start-sek-luft) - Sekundaerluftpumpe ansteuern
- [STOP_SEK_LUFT](#job-stop-sek-luft) - Sekundaerluftpumpe ansteuern
- [STEUERN_SLV](#job-steuern-slv) - Sekundaerluftventil ansteuern 0 oder 255
- [START_SLV](#job-start-slv) - Sekundaerluftventil ansteuern
- [STOP_SLV](#job-stop-slv) - Sekundaerluftventil ansteuern
- [FS_QUICK_LESEN](#job-fs-quick-lesen) - Auslesen des QUICK Fehlerspeichers
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers
- [FS_SHADOW_LESEN](#job-fs-shadow-lesen) - Auslesen des Fehlerspeichers
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [DIAGNOSE_ERHALTEN](#job-diagnose-erhalten) - Erhalten der Diagnose
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Ende der Diagnose
- [SYSTEM_ADRESSEN_LESEN](#job-system-adressen-lesen) - Auslesen der System-Adressen
- [UPROG_EIN](#job-uprog-ein) - Programmierspannung einschalten
- [UPROG_AUS](#job-uprog-aus) - Programmierspannung ausschalten
- [CO_ABGLEICH_LESEN](#job-co-abgleich-lesen) - CO-Abgleich lesen
- [CO_ABGLEICH_VERSTELLEN](#job-co-abgleich-verstellen) - CO-Abgleich lesen, Verstelloffset aufrechnen und uebergeben
- [CO_ABGLEICH_PROGRAMMIEREN](#job-co-abgleich-programmieren) - CO-Abgleich programmieren
- [LL_ABGLEICH_LESEN](#job-ll-abgleich-lesen) - LL-Abgleich lesen
- [LL_ABGLEICH_VERSTELLEN](#job-ll-abgleich-verstellen) - LL-Abgleich lesen
- [LL_ABGLEICH_PROGRAMMIEREN](#job-ll-abgleich-programmieren) - LL-Abgleich programmieren
- [ADAPT_SELEKTIV_LOESCHEN](#job-adapt-selektiv-loeschen) - Adaptionen selektiv loeschen ,Uebergabeparameter AUSWAHLBYTE_1=Byte 1 : AUSWAHLBYTE_2=Byte 2
- [ADAPT_LOESCHEN](#job-adapt-loeschen) - Adaptionen loeschen
- [STEUERN_SYNC_MODE](#job-steuern-sync-mode) - Status EWS - Mode
- [STATUS_SYNC_MODE](#job-status-sync-mode) - Status EWS - Mode
- [STATUS_L_SONDE](#job-status-l-sonde) - Lambdasondenspannung Sonde 1
- [STATUS_INT](#job-status-int) - Lambdaregelfaktor auslesen
- [STATUS_MUL](#job-status-mul) - Adaption Gemisch multiplikativ auslesen
- [STATUS_ADD](#job-status-add) - Adaption Gemisch additiv auslesen
- [STATUS_LMM](#job-status-lmm) - Luftmasse lesen
- [STATUS_LL_LUFTBEDARF](#job-status-ll-luftbedarf) - Luftmasse lesen
- [STATUS_DKP](#job-status-dkp) - Drosselklappenspannung auslesen
- [ABGAS_VARIANTE_LESEN](#job-abgas-variante-lesen) - Auslesen der Abgasvariante
- [LESEN_SYSTEMCHECK_LAUFUNRUHE](#job-lesen-systemcheck-laufunruhe) - Systemcheck Laufunruhe lesen
- [START_SYSTEMCHECK_SEK_LUFT](#job-start-systemcheck-sek-luft) - SLS Funktionstest
- [STOP_SYSTEMCHECK_SEK_LUFT](#job-stop-systemcheck-sek-luft) - SLS Funktionstest Stop
- [LESEN_SYSTEMCHECK_SEK_LUFT](#job-lesen-systemcheck-sek-luft) - SLS Funktionstest Status
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.

<a id="job-ram-lesen"></a>
### RAM_LESEN

Beliebige RAM - Zellen auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RAM_LESEN_ADRESSE | long | Uebergabeparameter, Startadresse High-Middle-Low |
| RAM_LESEN_ANZAHL_BYTE | long | Uebergabeparameter, Anzahl der auszulesenden BYTES |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| RAM_LESEN_WERT | binary | nichts |
| RAM_LESEN_EINH | string | Einheit HEX |

<a id="job-rom-lesen"></a>
### ROM_LESEN

Beliebige EPROM - Zellen auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ROM_LESEN_ADRESSE | long | Uebergabeparameter, Startadresse High-Middle-Low |
| ROM_LESEN_ANZAHL_BYTE | long | Uebergabeparameter, Anzahl der auszulesenden BYTES |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ROM_LESEN_WERT | binary | nichts |
| ROM_LESEN_EINH | string | Einheit HEX |

<a id="job-ecu-config"></a>
### ECU_CONFIG

Ident-Daten fuer DME

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| ASC_VORHANDEN | int | ASC vorhanden 1=ja ,  0=nein , 0xff=nicht unterstuetzt |
| KAT_VORHANDEN | int | KAT vorhanden 1=ja ,  0=nein , 0xff=nicht unterstuetzt |
| EGS_VORHANDEN | int | EGS vorhanden 1=ja ,  0=nein , 0xff=nicht unterstuetzt |
| AC_VORHANDEN | int | Klimaanlage. vorhanden 1=ja ,  0=nein , 0xff=nicht unterstuetzt |
| LDP_VORHANDEN | int | LDP vorhanden 1=ja ,  0=nein , 0xff=nicht unterstuetzt |
| SLP_VORHANDEN | int | SLP vorhanden 1=ja ,  0=nein , 0xff=nicht unterstuetzt |
| ANZAHL_ZYLINDER | int | ANZAHL Zylinder |

<a id="job-pruefcode-lesen"></a>
### PRUEFCODE_LESEN

Pruefcode-Daten in Hex auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| PRUEFCODE | binary | Daten in Hex-Format |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer DME

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
| ID_AI_NR | string | Aenderungsindex |
| ID_PROD_NR | string | Produktionsnummer |
| ID_AIF_VORHANDEN | int | Ist ein AIF vorhanden (0 (nein)/ 1 (ja)) |
| ID_EWS_SS | int | Identifikation EWS-Schnittstelle |
| ID_MOTOR | string | SG - Identifikation fuer MoTest |
| ID_LAMBDA_STEREO | int | Parameter fuer MoTest 0=Mono, 1=STEREO |
| ID_EML | int | Parameter fuer MoTest 0=Kein EML verb, 1=EML M70, 2=EML M73 |
| ID_LU_MESSUNG | int | Parameter fuer MoTest 1=Laufunruhemessung sonst 0 |
| ID_OBD2 | int | Parameter fuer MoTest 0=ECE, 1=OBD2-Fahrzeug |
| ID_SG_HERSTELLER | int | Parameter fuer MoTest 0=Bosch, 1=Siemens-Fahrzeug |

<a id="job-aif-lesen"></a>
### AIF_LESEN

Auslesen des Anwender-Info-Feldes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| AIF_FG_NR | string | Fahrgestellnummer |
| AIF_DATUM | string | Fertigungsdatum |
| AIF_AENDERUNGS_INDEX | string | Aenderungsindex |
| AIF_SW_NR | long | Softwarenummer |
| AIF_BEHOERDEN_NR | long | Behoerdennummer |
| AIF_ZB_NR | long | Zusbaunummer |
| AIF_PROGG_NR | string | Programmiergeraet Seriennummer |
| AIF_WERKSCODE | string | Haendlernummer (Werkscode) |
| AIF_KM_STAND | long | km-Stand |
| AIF_ANZAHL_PROG | int | Anzahl Programmiervorgaenge |

<a id="job-ident-aif"></a>
### IDENT_AIF

Ident und AIF zusammen lesen

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
| ID_AI_NR | string | Aenderungsindex |
| ID_PROD_NR | string | Produktionsnummer |
| AIF_FG_NR | string | Fahrgestellnummer |
| AIF_DATUM | string | Fertigungsdatum |
| AIF_AENDERUNGS_INDEX | string | Aenderungsindex |
| AIF_SW_NR | long | Softwarenummer |
| AIF_BEHOERDEN_NR | long | Behoerdennummer |
| AIF_ZB_NR | long | Zusbaunummer |
| AIF_PROGG_NR | string | Programmiergeraet Seriennummer |
| AIF_WERKSCODE | string | Haendlernummer (Werkscode) |
| AIF_KM_STAND | long | km-Stand |
| AIF_ANZAHL_PROG | int | Anzahl Programmiervorgaenge |

<a id="job-status-digital-obdii"></a>
### STATUS_DIGITAL_OBDII

Status Schalteingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| STAT_MIL | int | Ueberwachung MIL Status (DATA A, Byte 6, 1xxx xxxx) |
| ANZAHL_MIL | int | Anzahl von MIL Fehlern (DATA A, Byte 6, x111 1111) |
| STAT_UBW_KOMP | int | Ueberwachung uebriger Komponenten (DATA B, Byte 7, x0xx x1xx) |
| STAT_UBW_KVS | int | Ueberwachung Kraftstoffversorgung (DATA B, Byte 7, xx0x xx1x) |
| STAT_UBW_AUS | int | Ueberwachung Verbrennungsaussetzer (DATA B, Byte 7, xxx0 xxx1) |
| STAT_UBW_LSH | int | Ueberwachung Lambdasondenheizung (DATA C, Byte 8, x1xx xxxx) |
| STAT_UBW_LS | int | Ueberwachung Lambdasonden (DATA C, Byte 8, xx1x xxxx) |
| STAT_UBW_SLS | int | Ueberwachung Sekundaerluft (DATA C, Byte 8, xxxx 1xxx) |
| STAT_UBW_KKV | int | Ueberwachung Katalysator (DATA C, Byte 8, xxxx xxx1) |
| STAT_RDY_LSH | int | Lambdasondenheizungsueberwachung (DATA D, Byte 9, x1xx xxxx) |
| STAT_RDY_LS | int | Lambdasondenueberwachung (DATA D, Byte 9, xx1x xxxx) |
| STAT_RDY_SLS | int | Sekundaeluftdiagnose (DATA D, Byte 9, xxxx 1xxx) |
| STAT_RDY_KKV | int | Katalysatorueberwachung (DATA D, Byte 9, xxxx xxx1) |
| STAT_RDY_KOMP | int | Readiness der uebrigen Komponenten (DATA B, Byte 7, x1xx xxxx) |
| STAT_RDY_KVS | int | Readiness Kraftstoffsystem (DATA B, Byte 7, xx1x xxxx) |
| STAT_RDY_AUS | int | Readiness Verbrennungsaussetzer (DATA B, Byte 7, xxx1 xxxx) |
| STAT_UBW_AGR | int | Ueberwachung Abgasrueckfuehrung (DATA C, Byte 8, 1xxx xxxx) |
| STAT_UBW_KLIMA | int | Ueberwachung Klimaanlage (DATA C, Byte 8, xxx1 xxxx) |
| STAT_UBW_TES | int | Ueberwachung Tankentlueftungssystem (DATA C, Byte 8, xxxx x1xx) |
| STAT_UBW_KATHEIZ | int | Ueberwachung Katalysatorheizung (DATA C, Byte 8, xxxx xx1x) |
| KM_STAND_MIL_AN | unsigned int | Kilometerstand MIL an |

<a id="job-initialisierung"></a>
### initialisierung

Default Init-Job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn job erfolgreich 0 wenn job nicht erfolgreich |

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

<a id="job-seed-key"></a>
### SEED_KEY

Schutzmechanismus SEED_KEY

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_SEED_KEY | binary | Rueckgabewert Status |
| Z_ZAHL | int | Zufallszahl |

<a id="job-status-codier-checksumme"></a>
### STATUS_CODIER_CHECKSUMME

Codier - Checksumme abfragen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_CHECKSUMME_WERT | int | Ergebnis |

<a id="job-status-motordrehzahl"></a>
### STATUS_MOTORDREHZAHL

Motordrehzahl auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_MOTORDREHZAHL_WERT | real | Ergebnis Motordrehzahl |
| STATUS_MOTORDREHZAHL_WERT | real | Ergebnis Motordrehzahl |
| STAT_MOTORDREHZAHL_EINH | string | Einheit Motordrehzahl |

<a id="job-status-motortemperatur"></a>
### STATUS_MOTORTEMPERATUR

Motortemperatur auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_MOTORTEMPERATUR_WERT | real | Ergebnis Motortemperatur |
| STATUS_MOTORTEMPERATUR_WERT | real | Ergebnis Motortemperatur |
| STAT_MOTORTEMPERATUR_EINH | string | Einheit Motortemperatur |

<a id="job-status-kuehlw-ausl-temperatur"></a>
### STATUS_KUEHLW_AUSL_TEMPERATUR

Kuehlwasserauslasstemperatur auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_KUEHLW_AUSL_TEMPERATUR_WERT | real | Ergebnis Kuehlwasserauslasstemperatur |
| STAT_KUEHLW_AUSL_TEMPERATUR_EINH | string | Einheit Kuehlwasserauslasstemperatur |

<a id="job-status-an-lufttemperatur"></a>
### STATUS_AN_LUFTTEMPERATUR

Ansauglufttemperatur auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_AN_LUFTTEMPERATUR_WERT | real | Ergebnis Ansauglufttemperatur |
| STATUS_AN_LUFTTEMPERATUR_WERT | real | Nicht verwenden |
| STAT_AN_LUFTTEMPERATUR_EINH | string | Einheit Ansauglufttemperatur |

<a id="job-status-last"></a>
### STATUS_LAST

Lastsignal auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_LAST_WERT | real | Ergebnis Lastsignal WRGL |
| STAT_LAST_EINH | string | Einheit Lastsignal WRGL |

<a id="job-status-ubatt"></a>
### STATUS_UBATT

Batteriespannung auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_UBATT_WERT | real | Ergebnis Batteriespannung |
| STATUS_UBATT_WERT | real | Nicht verwenden Dummy |
| STAT_UBATT_EINH | string | Einheit Batteriespannung |

<a id="job-status-versorgung-dkp"></a>
### STATUS_VERSORGUNG_DKP

Versorgungsspannung DKP auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_VERSORGUNG_DKP_WERT | real | Ergebnis Versorgungsspannung DKP |
| STAT_VERSORGUNG_DKP_EINH | string | Einheit Versorgungsspannung DKP |

<a id="job-status-versorgung-hfm-tan-tmo-tka"></a>
### STATUS_VERSORGUNG_HFM_TAN_TMO_TKA

Versorgungsspannung HFM_TAN_TMO_TKA auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_VERSORGUNG_HFM_TAN_TMO_TKA_WERT | real | Ergebnis Versorgungsspannung HFM_TAN_TMO_TKA |
| STAT_VERSORGUNG_HFM_TAN_TMO_TKA_EINH | string | Einheit Versorgungsspannung HFM_TAN_TMO_TKA |

<a id="job-status-geschwindigkeit"></a>
### STATUS_GESCHWINDIGKEIT

Geschwindigkeit auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_GESCHWINDIGKEIT_WERT | real | Ergebnis Geschwindigkeit |
| STAT_GESCHWINDIGKEIT_EINH | string | Einheit Geschwindigkeit |

<a id="job-status-dkp-spannung"></a>
### STATUS_DKP_SPANNUNG

Drosselklappenspannung auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_DKP_SPANNUNG_WERT | real | Ergebnis Drosselklappenspannung |
| STAT_DKP_SPANNUNG_EINH | string | Einheit DK-Spannung |

<a id="job-status-dkp-winkel"></a>
### STATUS_DKP_WINKEL

Drosselklappenwinkel auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_DKP_WINKEL_WERT | real | Ergebnis Drosselklappenwinkel |
| STAT_DKP_WINKEL_EINH | string | Einheit DK-Winkel |
| STAT_ROHWERT1 | int | Ergebnis |
| STAT_ROHWERT2 | int | Ergebnis |

<a id="job-status-lmm-spannung"></a>
### STATUS_LMM_SPANNUNG

Lastsignal Spg auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_LMM_SPANNUNG_WERT | real | Ergebnis Lastsignal SPG |
| STAT_LMM_SPANNUNG_EINH | string | Einheit Lastsignal |

<a id="job-status-kl15-spannung"></a>
### STATUS_KL15_SPANNUNG

Lastsignal Spg auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_KL15_SPANNUNG_WERT | real | Ergebnis Lastsignal SPG |
| STAT_KL15_SPANNUNG_EINH | string | Einheit Lastsignal |

<a id="job-status-zuendwinkel"></a>
### STATUS_ZUENDWINKEL

Zuendwinkel auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_ZUENDWINKEL_WERT | real | Ergebnis Zuendwinkel |
| STAT_ZUENDWINKEL_EINH | string | Einheit Zuendwinkel |

<a id="job-status-ls-vkat-signal-1"></a>
### STATUS_LS_VKAT_SIGNAL_1

Lambdasondenspannung Sonde 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_LS_VKAT_SIGNAL_1_WERT | real |  |
| STAT_LS_VKAT_SIGNAL_1_EINH | string | Einheit V |

<a id="job-status-ls-nkat-signal-1"></a>
### STATUS_LS_NKAT_SIGNAL_1

Lambdasondenspannung Sonde 1 nach KAT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_LS_NKAT_SIGNAL_1_WERT | real |  |
| STAT_LS_NKAT_SIGNAL_1_EINH | string | Einheit V |

<a id="job-status-lambda-integrator-1"></a>
### STATUS_LAMBDA_INTEGRATOR_1

Lambdaregelfaktor auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_LAMBDA_INTEGRATOR_1_WERT | real | Ergebnis Lambdaregelfaktor |
| STAT_LAMBDA_INTEGRATOR_1_EINH | string | Einheit Lambdaregelfaktor |

<a id="job-status-lambda-mul-1"></a>
### STATUS_LAMBDA_MUL_1

Adaption Gemisch multiplikativ auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_LAMBDA_MUL_1_WERT | real | Ergebnis Adaption Gemisch multiplikativ |
| STAT_LAMBDA_MUL_1_EINH | string | Einheit Adaption Gemisch multiplikativ |

<a id="job-status-lambda-add-1"></a>
### STATUS_LAMBDA_ADD_1

Adaption Gemisch additiv auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_LAMBDA_ADD_1_WERT | real | Ergebnis Adaption Gemisch additiv |
| STAT_LAMBDA_ADD_1_EINH | string | Einheit Adaption Gemisch additiv |

<a id="job-status-te-tastverhaeltnis"></a>
### STATUS_TE_TASTVERHAELTNIS

TE Tastverhaeltnis auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_TE_TASTVERHAELTNIS_WERT | real | Ergebnis TE Tastverhaeltnis |
| STAT_TE_TASTVERHAELTNIS_EINH | string | Einheit TE_Tastverhaeltnis |

<a id="job-status-einspritzzeit"></a>
### STATUS_EINSPRITZZEIT

Auslesen der Einspritzzeit pro Umdrehung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_EINSPRITZZEIT_WERT | real | Ergebnis Einspritzzeit |
| STAT_EINSPRITZZEIT_EINH | string | Einheit Einspritzzeit |

<a id="job-status-lmm-masse"></a>
### STATUS_LMM_MASSE

Luftmasse lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_LMM_MASSE_WERT | real | Ergebnis Masse Luft |
| STAT_LMM_MASSE_EINH | string | Einheit Masse Luft |

<a id="job-status-ll-integrator"></a>
### STATUS_LL_INTEGRATOR

Auslesen des Leerlaufintegrators

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_LL_INTEGRATOR_WERT | real | Ergebnis Leerlaufintegrator |
| STAT_LL_INTEGRATOR_EINH | string | Einheit Leerlaufintegrator |

<a id="job-status-ll-soll-luftmasse"></a>
### STATUS_LL_SOLL_LUFTMASSE

LL Soll LM auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_LL_SOLL_LUFTMASSE_WERT | real | Ergebnis LL Soll LM auslesen |
| STAT_LL_SOLL_LUFTMASSE_EINH | string | Einheit LL Soll LM |

<a id="job-status-ll-adaption"></a>
### STATUS_LL_ADAPTION

LL Soll LM auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_LL_ADAPTION_WERT | real | Ergebnis LL Soll LM auslesen |
| STAT_LL_ADAPTION_EINH | string | Einheit LL Soll LM |

<a id="job-status-ll-solldrehzahl"></a>
### STATUS_LL_SOLLDREHZAHL

Solldrehzahl Leerlaufregler auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_LL_SOLLDREHZAHL_WERT | real | Ergebnis Solldrehzahl |
| STAT_LL_SOLLDREHZAHL_EINH | string | Einheit Solldrehzahl |

<a id="job-status-dk-adaption"></a>
### STATUS_DK_ADAPTION

Adaption Drosselklappenpotentiometer auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_DK_ADAPTION_WERT | real | Ergebnis Adaption DKP |
| STAT_DK_ADAPTION_EINH | string | Einheit Adaption DKP |

<a id="job-status-te-adaption"></a>
### STATUS_TE_ADAPTION

Adaption Tankentlueftung auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_TE_ADAPTION_WERT | real | Ergebnis Adaption TE |
| STAT_TE_ADAPTION_EINH | string | Einheit Adaption TE |

<a id="job-status-bsz"></a>
### STATUS_BSZ

Betriebsstundenzaehlers auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_BSZ_WERT | real | Ergebnis Batteriespannungr |
| STAT_BSZ_EINH | string | Einheit Batteriespannung |

<a id="job-status-e-luefter-tv"></a>
### STATUS_E_LUEFTER_TV

Tastverhaeltnis E-Luefter Ansteuerung auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_E_LUEFTER_TV_WERT | real | Ergebnis Tastverhaeltnis E-Luefter Ansteuerung |
| STAT_E_LUEFTER_TV_EINH | string | Einheit Tastverhaeltnis E-Luefter Ansteuerung |

<a id="job-status-kfk-tv"></a>
### STATUS_KFK_TV

Tastverhaeltnis Ansteuerung Kennfeldkuehlung auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_KFK_TV_WERT | real | Ergebnis Tastverhaeltnis Ansteuerung Kennfeldkuehlung |
| STAT_KFK_TV_EINH | string | Einheit Tastverhaeltnis Ansteuerung Kennfeldkuehlung |

<a id="job-status-ls-vkat-heizung-tv-1"></a>
### STATUS_LS_VKAT_HEIZUNG_TV_1

Tastverhaeltnis  Lambdasondenheizung vor KAT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_LS_VKAT_HEIZUNG_TV_1_WERT | real | Ergebnis Tastverhaeltnis Ansteuerung Lambdasondenheizung |
| STAT_LS_VKAT_HEIZUNG_TV_1_EINH | string | Einheit Tastverhaeltnis Ansteuerung Lambdasondenheizung |

<a id="job-status-ls-nkat-heizung-tv-1"></a>
### STATUS_LS_NKAT_HEIZUNG_TV_1

Tastverhaeltnis Ansteuerung Lambdasondenheizung nach KAT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_LS_NKAT_HEIZUNG_TV_1_WERT | real | Ergebnis Tastverhaeltnis Ansteuerung Lambdasondenheizung nach KAT |
| STAT_LS_NKAT_HEIZUNG_TV_1_EINH | string | Einheit Tastverhaeltnis Ansteuerung Lambdasondenheizung nach KAT |

<a id="job-status-ll-steller-tv"></a>
### STATUS_LL_STELLER_TV

Tastverhaeltnis Ansteuerung  LL-Steller auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_LL_STELLER_TV_WERT | real | Ergebnis Tastverhaeltnis Ansteuerung  LL-Steller |
| STAT_LL_STELLER_TV_EINH | string | Einheit Tastverhaeltnis Ansteuerung  LL-Steller |

<a id="job-status-systemcheck-laufunruhe"></a>
### STATUS_SYSTEMCHECK_LAUFUNRUHE

Systemcheck Laufunruhe lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_SYSTEMCHECK_LAUFUNRUHE_ZYL1_WERT | real |  |
| STAT_SYSTEMCHECK_LAUFUNRUHE_ZYL2_WERT | real |  |
| STAT_SYSTEMCHECK_LAUFUNRUHE_ZYL3_WERT | real |  |
| STAT_SYSTEMCHECK_LAUFUNRUHE_ZYL4_WERT | real |  |
| STAT_SYSTEMCHECK_LAUFUNRUHE_EINH | string | Einheit |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

Status Schalteingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_KL15_EIN | int | STAT Klemme 15, 0=Aus / 1=Ein |
| STAT_START_EIN | int | Start 0=Nein / 1=Ja |
| STAT_LL_EIN | int | Leerlauf 0=Nein / 1=Ja |
| STAT_TL_EIN | int | Teillast 0=Nein / 1=Ja |
| STAT_VL_EIN | int | Beschleunigungsanreicherung 0=Aus / 1=Ein |
| STAT_SCHUBAB_EIN | int | STAT Schubabschaltung 0=Aus / 1=Ein |
| STAT_TEV_EIN | int | STAT Tankentlueftungsventil 0=Aus / 1=Ein |
| STAT_LAMBDAREGELUNG_1_EIN | int | Lambdaregelung 0=Nein / 1=Ja |
| STAT_EGS_VORHANDEN | int | EGS verbaut 0=Nein / 1=Ja |
| STAT_ASC_VORHANDEN | int | ASC verbaut 0=Nein / 1=Ja |
| STAT_KAT_VORHANDEN | int | KAT verbaut 0=Nein / 1=Ja |
| STAT_KLIMA_VORHANDEN | int | Klima verbaut 0=Nein / 1=Ja |
| STAT_KO_EIN | int | Klima-Anforderung 0=Nein / 1=Ja |
| STAT_AC_EIN | int | Anforderung Klimabereitschaft 0=Nein / 1=Ja |
| STAT_KO_ANSTEUERUNG_EIN | int | Klimakompressor angesteuert 0=Nein / 1=Ja |
| STAT_DISA_ANSTEUERUNG_EIN | int | Disa-Ansteuerung 0=Nein / 1=Ja |
| STAT_AD_GUT_EIN | int | Geberradadaption abgeschlossen 0=Nein / 1=Ja |
| STAT_LU_AKTIV_EIN | int | Laufunruhe aktiv 0=Nein / 1=Ja |
| STAT_FAHRSTUFE_EIN | int | Fahrstufe EIN 0=Nein / 1=Ja |
| STAT_KLOPFREGELUNG_EIN | int | Klopfregelung EIN 0=Nein / 1=Ja |
| STAT_LAMBDASONDENHEIZUNG_EIN | int | Lambdasondenheizung EIN 0=Nein / 1=Ja |
| STAT_LAMBDASONDENHEIZUNG_GETAKTET_EIN | int | Lambdasondenheizunggetaktet 0=Nein / 1=Ja |
| STAT_LAMBDASONDENBEREITSCHAFT_EIN | int | Lambdasondenbereitschaft 0=Nein / 1=Ja |
| STAT_FEHLERLAMPE_EIN | int | Fehlerlampe an 0=Nein / 1=Ja |
| STAT_ASC_EINGRIFF_EIN | int | ASC Eingriff 0=Nein / 1=Ja |
| STAT_EKP_ANSTEUERUNG_EIN | int | EKP angesteuert 0=Nein / 1=Ja |
| STAT_TAUPUNKT | int | Taupunkt ueberschritten 0=Nein / 1=Ja |
| STAT_EWS_OK | int | EWS ok 0=Nein / 1=Ja |
| STAT_SSP | int | SSP geschlossen 0=Nein / 1=Ja |
| STAT_IN_OUT_FZG_TYP | int | EKP angesteuert 0=E46 / 1=E36 |
| STAT_OV_B_AUTOMAT | int | Automat erkannt 0=Nein / 1=Ja |
| STAT_OV_B_KLIMA | int | Klima erkannt 0=Nein / 1=Ja |
| STAT_SLV_EIN | int | Automat erkannt 0=Nein / 1=Ja |
| STAT_SLP_EIN | int | Klima erkannt 0=Nein / 1=Ja |
| STAT_TAUPUNKT_NKAT | int | Taupunkt nach KAT  ueberschritten 0=Nein / 1=Ja |
| STAT_SG_JUNGF | int | Status Steuergeraet |
| STATUS_KO_EIN | int | Nicht verwenden |
| STATUS_AC_EIN | int | Nicht verwenden |
| STATUS_LL_EIN | int | Nicht verwenden |
| STATUS_TL_EIN | int | Nicht verwenden |
| STATUS_VL_EIN | int | Nicht verwenden |
| STATUS_MILANSTEUERUNG | int | MIL 0=nicht angest./ 1=angest. |
| STATUS_SLS_TEST | int | SLS 0=nicht angest./ 1=angest. |

<a id="job-status-ueberdreh"></a>
### STATUS_UEBERDREH

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_UEBERDREH_NMAXSP | real |  |
| STAT_UEBERDREH_NMAXBS | real |  |
| STAT_UEBERDREH_NMAXHZ | real |  |

<a id="job-steuern-ev-1"></a>
### STEUERN_EV_1

EV 1 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ev-2"></a>
### STEUERN_EV_2

EV 2 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ev-3"></a>
### STEUERN_EV_3

EV 3 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ev-4"></a>
### STEUERN_EV_4

EV 4 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ev-1-aus"></a>
### STEUERN_EV_1_AUS

EV 1 ausschalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ev-2-aus"></a>
### STEUERN_EV_2_AUS

EV 2 ausschalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ev-3-aus"></a>
### STEUERN_EV_3_AUS

EV 3 ausschalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ev-4-aus"></a>
### STEUERN_EV_4_AUS

EV 4 ausschalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-disa"></a>
### STEUERN_DISA

Differenziertere Saugrohranlage ansteuern,0 oder 0xFF

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | 0 oder 0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ssp"></a>
### STEUERN_SSP

Saugstrahlpumpenventil ansteuern, 0 oder 255

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | 0 oder 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-e-luefter"></a>
### STEUERN_E_LUEFTER

Elektroluefter ansteuern, 0 oder 29 - 228

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | 0 oder 29-228 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ls-heizung"></a>
### STEUERN_LS_HEIZUNG

Lambdasondenheizungsrelais ansteuern, 0 - 255

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | 0 oder 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ls-heizung-hk"></a>
### STEUERN_LS_HEIZUNG_HK

Lambdasondenheizungsrelais ansteuern hinter KAT, 0-255

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | 0-255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-tev"></a>
### STEUERN_TEV

Tankentlueftungsventil  ansteuern, 0 oder 255

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | 0 oder 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ko"></a>
### STEUERN_KO

Klimakompressor ansteuern, 0 oder 255

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | 0 oder 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ekp"></a>
### STEUERN_EKP

EKP ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ll-steller"></a>
### STEUERN_LL_STELLER

Einwegdrehsteller ansteuern, 0 oder 255

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | 0 oder 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-kf-thermostat"></a>
### STEUERN_KF_THERMOSTAT

KennfeldkuehlungHeizung  ansteuern, 0 oder 255

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | 0 oder 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-slp"></a>
### STEUERN_SLP

Sekundaerluftpumpe ansteuern, 0 oder 255

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-start-sek-luft"></a>
### START_SEK_LUFT

Sekundaerluftpumpe ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-stop-sek-luft"></a>
### STOP_SEK_LUFT

Sekundaerluftpumpe ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-slv"></a>
### STEUERN_SLV

Sekundaerluftventil ansteuern 0 oder 255

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-start-slv"></a>
### START_SLV

Sekundaerluftventil ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-stop-slv"></a>
### STOP_SLV

Sekundaerluftventil ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-fs-quick-lesen"></a>
### FS_QUICK_LESEN

Auslesen des QUICK Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ANZ_NR | int | Anzahl der gespeicherten Fehler |
| F_BSZ_AKT | real | Betriebsstundenzahler aktuell |
| F_BSZ_ALT | real | Betriebsstundenzaehler beim letzten Loeschen |

<a id="job-fs-lesen"></a>
### FS_LESEN

Auslesen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ART_ANZ | int | Anzahl der Fehlerarten des SG |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen des einzelnen Fehlers |
| F_ANZ_NR | int | Anzahl der gespeicherten Fehler |
| F_ORT_NR | int | Fehlercode des SG als Index |
| F_ORT_TEXT | string | Fehlercode des SG als Text |
| F_HFK | int | Haeufigkeit des einzelnen Fehlers |
| F_LZ | int | Fehlerlogistikzaehler |
| F_ART1_NR | int | Fehlerart 1 Index |
| F_ART1_TEXT | string | Fehlerart 1 Text |
| F_ART2_NR | int | Fehlerart 2 Index |
| F_ART2_TEXT | string | Fehlerart 2 Text |
| F_ART3_NR | int | Fehlerart 3 Index |
| F_ART3_TEXT | string | Fehlerart 3 Text |
| F_ART4_NR | int | Fehlerart 4 Index |
| F_ART4_TEXT | string | Fehlerart 4 Text |
| F_ART5_NR | int | Fehlerart 5 Index |
| F_ART5_TEXT | string | Fehlerart 5 Text |
| F_ART6_NR | int | Fehlerart 6 Index |
| F_ART6_TEXT | string | Fehlerart 6 Text |
| F_ART7_NR | int | Fehlerart 7 Index |
| F_ART7_TEXT | string | Fehlerart 7 Text |
| F_ART8_NR | int | Fehlerart 8 Index |
| F_ART8_TEXT | string | Fehlerart 8  Text |
| F_VORHANDEN | int | Statusbit Fehler vorhanden |
| F_ART_BYTE | int | Fehlerartbyte als Rohwert ausgeben |
| F_UW1_NR | int | Satz 1 Umweltbedingung 1 Index |
| F_UW1_TEXT | string | Satz 1 Umweltbedingung 1 Einheit |
| F_UW1_EINH | string | Satz 1 Umweltbedingung 1 Text |
| F_UW1_WERT | real | Satz 1 Umweltbedingung 1 Wert |
| F_UW2_NR | int | Satz 1 Umweltbedingung 2 Index |
| F_UW2_TEXT | string | Satz 1 Umweltbedingung 2 Text |
| F_UW2_EINH | string | Satz 1 Umweltbedingung 2 Einheit |
| F_UW2_WERT | real | Satz 1 Umweltbedingung 2 Wert |
| F_UW3_NR | int | Satz 1 Umweltbedingung 3 Index |
| F_UW3_TEXT | string | Satz 1 Umweltbedingung 3 Text |
| F_UW3_EINH | string | Satz 1 Umweltbedingung 3 Einheit |
| F_UW3_WERT | real | Satz 1 Umweltbedingung 3 Wert |
| F_UW4_NR | int | Satz 1 Umweltbedingung 4 Index |
| F_UW4_TEXT | string | Satz 1 Umweltbedingung 4 Text |
| F_UW4_EINH | string | Satz 1 Umweltbedingung 4 Einheit |
| F_UW4_WERT | real | Satz  1 Umweltbedingung 4  Wert |
| F_UW5_NR | int | Satz 2 Umweltbedingung 1 Index |
| F_UW5_TEXT | string | Satz 2 Umweltbedingung 1 Text |
| F_UW5_EINH | string | Satz 2 Umweltbedingung 1 Einheit |
| F_UW5_WERT | real | Satz  2 Umweltbedingung 1  Wert |
| F_UW6_NR | int | Satz 2 Umweltbedingung 2 Index |
| F_UW6_TEXT | string | Satz 2 Umweltbedingung 2 Text |
| F_UW6_EINH | string | Satz 2 Umweltbedingung 2 Einheit |
| F_UW6_WERT | real | Satz  2 Umweltbedingung 2  Wert |
| F_UW7_NR | int | Satz 2 Umweltbedingung 3 Index |
| F_UW7_TEXT | string | Satz 2 Umweltbedingung 3 Text |
| F_UW7_EINH | string | Satz 2 Umweltbedingung 3 Einheit |
| F_UW7_WERT | real | Satz  2 Umweltbedingung 3  Wert |
| F_UW8_NR | int | Satz 2 Umweltbedingung 4 Index |
| F_UW8_TEXT | string | Satz 2 Umweltbedingung 4 Text |
| F_UW8_EINH | string | Satz 2 Umweltbedingung 4 Einheit |
| F_UW8_WERT | real | Satz  2 Umweltbedingung 4  Wert |
| F_UW9_NR | int | Satz 3 Umweltbedingung 1 Index |
| F_UW9_TEXT | string | Satz 3 Umweltbedingung 1 Text |
| F_UW9_EINH | string | Satz 3 Umweltbedingung 1 Einheit |
| F_UW9_WERT | real | Satz 3 Umweltbedingung 1  Wert |
| F_UW10_NR | int | Satz 3 Umweltbedingung 2 Index |
| F_UW10_TEXT | string | Satz 3 Umweltbedingung 2 Text |
| F_UW10_EINH | string | Satz 3 Umweltbedingung 2 Einheit |
| F_UW10_WERT | real | Satz  3 Umweltbedingung 2  Wert |
| F_UW11_NR | int | Satz 3 Umweltbedingung 3 Index |
| F_UW11_TEXT | string | Satz 3 Umweltbedingung 3 Text |
| F_UW11_EINH | string | Satz 3 Umweltbedingung 3 Einheit |
| F_UW11_WERT | real | Satz  3 Umweltbedingung 3  Wert |
| F_UW12_NR | int | Satz 3 Umweltbedingung 4 Index |
| F_UW12_TEXT | string | Satz 3 Umweltbedingung 4 Text |
| F_UW12_EINH | string | Satz 3 Umweltbedingung 4 Einheit |
| F_UW12_WERT | real | Satz 3 Umweltbedingung 4  Wert |
| F_HEX_CODE | binary | Hexdump des Fehlersatzes |
| F_UW_SATZ | int | Anzahl der Umweltsaetze , Steuerung der Anzeige in der Applikation |
| F_ART_LONG | string | 1 Byte: CARB-Fehlerartbyte (Byte 7), 2 Byte: Fehlerart entprellt (Byte 6) |

<a id="job-fs-shadow-lesen"></a>
### FS_SHADOW_LESEN

Auslesen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ART_ANZ | int | Anzahl der Fehlerarten des SG |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen des einzelnen Fehlers |
| F_ANZ_NR | int | Anzahl der gespeicherten Fehler |
| F_ORT_NR | int | Fehlercode des SG als Index |
| F_ORT_TEXT | string | Fehlercode des SG als Text |
| F_HFK | int | Haeufigkeit des einzelnen Fehlers |
| F_LOGISTIK | int | Fehlerlogistikzaehler |
| F_ART1_NR | int | Fehlerart 1 Index |
| F_ART1_TEXT | string | Fehlerart 1 Text |
| F_ART2_NR | int | Fehlerart 2 Index |
| F_ART2_TEXT | string | Fehlerart 2 Text |
| F_ART3_NR | int | Fehlerart 3 Index |
| F_ART3_TEXT | string | Fehlerart 3 Text |
| F_ART4_NR | int | Fehlerart 4 Index |
| F_ART4_TEXT | string | Fehlerart 4 Text |
| F_ART5_NR | int | Fehlerart 5 Index |
| F_ART5_TEXT | string | Fehlerart 5 Text |
| F_ART6_NR | int | Fehlerart 6 Index |
| F_ART6_TEXT | string | Fehlerart 6 Text |
| F_ART7_NR | int | Fehlerart 7 Index |
| F_ART7_TEXT | string | Fehlerart 7 Text |
| F_ART8_NR | int | Fehlerart 8 Index |
| F_ART8_TEXT | string | Fehlerart 8  Text |
| F_ART | string | Fehlerartbyte |
| F_UW1_NR | int | Satz 1 Umweltbedingung 1 Index |
| F_UW1_TEXT | string | Satz 1 Umweltbedingung 1 Einheit |
| F_UW1_EINH | string | Satz 1 Umweltbedingung 1 Text |
| F_UW1_WERT | real | Satz 1 Umweltbedingung 1 Wert |
| F_UW2_NR | int | Satz 1 Umweltbedingung 2 Index |
| F_UW2_TEXT | string | Satz 1 Umweltbedingung 2 Text |
| F_UW2_EINH | string | Satz 1 Umweltbedingung 2 Einheit |
| F_UW2_WERT | real | Satz 1 Umweltbedingung 2 Wert |
| F_UW3_NR | int | Satz 1 Umweltbedingung 3 Index |
| F_UW3_TEXT | string | Satz 1 Umweltbedingung 3 Text |
| F_UW3_EINH | string | Satz 1 Umweltbedingung 3 Einheit |
| F_UW3_WERT | real | Satz 1 Umweltbedingung 3 Wert |
| F_UW4_NR | int | Satz 1 Umweltbedingung 4 Index |
| F_UW4_TEXT | string | Satz 1 Umweltbedingung 4 Text |
| F_UW4_EINH | string | Satz 1 Umweltbedingung 4 Einheit |
| F_UW4_WERT | real | Satz  1 Umweltbedingung 4  Wert |
| F_UW5_NR | int | Satz 2 Umweltbedingung 1 Index |
| F_UW5_TEXT | string | Satz 2 Umweltbedingung 1 Text |
| F_UW5_EINH | string | Satz 2 Umweltbedingung 1 Einheit |
| F_UW5_WERT | real | Satz  2 Umweltbedingung 1  Wert |
| F_UW6_NR | int | Satz 2 Umweltbedingung 2 Index |
| F_UW6_TEXT | string | Satz 2 Umweltbedingung 2 Text |
| F_UW6_EINH | string | Satz 2 Umweltbedingung 2 Einheit |
| F_UW6_WERT | real | Satz  2 Umweltbedingung 2  Wert |
| F_UW7_NR | int | Satz 2 Umweltbedingung 3 Index |
| F_UW7_TEXT | string | Satz 2 Umweltbedingung 3 Text |
| F_UW7_EINH | string | Satz 2 Umweltbedingung 3 Einheit |
| F_UW7_WERT | real | Satz  2 Umweltbedingung 3  Wert |
| F_UW8_NR | int | Satz 2 Umweltbedingung 4 Index |
| F_UW8_TEXT | string | Satz 2 Umweltbedingung 4 Text |
| F_UW8_EINH | string | Satz 2 Umweltbedingung 4 Einheit |
| F_UW8_WERT | real | Satz  2 Umweltbedingung 4  Wert |
| F_UW9_NR | int | Satz 3 Umweltbedingung 1 Index |
| F_UW9_TEXT | string | Satz 3 Umweltbedingung 1 Text |
| F_UW9_EINH | string | Satz 3 Umweltbedingung 1 Einheit |
| F_UW9_WERT | real | Satz 3 Umweltbedingung 1  Wert |
| F_UW10_NR | int | Satz 3 Umweltbedingung 2 Index |
| F_UW10_TEXT | string | Satz 3 Umweltbedingung 2 Text |
| F_UW10_EINH | string | Satz 3 Umweltbedingung 2 Einheit |
| F_UW10_WERT | real | Satz  3 Umweltbedingung 2  Wert |
| F_UW11_NR | int | Satz 3 Umweltbedingung 3 Index |
| F_UW11_TEXT | string | Satz 3 Umweltbedingung 3 Text |
| F_UW11_EINH | string | Satz 3 Umweltbedingung 3 Einheit |
| F_UW11_WERT | real | Satz  3 Umweltbedingung 3  Wert |
| F_UW12_NR | int | Satz 3 Umweltbedingung 4 Index |
| F_UW12_TEXT | string | Satz 3 Umweltbedingung 4 Text |
| F_UW12_EINH | string | Satz 3 Umweltbedingung 4 Einheit |
| F_UW12_WERT | real | Satz 3 Umweltbedingung 4  Wert |
| F_HEX_CODE | binary | Hexdump des Fehlersatzes |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-diagnose-erhalten"></a>
### DIAGNOSE_ERHALTEN

Erhalten der Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Ende der Diagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-system-adressen-lesen"></a>
### SYSTEM_ADRESSEN_LESEN

Auslesen der System-Adressen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| ADRESSE_UPROG | string | Adresse Programmierspannung |
| ADRESSE_DATEN_REFERENZ | string | Adresse Daten Referenz |
| ADRESSE_ZIF_BACKUP | string | Adresse Einfachablage |
| ADRESSE_LOESCHDAUER | string | Adresse Loeschdauer |
| ADRESSE_HW_REFERENZ | string | Adresse HW Referenz |
| ADRESSE_PRG_REFERENZ | string | Adresse Programm Referenz |
| ADRESSE_AIF | string | Adresse Anwender Info Feld |
| ADRESSE_MAX_BLOCK_LAENGE | string | Adresse der maximalen Blocklaenge |
| ADRESSE_HERST_FERT_DATUM | string | Adresse des Hersteller Fertigungsdatum |
| ADRESSE_EEPROM_SUBSTITUT | string | Adresse des EEPROM-Substituts |

<a id="job-uprog-ein"></a>
### UPROG_EIN

Programmierspannung einschalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STATUS_UPROG_WERT | real | Programmierspannung als Info zurueck |
| STATUS_UPROG_EINH | string | Einheit V |

<a id="job-uprog-aus"></a>
### UPROG_AUS

Programmierspannung ausschalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-co-abgleich-lesen"></a>
### CO_ABGLEICH_LESEN

CO-Abgleich lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STATUS_CO_ABGLEICH_WERT | int | Aktuellen Abgleichwert |

<a id="job-co-abgleich-verstellen"></a>
### CO_ABGLEICH_VERSTELLEN

CO-Abgleich lesen, Verstelloffset aufrechnen und uebergeben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CO_VERSTELL_WERT | int | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-co-abgleich-programmieren"></a>
### CO_ABGLEICH_PROGRAMMIEREN

CO-Abgleich programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-ll-abgleich-lesen"></a>
### LL_ABGLEICH_LESEN

LL-Abgleich lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STATUS_LL_ABGLEICH_WERT | real | Aktuellen Abgleichwert umgerechnet |

<a id="job-ll-abgleich-verstellen"></a>
### LL_ABGLEICH_VERSTELLEN

LL-Abgleich lesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LL_VERSTELL_WERT | int | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-ll-abgleich-programmieren"></a>
### LL_ABGLEICH_PROGRAMMIEREN

LL-Abgleich programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-adapt-selektiv-loeschen"></a>
### ADAPT_SELEKTIV_LOESCHEN

Adaptionen selektiv loeschen ,Uebergabeparameter AUSWAHLBYTE_1=Byte 1 : AUSWAHLBYTE_2=Byte 2

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHLBYTE_1 | int | Auswahlbyte 1 |
| AUSWAHLBYTE_2 | int | Auswahlbyte 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-adapt-loeschen"></a>
### ADAPT_LOESCHEN

Adaptionen loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-sync-mode"></a>
### STEUERN_SYNC_MODE

Status EWS - Mode

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STEUERN_SYNC_MODE_STATUS | int | Statusflag |
| STEUERN_SYNC_MODE_TEXT | string | Statustext |

<a id="job-status-sync-mode"></a>
### STATUS_SYNC_MODE

Status EWS - Mode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STATUS_SYNC_MODE_STATUS | int | Statusflag |
| STATUS_SYNC_MODE_TEXT | string | Statustext |

<a id="job-status-l-sonde"></a>
### STATUS_L_SONDE

Lambdasondenspannung Sonde 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_L_SONDE_WERT | real |  |
| STATUS_L_SONDE_EINH | string | Einheit V |

<a id="job-status-int"></a>
### STATUS_INT

Lambdaregelfaktor auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_INT_WERT | real | Ergebnis Lambdaregelfaktor |
| STATUS_INT_EINH | string | Einheit Lambdaregelfaktor |

<a id="job-status-mul"></a>
### STATUS_MUL

Adaption Gemisch multiplikativ auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_MUL_WERT | real | Ergebnis Adaption Gemisch multiplikativ |
| STATUS_MUL_EINH | string | Einheit Adaption Gemisch multiplikativ |

<a id="job-status-add"></a>
### STATUS_ADD

Adaption Gemisch additiv auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_ADD_WERT | real | Ergebnis Adaption Gemisch additiv |
| STATUS_ADD_EINH | string | Einheit Adaption Gemisch additiv |

<a id="job-status-lmm"></a>
### STATUS_LMM

Luftmasse lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_LMM_WERT | real | Ergebnis Masse Luft |
| STATUS_LMM_EINH | string | Einheit Masse Luft |

<a id="job-status-ll-luftbedarf"></a>
### STATUS_LL_LUFTBEDARF

Luftmasse lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_LL_LUFTBEDARF_WERT | real | Ergebnis Masse Luft |
| STATUS_LL_LUFTBEDARF_EINH | string | Einheit Masse Luft |

<a id="job-status-dkp"></a>
### STATUS_DKP

Drosselklappenspannung auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_DKP_WERT | real | Ergebnis Drosselklappenspannung |
| STATUS_DKP_EINH | string | Einheit DK-Spannung |

<a id="job-abgas-variante-lesen"></a>
### ABGAS_VARIANTE_LESEN

Auslesen der Abgasvariante

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| ABGAS_VARIANTE_WERT | int | Abgasvariante 0=KAT-V , 1= KAT |

<a id="job-lesen-systemcheck-laufunruhe"></a>
### LESEN_SYSTEMCHECK_LAUFUNRUHE

Systemcheck Laufunruhe lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| LESEN_SYSTEMCHECK_LAUFUNRUHE_ZYL1_WERT | int |  |
| LESEN_SYSTEMCHECK_LAUFUNRUHE_ZYL2_WERT | int |  |
| LESEN_SYSTEMCHECK_LAUFUNRUHE_ZYL3_WERT | int |  |
| LESEN_SYSTEMCHECK_LAUFUNRUHE_ZYL4_WERT | int |  |
| LESEN_SYSTEMCHECK_LAUFUNRUHE_EINH | string | Einheit |

<a id="job-start-systemcheck-sek-luft"></a>
### START_SYSTEMCHECK_SEK_LUFT

SLS Funktionstest

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| START_SYSTEMCHECK_SEK_LUFT_STATUS | int |  |
| START_SYSTEMCHECK_STATUS | string |  |

<a id="job-stop-systemcheck-sek-luft"></a>
### STOP_SYSTEMCHECK_SEK_LUFT

SLS Funktionstest Stop

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-lesen-systemcheck-sek-luft"></a>
### LESEN_SYSTEMCHECK_SEK_LUFT

SLS Funktionstest Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| LESEN_SYSTEMCHECK_SEK_LUFT_STATUS | int | Zustandsflag |
| STAT_SYSTEMCHECK_SEK_LUFT | int | Ergebnis 0 = n.I.O    1= i.O |
| LESEN_SYSTEMCHECK_SEK_LUFT_ERGEBNIS | int | Ergebnis 0 = n.I.O    1= i.O |
| LESEN_SYSTEMCHECK_MELDUNG | string |  |
| LESEN_SYSTEMCHECK_STATUS | string |  |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| BYTE1 | int | 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | 0-255 bzw. 0x00-0xFF |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_ARGUMENT, wenn Argumente nicht uebergeben oder ausser Bereich |

## Tables

### Index

- [BITS](#table-bits) (38 × 4)
- [FORTTEXTE](#table-forttexte) (63 × 5)
- [FARTMATRIX](#table-fartmatrix) (71 × 17)
- [FARTTEXTE](#table-farttexte) (65 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (14 × 6)
- [OBD_BITS](#table-obd-bits) (19 × 4)
- [BETRIEBSWTAB](#table-betriebswtab) (1 × 17)
- [JOBRESULT](#table-jobresult) (13 × 2)

<a id="table-bits"></a>
### BITS

Dimensions: 38 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| STAT_Kl15 | 0 | 0x01 | 0x01 |
| STAT_S | 0 | 0x02 | 0x02 |
| STAT_LL | 0 | 0x04 | 0x04 |
| STAT_TL | 0 | 0x08 | 0x08 |
| STAT_VL | 0 | 0x10 | 0x10 |
| STAT_SCHUB | 0 | 0x20 | 0x20 |
| STAT_TEV | 0 | 0x40 | 0x40 |
| STAT_LAM | 0 | 0x80 | 0x80 |
| STAT_V_EGS | 1 | 0x01 | 0x01 |
| STAT_V_ASC | 1 | 0x02 | 0x02 |
| STAT_V_KAT | 1 | 0x04 | 0x04 |
| STAT_V_KLIMA | 4 | 0x80 | 0x80 |
| STAT_A_KLIMA | 1 | 0x10 | 0x10 |
| STAT_A_KLIMABER | 1 | 0x20 | 0x20 |
| STAT_KLIMAAN | 1 | 0x40 | 0x40 |
| STAT_DISA_AN | 1 | 0x80 | 0x80 |
| STAT_FS | 2 | 0x01 | 0x01 |
| STAT_KLOPF | 2 | 0x02 | 0x02 |
| STAT_LSH | 2 | 0x04 | 0x04 |
| STAT_LSH_TAKT | 2 | 0x08 | 0x08 |
| STAT_LAMBDABER | 2 | 0x10 | 0x10 |
| STAT_FL | 2 | 0x20 | 0x20 |
| STAT_ASC | 2 | 0x40 | 0x40 |
| STAT_EKP | 2 | 0x80 | 0x80 |
| STAT_TAUPKT | 3 | 0x01 | 0x01 |
| STAT_EWS | 3 | 0x02 | 0x02 |
| STAT_SSP | 3 | 0x04 | 0x04 |
| STAT_JUNGF | 3 | 0x08 | 0x08 |
| STAT_SLV | 3 | 0x10 | 0x10 |
| STAT_SLP | 3 | 0x20 | 0x20 |
| STAT_TAUPKT_HK | 3 | 0x80 | 0x80 |
| STATUS_MILANSTEUERUNG | 4 | 0x01 | 0x01 |
| STATUS_SLS_TEST | 4 | 0x02 | 0x02 |
| STAT_AD_GUT | 4 | 0x04 | 0x04 |
| STAT_LU_AKTIV | 4 | 0x08 | 0x08 |
| STAT_V_FZG_TYP | 4 | 0x20 | 0x20 |
| STAT_OV_B_AUTOMAT | 4 | 0x40 | 0x40 |
| STAT_OV_B_KLIMA | 4 | 0x80 | 0x80 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 63 rows × 5 columns

| ORT | ORTTEXT | UW_1 | UW_2 | UW_3 |
| --- | --- | --- | --- | --- |
| 0x64 | Ansteuerung Zuendung Zylinder 1 | 0x01 | 0x04 | 0x0b |
| 0x65 | Ansteuerung Zuendung Zylinder 2 | 0x01 | 0x04 | 0x0b |
| 0x66 | Ansteuerung Zuendung Zylinder 3 | 0x01 | 0x04 | 0x0b |
| 0x67 | Ansteuerung Zuendung Zylinder 4 | 0x01 | 0x04 | 0x0b |
| 0x68 | Ansteuerung Einspritzventil Zylinder 1 | 0x01 | 0x04 | 0x05 |
| 0x69 | Ansteuerung Einspritzventil Zylinder 2 | 0x01 | 0x04 | 0x05 |
| 0x6A | Ansteuerung Einspritzventil Zylinder 3 | 0x01 | 0x04 | 0x05 |
| 0x6B | Ansteuerung Einspritzventil Zylinder 4 | 0x01 | 0x04 | 0x05 |
| 0x6C | Ansteuerung Elektroluefter | 0x01 | 0x02 | 0x05 |
| 0x6E | Ansteuerung Klimakompressor | 0x01 | 0x02 | 0x04 |
| 0x6F | Ansteuerung Relais Kraftstoffpumpe | 0x01 | 0x02 | 0x05 |
| 0x70 | Ansteuerung Magnetventil Saugrohr (DISA) | 0x01 | 0x02 | 0x05 |
| 0x71 | Ansteuerung Magnetventil Tankentlueftung | 0x01 | 0x03 | 0x05 |
| 0x72 | Ansteuerung Magnetventil Saugstrahlpumpe | 0x01 | 0x02 | 0x05 |
| 0x73 | Ansteuerung Kennfeldkuehlung | 0x01 | 0x02 | 0x05 |
| 0x75 | Ansteuerung Leerlaufsteller | 0x01 | 0x02 | 0x05 |
| 0x76 | Ansteuerung Lambdasondenheizung vor KAT | 0x01 | 0x02 | 0x05 |
| 0x77 | Signal Drosselklappenpotentiometer | 0x01 | 0x02 | 0x04 |
| 0x78 | Signal Luftmassenmesser | 0x01 | 0x02 | 0x07 |
| 0x79 | Signal Ansauglufttemperatur | 0x01 | 0x04 | 0x05 |
| 0x7A | Signal Kuehlmitteltemperatur | 0x01 | 0x03 | 0x05 |
| 0x7B | Signal Kuehlwasserauslasstemperatur | 0x01 | 0x02 | 0x05 |
| 0x7C | Batteriespannung Hauptrelais | 0x0b | 0x02 | 0x05 |
| 0x7D | Signal Lambdasonde vor KAT | 0x01 | 0x02 | 0x08 |
| 0x7E | Signal CAN ASC | 0x01 | 0x02 | 0x05 |
| 0x7F | Anforderung CAN ASC | 0x01 | 0x02 | 0x05 |
| 0x80 | Signal CAN EGS | 0x01 | 0x02 | 0x05 |
| 0x81 | Anforderung CAN EGS | 0x01 | 0x02 | 0x05 |
| 0x82 | Signal CAN IKE | 0x01 | 0x02 | 0x05 |
| 0x83 | Signal Geschwindigkeit | 0x01 | 0x06 | 0x05 |
| 0x84 | Referenzspannung fuer Luftmassenmesser | 0x01 | 0x02 | 0x05 |
| 0x85 | Referenzspannung fuer Drosselklappenpotentiometer | 0x01 | 0x02 | 0x05 |
| 0x87 | Signal Nockenwellengeber | 0x01 | 0x02 | 0x04 |
| 0x88 | Signal Kurbelwellengeber | 0x01 | 0x02 | 0x05 |
| 0x89 | Signal Klopfsensor 1 | 0x01 | 0x02 | 0x04 |
| 0x8A | Signal Klopfsensor 2 | 0x01 | 0x02 | 0x04 |
| 0x8B | Signal Lambdasonde nach KAT | 0x01 | 0x02 | 0x05 |
| 0x8C | Schnittstelle DME - EWS | 0x01 | 0x06 | 0x0b |
| 0x8D | Lambdaregelung Regelanschlag | 0x01 | 0x04 | 0x05 |
| 0x8E | Klopf-Regelung-Selbsttest | 0x01 | 0x02 | 0x04 |
| 0x8F | Steuergeraete Selbsttest | 0x02 | 0x03 | 0x05 |
| 0x90 | Manipulationsschutz EWS | 0x01 | 0x06 | 0x0b |
| 0x91 | Aussetzer bei Zylinder 1 | 0x01 | 0x04 | 0x06 |
| 0x92 | Aussetzer bei Zylinder 2 | 0x01 | 0x04 | 0x06 |
| 0x93 | Aussetzer bei Zylinder 3 | 0x01 | 0x04 | 0x06 |
| 0x94 | Aussetzer bei Zylinder 4 | 0x01 | 0x04 | 0x06 |
| 0x95 | Ansteuerung Ventil Sekundaerluft | 0x01 | 0x02 | 0x0b |
| 0x96 | Ansteuerung Relais Sekundaerluftpumpe | 0x01 | 0x02 | 0x0b |
| 0x97 | Sekundaerluftsysstem Plausibilitaet | 0x01 | 0x02 | 0x05 |
| 0x98 | SG-Selbsttest E2PROM-Emulation | 0x02 | 0x03 | 0x05 |
| 0x99 | Ansteuerung Lambdasondenheizung nach KAT | 0x01 | 0x02 | 0x05 |
| 0x9B | Aussetzer abgasrelevant Summe | 0x01 | 0x02 | 0x04 |
| 0x9C | Aussetzer katschaedigend Zyl.1 | 0x01 | 0x02 | 0x04 |
| 0x9D | Aussetzer katschaedigend Zyl.2 | 0x01 | 0x02 | 0x04 |
| 0x9E | Aussetzer katschaedigend Zyl.3 | 0x01 | 0x02 | 0x04 |
| 0x9F | Aussetzer katschaedigend Zyl.4 | 0x01 | 0x02 | 0x04 |
| 0xA0 | Aussetzer katschaedigend Summe | 0x01 | 0x02 | 0x04 |
| 0xA5 | Katalysatorkonvertierung | 0x01 | 0x02 | 0x04 |
| 0xA6 | Periodendauer Lambdasonde vor Kat | 0x01 | 0x02 | 0x05 |
| 0xA9 | Heizleistung Sonde vor Kat    | 0x01 | 0x02 | 0x05 |
| 0xAA | Heizleistung Sonde nach Kat | 0x01 | 0x02 | 0x05 |
| 0xAB | Pruefung Kraftstoff-Versorgungssystem | 0x01 | 0x02 | 0x05 |
| 0xXY | Unbekannter Fehlerort | 0x00 | 0x00 | 0x00 |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 71 rows × 17 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 | A6_0 | A6_1 | A7_0 | A7_1 | A8_0 | A8_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x64 | 0x00 | 0x71 | 0x00 | 0x00 | 0x00 | 0x23 | 0x00 | 0x54 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x65 | 0x00 | 0x71 | 0x00 | 0x00 | 0x00 | 0x23 | 0x00 | 0x54 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x66 | 0x00 | 0x71 | 0x00 | 0x00 | 0x00 | 0x23 | 0x00 | 0x54 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x67 | 0x00 | 0x71 | 0x00 | 0x00 | 0x00 | 0x23 | 0x00 | 0x54 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x68 | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x69 | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x6A | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x6B | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x6C | 0x00 | 0x11 | 0x00 | 0x62 | 0x00 | 0x13 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x6D | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x14 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x6E | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x63 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x6F | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x70 | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x71 | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x72 | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x73 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x74 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x74 | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x14 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x75 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x74 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x76 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x74 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x77 | 0x00 | 0x31 | 0x00 | 0x12 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x78 | 0x00 | 0x11 | 0x00 | 0x72 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x79 | 0x00 | 0x31 | 0x00 | 0x12 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x7A | 0x00 | 0x31 | 0x00 | 0x12 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x7B | 0x00 | 0x31 | 0x00 | 0x12 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x7C | 0x00 | 0x41 | 0x00 | 0x32 | 0x00 | 0x13 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x7D | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x7E | 0x00 | 0xC1 | 0x00 | 0xD2 | 0x00 | 0xC3 | 0x00 | 0xC4 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x7F | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x14 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x80 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xD3 | 0x00 | 0xD4 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x81 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x14 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x82 | 0x00 | 0xD1 | 0x00 | 0xE2 | 0x00 | 0xE3 | 0x00 | 0xE4 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x83 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x13 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x84 | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x85 | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x86 | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x14 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x87 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x34 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x88 | 0x00 | 0x00 | 0x00 | 0x82 | 0x00 | 0x00 | 0x00 | 0x44 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x89 | 0x00 | 0x21 | 0x00 | 0x22 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x8A | 0x00 | 0x21 | 0x00 | 0x22 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x8B | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x8C | 0x00 | 0x14 | 0x00 | 0x92 | 0x00 | 0x00 | 0x00 | 0x44 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x8D | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x8E | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0xA4 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x8F | 0x00 | 0x61 | 0x00 | 0x42 | 0x00 | 0x43 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x90 | 0x00 | 0x00 | 0x00 | 0xA2 | 0x00 | 0x73 | 0x00 | 0x94 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x91 | 0x00 | 0x91 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x92 | 0x00 | 0x91 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x93 | 0x00 | 0x91 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x94 | 0x00 | 0x91 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x95 | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x96 | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x97 | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x14 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x98 | 0x00 | 0xB1 | 0x00 | 0xC2 | 0x00 | 0x83 | 0x00 | 0xB4 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x99 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x74 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x9A | 0x00 | 0xA1 | 0x00 | 0x52 | 0x00 | 0x53 | 0x00 | 0x00 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x9B | 0x00 | 0x91 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x14 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x9C | 0x00 | 0x91 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x14 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x9D | 0x00 | 0x91 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x14 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x9E | 0x00 | 0x91 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x14 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0x9F | 0x00 | 0x91 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x14 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0xA0 | 0x00 | 0x91 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x14 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0xA5 | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x14 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0xA6 | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x14 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0xA9 | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x14 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0xAA | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x14 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0xAB | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x14 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0xAC | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x14 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0xAD | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x14 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0xAE | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x14 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0xAF | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x13 | 0x00 | 0x14 | 0x00 | 0x15 | 0x00 | 0x16 | 0x07 | 0x17 | 0x00 | 0x18 |
| 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY |  0xXY | 0xXY |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 65 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | Kurzschluss gegen Ubatt oder Gemisch zu fett |
| 0x02 | Kurzschluss gegen Masse oder Gemisch zu mager |
| 0x03 | Unterbrechung oder kein Signal |
| 0x04 | Fettanschlag |
| 0x05 | Mageranschlag |
| 0x06 | EPROM Erase Fehler |
| 0x11 | Kurzschluss Ubatt |
| 0x21 | Signal zu gross |
| 0x31 | Kurzschluss gegen Ubatt oder Unterbrechung |
| 0x41 | Spannung groesser 16,8 V |
| 0x51 | Kurzschluss gegen Ubatt oder Uebertemperatur |
| 0x61 | Fehler bei Flashtest |
| 0x71 | Steuergeraeteausgang Zuendung defekt |
| 0x81 | Abtastfehler |
| 0x91 | Aussetzer |
| 0xA1 | unmoeglicher Resetfehler |
| 0xB1 | Programmierfehler |
| 0xC1 | zuviele ASC2-Botschaften |
| 0xD1 | zuviele INSTR2-Botschaften |
| 0x12 | Kurzschluss gegen Masse |
| 0x22 | Signal zu klein |
| 0x32 | Spannung kleiner 5.7 V |
| 0x42 | Fehler bei RAM-Test |
| 0x52 | Unerlaubter System-Reset |
| 0x62 | Kurzschluss gegen Masse oder Funktionsfehler Elektroluefter |
| 0x72 | Kurzschluss gegen Masse oder Unterbrechung |
| 0x82 | fehlt |
| 0x92 | kein Signal |
| 0xA2 | Startwertprogrammierung fehlt |
| 0xB2 | Fehler beim Loeschen |
| 0xC2 | Erase-Fehler: Bank 1 defekt |
| 0xD2 | Unterbrechung ASC2-Botschaft |
| 0xE2 | Unterbrechung INSTR2-Botschaft |
| 0x13 | Unterbrechung |
| 0x23 | Unterbrechung Primaerkreis |
| 0x33 | Unterbrechung oder Uebertemperatur |
| 0x43 | Unterbrechung QSPI |
| 0x53 | Watchdog-Reset |
| 0x63 | Unterbrechung oder Kurzschluss Masse |
| 0x73 | DME und EWS passen nicht zusammen |
| 0x83 | Erase-Fehler: Bank 2 defekt |
| 0xC3 | Unterbrechung ASC1-Botschaft |
| 0xD3 | Unterbrechung EGS1-Botschaft |
| 0xE3 | Unterbrechung INSTR3-Botschaft |
| 0x14 | unplausibel |
| 0x24 | Uebertemperatur |
| 0x34 | fehlt oder unplausibel |
| 0x44 | gestoert |
| 0x54 | Unterbrechung Sekundaerkreis |
| 0x64 | Erase-Fehler Eprom-Emulation |
| 0x74 | elektrischer Fehler |
| 0x84 | Uebertragung gestoert |
| 0x94 | Manipulation |
| 0xA4 | Klopfbaustein defekt |
| 0xB4 | CRC-Fehler |
| 0xC4 | zuviele ASC1-Botschaften |
| 0xD4 | zuviele EGS1-Botschaften |
| 0xE4 | zuviele INSTR3-Botschaften |
| 0x15 | Fehler steuert MIL an |
| 0x16 | Fehler in Filterung |
| 0x17 | Fehler momentan vorhanden |
| 0x07 | Fehler momentan nicht vorhanden |
| 0x18 | Fehler gilt als sporadisch |
| 0xXY | unbekannte Fehlerart |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 14 rows × 6 columns

| UWNR | UWTEXT | UW_EINH | UWF_A | UWF_B | UWF_C |
| --- | --- | --- | --- | --- | --- |
| 0x00 | NULL | -- | 1 | 0 | 1 |
| 0x01 | Motordrehzahl | 1/min | 40 | 0 | 1 |
| 0x02 | Kuehlmitteltemperatur | Grad C | 0.75 | 48 | 1 |
| 0x03 | Ansauglufttemperatur | Grad C | 0.75 | 48 | 1 |
| 0x04 | Wahre Regelgroesse Last | mg/AS/Z | 3 | 0 | 1 |
| 0x05 | Batteriespannung | V | 9.48 | 0 | 100 |
| 0x06 | Geschwindigkeit | km/h | 1 | 0 | 1 |
| 0x07 | Drosselpotispg | V | 1,960 | 0 | 100 |
| 0x08 | Lambdasondenspannung vor KAT | V | 1.25 | 0 | 256 |
| 0x09 | Reset-Status-Register | 1 | 1 | 0 | 1 |
| 0x0A | NULL | -- | 1 | 0 | 1 |
| 0x0B | Spannung an Klemme 15 | V | 9.48 | 0 | 100 |
| 0x0C | Lambdasondenspannung nach KAT | V | 5 | 0 | 256 |
| 0xXY | unbekannte Umweltbedingung | -- | 1 | 0 | 1 |

<a id="table-obd-bits"></a>
### OBD_BITS

Dimensions: 19 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| S_MIL | 0 | 0x80 | 0x80 |
| S_RDY_KOMP | 1 | 0x40 | 0x40 |
| S_RDY_KVS | 1 | 0x20 | 0x20 |
| S_RDY_AUS | 1 | 0x10 | 0x10 |
| S_UB_KOMP | 1 | 0x04 | 0x04 |
| S_UB_TANK | 1 | 0x02 | 0x02 |
| S_UB_VER_AUS | 1 | 0x01 | 0x01 |
| S_UBW_AGR | 2 | 0x80 | 0x80 |
| S_UB_LAMBDASHZ | 2 | 0x40 | 0x40 |
| S_UB_LAMBDAS | 2 | 0x20 | 0x20 |
| S_UBW_KLIMA | 2 | 0x10 | 0x10 |
| S_UB_SE_LU | 2 | 0x08 | 0x08 |
| S_UBW_TES | 2 | 0x04 | 0x04 |
| S_UBW_KATHEIZ | 2 | 0x02 | 0x02 |
| S_UB_KAT | 2 | 0x01 | 0x01 |
| S_LAMBDASHZ_UB | 3 | 0x40 | 0x40 |
| S_LAMBDAS_UB | 3 | 0x20 | 0x20 |
| S_SE_LU_DIA | 3 | 0x08 | 0x08 |
| S_KAT_DIA | 3 | 0x01 | 0x01 |

<a id="table-betriebswtab"></a>
### BETRIEBSWTAB

Dimensions: 1 rows × 17 columns

| NAME | TELEGRAM | POS_ADR | LEN_ADR | ADR | BYTE | DATA_TYPE | COMPU_TYPE | FACT_A | FACT_B | MASK | VALUE | ANZ | MEAS | RANGE | JOBNAME | LNAME |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| KM_MIL_AN | 12050BA3 | 0 | 0 | 0 | 7 | 5 | -- | 1 | 0 | 0 | 0 | 1.0 | km |   | STATUS_DIGITL_OBDII | Kilometerstand MIL an |

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 13 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0x11 | AIF_NICHT_PROGRAMMIERT |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xB2 | ERROR_ECU_NUMBER |
| 0xFF | ERROR_ECU_NACK |
| 0x01 | ERROR_ECU_KEINE_ANSTEUERUNG_BEI_DIESER_PIN_NUMMER |
| 0x02 | ERROR_ECU_KEINE_ANSTEUERUNG_DA_TASTVERHAELTNIS_UNGUELTIG |
| 0x03 | ERROR_ECU_KEINE_ANSTEUERUNG_DA_PERIODENDAUER_UNGUELTIG |
| 0x04 | ERROR_ECU_KEINE_ANSTEUERUNG_DA_ANSTEUERBEDINGUNG_NICHT_ERFUELLT |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |
