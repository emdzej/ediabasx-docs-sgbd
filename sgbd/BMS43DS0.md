# BMS43DS0.prg

- Jobs: [70](#jobs)
- Tables: [6](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | BMS 43 fuer M43 mit ASC |
| ORIGIN | BMW TP-421 Weber |
| REVISION | 1.10 |
| AUTHOR | BMW EE-30 Astalosch , BMW TP-421 Weber |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [ISN_LESEN](#job-isn-lesen)
- [RAM_LESEN](#job-ram-lesen) - Beliebige RAM - Zellen auslesen
- [ROM_LESEN](#job-rom-lesen) - Beliebige EPROM - Zellen auslesen
- [IDENT](#job-ident) - Ident-Daten fuer DME
- [ADAPT_LOESCHEN](#job-adapt-loeschen) - Adaptionen loeschen
- [EDIC_RESET](#job-edic-reset) - EDIC-Reset
- [initialisierung](#job-initialisierung) - Default Init-Job
- [INFO](#job-info) - Information SGBD
- [STATUS_CODIER_CHECKSUMME](#job-status-codier-checksumme) - Codier - Checksumme abfragen
- [ABGAS_VARIANTE_LESEN](#job-abgas-variante-lesen) - Auslesen der Abgasvariante
- [STATUS_MOTORDREHZAHL](#job-status-motordrehzahl) - Motordrehzahl auslesen
- [STATUS_MOTORTEMPERATUR](#job-status-motortemperatur) - Motortemperatur auslesen
- [STATUS_AN_LUFTTEMPERATUR](#job-status-an-lufttemperatur) - Ansauglufttemperatur auslesen
- [STATUS_LAST](#job-status-last) - Lastsignal auslesen
- [STATUS_UBATT](#job-status-ubatt) - Batteriespannung auslesen
- [STATUS_GESCHWINDIGKEIT](#job-status-geschwindigkeit) - Geschwindigkeit auslesen
- [STATUS_DKP_VOLT](#job-status-dkp-volt) - Drosselklappenwinkel auslesen
- [STATUS_LASTSIGNAL_RSLT4](#job-status-lastsignal-rslt4) - Lastsignal RSLT4 auslesen
- [STATUS_ZUENDWINKEL](#job-status-zuendwinkel) - Zuendwinkel auslesen
- [STATUS_INT](#job-status-int) - Lambdaregelfaktor auslesen
- [STATUS_TE_TASTVERHAELTNIS](#job-status-te-tastverhaeltnis) - TE Tastverhaeltnis auslesen
- [STATUS_EINSPRITZZEIT_P_U](#job-status-einspritzzeit-p-u) - Auslesen der Einspritzzeit pro Umdrehung
- [STATUS_LMM](#job-status-lmm) - Luftmenge lesen
- [STATUS_LEERLAUFINTEGRATOR](#job-status-leerlaufintegrator) - Auslesen des Leerlaufintegrators
- [STATUS_LL_LUFTBEDARF](#job-status-ll-luftbedarf) - LL Soll LM auslesen
- [STATUS_ADAP_LEERLAUFLUFT_U](#job-status-adap-leerlaufluft-u) - Adaption Leerlaufluft lesen
- [STATUS_MUL](#job-status-mul) - Adaption Gemisch multiplikativ auslesen
- [STATUS_ADD](#job-status-add) - Adaption Gemisch additiv auslesen
- [STATUS_L_SONDE](#job-status-l-sonde) - Lambdasondendifferenzspannung 1
- [STATUS_SOLLDREHZAHL_LLR](#job-status-solldrehzahl-llr) - Solldrehzahl Leerlaufregler auslesen
- [STATUS_ADAP_DKP_U](#job-status-adap-dkp-u) - Adaption Drosselklappenpotentiometer auslesen
- [STATUS_BSZ](#job-status-bsz) - Betriebsstundenzaehlers auslesen
- [STATUS_DIGITAL](#job-status-digital) - Status Schalteingaenge
- [STEUERN_EV_1](#job-steuern-ev-1) - EV 1 ansteuern
- [STEUERN_EV_2](#job-steuern-ev-2) - EV 2 ansteuern
- [STEUERN_EV_3](#job-steuern-ev-3) - EV 3 ansteuern
- [STEUERN_EV_4](#job-steuern-ev-4) - EV 4 ansteuern
- [STEUERN_EV_1_AUS](#job-steuern-ev-1-aus) - EV 1 ausschalten
- [STEUERN_EV_2_AUS](#job-steuern-ev-2-aus) - EV 2 ausschalten
- [STEUERN_EV_3_AUS](#job-steuern-ev-3-aus) - EV 3 ausschalten
- [STEUERN_EV_4_AUS](#job-steuern-ev-4-aus) - EV 4 ausschalten
- [STEUERN_DISA](#job-steuern-disa) - Differenziertere Saugrohranlage ansteuern
- [STEUERN_E_LUEFTER](#job-steuern-e-luefter) - Elektroluefter ansteuern
- [STEUERN_LSH](#job-steuern-lsh) - Lambdasondenheizungsrelais ansteuern
- [STEUERN_TEV](#job-steuern-tev) - Tankentlueftungsventil  ansteuern
- [STEUERN_KO](#job-steuern-ko) - Klimakompressor ansteuern
- [STEUERN_LL_STELLER](#job-steuern-ll-steller) - Einwegdrehsteller ansteuern
- [FS_QUICK_LESEN](#job-fs-quick-lesen) - Auslesen des QUICK Fehlerspeichers
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers
- [FS_SHADOW_LESEN](#job-fs-shadow-lesen) - Auslesen des Fehlerspeichers
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [DIAGNOSE_ERHALTEN](#job-diagnose-erhalten) - Erhalten der Diagnose
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Ende der Diagnose
- [SYSTEM_ADRESSEN_LESEN](#job-system-adressen-lesen) - Auslesen der System-Adressen
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender-Info-Feldes
- [DATENSATZNUMMER_LESEN](#job-datensatznummer-lesen) - Auslesen der Datensatznummer
- [MAX_BLOCK_LESEN](#job-max-block-lesen) - Auslesen der maximalen Blocklaenge
- [UPROG_EIN](#job-uprog-ein) - Programmierspannung einschalten
- [UPROG_AUS](#job-uprog-aus) - Programmierspannung ausschalten
- [CO_ABGLEICH_LESEN](#job-co-abgleich-lesen) - CO-Abgleich lesen
- [CO_ABGLEICH_VERSTELLEN](#job-co-abgleich-verstellen) - CO-Abgleich lesen
- [CO_ABGLEICH_PROGRAMMIEREN](#job-co-abgleich-programmieren) - CO-Abgleich programmieren
- [ADAP_SELEKTIV_ZURUECK](#job-adap-selektiv-zurueck) - Adaptionen loeschen
- [STATUS_LMM_MASSE](#job-status-lmm-masse) - Luftmenge lesen
- [STATUS_EINSPRITZZEIT](#job-status-einspritzzeit) - Auslesen der Einspritzzeit pro Umdrehung
- [STATUS_LS_VKAT_SIGNAL_1](#job-status-ls-vkat-signal-1) - Lambdasondendifferenzspannung 1
- [STATUS_LAMBDA_INTEGRATOR_1](#job-status-lambda-integrator-1) - Lambdaregelfaktor auslesen
- [STATUS_LAMBDA_ADD_1](#job-status-lambda-add-1) - Adaption Gemisch additiv auslesen
- [STATUS_LAMBDA_MUL_1](#job-status-lambda-mul-1) - Adaption Gemisch multiplikativ auslesen
- [ECU_CONFIG](#job-ecu-config) - Ident-Daten fuer DME

<a id="job-isn-lesen"></a>
### ISN_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ISN_LESEN_WERT | string | ISN als  WERT |
| JOB_STATUS | string |  |

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
| ID_MOTOR | string | SG - Identifikation fuer MoTest |
| ID_LAMBDA_STEREO | int | Parameter fuer MoTest 0=Mono, 1=STEREO |
| ID_EML | int | Parameter fuer MoTest 0=Kein EML verb, 1=EML M70, 2=EML M73 |
| ID_LU_MESSUNG | int | Parameter fuer MoTest 1=Laufunruhemessung sonst 0 |
| ID_OBD2 | int | Parameter fuer MoTest 0=ECE, 1=OBD2-Fahrzeug |
| ID_SG_HERSTELLER | int | Parameter fuer MoTest 0=Bosch, 1=Siemens-Fahrzeug |
| ID_EWS_SS | int | Identifikation EWS-Schnittstelle |

<a id="job-adapt-loeschen"></a>
### ADAPT_LOESCHEN

Adaptionen loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-edic-reset"></a>
### EDIC_RESET

EDIC-Reset

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

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

<a id="job-status-codier-checksumme"></a>
### STATUS_CODIER_CHECKSUMME

Codier - Checksumme abfragen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_CHECKSUMME_WERT | int | Ergebnis |

<a id="job-abgas-variante-lesen"></a>
### ABGAS_VARIANTE_LESEN

Auslesen der Abgasvariante

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| ABGAS_VARIANTE_WERT | int | Abgasvariante 0=KAT-V , 1= KAT |

<a id="job-status-motordrehzahl"></a>
### STATUS_MOTORDREHZAHL

Motordrehzahl auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_MOTORDREHZAHL_WERT | long | Ergebnis Motordrehzahl |
| STAT_MOTORDREHZAHL_WERT | long | Ergebnis Motordrehzahl |
| STATUS_MOTORDREHZAHL_EINH | string | Einheit Motordrehzahl |

<a id="job-status-motortemperatur"></a>
### STATUS_MOTORTEMPERATUR

Motortemperatur auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_MOTORTEMPERATUR_WERT | real | Ergebnis Motortemperatur |
| STAT_MOTORTEMPERATUR_WERT | real | Ergebnis Motortemperatur |
| STATUS_MOTORTEMPERATUR_EINH | string | Einheit Motortemperatur |

<a id="job-status-an-lufttemperatur"></a>
### STATUS_AN_LUFTTEMPERATUR

Ansauglufttemperatur auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_AN_LUFTTEMPERATUR_WERT | real | Ergebnis Ansauglufttemperatur |
| STAT_AN_LUFTTEMPERATUR_WERT | real | Ergebnis Ansauglufttemperatur |
| STATUS_AN_LUFTTEMPERATUR_EINH | string | Einheit Ansauglufttemperatur |

<a id="job-status-last"></a>
### STATUS_LAST

Lastsignal auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_LAST_WERT | real | Ergebnis Lastsignal TL |
| STAT_LAST_WERT | real | Ergebnis Lastsignal TL |
| STATUS_LAST_EINH | string | Einheit Lastsignal TL |

<a id="job-status-ubatt"></a>
### STATUS_UBATT

Batteriespannung auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_UBATT_WERT | real | Ergebnis Batteriespannungr |
| STAT_UBATT_WERT | real | Ergebnis Batteriespannungr |
| STATUS_UBATT_EINH | string | Einheit Batteriespannung |

<a id="job-status-geschwindigkeit"></a>
### STATUS_GESCHWINDIGKEIT

Geschwindigkeit auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_GESCHWINDIGKEIT_WERT | real | Ergebnis Geschwindigkeit |
| STATUS_GESCHWINDIGKEIT_EINH | string | Einheit Geschwindigkeit |

<a id="job-status-dkp-volt"></a>
### STATUS_DKP_VOLT

Drosselklappenwinkel auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_DKP_VOLT_WERT | real | Ergebnis Drosselklappenwinkel |
| STATUS_DKP_VOLT_EINH | string | Einheit DKWinkel |

<a id="job-status-lastsignal-rslt4"></a>
### STATUS_LASTSIGNAL_RSLT4

Lastsignal RSLT4 auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_LASTSIGNAL_RSLT4_WERT | real | Ergebnis Lastsignal RSLT4 |
| STATUS_LASTSIGNAL_RSLT4_EINH | string | Einheit Lastsignal |

<a id="job-status-zuendwinkel"></a>
### STATUS_ZUENDWINKEL

Zuendwinkel auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_ZUENDWINKEL_WERT | real | Ergebnis Zuendwinkel |
| STAT_ZUENDWINKEL_WERT | real | Ergebnis Zuendwinkel |
| STATUS_ZUENDWINKEL_EINH | string | Einheit Zuendwinkel |

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

<a id="job-status-te-tastverhaeltnis"></a>
### STATUS_TE_TASTVERHAELTNIS

TE Tastverhaeltnis auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_TE_TASTVERHAELTNIS_WERT | long | Ergebnis TE Tastverhaeltnis |
| STATUS_TE_TASTVERHAELTNIS_EINH | string | Einheit TE_Tastverhaeltnis |

<a id="job-status-einspritzzeit-p-u"></a>
### STATUS_EINSPRITZZEIT_P_U

Auslesen der Einspritzzeit pro Umdrehung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_EINSPRITZZEIT_P_U_WERT | real | Ergebnis Einspritzzeit |
| STATUS_EINSPRITZZEIT_P_U_EINH | string | Einheit Einspritzzeit |

<a id="job-status-lmm"></a>
### STATUS_LMM

Luftmenge lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_LMM_WERT | real | Ergebnis Luftmenge |
| STATUS_LMM_EINH | string | Einheit Luftmenge |

<a id="job-status-leerlaufintegrator"></a>
### STATUS_LEERLAUFINTEGRATOR

Auslesen des Leerlaufintegrators

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_LEERLAUFINTEGRATOR_WERT | long | Ergebnis Leerlaufintegrator |
| STATUS_LEERLAUFINTEGRATOR_EINH | string | Einheit Leerlaufintegrator |

<a id="job-status-ll-luftbedarf"></a>
### STATUS_LL_LUFTBEDARF

LL Soll LM auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_LL_LUFTBEDARF_WERT | long | Ergebnis LL Soll LM auslesen |
| STATUS_LL_LUFTBEDARF_EINH | string | Einheit LL Soll LM |

<a id="job-status-adap-leerlaufluft-u"></a>
### STATUS_ADAP_LEERLAUFLUFT_U

Adaption Leerlaufluft lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_ADAP_LEERLAUFLUFT_WERT | real | Ergebnis Ergebnis Adaption Leerlaufluft |
| STATUS_ADAP_LEERLAUFLUFT_EINH | string | Einheit Adaption Leerlaufluft |

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

<a id="job-status-l-sonde"></a>
### STATUS_L_SONDE

Lambdasondendifferenzspannung 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_L_SONDE_WERT | real |  |
| STATUS_L_SONDE_EINH | string | Einheit V |

<a id="job-status-solldrehzahl-llr"></a>
### STATUS_SOLLDREHZAHL_LLR

Solldrehzahl Leerlaufregler auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_SOLLDREHZAHL_LLR_WERT | real | Ergebnis Solldrehzahl |
| STATUS_SOLLDREHZAHL_LLR_EINH | string | Einheit Solldrehzahl |

<a id="job-status-adap-dkp-u"></a>
### STATUS_ADAP_DKP_U

Adaption Drosselklappenpotentiometer auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_ADAP_DKP_WERT | real | Ergebnis Adaption DKP |
| STATUS_ADAP_DKP_EINH | string | Einheit Adaption DKP |

<a id="job-status-bsz"></a>
### STATUS_BSZ

Betriebsstundenzaehlers auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_BSZ_WERT | real | Ergebnis Batteriespannungr |
| STATUS_BSZ_EINH | string | Einheit Batteriespannung |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

Status Schalteingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_KL15_EIN | int | Status Klemme 15, 0=Aus / 1=Ein |
| STATUS_AC_EIN | int | Eingang Klimaanforderung, 0=Aus / 1=Ein |
| STAT_AC_EIN | int | Eingang Klimaanforderung, 0=Aus / 1=Ein |
| STATUS_KO_EIN | int | Eingang Klimaanlage, 0=Aus / 1=Ein |
| STAT_KO_EIN | int | Eingang Klimaanlage, 0=Aus / 1=Ein |
| STATUS_EL_EIN | int | Eingang Elektroluefter, 0=Aus / 1=Ein |
| STATUS_EWS_OK_EIN | int | EWS erkannt OK, 0=NOK / 1=OK |
| STATUS_FS_EIN | int | Fahrstufe erkannt ueber CAN, 0=Nein / 1=Ja |
| STATUS_GE_EIN | int | Getriebeeingriff 0=Nein / 1=Ja |
| STATUS_ED_FSP_FEHLERZAEHLER_EIN | int | Fehlerlampe 0=Aus / 1=Ein |
| STATUS_START_AKTIV_EIN | int | Start 0=Nein / 1=Ja |
| STATUS_LL_EIN | int | Leerlauf 0=Nein / 1=Ja |
| STATUS_TL_EIN | int | Teillast 0=Nein / 1=Ja |
| STATUS_VL_EIN | int | Vollast 0=Nein / 1=Ja |
| STATUS_BESCHLANR_AKTIV_EIN | int | Beschleunigungsanreicherung 0=Aus / 1=Ein |
| STATUS_SCHUBAB_AKTIV_EIN | int | Status Schubabschaltung 0=Aus / 1=Ein |
| STATUS_TEV_AKTIV_EIN | int | Status Tankentlueftungsventil 0=Aus / 1=Ein |
| STATUS_LAMBDA_AKTIV_EIN | int | Status Lambdaregelung 0=Aus / 1=Ein |
| STATUS_ASC_KNOWN_EIN | int | ASC erkannt 0=Nein / 1=Ja |
| STATUS_EGS_KNOWN_EIN | int | EGS erkannt 0=Nein / 1=Ja |
| STATUS_KAT_EIN | int | Katalysator vorhanden 0=Nein / 1=Ja |
| STATUS_B_KKO_VERB | int | Klimaanlage verbaut 0=Nein / 1=Ja |
| STATUS_PORT_C_BIT_6 | int | Klimaanlage angesteuert 0=Aus / 1=Ein |
| STATUS_PORT_C_BIT_5 | int | Elektroluefter angesteuert 0=Aus / 1=Ein |
| STATUS_KR_EIN | int | Status Klopfregelung 0=Aus / 1=Ein |
| STATUS_PORT_ADB_BIT_0 | int | Status EKP softwaremaessig angesteuert 0=Aus / 1=Ein |
| STATUS_PORT_ADB_BIT_3 | int | Status DISA auf langem Saugrohr 0=Aus / 1=Ein |

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

Differenziertere Saugrohranlage ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-e-luefter"></a>
### STEUERN_E_LUEFTER

Elektroluefter ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-lsh"></a>
### STEUERN_LSH

Lambdasondenheizungsrelais ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-tev"></a>
### STEUERN_TEV

Tankentlueftungsventil  ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ko"></a>
### STEUERN_KO

Klimakompressor ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ll-steller"></a>
### STEUERN_LL_STELLER

Einwegdrehsteller ansteuern

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
| F_LOGISTIK | int | Fehlerlogistikzaehler |
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

<a id="job-fs-shadow-lesen"></a>
### FS_SHADOW_LESEN

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
| F_LOGISTIK | int | Fehlerlogistikzaehler |
| F_LZ | int | Fehlerlogistikzaehler |
| F_ART_ANZ | int | Anzahl der Fehlerarten des SG |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen des einzelnen Fehlers |
| F_ART1_AKT_NR | int | Fehlerart 1 Index (Aktuell) |
| F_ART1_AKT_TEXT | string | Fehlerart 1 Text (Aktuell) |
| F_ART2_AKT_NR | int | Fehlerart 2 Index (Aktuell) |
| F_ART2_AKT_TEXT | string | Fehlerart 2 Text (Aktuell) |
| F_ART3_AKT_NR | int | Fehlerart 3 Index (Aktuell) |
| F_ART3_AKT_TEXT | string | Fehlerart 3 Text (Aktuell) |
| F_ART4_AKT_NR | int | Fehlerart 4 Index (Aktuell) |
| F_ART4_AKT_TEXT | string | Fehlerart 4 Text (Aktuell) |
| F_ART5_AKT_NR | int | Fehlerart 5 Index (Aktuell) |
| F_ART5_AKT_TEXT | string | Fehlerart 5 Text (Aktuell) |
| F_ART6_AKT_NR | int | Fehlerart 6 Index (Aktuell) |
| F_ART6_AKT_TEXT | string | Fehlerart 6 Text (Aktuell) |
| F_ART7_AKT_NR | int | Fehlerart 7 Index (Aktuell) |
| F_ART7_AKT_TEXT | string | Fehlerart 7 Text (Aktuell) |
| F_ART8_AKT_NR | int | Fehlerart 8 Index (Aktuell) |
| F_ART8_AKT_TEXT | string | Fehlerart 8  Text (Aktuell) |
| F_ART_AKT | string | Fehlerart (Aktuell) |
| F_ART1_E_NR | int | Fehlerart 1 Index (Entprellt) |
| F_ART1_E_TEXT | string | Fehlerart 1 Text (Entprellt) |
| F_ART2_E_NR | int | Fehlerart 2 Index (Entprellt) |
| F_ART2_E_TEXT | string | Fehlerart 2 Text (Entprellt) |
| F_ART3_E_NR | int | Fehlerart 3 Index (Entprellt) |
| F_ART3_E_TEXT | string | Fehlerart 3 Text (Entprellt) |
| F_ART4_E_NR | int | Fehlerart 4 Index (Entprellt) |
| F_ART4_E_TEXT | string | Fehlerart 4 Text (Entprellt) |
| F_ART5_E_NR | int | Fehlerart 5 Index (Entprellt) |
| F_ART5_E_TEXT | string | Fehlerart 5 Text (Entprellt) |
| F_ART6_E_NR | int | Fehlerart 6 Index (Entprellt) |
| F_ART6_E_TEXT | string | Fehlerart 6 Text (Entprellt) |
| F_ART7_E_NR | int | Fehlerart 7 Index (Entprellt) |
| F_ART7_E_TEXT | string | Fehlerart 7 Text (Entprellt) |
| F_ART8_E_NR | int | Fehlerart 8 Index (Entprellt) |
| F_ART8_E_TEXT | string | Fehlerart 8 Text (Entprellt) |
| F_ART_ENT | string | Fehlerart (Entprellt) |
| F_FILTER_Z | int | Fehlerfilterzaehler |
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
| F_UW1_2_NR | int | Satz 2 Umweltbedingung 1 Index |
| F_UW1_2_TEXT | string | Satz 2 Umweltbedingung 1 Einheit |
| F_UW1_2_EINH | string | Satz 2 Umweltbedingung 1 Text |
| F_UW1_2_WERT | real | Satz 2 Umweltbedingung 1 Wert |
| F_UW2_2_NR | int | Satz 2 Umweltbedingung 2 Index |
| F_UW2_2_TEXT | string | Satz 2 Umweltbedingung 2 Text |
| F_UW2_2_EINH | string | Satz 2 Umweltbedingung 2 Einheit |
| F_UW2_2_WERT | real | Satz 2 Umweltbedingung 2 Wert |
| F_UW3_2_NR | int | Satz 2 Umweltbedingung 3 Index |
| F_UW3_2_TEXT | string | Satz 2 Umweltbedingung 3 Text |
| F_UW3_2_EINH | string | Satz 2 Umweltbedingung 3 Einheit |
| F_UW3_2_WERT | real | Satz 2 Umweltbedingung 3 Wert |
| F_UW1_3_NR | int | Satz 3 Umweltbedingung 1 Index |
| F_UW1_3_TEXT | string | Satz 3 Umweltbedingung 1 Einheit |
| F_UW1_3_EINH | string | Satz 3 Umweltbedingung 1 Text |
| F_UW1_3_WERT | real | Satz 3 Umweltbedingung 1 Wert |
| F_UW2_3_NR | int | Satz 3 Umweltbedingung 2 Index |
| F_UW2_3_TEXT | string | Satz 3 Umweltbedingung 2 Text |
| F_UW2_3_EINH | string | Satz 3 Umweltbedingung 2 Einheit |
| F_UW2_3_WERT | real | Satz 3 Umweltbedingung 2 Wert |
| F_UW3_3_NR | int | Satz 3 Umweltbedingung 3 Index |
| F_UW3_3_TEXT | string | Satz 3 Umweltbedingung 3 Text |
| F_UW3_3_EINH | string | Satz 3 Umweltbedingung 3 Einheit |
| F_UW3_3_WERT | real | Satz 3 Umweltbedingung 3 Wert |
| F_UW4_NR | int | Satz 1 Umweltbedingung 4 Index |
| F_UW4_TEXT | string | Satz 1 Umweltbedingung 4 Text |
| F_UW4_EINH | string | Satz 1 Umweltbedingung 4 Einheit |
| F_UW4_WERT | real | Satz  1 Umweltbedingung 4  Wert |
| F_UW4_2_NR | int | Satz 2 Umweltbedingung 4 Index |
| F_UW4_2_TEXT | string | Satz 2 Umweltbedingung 4 Text |
| F_UW4_2_EINH | string | Satz 2 Umweltbedingung 4 Einheit |
| F_UW4_2_WERT | real | Satz 2 Umweltbedingung 4  Wert |
| F_UW4_3_NR | int | Satz 3 Umweltbedingung 4 Index |
| F_UW4_3_TEXT | string | Satz 3 Umweltbedingung 4 Text |
| F_UW4_3_EINH | string | Satz 3 Umweltbedingung 4 EINH |
| F_UW4_3_WERT | real | Satz 3 Umweltbedingung 4  Wert |
| F_HEX | binary | Hex-Dump |

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
| AIF_ANZAHL_PROG | int | Anzahl Programmiervorgaenge |

<a id="job-datensatznummer-lesen"></a>
### DATENSATZNUMMER_LESEN

Auslesen der Datensatznummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| DS_NR | string | Datensatznummer |

<a id="job-max-block-lesen"></a>
### MAX_BLOCK_LESEN

Auslesen der maximalen Blocklaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| MAX_BLOCK_WERT | int | Blocklaenge in Byte |

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

CO-Abgleich lesen

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
| STATUS_CO_PROGRAMMIEREN_WERT | int | Aktuellen Abgleichwert |

<a id="job-adap-selektiv-zurueck"></a>
### ADAP_SELEKTIV_ZURUECK

Adaptionen loeschen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHLBYTE | long | Auswahlbyte fuer das Selektieren |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-status-lmm-masse"></a>
### STATUS_LMM_MASSE

Luftmenge lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_LMM_MASSE_WERT | real | Ergebnis Luftmenge |
| STAT_LMM_MASSE_EINH | string | Einheit Luftmenge |

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

<a id="job-status-ls-vkat-signal-1"></a>
### STATUS_LS_VKAT_SIGNAL_1

Lambdasondendifferenzspannung 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_LS_VKAT_SIGNAL_1_WERT | real |  |
| STAT_LS_VKAT_SIGNAL_1_EINH | string | Einheit V |

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

<a id="job-ecu-config"></a>
### ECU_CONFIG

Ident-Daten fuer DME

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| EGS_VORHANDEN | int | EGS vorhanden 1=ja ,  0=nein , 0xff=nicht unterstuetzt |

## Tables

### Index

- [BITS](#table-bits) (25 × 4)
- [FORTTEXTE](#table-forttexte) (40 × 5)
- [FARTMATRIX](#table-fartmatrix) (38 × 17)
- [FARTTEXTE](#table-farttexte) (10 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (11 × 6)
- [JOBRESULT](#table-jobresult) (8 × 2)

<a id="table-bits"></a>
### BITS

Dimensions: 25 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| STATUS_Kl15 | 0 | 0x01 | 0x01 |
| STATUS_AC_R | 0 | 0x02 | 0x02 |
| STATUS_KO_R | 0 | 0x04 | 0x04 |
| STATUS_EL_R | 0 | 0x08 | 0x08 |
| STATUS_EWS | 0 | 0x10 | 0x10 |
| STATUS_FS | 0 | 0x20 | 0x20 |
| STATUS_GE | 0 | 0x40 | 0x40 |
| STATUS_FSP | 0 | 0x80 | 0x80 |
| STATUS_S | 1 | 0x01 | 0x01 |
| STATUS_LL | 1 | 0x02 | 0x02 |
| STATUS_TL | 1 | 0x04 | 0x04 |
| STATUS_VL | 1 | 0x08 | 0x08 |
| STATUS_BESCH | 1 | 0x10 | 0x10 |
| STATUS_SCHUB | 1 | 0x20 | 0x20 |
| STATUS_TEV | 1 | 0x40 | 0x40 |
| STATUS_LAM | 1 | 0x80 | 0x80 |
| STATUS_ASC_D | 2 | 0x01 | 0x01 |
| STATUS_EGS_D | 2 | 0x02 | 0x02 |
| STATUS_KAT | 2 | 0x04 | 0x04 |
| STATUS_B_KKO | 2 | 0x08 | 0x08 |
| STATUS_AC | 2 | 0x10 | 0x10 |
| STATUS_EL | 2 | 0x20 | 0x20 |
| STATUS_B_KR | 2 | 0x40 | 0x40 |
| STATUS_EKP | 2 | 0x80 | 0x80 |
| STATUS_DISA | 3 | 0x01 | 0x01 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 40 rows × 5 columns

| ORT | ORTTEXT | UW_1 | UW_2 | UW_3 |
| --- | --- | --- | --- | --- |
| 0x00 | -- | 0x00 | 0x00 | 0x00 |
| 0x01 | Relais elektrische Kraftstoffpumpe | 0x01 | 0x02 | 0x05 |
| 0x02 | Lerrlaufsteller Schliesser | 0x02 | 0x04 | 0x05 |
| 0x03 | Einspritzventil Zylinder 2 | 0x01 | 0x04 | 0x05 |
| 0x04 | Einspritzventil Zylinder 4 | 0x01 | 0x04 | 0x05 |
| 0x0C | Drosselklappenpotentiometer | 0x01 | 0x02 | 0x04 |
| 0x0F | Klopfsensor 1 | 0x01 | 0x02 | 0x04 |
| 0x12 | Differenzierte Saugrohranlage | 0x01 | 0x02 | 0x05 |
| 0x18 | Zuendspule Zylinder 3 | 0x01 | 0x04 | 0x05 |
| 0x19 | Zuendspule Zylinder 1 | 0x01 | 0x04 | 0x05 |
| 0x1D | Leerlaufsteller Oeffner | 0x02 | 0x04 | 0x05 |
| 0x1F | Einspritzventil Zylinder 3 | 0x01 | 0x04 | 0x05 |
| 0x20 | Einspritzventil Zylinder 1 | 0x01 | 0x04 | 0x05 |
| 0x24 | Tankentlueftungsventil | 0x01 | 0x03 | 0x05 |
| 0x25 | Lambdasondenheizung | 0x01 | 0x02 | 0x05 |
| 0x29 | Luftmengenmesser | 0x01 | 0x02 | 0x07 |
| 0x2A | Klopfsensor 2 | 0x01 | 0x02 | 0x04 |
| 0x2C | Nockenwellen-Geber | 0x01 | 0x02 | 0x04 |
| 0x2E | Elektr. Luefter | 0x01 | 0x02 | 0x05 |
| 0x30 | Relais Klimakompressor | 0x01 | 0x02 | 0x04 |
| 0x33 | Zuendspule Zylinder 4 | 0x01 | 0x04 | 0x05 |
| 0x34 | Zuendspule Zylinder 2 | 0x01 | 0x04 | 0x05 |
| 0x36 | Batteriespannung | 0x01 | 0x02 | 0x05 |
| 0x43 | Kurbelwellen-Geber | 0x02 | 0x03 | 0x05 |
| 0x46 | Lambdasonde | 0x01 | 0x02 | 0x08 |
| 0x49 | Geschwindigkeits-Signal | 0x01 | 0x04 | 0x06 |
| 0x4C | CO-Potentiometer | 0x01 | 0x02 | 0x05 |
| 0x4D | Ansauglufttemperatur | 0x01 | 0x04 | 0x05 |
| 0x4E | Motortemperatur | 0x01 | 0x03 | 0x05 |
| 0x51 | Diebstahlwarnanlage-PIN | 0x01 | 0x02 | 0x05 |
| 0x52 | Schalter-Klimaanlage | 0x01 | 0x04 | 0x05 |
| 0x53 | Schalter Aircondition | 0x01 | 0x04 | 0x05 |
| 0xC8 | Steuergeraete Selbstest | 0x02 | 0x05 | 0x09 |
| 0xC9 | Lambdareglergrenze | 0x01 | 0x04 | 0x05 |
| 0xCE | Klopfregelung | 0x01 | 0x02 | 0x04 |
| 0xD8 | CAN-ASC-Signal | 0x01 | 0x02 | 0x05 |
| 0xEC | CAN-EGS-Signal | 0x01 | 0x02 | 0x05 |
| 0x40 | CAN Funktion EGS | 0x01 | 0x02 | 0x05 |
| 0xDC | EWS-Funktion | 0x01 | 0x02 | 0x05 |
| 0xXY | unbekannter Fehlerort | 0x00 | 0x00 | 0x00 |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 38 rows × 17 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 | A6_0 | A6_1 | A7_0 | A7_1 | A8_0 | A8_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x02 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x03 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x04 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x0C | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x0F | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x12 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x18 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x19 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x1D | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x1F | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x20 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x24 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x25 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x29 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x2A | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x2C | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x2E | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x30 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x33 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x34 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x36 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x43 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x46 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x49 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x4D | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x4E | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x51 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x52 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0xC8 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0xC9 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0xCE | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0xD8 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x4C | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0xEC | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0x40 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0xDC | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 |
| 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 10 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | Kurzschluss gegen U-Batt |
| 0x02 | Kurzschluss gegen Masse |
| 0x03 | Leitungsunterbrechung |
| 0x04 | unplausibler Wert |
| 0x05 | SG-spezifische Bedeutung |
| 0x06 | SG-spezifische Bedeutung |
| 0x07 | Fehler momentan vorhanden |
| 0x08 | sporadischer Fehler |
| 0xXY | -- |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 11 rows × 6 columns

| UWNR | UWTEXT | UW_EINH | UWF_A | UWF_B | UWF_C |
| --- | --- | --- | --- | --- | --- |
| 0x00 | ----   | ---- |  |  |  |
| 0x01 | Motordrehzahl | 1/min | 40 | 0 | 1 |
| 0x02 | Motortemperatur | Grad C | 0.75 | 48 | 1 |
| 0x03 | Ansauglufttemperatur | Grad C | 0.75 | 48 | 1 |
| 0x04 | Last | ms | 64 | 0 | 1000 |
| 0x05 | Batteriespannung | V | 0.1 | 0 | 1 |
| 0x06 | Geschwindigkeit | km/h | 1 | 0 | 1 |
| 0x07 | Drosselklappenwinkel | % | 100 | 0 | 256 |
| 0x08 | Lambdasondenspannung | V | 1.25 | 0 | 256 |
| 0x09 | Reset-Status-Register | 1 | 1 | 0 | 1 |
| 0xXY | unbekannte Umweltbedingung | -- |  |  |  |

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
