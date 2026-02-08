# hcp_72.prg

- Jobs: [113](#jobs)
- Tables: [107](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Hybrid Control Processor (HCP) |
| ORIGIN | BMW EA-412 Andreas_Glotz |
| REVISION | 7.002 |
| AUTHOR | Micronova_AG EA-412 Martin_Flach, Hays_AG EA-412 Tilo_Grune, ES |
| COMMENT | Erst ab EDIABAS-Version 7.1 benutzbar, da zu viele STRING-Variable im Job FSP_Detail_Lesen |
| PACKAGE | 1.15 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen (alle Fehler / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $02 ReadDTCByStatusMask UDS  : $0C StatusMask (Bit2, Bit3) Modus: Default
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen UDS  : $14 ClearDiagnosticInformation UDS  : $FF DTCHighByte UDS  : $FF DTCMiddleByte UDS  : $FF DTCLowByte Modus: Default
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels UDS  : $22   ReadDataByIdentifier UDS  : $1000 TestStamp Modus: Default
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. UDS  : $2E   WriteDataByIdentifier UDS  : $1000 TestStamp Modus: Default
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode des SG aufrecht erhalten UDS  : $3E TesterPresent UDS  : $?0 suppressPosRspMsgIndication Modus: Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen UDS  : $10 StartDiagnosticSession Modus: einstellbar mit diesem Job
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Harter Reset des Steuergeraets UDS  : $11 EcuReset UDS  : $01 HardReset Modus: Default
- [FS_LESEN_DETAIL](#job-fs-lesen-detail) - Fehlerspeicher lesen(einzelner Fehler / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $06 reportDTCExtendedDataRecordByDTCNumber Modus: Default
- [IDENT](#job-ident) - Identdaten auslesen UDS  : $22   ReadDataByIdentifier UDS  : $3F51 Sub-Parameter SGBD-Index UDS  : $3F3C Sub-Parameter SGBD-Index UDS  : $3F36 Sub-Parameter SGBD-Index UDS  : $3F38 Sub-Parameter SGBD-Index UDS  : $3F3A Sub-Parameter SGBD-Index UDS  : $3F30 Sub-Parameter SGBD-Index Modus: Default
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender Informations Feldes Standard Flashjob Modus: Default
- [DATEN_REFERENZ_LESEN](#job-daten-referenz-lesen) - Auslesen der Daten Referenz KWP2000: $22   ReadDataByCommonIdentifier $2504 DREF Modus  : Default
- [ZIF_LESEN](#job-zif-lesen) - Auslesen des Zulieferinfofeldes KWP2000: $22   ReadDataByCommonIdentifier $2503 ProgrammReferenz und KWP2000: $1A   ReadECUIdentification $91   VehicleManufacturerECUHardware*Number oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus: Default
- [SERIENNUMMER_LESEN](#job-seriennummer-lesen) - Seriennummer des Steuergeraets UDS  : $22   ReadDataByIdentifier UDS  : $F18C Sub-Parameter ECUSerialNumber Modus: Default
- [STATUS_ABSCHALTVERHINDERER](#job-status-abschaltverhinderer) - Lese den aktuellen Aussschaltverhinderer $22     SID ReadDataByIdentifier $02 $00 DID Messwert Modus: Default
- [STATUS_MOMENTENAUFTEILUNG_BESCHLEUNIGEN](#job-status-momentenaufteilung-beschleunigen) - Anteil des verbrennungsmotorischen Momentes am gesamten Antriebsmoment $22     SID ReadDataByIdentifier $02 $01 DID Messwert Modus: Default
- [STATUS_AKTIVIERUNG_LADEN_HV_BATTERIE](#job-status-aktivierung-laden-hv-batterie) - Status des Ladevorgangs $22   SID ReadDataByIdentifier $02 $02 DID Messwert Modus: Default
- [STATUS_APM_JUMPASSIST](#job-status-apm-jumpassist) - Zustände des Jump Assist $22     SID ReadDataByIdentifier $02 $03 DID Messwert Modus: Default
- [STATUS_EKK_ABSCHALTBEDINGUNG](#job-status-ekk-abschaltbedingung) - Grund fuer die Abschaltung des Klimakompressors $22     SID ReadDataByIdentifier $02 $07 DID Messwert Modus: Default
- [STATUS_EKK_LEISTUNGSLIMITIERUNG_BOOST](#job-status-ekk-leistungslimitierung-boost) - Leistungslimitierung als Grund fuer die Abschaltung des Klimakompressor $22     SID ReadDataByIdentifier $02 $08 DID Messwert Modus: Default
- [STATUS_EKK_LEISTUNGSLIMITIERUNG_REVGRADE](#job-status-ekk-leistungslimitierung-revgrade) - Rueckwaertssteigfaehigkeit als Grund fuer die Abschaltung des Klimakompressor $22     SID ReadDataByIdentifier $02 $09 DID Messwert Modus: Default
- [STATUS_MOMENTENAUFTEILUNG_BREMSEN](#job-status-momentenaufteilung-bremsen) - TO-Anteil der Mechanischen Bremse Reku-Anteil wäre der Kehrwert $22     SID ReadDataByIdentifier $02 $05 DID Messwert Modus: Default
- [STATUS_EMPI](#job-status-empi) - EMPI HV Stromwert, EMPI Mode, Drehzahl absolut/relativ $22     SID ReadDataByIdentifier $02 $0A DID HV Stromwert $02 $0B DID EMPI Mode Modus: Default
- [STATUS_HCP_ANTRIEBSART](#job-status-hcp-antriebsart) - Rückmeldung der aktuell anliegenden Antriebsart z.B.: E-Fahren, Rekuperation, Boost etc. $22     SID ReadDataByIdentifier $02 $13 DID Messwert Modus: Default
- [STATUS_HPMR_STATE](#job-status-hpmr-state) - Status des HPMR auslesen $22 SID ReadDataByIdentifier $02 $13 DID Messwert Modus: Default
- [STATUS_RECUPERATIONSMOMENT](#job-status-recuperationsmoment) - Ist-Wert Reku-Moment $22     SID ReadDataByIdentifier $02 $21 DID Messwert Ist-Wert zusätzliches Schubmoment $22     SID ReadDataByIdentifier $02 $0C DID Messwert Modus: Default
- [STATUS_WAKE_UP](#job-status-wake-up) - Gibt den Status der WakeUp-Leitung aus $22     SID ReadDataByIdentifier $02 $12 DID Messwert Modus: Default
- [STATUS_HV_ISOLATION](#job-status-hv-isolation) - Liest Isolationsstatus Batterie aus $22     SID ReadDataByIdentifier $02 $16 DID Messwert Liest Isolationsstatus des MCP A aus $22     SID ReadDataByIdentifier $02 $17 DID Messwert Liest Isolationsstatus des MCP B aus $22     SID ReadDataByIdentifier $02 $18 DID Messwert Modus: Default
- [STATUS_HVIL](#job-status-hvil) - Auslesen des HVIL-Zustandes (falls HVIL unterbrochen, dann n.i.O.) $22     SID ReadDataByIdentifier $02 $19 DID Messwert Auslesen des HVIL-Zustandes aus Sicht der PEB fuer MCP A $22     SID ReadDataByIdentifier $02 $1B DID Messwert Auslesen des HVIL-Zustandes aus Sicht der PEB fuer MCP B $22     SID ReadDataByIdentifier $02 $1C DID Messwert Auslesen des HVIL-Zustandes aus Sicht der Batterie $22     SID ReadDataByIdentifier $02 $1A DID Messwert Modus: Default
- [STATUS_KL_15](#job-status-kl-15) - Gibt den Status der Klemme 15 aus $22     SID ReadDataByIdentifier $02 $23 DID Messwert Gibt den Spannungswert der Klemme 15 aus $22     SID ReadDataByIdentifier $02 $24 DID Messwert Modus: Default
- [STEUERN_ANTRIEBSART](#job-steuern-antriebsart) - Auswahl: Forciertes E-Fahren, explizites Nicht E-Fahren, normal $2E     SID ReadDataByIdentifier $F2 $2  DID Messwert Modus: Default
- [STEUERN_APM](#job-steuern-apm) - Setzen das APM in einen bestimmten Betriebsmodus HV-Sicherheitskonzept wird nicht überstimmt!! Eingangsbedingungen werden über CCM im Kombi angezeigt $2E       SID ReadDataByIdentifier $F2 $0  DID Messwert Steuern der LV-Output-Spannung der APM. Eingabe der Spannung in Volt. $2E       SID ReadDataByIdentifier $F2 $4  DID Messwert Modus: Default
- [STEUERN_APM_LIMIT](#job-steuern-apm-limit) - Aktivierung/Deaktivieren der Limitierung $2E     SID ReadDataByIdentifier $F2 $3  DID Messwert Modus: Default
- [STEUERN_ENERGIESPARMODE](#job-steuern-energiesparmode) - Steuern der des Energiesparmodes (FETRAWE) Ist Klemmensicher und mit DTC-Eintrag verbunden $2E     SID ReadDataByIdentifier $F2 $5  DID Messwert Modus: Default
- [STEUERN_ENGDSRD](#job-steuern-engdsrd) - Externe Steuerung des Motorstatus Hinweis: ENERGIESPARMODE muss aktiviert sein und STEUERN_COMPLETECONTROL_SCHALTER ausgeführt werden. $2E     SID ReadDataByIdentifier $F2 $6  DID Messwert Modus: Default
- [STEUERN_LADEN_HV_BATTERIE](#job-steuern-laden-hv-batterie) - Einschalten/Ausschalten der Ladefunktion $2E     SID ReadDataByIdentifier $F2 $1  DID Messwert Modus: Default
- [STEUERN_LL_DREHZAHL](#job-steuern-ll-drehzahl) - Sollvorgabe Verbrennungsmotor-Drehzahl in Neutral $2E     SID ReadDataByIdentifier $F2 $8  DID Messwert Modus: Default
- [STEUERN_NI_MODE_1](#job-steuern-ni-mode-1) - Sollvorgabe Verbrennungsmotor-Drehzahl in Mode 1 Hinweis: ENERGIESPARMODE muss aktiviert sein und STEUERN_COMPLETECONTROL_SCHALTER ausgeführt werden. $2E     SID ReadDataByIdentifier $F2 $0A DID Messwert Modus: Default
- [STEUERN_NI_MODE_2](#job-steuern-ni-mode-2) - Sollvorgabe Verbrennungsmotor-Drehzahl in Mode 2 Hinweis: ENERGIESPARMODE muss aktiviert sein und STEUERN_COMPLETECONTROL_SCHALTER ausgeführt werden. $2E     SID ReadDataByIdentifier $F2 $0B ADID Messwert Modus: Default
- [STEUERN_RNGDSRD](#job-steuern-rngdsrd) - Vorgabe Gang für OHSR-Schnittstelle Hinweis: ENERGIESPARMODE muss aktiviert sein und STEUERN_COMPLETECONTROL_SCHALTER ausgeführt werden. $2E     SID ReadDataByIdentifier $F2 $0D DID Messwert Modus: Default
- [STATUS_ANTRIEBSART_ZUGRIFF](#job-status-antriebsart-zugriff) - Gibt den Status der aktuell anliegenden extern eingesteuerten Antriebsart an. $22     SID ReadDataByIdentifier $02 $31 DID Messwert Modus: Default
- [STATUS_BATT_CONN](#job-status-batt-conn) - Gibt an ob das Batterie-Schütz /Relais betätigt ist. $22     SID ReadDataByIdentifier $02 $29 DID Messwert Modus: Default
- [STATUS_E_MOTOR_CONTROL_CHECK](#job-status-e-motor-control-check) - Liest die erzielte E-Maschinen Drehzahl nach E-Motor Control Check aus. $22   SID ReadDataByIdentifier $02 $30 DID Messwert Modus: Default
- [STATUS_ENERGIESPARMODE](#job-status-energiesparmode) - Rückgabe des aktuell anliegenenden FETRAWE-Status. Hinweis: Nur in Verbindung mit Energiesparmode Werkstatt. Fehlereintrag wird beim Setzen angelegt. $22     SID ReadDataByIdentifier $02 $XX DID Messwert Modus: Default
- [STATUS_IO_LESEN](#job-status-io-lesen) - Rückgabe des aktuellen Ist- Ganges. $22     SID ReadDataByIdentifier $02 $2C DID Messwert Modus: Default
- [STATUS_LESEN_PWRLNCH_COUNTER](#job-status-lesen-pwrlnch-counter) - Job liest die Anzahl der durchgeführten PowerLunches und die Anzahl der PowerLaunches nach dem letzten Reset aus. $22     SID ReadDataByIdentifier $02 $3F DID Messwert Modus: Default
- [STATUS_LL_REGELUNG](#job-status-ll-regelung) - Rückmeldung ob Leerlaufregelung i.O. ist $22     SID ReadDataByIdentifier $02 $35 DID Messwert Modus: Default
- [STATUS_PARKSENSOREN](#job-status-parksensoren) - Liest den plausibilitierten Zustand der Parksensoren (TCM und DSM) aus. $22     SID ReadDataByIdentifier $02 $27 DID Messwert Modus: Default
- [STATUS_SOC_ACC_LESEN](#job-status-soc-acc-lesen) - Rückgabe der Güte des SOC-Wertes. $22     SID ReadDataByIdentifier $02 $2D DID Messwert Modus: Default
- [STEUERN_COMPLETECONTROL_SCHALTER](#job-steuern-completecontrol-schalter) - Schalter für Completecontrol Darf nicht im Service ausgeführt werden $2E     SID WriteDataByIdentifier $F2 $18 DID Messwert Modus: Default
- [STEUERN_ERZWUNGENE_SCHUBABSCHALTUNG](#job-steuern-erzwungene-schubabschaltung) - Kann die Schubabschaltung erzwingen. FETRAWE-Mode muss gesetzt sein $2E     SID WriteDataByIdentifier $F2 $19 DID Messwert Modus: Default
- [STATUS_KOMPRESSIONSTEST](#job-status-kompressionstest) - Liest die Variablen zum Kompressionstest aus. $22   SID ReadDataByIdentifier $02 $52 DID Messwert Modus: Default
- [STEUERN_KOMPRESSIONSTEST](#job-steuern-kompressionstest) - Schaltet Kompressionstest VM an ENERGIEPARMODE muss an sein $2E       SID WriteDataByIdentifier $F2 $1D   DID Messwert Modus: Default
- [STEUERN_PWRLNCH_CNT_RESET](#job-steuern-pwrlnch-cnt-reset) - Job zum Resettieren/Zurücksetzen des PowerLaunch Zählers. Hinweis: Nur in Verbindung mit Energiesparmode Werkstatt Keine Übergabeparameter $2E     SID WriteDataByIdentifier $F2 $15 DID Messwert Modus: Default
- [STEUERN_SOC_SOLL](#job-steuern-soc-soll) - Schaltet SOC Vorgabe an ENERGIEPARMODE muss an sein Aus nach 300s $2E      SID WriteDataByIdentifier $F2 $1C  DID Messwert Modus: Default
- [STEUERN_SOC_SOLL_WERT](#job-steuern-soc-soll-wert) - Sollvorgabe SOC, nur innerhalb der i.O. Grenzen, nur in Verbindung mit FETRAWE Vorher muss der Job STEUERN_SOC_SOLL ausgeführt werden 0=AUS oder nach 1200s $22     SID ReadDataByIdentifier $02 $1B DID Messwert Modus: Default
- [STATUS_DEGRADATION_SOURCE](#job-status-degradation-source) - Rückmeldung Ursache der aktuellen Degradation im Fzg
- [STATUS_STRSTP_ZAEHLER](#job-status-strstp-zaehler) - Liest den Historienspeicher der HCP hinsichtlich der Anzahl der absolvierten Starts aus.
- [STATUS_HISR_HOS](#job-status-hisr-hos) - Der Job gibt die Energieanteile und die Zeitanteile der verschieden Usecases /Modies an. Zusätzlich werden die Gesamtenergiemenge und die Gesamtzeit ausgegeben. Die Gesamtwerte können nicht zurückgesetzt werden.
- [STATUS_HISR_RING](#job-status-hisr-ring) - Ließt den Historyspeicher der HCP Betriebsstatisitik aus. Es werden maximal 40 Einträge zurückgeliefert. Es werden immer alle Results zurückgegeben, auch wenn weniger als 40 Fehler gespeichert sind.
- [STATUS_HISR_AUSLESEN_01](#job-status-hisr-auslesen-01) - HISR Werte01 auslesen (Übersicht)
- [STATUS_HISR_AUSLESEN_02](#job-status-hisr-auslesen-02) - HISR Werte02 auslesen (Zeitangaben)
- [STATUS_HISR_AUSLESEN_03](#job-status-hisr-auslesen-03) - HISR Werte03 auslesen (Counter)
- [STATUS_HISR_AUSLESEN_04](#job-status-hisr-auslesen-04) - HISR Werte04 auslesen
- [STEUERN_HISR_AV_RESET_HAEUFIGKEIT](#job-steuern-hisr-av-reset-haeufigkeit) - Löscht die Häufigkeit des Ausschaltverhinderer (AV) Historienspeicher
- [STEUERN_HISR_AV_RESET_KM_UND_AKTIV](#job-steuern-hisr-av-reset-km-und-aktiv) - Löscht beide Kilometerstände und Aktiv-Status des Ausschaltverhinderer (AV) Historienspeicher
- [STEUERN_SOC_STIMUL](#job-steuern-soc-stimul) - Job schaltet die SOC Stimmulierung ein. Batterie wird entladen und gelanden um den SOC-Wert zu bestimmen. AUS nach 1200s $2E     SID WriteDataByIdentifier $F2 $14 DID Messwert Modus: Default
- [STATUS_ADAPTIONSWERTE_LESEN](#job-status-adaptionswerte-lesen) - Liest die Adaptionswerte von PyroFuse(integriert in der SBK - SicherheitsBatterieKlemme), Batterie, CC-Meldung aus. Siehe Argumente. $22      SID WriteDataByIdentifier $02 $32  DID Messwert Modus: Default
- [STEUERN_ADAPTIONSWERTE_LOESCHEN](#job-steuern-adaptionswerte-loeschen) - Löscht die Adaptionswerte. Siehe Argumente. $2E     SID WriteDataByIdentifier $F2 $1A DID Messwert Modus: Default
- [STEUERN_BATTERIE_ADAPTIONSWERTE_LOESCHEN](#job-steuern-batterie-adaptionswerte-loeschen) - Löscht die Adaptionswerte in der HV-Batterie. Ausschließlich im Werkstattmode möglich. $2E     SID WriteDataByIdentifier $F2 $27 DID Messwert Modus: Default
- [STEUERN_COMPLETECONTROL_PIN](#job-steuern-completecontrol-pin) - Freigabe Code für Steuern Antriebsart Complete Control Es muss der entsprechenden Freigabecode übergeben werden, damit keine Beschädigungen im Getriebe auftreten können. $2E     SID WriteDataByIdentifier $F2 $17 DID Messwert Modus: Default
- [STEUERN_E_MOTOR_CONTROL_CHECK](#job-steuern-e-motor-control-check) - Anstossen des E-Motor Control Check Zur Überprüfung der E-Maschinen. Die E-Maschinen werden für max. 60s gedreht Service Hinweise: Nur in Verbindung mit Energiesparmode Werkstatt. WÄHREND TEST KEINESFALLS START-STOP-TASTER DRÜCKEN!!! BAUTEILSCHÄDIGUNG.  $2E       SID WriteDataByIdentifier $F2 $16   DID Messwert Modus: Default
- [STATUS_CRASH_DETECTION_SIGNAL](#job-status-crash-detection-signal) - Gibt den Status der Crash Detection Leitung aus $22     SID ReadDataByIdentifier $02 $26 DID Messwert Modus: Default
- [STATUS_GESAMTFZG_DEGRADATION](#job-status-gesamtfzg-degradation) - Auslesen der strategischen EM-A Degradation $22     SID ReadDataByIdentifier $02 $0F DID Messwert Auslesen der strategischen EM-B Degradation $22     SID ReadDataByIdentifier $02 $10 DID Messwert Auslesen der strategischen Verbrennungsmotordegradation $22     SID ReadDataByIdentifier $02 $11 DID Messwert Auslesen der strategischen Batterieladedegradation $22     SID ReadDataByIdentifier $02 $0E DID Messwert Auslesen der strategischen Batterieentladedegradation $22     SID ReadDataByIdentifier $02 $0D DID Messwert Modus: Default
- [STATUS_AKTUELLE_GETRIEBEPOSITION](#job-status-aktuelle-getriebeposition) - Status der Getriebeposition P / R / N / D $22     SID ReadDataByIdentifier $02 $28 DID Messwert Modus: Default
- [STATUS_EMF_HILFERUF](#job-status-emf-hilferuf) - Lese Anzahl der EMF Hilferufe in D/S/M/R/N
- [STATUS_VOLTAGE_HCP_HV_SIDE](#job-status-voltage-hcp-hv-side) - Auslesen der Hochvolt-Spannung und des Interlock Status ACHTUNG: Die Spannungsfreiheit wird nicht durch diesen Aufruf garantiert! Bitte Hochvolt-Sicherheits-Maßnahmen beachten. $22     SID ReadDataByIdentifier $02 $25 DID Messwert Modus: Default
- [STATUS_HCP_TELESERVICE_MONITORING](#job-status-hcp-teleservice-monitoring) - Results folgender Jobs hintereinander: STATUS_LESEN_PWRLNCH_COUNTER STATUS_ABSCHALTVERHINDERER STATUS_DEGRATIONS_SOURCE STATUS_EMF_HILFERUF STATUS_HCP_RBM_RATIO
- [STATUS_BATTERIE_KUEHLUNG](#job-status-batterie-kuehlung) - Job ließt die Daten der Batteriekühlung aus.
- [STEUERN_BATTERIE_KUEHLUNG](#job-steuern-batterie-kuehlung) - Job zum Ansteuern der Kühlsystemkonfiguration
- [STATUS_HCP_RBM_RATIOS](#job-status-hcp-rbm-ratios) - Auslesen der Ratios vom HCP
- [STATUS_BATTERIE_EQUILIBRIERUNG](#job-status-batterie-equilibrierung) - Zustand Batterie-Equilibrierung
- [STEUERN_BATTERIE_EQUILIBRIERUNG](#job-steuern-batterie-equilibrierung) - Steuern der Batterie-Equilibrierung.
- [STATUS_BATTERIE_NUTZUNG](#job-status-batterie-nutzung) - Liest die Variablen der Batterienutzung aus.
- [STEUERN_KURZSCHLUSS_UVW_EMP](#job-steuern-kurzschluss-uvw-emp) - Steuert aktiven Kurzschluss an EMP
- [STEUERN_TIMER_BATTERIE_KUEHLUNG](#job-steuern-timer-batterie-kuehlung) - Job zum Vorgeben der maximalen Laufzeit des JOBS STEUERN_BATTERIE_KUEHLUNG
- [STATUS_BATTERIE_ADAPTIONSWERTE_LESEN](#job-status-batterie-adaptionswerte-lesen) - Batterie Adaptionswert lesen Daten muessen vor dem Flashen gesichert werden.
- [STATUS_BATTERIE_ADAPTIONSWERTE_GESCHRIEBEN](#job-status-batterie-adaptionswerte-geschrieben) - Ließt den Status nach dem Adaptionswerte schreiben aus.
- [STEUERN_BATTERIE_ADAPTIONSWERTE_SCHREIBEN](#job-steuern-batterie-adaptionswerte-schreiben) - Daten muessen nach dem Flashen geschrieben werden. SG muss vorher in Werkstattmode gesetzt werden
- [STATUS_VM_LEISTUNGSMESSUNG](#job-status-vm-leistungsmessung) - Rückmeldung des Status Motorleistungstest
- [STATUS_VM_LEISTUNG_LESEN](#job-status-vm-leistung-lesen) - Rückgabe der VM-Werte
- [STEUERN_VM_LEISTUNGSMESSUNG](#job-steuern-vm-leistungsmessung) - Für Motorleistungstest müssen elektrische Antriebskomponenten neutralisiert werden. Fzg. fährt rein verbrennungsmotorisch. 1= nur Verbrennungsmotor 0= VM und E-Motor ENERGIEPARMODE muss an sein Job ist 10 Minuten aktiv und kann nicht ausgeschalten werden!
- [STATUS_BATTERIE_EQUIL_HISTORIE](#job-status-batterie-equil-historie) - Historie der Batterie Equilibrierung
- [STEUERN_HISR_HOS_RESET](#job-steuern-hisr-hos-reset) - Erwirkt einen Reset der Betriebsstrategieanalyse ENERGIEPARMODE muss an sein
- [STATUS_VITAL_VARIABLES_DREHZAHLEN](#job-status-vital-variables-drehzahlen) - Liest die Werte von charakteristischen Drehzahlen und Geschwindigkeiten aus
- [STATUS_VITAL_VARIABLES_LEISTUNGEN](#job-status-vital-variables-leistungen) - Liest die Werte von charakteristischen Leistungen, Spannungen, Stroemen und Ladezustaenden aus
- [STATUS_VITAL_VARIABLES_MOMENTE](#job-status-vital-variables-momente) - Liest die Werte von charakteristischen Momenten aus
- [STATUS_VITAL_VARIABLES_STATUS](#job-status-vital-variables-status) - Liest die Werte von charakteristischen Status aus
- [STATUS_VITAL_VARIABLES_TEMPERATUREN](#job-status-vital-variables-temperaturen) - Liest die Werte von charakteristischen Temperaturen aus
- [LESEN_INDIVIDUALDATA_LISTE](#job-lesen-individualdata-liste) - Lesen eines Listeneintrags der Individualisierungsdaten KWP2000: $21 ReadDataByLocalIdentifier (not used) $01 recordLocalIdentifier (not used)
- [LESE_INDIVIDUALDATA](#job-lese-individualdata) - Lesen von Individualisierungsdaten Modus   : Default
- [SCHREIBEN_INDIVIDUALDATA](#job-schreiben-individualdata) - Schreiben von Individualisierungsdaten Modus   : Default
- [_STATUS_FLASHPROG_PRECONDITION_LESEN](#job-status-flashprog-precondition-lesen) - Status der Vorbedingungen fuer das Flashen ueber WinKFP $22     SID ReadDataByIdentifier $03 $01 DID Messwert Modus: Default
- [_STATUS_PROZESSOR_LESEN_JOBS](#job-status-prozessor-lesen-jobs) - Reset-Statistik, Resetursachen, Resetadressen Status der Level 3-Tests, NVM-Status/Checksummen Hoechste erreichte Anzahl von(Running-)Resets zwischen 2 PowerUp-Resets PowerUp-Reset setzt Wert zurueck Wert wird bei Klemme15- und Batteriewechsel nicht zurueckgesetzt $22     SID ReadDataByIdentifier $20 $4B DID Messwert Anzahl der Resets seit der letzten Neuprogrammierung Powerup-Resets(Watchdog) werden nicht erfasst Klemme15- und Batteriewechsel haben auf den Wert keinen Einfluss $22     SID ReadDataByIdentifier $20 $4A DID Messwert Ursache des letzten Resets $22     SID ReadDataByIdentifier $12 $DE DID Messwert Adresse, an der der letzte Resets aufgetreten  ist $22     SID ReadDataByIdentifier $12 $E7 DID Messwert Adresse, an der vom RAM-Test eine Fehler festgestellt wurde $22     SID ReadDataByIdentifier $20 $34 DID Messwert Status der Processorueberwachung FUSI-Level 3 $22     SID ReadDataByIdentifier $20 $39 DID Messwert Status der Checksummen- und Lesepruefung aller NVM-RAM Bereiche $22     SID ReadDataByIdentifier $20 $33 DID Messwert Modus: Default
- [_STATUS_REMEDIAL_ACTION_HISTORY](#job-status-remedial-action-history) - Gibt den Fehler bitkodiert zurück
- [_STATUS_REMEDIAL_ACTION](#job-status-remedial-action) - Gibt die letzten Fehler bitcodiert zurueck $22     SID ReadDataByIdentifier $03 $02 DID Messwert Modus: Default
- [_STEUERN_REMEDIAL_ACTION_RESET](#job-steuern-remedial-action-reset) - Löschen des Historienspeichers RA Energiesparmode Werkstatt muss gesetzt sein
- [_BUILD_IDENT_LESEN](#job-build-ident-lesen) - Auslesen der Build Informations Felder Standard Flashjob Modus   : Default
- [_STEUERN_STANDLOAD_VERFUEGBAR](#job-steuern-standload-verfuegbar) - Entwicklerjob zur Bereitstellung der Standloadfunktion mit Gas&Bremspedal
- [_STATUS_BATTERIE_AKTIVE_LEISTUNG](#job-status-batterie-aktive-leistung) - Liest Status der Batterieleistung aus. Gibt an von welchem Kriterium die Leistung im Moment begrenzt ist.
- [_STATUS_SOCR_USECASE](#job-status-socr-usecase) - Rückgabe des aktuellen Betriebszustandes der HV-Speicherladestrategie
- [_STATUS_RESET_URSACHE](#job-status-reset-ursache) - Auslesen der Reset Ursache Es werden 6 Pakete zurückgeliefert  1 Paket: Reset der nicht durch einen PowerUp Reset verursacht wurde. 5 Pakete: Alle zuletzt aufgetretenen Resets Inhalt eines Pakets: - SOC der HV-Batterie - Spannung RunCrank - Background-LoopMax Wert - PLD Feedback-Wert - Sammelfehler für Processorhardware - E-MotorA Temperatur - E-MotorA-Inverter Temperatur - km-Stand - ResetSourceAddress - ResetSource - Program/Datenstand  Beschreibung der Results wird hier nur an Hand des 1.Paket gemacht. Die anderen Pakete sind analog zu betrachten.

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

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen (alle Fehler / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $02 ReadDTCByStatusMask UDS  : $0C StatusMask (Bit2, Bit3) Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| F_VERSION | int | Typ des Fehlerspeichers Fuer UDS immer 3 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_EREIGNIS_DTC | int | 0: DTC kein Ereignis DTC 1: DTC ist Ereignis DTC table FOrtTexte EREIGNIS_DTC |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen UDS  : $14 ClearDiagnosticInformation UDS  : $FF DTCHighByte UDS  : $FF DTCMiddleByte UDS  : $FF DTCLowByte Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | long | 0x??????: Angabe eines einzelnen Fehlers Default: 0xFFFFFF: alle Fehler |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels UDS  : $22   ReadDataByIdentifier UDS  : $1000 TestStamp Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. UDS  : $2E   WriteDataByIdentifier UDS  : $1000 TestStamp Modus: Default

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
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Diagnosemode des SG aufrecht erhalten UDS  : $3E TesterPresent UDS  : $?0 suppressPosRspMsgIndication Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SG_ANTWORT | string | "ja"   -&gt; SG soll antworten "nein" -&gt; SG soll nicht antworten table DigitalArgument TEXT Default:  SG soll antworten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-diagnose-mode"></a>
### DIAGNOSE_MODE

SG in bestimmten Diagnosemode bringen UDS  : $10 StartDiagnosticSession Modus: einstellbar mit diesem Job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | gewuenschter Diagnose-Modus table DiagMode MODE MODE_TEXT Defaultwert: DEFAULT (DefaultMode) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuergeraete-reset"></a>
### STEUERGERAETE_RESET

Harter Reset des Steuergeraets UDS  : $11 EcuReset UDS  : $01 HardReset Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-fs-lesen-detail"></a>
### FS_LESEN_DETAIL

Fehlerspeicher lesen(einzelner Fehler / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $06 reportDTCExtendedDataRecordByDTCNumber Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | long | gewaehlter Fehlercode |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| F_VERSION | int | Typ des Fehlerspeichers Fuer UDS immer 3 Nach aussen werden wir aber wie KWP2000 behandelt - deshalb 2! |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_EREIGNIS_DTC | int | 0: DTC kein Ereignis DTC 1: DTC ist Ereignis DTC table FOrtTexte EREIGNIS_DTC |
| F_READY_NR | int | Readyness Flag(Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag(Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden(Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden(Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag(Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag(Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_PCODE | unsigned int | optional / Pflicht fuer abgasrelevante SG Wertebereich 0x0000 - 0xFFFF 0x0000: wenn nicht belegt |
| F_PCODE_STRING | string | 5 stelliger Text in der Form 'Pxxxx' '--': wenn nicht belegt '??': wenn nicht bekannt |
| F_PCODE_TEXT | string | Fehler als Klartext '': wenn nicht belegt table PCodeTexte TEXT |
| F_PCODE7 | unsigned int | optional / fuer abgasrelevante SG Wertebereich 0x0000 - 0xFFFF 0x0000: wenn nicht belegt |
| F_PCODE7_STRING | string | 5 stelliger Text in der Form 'Pxxxx' '--': wenn nicht belegt '??': wenn nicht bekannt |
| F_PCODE7_TEXT | string | Fehler als Klartext '': wenn nicht belegt table PCodeTexte TEXT |
| F_HFK | int | Haufigkeitszaehler als Zahl Wertebereich 0 - 255 Bei mehr als 255 bleibt Zaehler stehen. Kein Ueberlauf |
| F_HLZ | int | Heilungsszaehler als Zahl Wertebereich 0 - 255 -1: ohne Haufigkeitszaehler |
| F_UEBERLAUF | int | 0: Kein Ueberlauf des Fehlerspeichers 1: Ueberlauf des Fehlerspeichers |
| F_FEHLERKLASSE_NR | int | 0: Keine Fehlerklasse verfuegbar 1: Ueberpruefung bei naechstem Werkstattbesuch 2: Ueberpruefung bei naechstem Halt 4: Ueberpruefung sofort erforderlich ! |
| F_FEHLERKLASSE_TEXT | string | Ausgabe der Fehlerklasse als Text table Fehlerklasse TEXT |
| F_ART_ANZ | int | Anzahl der Arten |
| F_UW_KM | long | Umweltbedingung Kilometerstand(3 Byte) Wertebereich: 0 - 16777215 km -1, wenn Kilometerstand nicht zur Verfuegung steht |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Je nach dieser Anzahl i(i = 1, 2, ...) existieren i mal folgende Results: (long)   F_UWi_NR   Index   der i. Umweltbedingung (string) F_UWi_TEXT Text    zur i. Umweltbedingung (real)   F_Uwi_WERT Wert    der i. Umweltbedingung (string) F_UWi_EINH Einheit der i. Umweltbedingung |
| _RESPONSE_SNAPSHOT | binary | Hex-Antwort von SG |
| _RESPONSE_EXTENDED_DATA | binary | Hex-Antwort von SG |
| _RESPONSE_SEVERITY | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-ident"></a>
### IDENT

Identdaten auslesen UDS  : $22   ReadDataByIdentifier UDS  : $3F51 Sub-Parameter SGBD-Index UDS  : $3F3C Sub-Parameter SGBD-Index UDS  : $3F36 Sub-Parameter SGBD-Index UDS  : $3F38 Sub-Parameter SGBD-Index UDS  : $3F3A Sub-Parameter SGBD-Index UDS  : $3F30 Sub-Parameter SGBD-Index Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | string | BMW-Hardware-Versionsindex (= Hardware Version Number Byte #3) |
| ID_COD_INDEX | int | Codier-Index Dummy-Wert |
| ID_DIAG_INDEX | long | Index zur Erkennung der SG-Variante Hybrid Generation 1.0 liefert nur 2 Antwort-Byte |
| ID_VAR_INDEX | int | Varianten-Index |
| ID_DATUM_JAHR | int | Herstelldatum(Jahr) |
| ID_DATUM_MONAT | int | Herstelldatum(Monat) |
| ID_DATUM_TAG | int | Herstelldatum(Tag) Dummy-Wert |
| ID_DATUM | string | Herstelldatum(TT.MM.JJJJ) |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Text table Lieferanten buffer_2 |
| ID_SW_NR_MCV | string | Softwarenummer(Nachrichten Katalog Version) |
| ID_SW_NR_FSV | string | Softwarenummer(Funktions Software Version) |
| ID_SW_NR_OSV | string | Softwarenummer(operating system version) |
| ID_SW_NR_RES | string | Softwarenummer(reserved - currently unused) Dummy-Wert |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _REQUEST1 | binary | Hex-Auftrag an SG |
| _RESPONSE1 | binary | Hex-Antwort von SG |
| _REQUEST2 | binary | Hex-Auftrag an SG |
| _RESPONSE2 | binary | Hex-Antwort von SG |
| _REQUEST3 | binary | Hex-Auftrag an SG |
| _RESPONSE3 | binary | Hex-Antwort von SG |
| _REQUEST4 | binary | Hex-Auftrag an SG |
| _RESPONSE4 | binary | Hex-Antwort von SG |
| _REQUEST5 | binary | Hex-Auftrag an SG |
| _RESPONSE5 | binary | Hex-Antwort von SG |
| _REQUEST6 | binary | Hex-Auftrag an SG |
| _RESPONSE6 | binary | Hex-Antwort von SG |

<a id="job-aif-lesen"></a>
### AIF_LESEN

Auslesen des Anwender Informations Feldes Standard Flashjob Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| AIF_FG_NR | string | Fahrgestellnummer 7-stellig |
| AIF_FG_NR_LANG | string | Fahrgestellnummer 17-stellig falls vorhanden, sonst 7-stellig |
| AIF_DATUM | string | Datum der SG-Programmierung in der Form TT.MM.JJJJ |
| AIF_ZB_NR | string | BMW/Rover Zusammenbaunummer |
| AIF_SW_NR | string | BMW/Rover Datensatznummer - Softwarenummer |
| AIF_BEHOERDEN_NR | string | BMW/Rover Behoerdennummer |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_SERIEN_NR | string | Tester Seriennummer |
| AIF_KM | string | km-Stand bei der Programmierung |
| AIF_PROG_NR | string | Programmstandsnummer |
| AIF_ANZ_FREI | int | Anzahl noch vorhandener AIF-Eintraege |
| AIF_ANZAHL_PROG | int | Anzahl Programmiervorgaenge |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST01 | binary | Hex-Auftrag an SG |
| _RESPONSE01 | binary | Hex-Antwort von SG |
| _REQUEST02 | binary | Hex-Auftrag an SG |
| _RESPONSE02 | binary | Hex-Antwort von SG |
| _REQUEST03 | binary | Hex-Auftrag an SG |
| _RESPONSE03 | binary | Hex-Antwort von SG |

<a id="job-daten-referenz-lesen"></a>
### DATEN_REFERENZ_LESEN

Auslesen der Daten Referenz KWP2000: $22   ReadDataByCommonIdentifier $2504 DREF Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATEN_REFERENZ | string | Daten Referenz Format: ZZZPPPxVBBxhdxxxx 17 Byte ASCII ZZZ   : Hardwarelieferant PPP   : Hardwarerelevanz zum Programmstand x     : nicht programmrelevante Varianten der Hardware V     : Projektvariante BB    : Programmstand x     : nicht datenrelevanter Änderungsindex h     : Programmstandersteller d     : Datenstandersteller xxxx  : frei aber eindeutig belegt |
| DATEN_REF_SG_KENNUNG | string | ZZZ |
| DATEN_REF_PROJEKT | string | PPPxV |
| DATEN_REF_PROGRAMM_STAND | string | BBxh |
| DATEN_REF_DATENSATZ | string | dxxxx |
| DATEN_REF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-zif-lesen"></a>
### ZIF_LESEN

Auslesen des Zulieferinfofeldes KWP2000: $22   ReadDataByCommonIdentifier $2503 ProgrammReferenz und KWP2000: $1A   ReadECUIdentification $91   VehicleManufacturerECUHardware*Number oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ZIF_PROGRAMM_REFERENZ | string | PRGREF ProgrammReferenz letzter lauffaehiger Programmstand Format: ZZZPPPxVBBxh 12 Byte ASCII ZZZ   : Hardwarelieferant PPP   : Hardwarerelevanz zum Programmstand x     : nicht programmrelevante Varianten der Hardware V     : Projektvariante BB    : Programmstand x     : nicht datenrelevanter Änderungsindex h     : Programmstandersteller |
| ZIF_SG_KENNUNG | string | ZZZ |
| ZIF_PROJEKT | string | PPPxV |
| ZIF_PROGRAMM_STAND | string | BBxh |
| ZIF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |
| ZIF_BMW_HW | string | VMECUH*N vehicleManufacturerECUHardware*Number BMW Hardware Nummer |
| ZIF_BMW_PST | string | Dummywert fuer BMW PST |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST01 | binary | Hex-Auftrag an SG |
| _RESPONSE01 | binary | Hex-Antwort von SG |
| _REQUEST02 | binary | Hex-Auftrag an SG |
| _RESPONSE02 | binary | Hex-Antwort von SG |

<a id="job-seriennummer-lesen"></a>
### SERIENNUMMER_LESEN

Seriennummer des Steuergeraets UDS  : $22   ReadDataByIdentifier UDS  : $F18C Sub-Parameter ECUSerialNumber Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SERIENNUMMER | string | Seriennummer des Steuergeraets |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-abschaltverhinderer"></a>
### STATUS_ABSCHALTVERHINDERER

Lese den aktuellen Aussschaltverhinderer $22     SID ReadDataByIdentifier $02 $00 DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_0_0_HV_BATTERY_PACK_VOLTAGE_LEVEL_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_0_0_HV_BATTERY_PACK_VOLTAGE_LEVEL_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_0_1_HV_BATTERY_POWER_LIMITS_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_0_1_HV_BATTERY_POWER_LIMITS_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_0_2_HV_BATTERY_MODULE_VOLTAGE_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_0_2_HV_BATTERY_MODULE_VOLTAGE_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_0_3_HV_BATTERY_STATE_OF_CHARGE_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_0_3_HV_BATTERY_STATE_OF_CHARGE_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_0_4_TRANSMISSION_RANGE_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_0_4_TRANSMISSION_RANGE_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_0_5_TRANSMISSION_RANGE_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_0_5_TRANSMISSION_RANGE_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_0_6_ECM_REQUEST_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_0_6_ECM_REQUEST_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_0_7_SOC_REGELUNG_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_0_7_SOC_REGELUNG_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_1_0_DRIVEABILITY_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_1_0_DRIVEABILITY_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_1_1_MINIMUM_RUN_TIME_NOT_MET_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_1_1_MINIMUM_RUN_TIME_NOT_MET_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_1_2_DEVICE_CONTROL_AUTOSTART_OVERRIDE_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_1_2_DEVICE_CONTROL_AUTOSTART_OVERRIDE_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_1_3_KEY_FORCED_AUTOSTART_REQUEST_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_1_3_KEY_FORCED_AUTOSTART_REQUEST_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_1_4_AUXILIARY_TRANSMISSION_PUMP_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_1_4_AUXILIARY_TRANSMISSION_PUMP_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_1_5_ELECTRIC_MOTOR_INVERTER_TEMPERATURE_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_1_5_ELECTRIC_MOTOR_INVERTER_TEMPERATURE_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_1_6_ELECTRIC_MOTOR_TEMPERATURE_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_1_6_ELECTRIC_MOTOR_TEMPERATURE_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_1_7_ENGINE_COOLANT_TEMPERATURE_UNDER_MINLIM_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_1_7_ENGINE_COOLANT_TEMPERATURE_UNDER_MINLIM_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_2_0_INHIBITER_DYNAMIC_CONTROL_LASH_MSE_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_2_0_INHIBITER_DYNAMIC_CONTROL_LASH_MSE_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_2_1_REVERSE_GRADE_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_2_1_REVERSE_GRADE_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_2_2_DATA_VALIDITY_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_2_2_DATA_VALIDITY_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_2_3_VEHICLE_SPEED_TOO_HIGH_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_2_3_VEHICLE_SPEED_TOO_HIGH_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_2_4_DRIVER_ABSENT_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_2_4_DRIVER_ABSENT_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_2_5_SYSTEM_VOLTAGE_LOW_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_2_5_SYSTEM_VOLTAGE_LOW_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_2_6_TRANS_RANGE_STATE_PRN_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_2_6_TRANS_RANGE_STATE_PRN_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_2_7_HV_BATTERY_PACK_TEMPERATURE_UNDER_MINLIM_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_2_7_HV_BATTERY_PACK_TEMPERATURE_UNDER_MINLIM_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_3_0_CLUTCH_2_STUCKED_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_3_0_CLUTCH_2_STUCKED_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_3_1_MAX_MOTOR_OIL_TEMPERATURE_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_3_1_MAX_MOTOR_OIL_TEMPERATURE_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_3_2_AMBIENT_TEMPERATURE_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_3_2_AMBIENT_TEMPERATURE_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_3_3_BATTERY_WARM_UP_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_3_3_BATTERY_WARM_UP_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_3_4_ENGINE_COOLANT_TEMPERATURE_OVER_MAXLIM_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_3_4_ENGINE_COOLANT_TEMPERATURE_OVER_MAXLIM_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_3_5_HV_BATTERY_PACK_TEMPERATURE_OVER_MAXLIM_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_3_5_HV_BATTERY_PACK_TEMPERATURE_OVER_MAXLIM_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_3_6_TRANSMISSION_TEMP_UNDER_MINLIM_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_3_6_TRANSMISSION_TEMP_UNDER_MINLIM_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_3_7_REMEDIAL_ACTIONS_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_3_7_REMEDIAL_ACTIONS_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_0_0_FIFR_EOVERDRIVE_NR | unsigned char | veraltete AV-s |
| STAT_0_0_FIFR_EOVERDRIVE_TEXT | string | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_0_1_FIFR_UEBERLADEN_BATTERIE_NR | unsigned char | Verhindern des Ueberladens der Batterie |
| STAT_0_1_FIFR_UEBERLADEN_BATTERIE_TEXT | string | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_0_2_FIFR_S_M_MODE_NR | unsigned char | S/M-Mode |
| STAT_0_2_FIFR_S_M_MODE_TEXT | string | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_0_3_FIFR_PEDAL_BETAETIGUNG_P_N_NR | unsigned char | Gaspedalbetaetigung in P/N |
| STAT_0_3_FIFR_PEDAL_BETAETIGUNG_P_N_TEXT | string | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_0_4_FIFIR_PADDEL_TIP_IN_NR | unsigned char | Paddle-TipIn |
| STAT_0_4_FIFIR_PADDEL_TIP_IN_TEXT | string | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_0_5_FIFR_EL_DRIVE_NOT_EFFICIENT_NR | unsigned char | eDrive nicht effizient |
| STAT_0_5_FIFR_EL_DRIVE_NOT_EFFICIENT_TEXT | string | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_0_6_FIFR_REMEDIAL_ACTIONS_DISALLOW_M1_NR | unsigned char | Remedial Actions erlauben M1 nicht |
| STAT_0_6_FIFR_REMEDIAL_ACTIONS_DISALLOW_M1_TEXT | string | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_0_7_FIFR_ALL_OTHER_REASONS_NR | unsigned char | Remedial Actions erlauben M1 nicht |
| STAT_0_7_FIFR_ALL_OTHER_REASONS_TEXT | string | Ursache der Abschaltverhinderung 0= nein/1=ja |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-momentenaufteilung-beschleunigen"></a>
### STATUS_MOMENTENAUFTEILUNG_BESCHLEUNIGEN

Anteil des verbrennungsmotorischen Momentes am gesamten Antriebsmoment $22     SID ReadDataByIdentifier $02 $01 DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOMENTENAUFTEILUNG_BESCHLEUNIGEN_WERT | real | TO-Anteil der mechanischen Bremse in Prozent E-Anteil wäre der Kehrwert 0 bis 100 "%" Aufloesung: 1 "%" |
| STAT_MOMENTENAUFTEILUNG_BESCHLEUNIGEN_EINH | string | Einheit des Momentes |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-aktivierung-laden-hv-batterie"></a>
### STATUS_AKTIVIERUNG_LADEN_HV_BATTERIE

Status des Ladevorgangs $22   SID ReadDataByIdentifier $02 $02 DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LADEVORGANG_BATTERIE_AKTIV | string | Status des Ladevorgangs 0= inaktive/1=aktiv |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-apm-jumpassist"></a>
### STATUS_APM_JUMPASSIST

Zustände des Jump Assist $22     SID ReadDataByIdentifier $02 $03 DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_APM_JUMP_ASSIST_MODE_NR | unsigned char | Zustände des Jump Assist 0= Funktion nicht verfügbar oder angefordert 1= Funktion angefordert 2= KL15 geschaltet/ Ladegerät auf 12V Seite angeschlossen Ladespannung &gt;13,2V 3= Ladung der HV Batterie läuft 4= Ladung abgeschlossen 5= Abgebrochen weil Netztteil zu klein/ Klemmenzustand geändert |
| STAT_APM_JUMP_ASSIST_MODE_TEXT | string | Zustände des Jump Assist als Text |
| STAT_APM_ASSIST_LADESTROM_WERT | unsigned int | Ladestrom des Jumpassist Bereich: 0-5 A Aufloesung: 0.1 A |
| STAT_APM_ASSIST_LADESTROM_EINH | string | Einheit des Stroms |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-ekk-abschaltbedingung"></a>
### STATUS_EKK_ABSCHALTBEDINGUNG

Grund fuer die Abschaltung des Klimakompressors $22     SID ReadDataByIdentifier $02 $07 DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EKK_ABSCHALTBEDINGUNG_AKTIV | unsigned char | Sammelstatus Abschaltgrund Klimakompressors 0 = nein(Abschaltung aktiv), 1 = ja(kein Abschaltgrund aktiv) |
| STAT_EKK_ABSCHALTBEDINGUNG_BATTERIE_AKTIV | unsigned char | Batterie als Abschaltgrund fuer den Klimakompressors 0 = nein/1 = ja |
| STAT_EKK_ABSCHALTBEDINGUNG_JUMPASSIST_AKTIV | unsigned char | Jumpassistent als Abschaltgrund fuer den Klimakompressors 0 = nein/1 = ja |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-ekk-leistungslimitierung-boost"></a>
### STATUS_EKK_LEISTUNGSLIMITIERUNG_BOOST

Leistungslimitierung als Grund fuer die Abschaltung des Klimakompressor $22     SID ReadDataByIdentifier $02 $08 DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EKK_LEISTUNGSLIMITIERUNG_BOOST_WERT | real | Leistungslimitierung als Grund fuer die Abschaltung des Klimakompressor 0 bis 20000 W Aufloesung: 500 W |
| STAT_EKK_LEISTUNGSLIMITIERUNG_BOOST_EINH | string | Einheit der Leistung |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-ekk-leistungslimitierung-revgrade"></a>
### STATUS_EKK_LEISTUNGSLIMITIERUNG_REVGRADE

Rueckwaertssteigfaehigkeit als Grund fuer die Abschaltung des Klimakompressor $22     SID ReadDataByIdentifier $02 $09 DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EKK_LEISTUNGSLIMITIERUNG_REVGRADE_WERT | real | Rueckwaertssteigfaehigkeit als Grund fuer die Abschaltung des Klimakompressor 0 bis 20000 W Aufloesung: 500 W |
| STAT_EKK_LEISTUNGSLIMITIERUNG_REVGRADE_EINH | string | Einheit der Leistung |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-momentenaufteilung-bremsen"></a>
### STATUS_MOMENTENAUFTEILUNG_BREMSEN

TO-Anteil der Mechanischen Bremse Reku-Anteil wäre der Kehrwert $22     SID ReadDataByIdentifier $02 $05 DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOMENT_BREMSEN_WERT | real | 0 bis 100 "%" Aufloesung: 1 "%" |
| STAT_MOMENT_BREMSEN_EINH | string | Einheit des Momentes |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-empi"></a>
### STATUS_EMPI

EMPI HV Stromwert, EMPI Mode, Drehzahl absolut/relativ $22     SID ReadDataByIdentifier $02 $0A DID HV Stromwert $02 $0B DID EMPI Mode Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EMPI_DREHZAHL_WERT | real | Gibt die aktuelle Drehzahl in 1/min aus |
| STAT_EMPI_DREHZAHL_EINH | string | Einheit der Drehzahl |
| STAT_EMPI_DREHZAHL_PROZENT_WERT | real | Gibt die aktuelle Drezahl in Prozent aus 1250 1/min entspricht 100 % Wertebereich: 0-100 % |
| STAT_EMPI_DREHZAHL_PROZENT_EINH | string | Drehzahl in "%" |
| STAT_EMPI_HV_STROM_WERT | real | Gibt den HV Stromwert zurück |
| STAT_EMPI_HV_STROM_EINH | string | Einheit des Stroms |
| STAT_EMPI_MODE_NR | unsigned char | Aktueller Mode der EMPI 0= Off mode 1= Speed control mode 2= Standby mode 3= Fault mode 4= Not Used 5= Not Used 6= Not Used 7= Signal Not Available |
| STAT_EMPI_MODE_TEXT | string | Aktueller Mode der EMPI als Text |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST01 | binary | Hex-Auftrag an SG |
| _RESPONSE01 | binary | Hex-Antwort von SG |
| _REQUEST03 | binary | Hex-Auftrag an SG |
| _RESPONSE03 | binary | Hex-Antwort von SG |
| _REQUEST04 | binary | Hex-Auftrag an SG |
| _RESPONSE04 | binary | Hex-Antwort von SG |

<a id="job-status-hcp-antriebsart"></a>
### STATUS_HCP_ANTRIEBSART

Rückmeldung der aktuell anliegenden Antriebsart z.B.: E-Fahren, Rekuperation, Boost etc. $22     SID ReadDataByIdentifier $02 $13 DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HCP_ANTRIEBSART_NR | unsigned char | Aktuell anliegende Antriebsart 1= kein Wert 2= Energierückgewinnung durch Rekuperation 3= Lastpunktanhebung 4= Elektrisches Fahren 5= Elektrisches Boosten 6= Lastpunktabsenkung 7= Motorstopautomatik 8= Batteriestandladen 9= Regeneratives Bremsen |
| STAT_HCP_ANTRIEBSART_TEXT | string | Aktuell anliegende Antriebsart als Text |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-hpmr-state"></a>
### STATUS_HPMR_STATE

Status des HPMR auslesen $22 SID ReadDataByIdentifier $02 $13 DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HPMR_STATE_NR | unsigned char | Status des HPMR 0= POWERUP 1= EVAL_BP_CLOSE (Evaluation Batteriepack Contactors Close) 2= DET_BP_CLOSED (Determine Batteriepack Contactors Closed) 3= EVAL_INV_ENABLE (Evaluation Inverter Enable) 4= DET_INV_ENABLED (Determine Inverter Enabled) 5= EVAL_ENG_SYS (Evaluation Engine System) 6= EVAL_REKEY_ALLOWED (Evaluatio Rekey Allowed) 7= OPERATIONAL 8= DET_ENG_STOPPED (Determine Engine Stopped) 9= DET_INV_DISABLED (Determine Inverter Disabled) 10= EVAL_BP_OPEN (Evaluation Batteripack Open) 11= DET_BP_OPENED (Determine Batteripack Opened) 12= DET_BUS_DISCHARGED (Determine Highvoltage Bus Discharged) 13= SHUTDOWN 14= JUMP_ASSIST |
| STAT_HPMR_STATE_TEXT | string | Status des HPMR als Text |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-recuperationsmoment"></a>
### STATUS_RECUPERATIONSMOMENT

Ist-Wert Reku-Moment $22     SID ReadDataByIdentifier $02 $21 DID Messwert Ist-Wert zusätzliches Schubmoment $22     SID ReadDataByIdentifier $02 $0C DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SCHUBMOMENT_WERT | real | Ist-Wert Reku-Moment -2000Nm bis 2000 Nm Aufloesung: 1 Nm |
| STAT_SCHUBMOMENT_EINH | string | Einheit des Moments |
| STAT_BREMSMOMENT_WERT | real | Ist-Wert zusätzliches Schubmoment -2000Nm bis 2000 Nm Aufloesung: 1 Nm |
| STAT_BREMSMOMENT_EINH | string | Einheit des Moments |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST_01 | binary | Hex-Auftrag an SG |
| _RESPONSE_01 | binary | Hex-Antwort von SG |
| _REQUEST_02 | binary | Hex-Auftrag an SG |
| _RESPONSE_02 | binary | Hex-Antwort von SG |

<a id="job-status-wake-up"></a>
### STATUS_WAKE_UP

Gibt den Status der WakeUp-Leitung aus $22     SID ReadDataByIdentifier $02 $12 DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HYBRID_ACCESSORY_WAKE_UP_NR | unsigned char | Gibt den Status der Wake Up Leitung aus 0 = nicht aktiv, 1 = aktiv |
| STAT_HYBRID_ACCESSORY_WAKE_UP_TEXT | string | Status der Wake Up Leitung als Text |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-hv-isolation"></a>
### STATUS_HV_ISOLATION

Liest Isolationsstatus Batterie aus $22     SID ReadDataByIdentifier $02 $16 DID Messwert Liest Isolationsstatus des MCP A aus $22     SID ReadDataByIdentifier $02 $17 DID Messwert Liest Isolationsstatus des MCP B aus $22     SID ReadDataByIdentifier $02 $18 DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HV_ISOLATION_BATTERIE_NR | unsigned char | Isolationsstatus Batterie 0= Initialer Zustand der Batterie Zustand unklar 1= Kein Isolationsfehler aus Sicht der Batterie 2= Isolationsfehler aus Sicht der Batterie |
| STAT_HV_ISOLATION_BATTERIE_TEXT | string | Isolationsstatus Batterie als Text |
| STAT_HV_ISOLATION_MCPA_NR | unsigned char | Isolationsstatus MCP A 0= Initialer Zustand der PEB, d.h. Zustand unklar 1= Kein Isolationsfehler aus Sicht der PEB 2= Isolationsfehler aus Sicht der PEB |
| STAT_HV_ISOLATION_MCPA_TEXT | string | Isolationsstatus MCP A als Text |
| STAT_HV_ISOLATION_MCPB_NR | unsigned char | Isolationsstatus MCP B 0= Initialer Zustand der PEB, d.h. Zustand unklar 1= Kein Isolationsfehler aus Sicht der PEB 2= Isolationsfehler aus Sicht der PEB |
| STAT_HV_ISOLATION_MCPB_TEXT | string | Isolationsstatus MCP B als Text |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST01 | binary | Hex-Auftrag an SG |
| _RESPONSE01 | binary | Hex-Antwort von SG |
| _REQUEST02 | binary | Hex-Auftrag an SG |
| _RESPONSE02 | binary | Hex-Antwort von SG |
| _REQUEST03 | binary | Hex-Auftrag an SG |
| _RESPONSE03 | binary | Hex-Antwort von SG |

<a id="job-status-hvil"></a>
### STATUS_HVIL

Auslesen des HVIL-Zustandes (falls HVIL unterbrochen, dann n.i.O.) $22     SID ReadDataByIdentifier $02 $19 DID Messwert Auslesen des HVIL-Zustandes aus Sicht der PEB fuer MCP A $22     SID ReadDataByIdentifier $02 $1B DID Messwert Auslesen des HVIL-Zustandes aus Sicht der PEB fuer MCP B $22     SID ReadDataByIdentifier $02 $1C DID Messwert Auslesen des HVIL-Zustandes aus Sicht der Batterie $22     SID ReadDataByIdentifier $02 $1A DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HVIL_NR | unsigned char | HVIL-Zustand (falls HVIL unterbrochen, dann n.i.O.) 0 = HVIL wird nicht bestromt oder Initialer Zustand des BPCM (HV Zustand unklar) 1 = HVIL ist geschlossen (HV kann aktiv sein) 2 = HVIL ist offen (Service kann an HV Arbeiten wenn 'service disconnect' entfernt und gegen Wiedereinschalten gesichert ist |
| STAT_HVIL_TEXT | string | HVIL-Zustand als Text table T_HVIL_GESAMT WERT TEXT |
| STAT_HVIL_MCPA_FAILED | string | HVIL-Zustandes aus Sicht der PEB fuer MCP A 0 = HVIL ist aus Sicht PEB geschlossen 1 = HVIL ist aus Sicht PEB offen |
| STAT_HVIL_MCPB_FAILED | string | HVIL-Zustandes aus Sicht der PEB fuer MCP B 0 = HVIL ist aus Sicht PEB geschlossen 1 = HVIL ist aus Sicht PEB offen |
| STAT_HV_BATTERIE_NR | unsigned char | HVIL-Zustand aus Sicht der Batterie 0 = HVIL wird aus sicht der Batterie nicht bestromt 1 = HVIL ist aus sicht der Batterie geschlossen (HV kann aktiv sein) 2 = HVIL ist aus sicht der Batterie offen (Service kann an HV Arbeiten wenn service Disconnect entfernt und gegen widereinschalten gesichert ist |
| STAT_HV_BATTERIE_TEXT | string | HVIL-Zustand als Text table T_HVIL_BATTERIE WERT TEXT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST01 | binary | Hex-Auftrag an SG |
| _RESPONSE01 | binary | Hex-Antwort von SG |
| _REQUEST02 | binary | Hex-Auftrag an SG |
| _RESPONSE02 | binary | Hex-Antwort von SG |
| _REQUEST03 | binary | Hex-Auftrag an SG |
| _RESPONSE03 | binary | Hex-Antwort von SG |
| _REQUEST04 | binary | Hex-Auftrag an SG |
| _RESPONSE04 | binary | Hex-Antwort von SG |

<a id="job-status-kl-15"></a>
### STATUS_KL_15

Gibt den Status der Klemme 15 aus $22     SID ReadDataByIdentifier $02 $23 DID Messwert Gibt den Spannungswert der Klemme 15 aus $22     SID ReadDataByIdentifier $02 $24 DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KL_15_EIN | string | Status der Klemme 15 als Text |
| STAT_KL_15_VOLTAGE_WERT | real | -32 bis 32 V Aufloesung: 0.25 V |
| STAT_KL_15_VOLTAGE_EINH | string | Einheit der Spannung |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST01 | binary | Hex-Auftrag an SG |
| _RESPONSE01 | binary | Hex-Antwort von SG |
| _REQUEST02 | binary | Hex-Auftrag an SG |
| _RESPONSE02 | binary | Hex-Antwort von SG |

<a id="job-steuern-antriebsart"></a>
### STEUERN_ANTRIEBSART

Auswahl: Forciertes E-Fahren, explizites Nicht E-Fahren, normal $2E     SID ReadDataByIdentifier $F2 $2  DID Messwert Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANTRIEBSART | unsigned char | Werttabelle 0 = Geregelte Einstellung 1 = Nur elektrisches Fahren 2 = Nur mit Verbrennungsmotor fahren |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-apm"></a>
### STEUERN_APM

Setzen das APM in einen bestimmten Betriebsmodus HV-Sicherheitskonzept wird nicht überstimmt!! Eingangsbedingungen werden über CCM im Kombi angezeigt $2E       SID ReadDataByIdentifier $F2 $0  DID Messwert Steuern der LV-Output-Spannung der APM. Eingabe der Spannung in Volt. $2E       SID ReadDataByIdentifier $F2 $4  DID Messwert Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | unsigned char | Wertetabelle 0= AUS 1= Buck 2= Boost |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST01 | binary | Hex-Auftrag an SG |
| _RESPONSE01 | binary | Hex-Antwort von SG |
| _REQUEST02 | binary | Hex-Auftrag an SG |
| _RESPONSE02 | binary | Hex-Antwort von SG |

<a id="job-steuern-apm-limit"></a>
### STEUERN_APM_LIMIT

Aktivierung/Deaktivieren der Limitierung $2E     SID ReadDataByIdentifier $F2 $3  DID Messwert Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION | unsigned char | Werttabelle 0 = inaktiv 1 = aktiv |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-energiesparmode"></a>
### STEUERN_ENERGIESPARMODE

Steuern der des Energiesparmodes (FETRAWE) Ist Klemmensicher und mit DTC-Eintrag verbunden $2E     SID ReadDataByIdentifier $F2 $5  DID Messwert Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION | unsigned char | Werttabelle 0 = inaktiv 1 = Fertigungsmode 2 = Transportmode 3 = FE+TRA 4 = Werkstattmode 5 = FE+WE 6 = WE+TRA 7 = FE+TRA+W |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-engdsrd"></a>
### STEUERN_ENGDSRD

Externe Steuerung des Motorstatus Hinweis: ENERGIESPARMODE muss aktiviert sein und STEUERN_COMPLETECONTROL_SCHALTER ausgeführt werden. $2E     SID ReadDataByIdentifier $F2 $6  DID Messwert Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION | unsigned char | Werttabelle 0 = kein Zugriff 1 = an 2 = aus |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-laden-hv-batterie"></a>
### STEUERN_LADEN_HV_BATTERIE

Einschalten/Ausschalten der Ladefunktion $2E     SID ReadDataByIdentifier $F2 $1  DID Messwert Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION | unsigned char | Einschalten/Ausschalten der Ladefunktion Wertetabelle 0 = aus 1 = START 2 = Standby 3 = Neustart 4 = Laden unterdruecken |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ll-drehzahl"></a>
### STEUERN_LL_DREHZAHL

Sollvorgabe Verbrennungsmotor-Drehzahl in Neutral $2E     SID ReadDataByIdentifier $F2 $8  DID Messwert Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DREHZAHL | real | Verbrennungsmotor-Drehzahl in Neutral 0 = AUS/OFF 0 U/min bis 8000 U/min Aufloesung: 10 U/min |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | ex-Antwort von SG |

<a id="job-steuern-ni-mode-1"></a>
### STEUERN_NI_MODE_1

Sollvorgabe Verbrennungsmotor-Drehzahl in Mode 1 Hinweis: ENERGIESPARMODE muss aktiviert sein und STEUERN_COMPLETECONTROL_SCHALTER ausgeführt werden. $2E     SID ReadDataByIdentifier $F2 $0A DID Messwert Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DREHZAHL | real | Verbrennungsmotor-Drehzahl in Mode 1 0 = AUS/OFF 0 U/min bis 8000 U/min Aufloesung: 10 U/min |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ni-mode-2"></a>
### STEUERN_NI_MODE_2

Sollvorgabe Verbrennungsmotor-Drehzahl in Mode 2 Hinweis: ENERGIESPARMODE muss aktiviert sein und STEUERN_COMPLETECONTROL_SCHALTER ausgeführt werden. $2E     SID ReadDataByIdentifier $F2 $0B ADID Messwert Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DREHZAHL | real | Verbrennungsmotor-Drehzahl in Mode 2 0 = AUS/OFF 0 U/min bis 8000 U/min Aufloesung: 10 U/min |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-rngdsrd"></a>
### STEUERN_RNGDSRD

Vorgabe Gang für OHSR-Schnittstelle Hinweis: ENERGIESPARMODE muss aktiviert sein und STEUERN_COMPLETECONTROL_SCHALTER ausgeführt werden. $2E     SID ReadDataByIdentifier $F2 $0D DID Messwert Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GANG | unsigned char | Werttabelle 0 = N0 1 = M1 2 = M2 3 = G1 4 = G2 5 = G3 6 = G4 7 = M1Off 8 = N |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-antriebsart-zugriff"></a>
### STATUS_ANTRIEBSART_ZUGRIFF

Gibt den Status der aktuell anliegenden extern eingesteuerten Antriebsart an. $22     SID ReadDataByIdentifier $02 $31 DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANTRIEBSART_NR | unsigned char | Gibt den Status der aktuell anliegenden extern eingesteuerten Antriebsart an. 0= kein Wert 1= Sicher AUS/OFF 2= Vollzugriff 3= exclusive E-Fahren bzw. Verbrennen |
| STAT_ANTRIEBSART_TEXT | string | Status der Antriebsart als Text. |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-batt-conn"></a>
### STATUS_BATT_CONN

Gibt an ob das Batterie-Schütz /Relais betätigt ist. $22     SID ReadDataByIdentifier $02 $29 DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BATTERIE_SCHUETZ_NR | unsigned char | Status Batterie-Schütz /Relais 0= Schuetz offen 1= Vorladung aktiv 2= geschlossen 3= Vorladung fehlgeschlagen 4= Vorladung verboten |
| STAT_BATTERIE_SCHUETZ_TEXT | string | Status Batterie-Schütz /Relais als Text |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-e-motor-control-check"></a>
### STATUS_E_MOTOR_CONTROL_CHECK

Liest die erzielte E-Maschinen Drehzahl nach E-Motor Control Check aus. $22   SID ReadDataByIdentifier $02 $30 DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_E_MOTOR_CONTROL_CHECK_DREHZAHL_MOTOR_A_WERT | real | Drehzahl der E-Maschine A nach dem Control Check Motor A in 1/min -65535 bis 65535 |
| STAT_E_MOTOR_CONTROL_CHECK_DREHZAHL_MOTOR_A_EINH | string | Einheit der Drehzahl |
| STAT_E_MOTOR_CONTROL_CHECK_DREHZAHL_MOTOR_B_WERT | real | Drehzahl der E-Maschine B nach dem Control Check Motor B in 1/min -65535 bis 65535 |
| STAT_E_MOTOR_CONTROL_CHECK_DREHZAHL_MOTOR_B_EINH | string | Einheit der Drehzahl |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-energiesparmode"></a>
### STATUS_ENERGIESPARMODE

Rückgabe des aktuell anliegenenden FETRAWE-Status. Hinweis: Nur in Verbindung mit Energiesparmode Werkstatt. Fehlereintrag wird beim Setzen angelegt. $22     SID ReadDataByIdentifier $02 $XX DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AKTION_NR | unsigned char | Rückgabe des aktuell anliegenenden FETRAWE-Status 0 = inaktiv 1 = Fertigungsmode 2 = Transportmode 3 = FE+TRA 4 = Werkstattmode 5 = FE+WE 6 = WE+TRA 7 = FE+TRA+W |
| STAT_AKTION_TEXT | string | Rückgabe des aktuell anliegenenden FETRAWE-Status als Text |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-io-lesen"></a>
### STATUS_IO_LESEN

Rückgabe des aktuellen Ist- Ganges. $22     SID ReadDataByIdentifier $02 $2C DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ISTGANG | unsigned char | Rückgabe des aktuellen Ist- Ganges |
| STAT_ISTGANG_TEXT | string | Wertetabelle: 0=  ungueltig 1=  1.Gang 2=  2.Gang 3=  3.Gang 4=  4.Gang 5=  5.Gang 6=  6.Gang 7=  7.Gang 60= Neutral 70= Rueckwaerts 80= Park 255=unbekannter Gang |
| STAT_ISTRANGE | unsigned char | Rueckgabe des aktuellen Ist-Range |
| STAT_ISTRANGE_TEXT | string | Wert definiert in T_TextIstRange |
| STAT_IST_I_WERT | real | Rueckgabe der aktuellen Getriebe-Uebersetzung |
| STAT_IST_I_EINH | string | - |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-lesen-pwrlnch-counter"></a>
### STATUS_LESEN_PWRLNCH_COUNTER

Job liest die Anzahl der durchgeführten PowerLunches und die Anzahl der PowerLaunches nach dem letzten Reset aus. $22     SID ReadDataByIdentifier $02 $3F DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PWRLNCH_CONTIN_CNT_WERT | real | Anzahl aller durchgeführten PowerLaunches. 0 bis 65535 |
| STAT_PWRLNCH_CONTIN_CNT_EINH | string | Einheit des Zaehlers |
| STAT_PWRLNCH_CNT_WERT | real | Anzahl aller durchgeführten PowerLaunches seit Reset. 0 bis 65535 |
| STAT_PWRLNCH_CNT_EINH | string | Einheit des Zaehlers |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-ll-regelung"></a>
### STATUS_LL_REGELUNG

Rückmeldung ob Leerlaufregelung i.O. ist $22     SID ReadDataByIdentifier $02 $35 DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LL_REGLER_NR | unsigned char | Rückmeldung, ob Leerlaufregelung i.O. ist Wertetabelle 0= Diagnose noch nicht abgeschlossen 1= LL-Drehzahl zu hoch 2= LL-Drehzahl zu niedrig 3= Diagnose i.O. abgeschlossen |
| STAT_LL_REGLER_TEXT | string | Rückmeldung der Leerlaufregelung als Text |
| STAT_LL_REGELABWEICHUNG_WERT | real | Rückmeldung Regelabweichungsintegral Aktuell anliegende LL-Regelabweichung Einheit 1/min Bereich:  -1E32 bis 1E32 |
| STAT_LL_REGELABWEICHUNG_EINH | string | Einheit der Regelabweichung |
| STAT_LEERLAUF_AKTIV | unsigned char | Gibt zurück ob sich das System in einem Zustand befindet, welches dem herkoemmlichen Zustand Leerlauf am naechsten kommt. 0= nicht aktiv 1= aktiv |
| STAT_LEERLAUF_AKTIV_TEXT | string | 0= nicht aktiv 1= aktiv |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-parksensoren"></a>
### STATUS_PARKSENSOREN

Liest den plausibilitierten Zustand der Parksensoren (TCM und DSM) aus. $22     SID ReadDataByIdentifier $02 $27 DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PARKSENSOREN_NR | unsigned char | Plausibilitierten Zustand der Parksensoren (TCM und DSM) aus. 0= Zustand unbestimmt 1= Park eingelegt 2= Park ausgelegt 3= Ungültig |
| STAT_PARKSENSOREN_TEXT | string | Plausibilitierten Zustand der Parksensoren (TCM und DSM) als Text |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-soc-acc-lesen"></a>
### STATUS_SOC_ACC_LESEN

Rückgabe der Güte des SOC-Wertes. $22     SID ReadDataByIdentifier $02 $2D DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SOC_ACC_WERT | real | Rückgabe der Güte des SOC-Wertes. 0 bis 100 % Aufloesung: 1 % |
| STAT_SOC_ACC_EINH | string | "%" |
| STAT_SOC_WERT | real | Rückgabe des SOC-Wertes in Prozent. 0 bis 100 % Aufloesung: 1 % |
| STAT_SOC_EINH | string | "%" |
| STAT_SOC_ACC_SFA_WERT | real | Rückgabe der Güte des SOC_SFA-Wertes. 0 bis 100 % Aufloesung: 1 % |
| STAT_SOC_ACC_SFA_EINH | string | "%" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-completecontrol-schalter"></a>
### STEUERN_COMPLETECONTROL_SCHALTER

Schalter für Completecontrol Darf nicht im Service ausgeführt werden $2E     SID WriteDataByIdentifier $F2 $18 DID Messwert Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SCHALTER_COMPLETECONTROL | unsigned char | Schalter für Completecontrol Werttabelle 0 = AUS 1 = EIN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-erzwungene-schubabschaltung"></a>
### STEUERN_ERZWUNGENE_SCHUBABSCHALTUNG

Kann die Schubabschaltung erzwingen. FETRAWE-Mode muss gesetzt sein $2E     SID WriteDataByIdentifier $F2 $19 DID Messwert Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION | unsigned char | Kann die Schubabschaltung erzwingen. Werttabelle 0 = AUS 1 = EIN(Schubabschaltung erzwingen) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-kompressionstest"></a>
### STATUS_KOMPRESSIONSTEST

Liest die Variablen zum Kompressionstest aus. $22   SID ReadDataByIdentifier $02 $52 DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TESTERGEBNIS_NR | unsigned char | Ergebnis des Testergebnisses |
| STAT_TESTERGEBNIS_TEXT | string | Wertetabelle 0= Kein Ergebnis 1= i.O. 2= n.i.O. |
| STAT_ABWEICHUNG_WERT | real | Kompressionstest Fehlerabweichung Drehmoment in Nm 0 bis 32000 Nm |
| STAT_ABWEICHUNG_EINH | string | "Nm" |
| STAT_KOMPR_TESTFREIGABE_NR | unsigned char | Ergebnis des Testfreigabe |
| STAT_KOMPR_TESTFREIGABE_TEXT | string | Wertetabelle 0= nein 1= ja |
| STAT_KOMPR_TEST_AKTIV_NR | unsigned char | Test aktiv/nicht aktiv |
| STAT_KOMPR_TEST_AKTIV_TEXT | string | Wertetabelle 0= nein 1= ja |
| STAT_KOMPR_TEST_BEENDET_NR | unsigned char | Kompressions Test beendet |
| STAT_KOMPR_TEST_BEENDET_TEXT | string | Wertetabelle 0= nein 1= ja |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-kompressionstest"></a>
### STEUERN_KOMPRESSIONSTEST

Schaltet Kompressionstest VM an ENERGIEPARMODE muss an sein $2E       SID WriteDataByIdentifier $F2 $1D   DID Messwert Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION | unsigned char | Schaltet Kompressionstest VM an ENERGIEPARMODE muss an sein Werttabelle 0= AUS 1= EIN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-pwrlnch-cnt-reset"></a>
### STEUERN_PWRLNCH_CNT_RESET

Job zum Resettieren/Zurücksetzen des PowerLaunch Zählers. Hinweis: Nur in Verbindung mit Energiesparmode Werkstatt Keine Übergabeparameter $2E     SID WriteDataByIdentifier $F2 $15 DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-soc-soll"></a>
### STEUERN_SOC_SOLL

Schaltet SOC Vorgabe an ENERGIEPARMODE muss an sein Aus nach 300s $2E      SID WriteDataByIdentifier $F2 $1C  DID Messwert Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION | unsigned char | Schaltet SOC Vorgabe an Werttabelle 0 = AUS 1 = EIN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-soc-soll-wert"></a>
### STEUERN_SOC_SOLL_WERT

Sollvorgabe SOC, nur innerhalb der i.O. Grenzen, nur in Verbindung mit FETRAWE Vorher muss der Job STEUERN_SOC_SOLL ausgeführt werden 0=AUS oder nach 1200s $22     SID ReadDataByIdentifier $02 $1B DID Messwert Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PROZENT | unsigned char | Sollvorgabe SOC, nur innerhalb der i.O. Grenzen ENERGIEPARMODE muss an sein Bereich: 34- 75 % Aufloesung:  1 % |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-degradation-source"></a>
### STATUS_DEGRADATION_SOURCE

Rückmeldung Ursache der aktuellen Degradation im Fzg

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DEGR_MOMENT_EMOT_A_TEMP_EMOT_A_AKTIV | unsigned char | Degradation Moment E-Maschine A durch Temperatur E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_EMOT_A_TEMP_EMOT_A_AKTIV_TEXT | string | Degradation Moment E-Maschine A durch Temperatur E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_EMOT_A_TEMP_INVERTER_EMOT_A_AKTIV | unsigned char | Degradation Moment E-Maschine A durch Temperatur Inverter E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_EMOT_A_TEMP_INVERTER_EMOT_A_AKTIV_TEXT | string | Degradation Moment E-Maschine A durch Temperatur Inverter E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_EMOT_A_TEMP_GETR_OEL_AKTIV | unsigned char | Degradation Moment E-Maschine A durch Temperatur Getriebeöl 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_EMOT_A_TEMP_GETR_OEL_AKTIV_TEXT | string | Degradation Moment E-Maschine A durch Temperatur Getriebeöl 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_RESERVE_1_3_AKTIV | unsigned char | - - |
| STAT_RESERVE_1_3_AKTIV_TEXT | string | - - |
| STAT_DEGR_MOMENT_EMOT_A_TEMP_APM_AKTIV | unsigned char | Degradation Moment E-Maschine A durch Temperatur APM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_EMOT_A_TEMP_APM_AKTIV_TEXT | string | Degradation Moment E-Maschine A durch Temperatur APM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_EMOT_B_TEMP_EMOT_B_AKTIV | unsigned char | Degradation Moment E-Maschine B durch Temperatur E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_EMOT_B_TEMP_EMOT_B_AKTIV_TEXT | string | Degradation Moment E-Maschine B durch Temperatur E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_EMOT_B_TEMP_INVERTER_EMOT_B_AKTIV | unsigned char | Degradation Moment E-Maschine B durch Temperatur Inverter E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_EMOT_B_TEMP_INVERTER_EMOT_B_AKTIV_TEXT | string | Degradation Moment E-Maschine B durch Temperatur Inverter E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_RESERVE_1_7_AKTIV | unsigned char | - - |
| STAT_RESERVE_1_7_AKTIV_TEXT | string | - - |
| STAT_DEGR_MOMENT_EMOT_B_TEMP_APM_AKTIV | unsigned char | Degradation Moment E-Maschine B durch Temperatur APM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_EMOT_B_TEMP_APM_AKTIV_TEXT | string | Degradation Moment E-Maschine B durch Temperatur APM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_EMOT_B_TEMP_GETR_OEL_AKTIV | unsigned char | Degradation Moment E-Maschine B durch Temperatur Getriebeöl 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_EMOT_B_TEMP_GETR_OEL_AKTIV_TEXT | string | Degradation Moment E-Maschine B durch Temperatur Getriebeöl 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_ENTLADELEISTUNG_FAHRMODUS_AKTIV | unsigned char | Degradation Batterie-Entladeleistung durch Fahrmodus 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_ENTLADELEISTUNG_FAHRMODUS_AKTIV_TEXT | string | Degradation Batterie-Entladeleistung durch Fahrmodus 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_ENTLADELEISTUNG_TEMP_HV_SPEICHER_AKTIV | unsigned char | Degradation Batterie-Entladeleistung durch Temperatur HV-Speicher 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_ENTLADELEISTUNG_TEMP_HV_SPEICHER_AKTIV_TEXT | string | Degradation Batterie-Entladeleistung durch Temperatur HV-Speicher 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_ENTLADELEISTUNG_SOC_AKTIV | unsigned char | Degradation Batterie-Entladeleistung durch SOC 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_ENTLADELEISTUNG_SOC_AKTIV_TEXT | string | Degradation Batterie-Entladeleistung durch SOC 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_ENTLADELEISTUNG_FAHRMODUS_EDRIVE_AKTIV | unsigned char | Degradation Batterie-Entladeleistung durch Fahrmodus bei eDrive 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_ENTLADELEISTUNG_FAHRMODUS_EDRIVE_AKTIV_TEXT | string | Degradation Batterie-Entladeleistung durch Fahrmodus bei eDrive 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_ENTLADELEISTUNG_TMP_HV_SPEICH_EDRIVE_AKTIV | unsigned char | Degradation Batterie-Entladeleistung durch Temperatur HV-Speicher bei eDrive 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_ENTLADELEISTUNG_TMP_HV_SPEICH_EDRIVE_AKTIV_TEXT | string | Degradation Batterie-Entladeleistung durch Temperatur HV-Speicher bei eDrive 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_ENTLADELEISTUNG_SOC_EDRIVE_AKTIV | unsigned char | Degradation Batterie-Entladeleistung durch SOC bei eDrive 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_ENTLADELEISTUNG_SOC_EDRIVE_AKTIV_TEXT | string | Degradation Batterie-Entladeleistung durch SOC bei eDrive 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_LADELEISTUNG_TEMP_HV_SPEICHER_AKTIV | unsigned char | Degradation Batterie-Ladeleistung durch Temperatur HV-Speicher 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_LADELEISTUNG_TEMP_HV_SPEICHER_AKTIV_TEXT | string | Degradation Batterie-Ladeleistung durch Temperatur HV-Speicher 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_LADELEISTUNG_SOC_AKTIV | unsigned char | Degradation Batterie-Ladeleistung durch SOC 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_LADELEISTUNG_SOC_AKTIV_TEXT | string | Degradation Batterie-Ladeleistung durch SOC 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_VMOT_TEMP_EMOT_A_AKTIV | unsigned char | Degradation Verbrennungsmotormoment durch Temperatur E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_VMOT_TEMP_EMOT_A_AKTIV_TEXT | string | Degradation Verbrennungsmotormoment durch Temperatur E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_VMOT_TEMP_EMOT_B_AKTIV | unsigned char | Degradation Verbrennungsmotormoment durch Temperatur E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_VMOT_TEMP_EMOT_B_AKTIV_TEXT | string | Degradation Verbrennungsmotormoment durch Temperatur E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_RESERVE_1_20_AKTIV | unsigned char | - - |
| STAT_RESERVE_1_20_AKTIV_TEXT | string | - - |
| STAT_DEGR_MOMENT_VMOT_TEMP_INVERTER_EMOT_A_AKTIV | unsigned char | Degradation Verbrennungsmotormoment durch Temperatur Inverter E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_VMOT_TEMP_INVERTER_EMOT_A_AKTIV_TEXT | string | Degradation Verbrennungsmotormoment durch Temperatur Inverter E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_VMOT_TEMP_INVERTER_EMOT_B_AKTIV | unsigned char | Degradation Verbrennungsmotormoment durch Temperatur Inverter E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_VMOT_TEMP_INVERTER_EMOT_B_AKTIV_TEXT | string | Degradation Verbrennungsmotormoment durch Temperatur Inverter E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_VMOT_TEMP_WMK_AKTIV | unsigned char | Degradation Verbrennungsmotormoment durch Temperatur WMK 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_VMOT_TEMP_WMK_AKTIV_TEXT | string | Degradation Verbrennungsmotormoment durch Temperatur WMK 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_EKK_TEMP_WMK_AKTIV | unsigned char | Degradation elektr. Klimakompressor durch Temperatur WMK 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_EKK_TEMP_WMK_AKTIV_TEXT | string | Degradation elektr. Klimakompressor durch Temperatur WMK 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_EKK_TEMP_EMOT_A_AKTIV | unsigned char | Degradation elektr. Klimakompressor durch Temperatur E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_EKK_TEMP_EMOT_A_AKTIV_TEXT | string | Degradation elektr. Klimakompressor durch Temperatur E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_EKK_TEMP_EMOT_B_AKTIV | unsigned char | Degradation elektr. Klimakompressor durch Temperatur E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_EKK_TEMP_EMOT_B_AKTIV_TEXT | string | Degradation elektr. Klimakompressor durch Temperatur E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_EKK_TEMP_GETR_OEL_AKTIV | unsigned char | Degradation elektr. Klimakompressor durch Temperatur Getriebeöl 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_EKK_TEMP_GETR_OEL_AKTIV_TEXT | string | Degradation elektr. Klimakompressor durch Temperatur Getriebeöl 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_EKK_TEMP_VMOT_KUEHLM_AKTIV | unsigned char | Degradation elektr. Klimakompressor durch Temperatur Kühlmittel VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_EKK_TEMP_VMOT_KUEHLM_AKTIV_TEXT | string | Degradation elektr. Klimakompressor durch Temperatur Kühlmittel VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_EKK_TEMP_VMOT_OEL_AKTIV | unsigned char | Degradation elektr. Klimakompressor durch Temperatur Öl VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_EKK_TEMP_VMOT_OEL_AKTIV_TEXT | string | Degradation elektr. Klimakompressor durch Temperatur Öl VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_RESERVE_1_30_AKTIV | unsigned char | - - |
| STAT_RESERVE_1_30_AKTIV_TEXT | string | - - |
| STAT_DEGR_EKK_TEMP_HV_SPEICHER_AKTIV | unsigned char | Degradation elektr. Klimakompressor durch Temperatur HV-Speicher 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_EKK_TEMP_HV_SPEICHER_AKTIV_TEXT | string | Degradation elektr. Klimakompressor durch Temperatur HV-Speicher 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_RESERVE_2_0_AKTIV | unsigned char | - - |
| STAT_RESERVE_2_0_AKTIV_TEXT | string | - - |
| STAT_RESERVE_2_1_AKTIV | unsigned char | - - |
| STAT_RESERVE_2_1_AKTIV_TEXT | string | - - |
| STAT_RESERVE_2_2_AKTIV | unsigned char | - - |
| STAT_RESERVE_2_2_AKTIV_TEXT | string | - - |
| STAT_RESERVE_2_3_AKTIV | unsigned char | - - |
| STAT_RESERVE_2_3_AKTIV_TEXT | string | - - |
| STAT_RESERVE_2_4_AKTIV | unsigned char | - - |
| STAT_RESERVE_2_4_AKTIV_TEXT | string | - - |
| STAT_RESERVE_2_5_AKTIV | unsigned char | - - |
| STAT_RESERVE_2_5_AKTIV_TEXT | string | - - |
| STAT_RESERVE_2_6_AKTIV | unsigned char | - - |
| STAT_RESERVE_2_6_AKTIV_TEXT | string | - - |
| STAT_DEGR_MOMENT_GETR_TEMP_EMOT_A_AKTIV | unsigned char | Degradation Getriebeausgangsmoment durch Temperatur E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_GETR_TEMP_EMOT_A_AKTIV_TEXT | string | Degradation Getriebeausgangsmoment durch Temperatur E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_GETR_TEMP_EMOT_B_AKTIV | unsigned char | Degradation Getriebeausgangsmoment durch Temperatur E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_GETR_TEMP_EMOT_B_AKTIV_TEXT | string | Degradation Getriebeausgangsmoment durch Temperatur E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_GETR_TEMP_GETR_OEL_AKTIV | unsigned char | Degradation Getriebeausgangsmoment durch Temperatur Getriebeöl 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_GETR_TEMP_GETR_OEL_AKTIV_TEXT | string | Degradation Getriebeausgangsmoment durch Temperatur Getriebeöl 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_GETR_TEMP_VMOT_KUEHLM_AKTIV | unsigned char | Degradation Getriebeausgangsmoment durch Temperatur Kühlmittel VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_GETR_TEMP_VMOT_KUEHLM_AKTIV_TEXT | string | Degradation Getriebeausgangsmoment durch Temperatur Kühlmittel VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_GETR_TEMP_VMOT_OEL_AKTIV | unsigned char | Degradation Getriebeausgangsmoment durch Temperatur Öl VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_GETR_TEMP_VMOT_OEL_AKTIV_TEXT | string | Degradation Getriebeausgangsmoment durch Temperatur Öl VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_GETR_TEMP_HV_SPEICHER_AKTIV | unsigned char | Degradation Getriebeausgangsmoment durch Temperatur HV-Speicher 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_GETR_TEMP_HV_SPEICHER_AKTIV_TEXT | string | Degradation Getriebeausgangsmoment durch Temperatur HV-Speicher 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_EMOT_A_AKTIV | unsigned char | Degradation SOCR durch Temperatur E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_EMOT_A_AKTIV_TEXT | string | Degradation SOCR durch Temperatur E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_EMOT_B_AKTIV | unsigned char | Degradation SOCR durch Temperatur E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_EMOT_B_AKTIV_TEXT | string | Degradation SOCR durch Temperatur E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_INVERTER_EMOT_A_AKTIV | unsigned char | Degradation SOCR durch Temperatur Inverter E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_INVERTER_EMOT_A_AKTIV_TEXT | string | Degradation SOCR durch Temperatur Inverter E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_INVERTER_EMOT_B_AKTIV | unsigned char | Degradation SOCR durch Temperatur Inverter E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_INVERTER_EMOT_B_AKTIV_TEXT | string | Degradation SOCR durch Temperatur Inverter E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_VMOT_KUEHLM_AKTIV | unsigned char | Degradation SOCR durch Temperatur Kühlmittel VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_VMOT_KUEHLM_AKTIV_TEXT | string | Degradation SOCR durch Temperatur Kühlmittel VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_VMOT_OEL_AKTIV | unsigned char | Degradation SOCR durch Temperatur Öl VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_VMOT_OEL_AKTIV_TEXT | string | Degradation SOCR durch Temperatur Öl VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_GETR_OEL_AKTIV | unsigned char | Degradation SOCR durch Temperatur Getriebeöl 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_GETR_OEL_AKTIV_TEXT | string | Degradation SOCR durch Temperatur Getriebeöl 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_RESERVE_2_20_AKTIV | unsigned char | - - |
| STAT_RESERVE_2_20_AKTIV_TEXT | string | - - |
| STAT_DEGR_SOCR_TEMP_AMP_AKTIV | unsigned char | Degradation SOCR durch Temperatur APM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_AMP_AKTIV_TEXT | string | Degradation SOCR durch Temperatur APM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_EMOT_A_AKTIV | unsigned char | Degradation Rekuperation durch Temperatur E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_EMOT_A_AKTIV_TEXT | string | Degradation Rekuperation durch Temperatur E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_EMOT_B_AKTIV | unsigned char | Degradation Rekuperation durch Temperatur E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_EMOT_B_AKTIV_TEXT | string | Degradation Rekuperation durch Temperatur E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_GETR_OEL_AKTIV | unsigned char | Degradation Rekuperation durch Temperatur Getriebeöl 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_GETR_OEL_AKTIV_TEXT | string | Degradation Rekuperation durch Temperatur Getriebeöl 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_VMOT_KUEHLM_AKTIV | unsigned char | Degradation Rekuperation durch Temperatur Kühlmittel VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_VMOT_KUEHLM_AKTIV_TEXT | string | Degradation Rekuperation durch Temperatur Kühlmittel VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_VMOT_OEL_AKTIV | unsigned char | Degradation Rekuperation durch Temperatur Öl VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_VMOT_OEL_AKTIV_TEXT | string | Degradation Rekuperation durch Temperatur Öl VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_HV_SPEICHER_AKTIV | unsigned char | Degradation Rekuperation durch Temperatur HV-Speicher 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_HV_SPEICHER_AKTIV_TEXT | string | Degradation Rekuperation durch Temperatur HV-Speicher 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_SOC_AKTIV | unsigned char | Degradation Rekuperation durch SOC 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_SOC_AKTIV_TEXT | string | Degradation Rekuperation durch SOC 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_INVERTER_EMOT_A_AKTIV | unsigned char | Degradation Rekuperation durch Temperatur Inverter E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_INVERTER_EMOT_A_AKTIV_TEXT | string | Degradation Rekuperation durch Temperatur Inverter E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_INVERTER_EMOT_B_AKTIV | unsigned char | Degradation Rekuperation durch Temperatur Inverter E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_INVERTER_EMOT_B_AKTIV_TEXT | string | Degradation Rekuperation durch Temperatur Inverter E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_APM_AKTIV | unsigned char | Degradation Rekuperation durch Temperatur APM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_APM_AKTIV_TEXT | string | Degradation Rekuperation durch Temperatur APM 1=Degradation aktiv /0=Degradation nicht aktiv |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-strstp-zaehler"></a>
### STATUS_STRSTP_ZAEHLER

Liest den Historienspeicher der HCP hinsichtlich der Anzahl der absolvierten Starts aus.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STRSTP_CNT_KEYCRNKNORMAL_WERT | real | Anzahl der Start Vorgänge "Schlüsselstart normal" |
| STAT_STRSTP_CNT_KEYCRNKNORMAL_EINH | string | "-" keine Einheit da Zähler |
| STAT_STRSTP_CNT_KEYCRNKLOWPWR_WERT | real | Anzahl der Start Vorgänge "Schlüsselstart geringe Batterieleistung" |
| STAT_STRSTP_CNT_KEYCRNKLOWPWR_EINH | string | "-" keine Einheit da Zähler |
| STAT_STRSTP_CNT_KEYCRNKLOWPWRB_WERT | real | Anzahl der Start Vorgänge "Schlüsselstart geringe Batterieleistung (Applikation B)" |
| STAT_STRSTP_CNT_KEYCRNKLOWPWRB_EINH | string | "-" keine Einheit da Zähler |
| STAT_STRSTP_CNT_KEYCRNKGREENENG_WERT | real | Anzahl der Start Vorgänge "Jungfernstart (Werk)" |
| STAT_STRSTP_CNT_KEYCRNKGREENENG_EINH | string | "-" keine Einheit da Zähler |
| STAT_STRSTP_CNT_KEYCRNKGENERIC_WERT | real | Anzahl der Start Vorgänge "Schlüsselstart Typ Vorhalt" |
| STAT_STRSTP_CNT_KEYCRNKGENERIC_EINH | string | "-" keine Einheit da Zähler |
| STAT_STRSTP_CNT_ASTRTSMOOTH_WERT | real | Anzahl der Start Vorgänge "Autostart sanft" |
| STAT_STRSTP_CNT_ASTRTSMOOTH_EINH | string | "-" keine Einheit da Zähler |
| STAT_STRSTP_CNT_ASTRTNORMAL_WERT | real | Anzahl der Start Vorgänge "Autostart normal" |
| STAT_STRSTP_CNT_ASTRTNORMAL_EINH | string | "-" keine Einheit da Zähler |
| STAT_STRSTP_CNT_ASTRTAGGRSV_WERT | real | Anzahl der Start Vorgänge "Autostart aggressiv" |
| STAT_STRSTP_CNT_ASTRTAGGRSV_EINH | string | "-" keine Einheit da Zähler |
| STAT_STRSTP_CNT_ASTRTGENERIC_WERT | real | Anzahl der Start Vorgänge "Autostart vorhalt" |
| STAT_STRSTP_CNT_ASTRTGENERIC_EINH | string | "-" keine Einheit da Zähler |
| STAT_STRSTP_CNT_COMPRESSTST_WERT | real | Anzahl der Start Vorgänge "Motorstart Kompressionstest" |
| STAT_STRSTP_CNT_COMPRESSTST_EINH | string | "-" keine Einheit da Zähler |
| STAT_STRSTP_CNT_STOPCTRLD_WERT | real | Anzahl der Stop Vorgänge "Geregelter Stop" |
| STAT_STRSTP_CNT_STOPCTRLD_EINH | string | "-" keine Einheit da Zähler |
| STAT_STRSTP_CNT_STOPIMMED_WERT | real | Anzahl der Stop Vorgänge "Schlüssel- oder Notstop" |
| STAT_STRSTP_CNT_STOPIMMED_EINH | string | "-" keine Einheit da Zähler |
| STAT_LASTSTARTTYPE_NR | unsigned char | Gibt zurück, welcher Start Typ das letzte Mal vorhanden war Werttabelle: 0 = Kein Wert 1 = Schlüsselstart normal 2 = Schlüsselstart geringe Batterieleistung 3 = Schlüsselstart geringe Batterieleistung (Applikation B) 4 = Jungfernstart (Werk) 5 = Schlüsselstart Typ Vorhalt 6 = Autostart sanft 7 = Autostart normal 8 = Autostart aggressiv 9 = Autostart vorhalt 10= Motorstart Kompressionstest |
| STAT_LASTSTARTTYPE_TEXT | string | Letzter Start Typ als Text |
| STAT_LASTSTOPTYPE_NR | unsigned char | Gibt zurück, welcher Stop Typ das letzte Mal vorhanden war Werttabelle: 0 = Kein Wert 11= Geregelter Stop 12= Schlüssel- oder Notstop |
| STAT_LASTSTOPTYPE_TEXT | string | Letzter Stop Typ als Text |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-hisr-hos"></a>
### STATUS_HISR_HOS

Der Job gibt die Energieanteile und die Zeitanteile der verschieden Usecases /Modies an. Zusätzlich werden die Gesamtenergiemenge und die Gesamtzeit ausgegeben. Die Gesamtwerte können nicht zurückgesetzt werden.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ENERGIEANTEIL_REKUPERATION_WERT | real | Energieanteil Bremsrekuperation in Prozent |
| STAT_ENERGIEANTEIL_REKUPERATION_EINH | string | "%" |
| STAT_ENERGIEANTEIL_SCHUBREKUPERATION_WERT | real | Energieanteil Schubrekuperation in Prozent |
| STAT_ENERGIEANTEIL_SCHUBREKUPERATION_EINH | string | "%" |
| STAT_ENERGIEANTEIL_BREMSREKUPERATION_WERT | real | Energieanteil Bremsrekuperation in Prozent |
| STAT_ENERGIEANTEIL_BREMSREKUPERATION_EINH | string | "%" |
| STAT_ENERGIEANTEIL_LASTPUNKTANHEBUNG_WERT | real | Energieanteil Lastpunktanhebung in Prozent |
| STAT_ENERGIEANTEIL_LASTPUNKTANHEBUNG_EINH | string | "%" |
| STAT_ENERGIEANTEIL_ELEKTRISCH_FAHREN_WERT | real | Energieanteil elektrisch Fahren in Prozent |
| STAT_ENERGIEANTEIL_ELEKTRISCH_FAHREN_EINH | string | "%" |
| STAT_ENERGIEANTEIL_BOOST_WERT | real | Energieanteil Boost in Prozent |
| STAT_ENERGIEANTEIL_BOOST_EINH | string | "%" |
| STAT_ENERGIEANTEIL_ASSIST_WERT | real | Energieanteil Assist in Prozent |
| STAT_ENERGIEANTEIL_ASSIST_EINH | string | "%" |
| STAT_ENERGIEANTEIL_MSA_WERT | real | Energieanteil MSA in Prozent |
| STAT_ENERGIEANTEIL_MSA_EINH | string | "%" |
| STAT_ENERGIEANTEIL_STANDLADEN_WERT | real | Energieanteil Standladen in Prozent |
| STAT_ENERGIEANTEIL_STANDLADEN_EINH | string | "%" |
| STAT_ENERGIE_ABSOLUT_WERT | real | Gesamtenergiemenge (nicht resetbar) in Mega Joule |
| STAT_ENERGIE_ABSOLUT_EINH | string | "MJ" |
| STAT_ZEITANTEIL_REKUPERATION_WERT | real | Zeit_Rekup_WERT |
| STAT_ZEITANTEIL_REKUPERATION_EINH | string | "%" |
| STAT_ZEITANTEIL_SCHUBREKUPERATION_WERT | real | Zeitanteil Schubrekuperation in Prozent |
| STAT_ZEITANTEIL_SCHUBREKUPERATION_EINH | string | "%" |
| STAT_ZEITANTEIL_BREMSREKUPERATION_WERT | real | Zeitanteil Bremsrekuperation in Prozent |
| STAT_ZEITANTEIL_BREMSREKUPERATION_EINH | string | "%" |
| STAT_ZEITANTEIL_LASTPUNKTANHEBUNG_WERT | real | Zeitanteil Lastpunktanhebung in Prozent |
| STAT_ZEITANTEIL_LASTPUNKTANHEBUNG_EINH | string | "%" |
| STAT_ZEITANTEIL_ELEKTRISCHFAHREN_WERT | real | Zeitanteil elektrisch Fahren in Prozent |
| STAT_ZEITANTEIL_ELEKTRISCHFAHREN_EINH | string | "%" |
| STAT_ZEITANTEIL_BOOST_WERT | real | Zeitanteil Boost in Prozent |
| STAT_ZEITANTEIL_BOOST_EINH | string | "%" |
| STAT_ZEITANTEIL_ASSIST_WERT | real | Zeitanteil Assist in Prozent |
| STAT_ZEITANTEIL_ASSIST_EINH | string | "%" |
| STAT_ZEITANTEIL_MSA_WERT | real | Zeitanteil MSA in Prozent |
| STAT_ZEITANTEIL_MSA_EINH | string | "%" |
| STAT_ZEITANTEIL_STANDLADEN_WERT | real | Zeitanteil Standladen in Prozent |
| STAT_ZEITANTEIL_STANDLADEN_EINH | string | "%" |
| STAT_ZEIT_ABSOLUT_WERT | real | Gesamtbetriebsstunden (nicht resetbar) |
| STAT_ZEIT_ABSOLUT_EINH | string | "h" |
| STAT_ZEITANTEIL_MODE_M_WERT | real | Zeitanteil Mode M in Prozent |
| STAT_ZEITANTEIL_MODE_M_EINH | string | "%" |
| STAT_ZEITANTEIL_MODE_S_WERT | real | Zeitanteil Mode S in Prozent |
| STAT_ZEITANTEIL_MODE_S_EINH | string | "%" |
| STAT_ZEITANTEIL_MODE_D_WERT | real | Zeit_ModeD_WERT |
| STAT_ZEITANTEIL_MODE_D_EINH | string | "%" |
| STAT_ZEITANTEIL_MODE_N_WERT | real | Zeitanteil Mode N in Prozent |
| STAT_ZEITANTEIL_MODE_N_EINH | string | "%" |
| STAT_ZEITANTEIL_MODE_P_WERT | real | Zeitanteil Mode P in Prozent |
| STAT_ZEITANTEIL_MODE_P_EINH | string | "%" |
| STAT_ZEITANTEIL_MODE_R_WERT | real | Zeitanteil Mode R in Prozent |
| STAT_ZEITANTEIL_MODE_R_EINH | string | "%" |
| STAT_KM_STAND_RESET_USECASES_WERT | real | Km-Stand seit dem letzten Reset |
| STAT_KM_STAND_RESET_USECASES_EINH | string | "km" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-hisr-ring"></a>
### STATUS_HISR_RING

Ließt den Historyspeicher der HCP Betriebsstatisitik aus. Es werden maximal 40 Einträge zurückgeliefert. Es werden immer alle Results zurückgegeben, auch wenn weniger als 40 Fehler gespeichert sind.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HISR_AV_01_NAME_NR | int | Index des Abschaltverhinderers = 1 |
| STAT_HISR_AV_01_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft wegen niedriger Motortemperatur |
| STAT_HISR_AV_01_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_01). |
| STAT_HISR_AV_01_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_01_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_01). |
| STAT_HISR_AV_01_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_01_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_01). |
| STAT_HISR_AV_01_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_01_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_01). |
| STAT_HISR_AV_01_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_02_NAME_NR | int | Index des Abschaltverhinderers = 2 |
| STAT_HISR_AV_02_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft systembedingt |
| STAT_HISR_AV_02_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_02). |
| STAT_HISR_AV_02_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_02_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_02). |
| STAT_HISR_AV_02_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_02_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_02). |
| STAT_HISR_AV_02_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_02_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_02). |
| STAT_HISR_AV_02_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_03_NAME_NR | int | Index des Abschaltverhinderers = 3 |
| STAT_HISR_AV_03_NAME_TEXT | string | Klartext des Abschaltverhinderers: Motorstart wurde durch Fahrer erzwungen |
| STAT_HISR_AV_03_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_03). |
| STAT_HISR_AV_03_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_03_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_03). |
| STAT_HISR_AV_03_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_03_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_03). |
| STAT_HISR_AV_03_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_03_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_03). |
| STAT_HISR_AV_03_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_04_NAME_NR | int | Index des Abschaltverhinderers = 4 |
| STAT_HISR_AV_04_NAME_TEXT | string | Klartext des Abschaltverhinderers: Motorstart wurde durch Fahrer erzwungen |
| STAT_HISR_AV_04_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_04). |
| STAT_HISR_AV_04_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_04_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_04). |
| STAT_HISR_AV_04_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_04_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_04). |
| STAT_HISR_AV_04_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_04_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_04). |
| STAT_HISR_AV_04_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_05_NAME_NR | int | Index des Abschaltverhinderers = 5 |
| STAT_HISR_AV_05_NAME_TEXT | string | Klartext des Abschaltverhinderers: Motorstart wurde durch Fahrer erzwungen |
| STAT_HISR_AV_05_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_05). |
| STAT_HISR_AV_05_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_05_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_05). |
| STAT_HISR_AV_05_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_05_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_05). |
| STAT_HISR_AV_05_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_05_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_05). |
| STAT_HISR_AV_05_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_06_NAME_NR | int | Index des Abschaltverhinderers = 6 |
| STAT_HISR_AV_06_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft wegen Batterieladezustand |
| STAT_HISR_AV_06_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_06). |
| STAT_HISR_AV_06_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_06_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_06). |
| STAT_HISR_AV_06_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_06_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_06). |
| STAT_HISR_AV_06_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_06_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_06). |
| STAT_HISR_AV_06_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_07_NAME_NR | int | Index des Abschaltverhinderers = 7 |
| STAT_HISR_AV_07_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft systembedingt |
| STAT_HISR_AV_07_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_07). |
| STAT_HISR_AV_07_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_07_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_07). |
| STAT_HISR_AV_07_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_07_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_07). |
| STAT_HISR_AV_07_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_07_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_07). |
| STAT_HISR_AV_07_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_08_NAME_NR | int | Index des Abschaltverhinderers = 8 |
| STAT_HISR_AV_08_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft wg.Steigung/Gefälle |
| STAT_HISR_AV_08_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_08). |
| STAT_HISR_AV_08_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_08_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_08). |
| STAT_HISR_AV_08_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_08_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_08). |
| STAT_HISR_AV_08_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_08_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_08). |
| STAT_HISR_AV_08_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_09_NAME_NR | int | Index des Abschaltverhinderers = 9 |
| STAT_HISR_AV_09_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft wegen Batterieladezustand |
| STAT_HISR_AV_09_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_09). |
| STAT_HISR_AV_09_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_09_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_09). |
| STAT_HISR_AV_09_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_09_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_09). |
| STAT_HISR_AV_09_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_09_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_09). |
| STAT_HISR_AV_09_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_10_NAME_NR | int | Index des Abschaltverhinderers = 10 |
| STAT_HISR_AV_10_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft wegen geringer Temperatur Hochvoltbatterie |
| STAT_HISR_AV_10_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_10). |
| STAT_HISR_AV_10_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_10_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_10). |
| STAT_HISR_AV_10_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_10_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_10). |
| STAT_HISR_AV_10_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_10_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_10). |
| STAT_HISR_AV_10_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_11_NAME_NR | int | Index des Abschaltverhinderers = 11 |
| STAT_HISR_AV_11_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft systembedingt |
| STAT_HISR_AV_11_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_11). |
| STAT_HISR_AV_11_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_11_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_11). |
| STAT_HISR_AV_11_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_11_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_11). |
| STAT_HISR_AV_11_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_11_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_11). |
| STAT_HISR_AV_11_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_12_NAME_NR | int | Index des Abschaltverhinderers = 12 |
| STAT_HISR_AV_12_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft wegen Batterieladezustand |
| STAT_HISR_AV_12_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_12). |
| STAT_HISR_AV_12_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_12_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_12). |
| STAT_HISR_AV_12_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_12_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_12). |
| STAT_HISR_AV_12_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_12_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_12). |
| STAT_HISR_AV_12_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_13_NAME_NR | int | Index des Abschaltverhinderers = 13 |
| STAT_HISR_AV_13_NAME_TEXT | string | Klartext des Abschaltverhinderers: keine Anzeige (nicht BMW relevant) |
| STAT_HISR_AV_13_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_13). |
| STAT_HISR_AV_13_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_13_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_13). |
| STAT_HISR_AV_13_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_13_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_13). |
| STAT_HISR_AV_13_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_13_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_13). |
| STAT_HISR_AV_13_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_14_NAME_NR | int | Index des Abschaltverhinderers = 14 |
| STAT_HISR_AV_14_NAME_TEXT | string | Klartext des Abschaltverhinderers: keine Anzeige (nicht BMW relevant) |
| STAT_HISR_AV_14_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_14). |
| STAT_HISR_AV_14_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_14_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_14). |
| STAT_HISR_AV_14_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_14_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_14). |
| STAT_HISR_AV_14_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_14_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_14). |
| STAT_HISR_AV_14_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_15_NAME_NR | int | Index des Abschaltverhinderers = 15 |
| STAT_HISR_AV_15_NAME_TEXT | string | Klartext des Abschaltverhinderers: wird auf DME definiert |
| STAT_HISR_AV_15_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_15). |
| STAT_HISR_AV_15_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_15_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_15). |
| STAT_HISR_AV_15_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_15_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_15). |
| STAT_HISR_AV_15_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_15_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_15). |
| STAT_HISR_AV_15_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_16_NAME_NR | int | Index des Abschaltverhinderers = 16 |
| STAT_HISR_AV_16_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft wegen Batterieladezustand |
| STAT_HISR_AV_16_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_16). |
| STAT_HISR_AV_16_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_16_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_16). |
| STAT_HISR_AV_16_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_16_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_16). |
| STAT_HISR_AV_16_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_16_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_16). |
| STAT_HISR_AV_16_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_17_NAME_NR | int | Index des Abschaltverhinderers = 17 |
| STAT_HISR_AV_17_NAME_TEXT | string | Klartext des Abschaltverhinderers: Motorstart wurde vom Fahrer erzwungen |
| STAT_HISR_AV_17_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_17). |
| STAT_HISR_AV_17_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_17_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_17). |
| STAT_HISR_AV_17_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_17_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_17). |
| STAT_HISR_AV_17_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_17_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_17). |
| STAT_HISR_AV_17_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_18_NAME_NR | int | Index des Abschaltverhinderers = 18 |
| STAT_HISR_AV_18_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft systembedingt |
| STAT_HISR_AV_18_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_18). |
| STAT_HISR_AV_18_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_18_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_18). |
| STAT_HISR_AV_18_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_18_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_18). |
| STAT_HISR_AV_18_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_18_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_18). |
| STAT_HISR_AV_18_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_19_NAME_NR | int | Index des Abschaltverhinderers = 19 |
| STAT_HISR_AV_19_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft systembedingt |
| STAT_HISR_AV_19_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_19). |
| STAT_HISR_AV_19_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_19_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_19). |
| STAT_HISR_AV_19_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_19_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_19). |
| STAT_HISR_AV_19_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_19_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_19). |
| STAT_HISR_AV_19_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_20_NAME_NR | int | Index des Abschaltverhinderers = 20 |
| STAT_HISR_AV_20_NAME_TEXT | string | Klartext des Abschaltverhinderers: Motorstart wurde vom Fahrer erzwungen |
| STAT_HISR_AV_20_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_20). |
| STAT_HISR_AV_20_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_20_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_20). |
| STAT_HISR_AV_20_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_20_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_20). |
| STAT_HISR_AV_20_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_20_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_20). |
| STAT_HISR_AV_20_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_21_NAME_NR | int | Index des Abschaltverhinderers = 21 |
| STAT_HISR_AV_21_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft systembedingt |
| STAT_HISR_AV_21_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_21). |
| STAT_HISR_AV_21_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_21_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_21). |
| STAT_HISR_AV_21_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_21_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_21). |
| STAT_HISR_AV_21_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_21_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_21). |
| STAT_HISR_AV_21_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_22_NAME_NR | int | Index des Abschaltverhinderers = 22 |
| STAT_HISR_AV_22_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft wegen hoher Temperatur im Hybridsystem |
| STAT_HISR_AV_22_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_22). |
| STAT_HISR_AV_22_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_22_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_22). |
| STAT_HISR_AV_22_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_22_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_22). |
| STAT_HISR_AV_22_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_22_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_22). |
| STAT_HISR_AV_22_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_23_NAME_NR | int | Index des Abschaltverhinderers = 23 |
| STAT_HISR_AV_23_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft wegen hoher Temperatur im Hybridsystem |
| STAT_HISR_AV_23_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_23). |
| STAT_HISR_AV_23_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_23_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_23). |
| STAT_HISR_AV_23_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_23_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_23). |
| STAT_HISR_AV_23_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_23_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_23). |
| STAT_HISR_AV_23_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_24_NAME_NR | int | Index des Abschaltverhinderers = 24 |
| STAT_HISR_AV_24_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft wegen niedriger Motortemperatur |
| STAT_HISR_AV_24_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_24). |
| STAT_HISR_AV_24_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_24_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_24). |
| STAT_HISR_AV_24_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_24_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_24). |
| STAT_HISR_AV_24_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_24_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_24). |
| STAT_HISR_AV_24_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_25_NAME_NR | int | Index des Abschaltverhinderers = 25 |
| STAT_HISR_AV_25_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft systembedingt |
| STAT_HISR_AV_25_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_25). |
| STAT_HISR_AV_25_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_25_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_25). |
| STAT_HISR_AV_25_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_25_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_25). |
| STAT_HISR_AV_25_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_25_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_25). |
| STAT_HISR_AV_25_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_26_NAME_NR | int | Index des Abschaltverhinderers = 26 |
| STAT_HISR_AV_26_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft systembedingt |
| STAT_HISR_AV_26_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_26). |
| STAT_HISR_AV_26_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_26_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_26). |
| STAT_HISR_AV_26_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_26_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_26). |
| STAT_HISR_AV_26_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_26_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_26). |
| STAT_HISR_AV_26_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_27_NAME_NR | int | Index des Abschaltverhinderers = 27 |
| STAT_HISR_AV_27_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft systembedingt |
| STAT_HISR_AV_27_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_27). |
| STAT_HISR_AV_27_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_27_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_27). |
| STAT_HISR_AV_27_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_27_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_27). |
| STAT_HISR_AV_27_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_27_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_27). |
| STAT_HISR_AV_27_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_28_NAME_NR | int | Index des Abschaltverhinderers = 28 |
| STAT_HISR_AV_28_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft systembedingt |
| STAT_HISR_AV_28_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_28). |
| STAT_HISR_AV_28_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_28_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_28). |
| STAT_HISR_AV_28_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_28_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_28). |
| STAT_HISR_AV_28_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_28_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_28). |
| STAT_HISR_AV_28_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_29_NAME_NR | int | Index des Abschaltverhinderers = 29 |
| STAT_HISR_AV_29_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft systembedingt |
| STAT_HISR_AV_29_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_29). |
| STAT_HISR_AV_29_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_29_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_29). |
| STAT_HISR_AV_29_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_29_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_29). |
| STAT_HISR_AV_29_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_29_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_29). |
| STAT_HISR_AV_29_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_30_NAME_NR | int | Index des Abschaltverhinderers = 30 |
| STAT_HISR_AV_30_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft wegen Komfortanforderung |
| STAT_HISR_AV_30_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_30). |
| STAT_HISR_AV_30_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_30_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_30). |
| STAT_HISR_AV_30_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_30_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_30). |
| STAT_HISR_AV_30_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_30_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_30). |
| STAT_HISR_AV_30_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_31_NAME_NR | int | Index des Abschaltverhinderers = 31 |
| STAT_HISR_AV_31_NAME_TEXT | string | Klartext des Abschaltverhinderers: keine Anzeige (nicht BMW relevant) |
| STAT_HISR_AV_31_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_31). |
| STAT_HISR_AV_31_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_31_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_31). |
| STAT_HISR_AV_31_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_31_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_31). |
| STAT_HISR_AV_31_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_31_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_31). |
| STAT_HISR_AV_31_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_32_NAME_NR | int | Index des Abschaltverhinderers = 32 |
| STAT_HISR_AV_32_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft wegen geringer Temperatur Hochvoltbatterie |
| STAT_HISR_AV_32_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_32). |
| STAT_HISR_AV_32_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_32_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_32). |
| STAT_HISR_AV_32_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_32_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_32). |
| STAT_HISR_AV_32_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_32_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_32). |
| STAT_HISR_AV_32_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_33_NAME_NR | int | Index des Abschaltverhinderers = 33 |
| STAT_HISR_AV_33_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft systembedingt |
| STAT_HISR_AV_33_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_33). |
| STAT_HISR_AV_33_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_33_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_33). |
| STAT_HISR_AV_33_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_33_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_33). |
| STAT_HISR_AV_33_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_33_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_33). |
| STAT_HISR_AV_33_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_34_NAME_NR | int | Index des Abschaltverhinderers = 34 |
| STAT_HISR_AV_34_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft wegen hoher Motortemperatur |
| STAT_HISR_AV_34_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_34). |
| STAT_HISR_AV_34_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_34_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_34). |
| STAT_HISR_AV_34_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_34_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_34). |
| STAT_HISR_AV_34_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_34_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_34). |
| STAT_HISR_AV_34_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_35_NAME_NR | int | Index des Abschaltverhinderers = 35 |
| STAT_HISR_AV_35_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft systembedingt |
| STAT_HISR_AV_35_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_35). |
| STAT_HISR_AV_35_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_35_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_35). |
| STAT_HISR_AV_35_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_35_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_35). |
| STAT_HISR_AV_35_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_35_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_35). |
| STAT_HISR_AV_35_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_36_NAME_NR | int | Index des Abschaltverhinderers = 36 |
| STAT_HISR_AV_36_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft wegen geringer Temperatur Hochvoltbatterie |
| STAT_HISR_AV_36_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_36). |
| STAT_HISR_AV_36_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_36_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_36). |
| STAT_HISR_AV_36_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_36_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_36). |
| STAT_HISR_AV_36_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_36_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_36). |
| STAT_HISR_AV_36_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_37_NAME_NR | int | Index des Abschaltverhinderers = 37 |
| STAT_HISR_AV_37_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft wegen hoher Motortemperatur |
| STAT_HISR_AV_37_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_37). |
| STAT_HISR_AV_37_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_37_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_37). |
| STAT_HISR_AV_37_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_37_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_37). |
| STAT_HISR_AV_37_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_37_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_37). |
| STAT_HISR_AV_37_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_38_NAME_NR | int | Index des Abschaltverhinderers = 38 |
| STAT_HISR_AV_38_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft wegen hoher Temperatur im Hybridsystem |
| STAT_HISR_AV_38_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_38). |
| STAT_HISR_AV_38_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_38_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_38). |
| STAT_HISR_AV_38_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_38_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_38). |
| STAT_HISR_AV_38_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_38_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_38). |
| STAT_HISR_AV_38_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_39_NAME_NR | int | Index des Abschaltverhinderers = 39 |
| STAT_HISR_AV_39_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft wegen niedriger Motortemperatur |
| STAT_HISR_AV_39_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_39). |
| STAT_HISR_AV_39_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_39_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_39). |
| STAT_HISR_AV_39_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_39_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_39). |
| STAT_HISR_AV_39_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_39_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_39). |
| STAT_HISR_AV_39_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| STAT_HISR_AV_40_NAME_NR | int | Index des Abschaltverhinderers = 40 |
| STAT_HISR_AV_40_NAME_TEXT | string | Klartext des Abschaltverhinderers: VM läuft systembedingt |
| STAT_HISR_AV_40_HAEUFIGKEIT_WERT | real | Gibt zurück wie oft der Fehler aufgeteten ist(AV_40). |
| STAT_HISR_AV_40_HAEUFIGKEIT_EINH | string | "-" |
| STAT_HISR_AV_40_ZULETZT_AKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt aktiv war(AV_40). |
| STAT_HISR_AV_40_ZULETZT_AKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_40_ZULETZT_DEAKTIV_KM_WERT | real | Gibt zurück, vor wieviel Kilometern der Fehler zuletzt deaktiv wurde(AV_40). |
| STAT_HISR_AV_40_ZULETZT_DEAKTIV_KM_EINH | string | "km" |
| STAT_HISR_AV_40_AKTIV_NR | unsigned char | Gibt zurück ob der Fehler noch aktiv ist(AV_40). |
| STAT_HISR_AV_40_AKTIV_TEXT | string | 0= inaktiv, 1= aktiv |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-hisr-auslesen-01"></a>
### STATUS_HISR_AUSLESEN_01

HISR Werte01 auslesen (Übersicht)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BAT_SCHUB_REKU_WERT | real | Energie EM/HV Schubrekuperation |
| STAT_BAT_SCHUB_REKU_EINH | string | kWh |
| STAT_BAT_BREMS_REKU_WERT | real | Energie EM/HV  Bremsrekuperation |
| STAT_BAT_BREMS_REKU_EINH | string | kWh |
| STAT_BAT_LPA_WERT | real | Energie EM/HV  Lastpunktanhebung |
| STAT_BAT_LPA_EINH | string | kWh |
| STAT_BAT_E_FAHREN_WERT | real | Energie EM/HV E-Fahren |
| STAT_BAT_E_FAHREN_EINH | string | kWh |
| STAT_BAT_BOOST_WERT | real | Energie EM/HV Boost |
| STAT_BAT_BOOST_EINH | string | kWh |
| STAT_BAT_ASSIST_WERT | real | Energie EM/HV Assist |
| STAT_BAT_ASSIST_EINH | string | kWh |
| STAT_BAT_MSA_WERT | real | Energie EM/HV MSA |
| STAT_BAT_MSA_EINH | string | kWh |
| STAT_BAT_STANDLADEN_WERT | real | Energie EM/HV Standladen |
| STAT_BAT_STANDLADEN_EINH | string | kWh |
| STAT_BAT_VM_WERT | real | Energie EM/HV  Verbrennungsmotor |
| STAT_BAT_VM_EINH | string | kWh |
| STAT_BAT_GESAMT_WERT | real | Energie EM/HV Gesamt (kein Reset) |
| STAT_BAT_GESAMT_EINH | string | MWh |
| STAT_TRANSOUT_SCHUB_REKU_WERT | real | Energie Getriebeausgang Schubrekuperation |
| STAT_TRANSOUT_SCHUB_REKU_EINH | string | kWh |
| STAT_TRANSOUT_BREMS_REKU_WERT | real | Energie Getriebeausgang Bremsrekuperation |
| STAT_TRANSOUT_BREMS_REKU_EINH | string | kWh |
| STAT_TRANSOUT_LPA_WERT | real | Energie Getriebeausgang Lastpunktanhebung |
| STAT_TRANSOUT_LPA_EINH | string | kWh |
| STAT_TRANSOUT_E_FAHREN_WERT | real | Energie Getriebeausgang E-Fahren |
| STAT_TRANSOUT_E_FAHREN_EINH | string | kWh |
| STAT_TRANSOUT_BOOST_WERT | real | Energie Getriebeausgang Boost |
| STAT_TRANSOUT_BOOST_EINH | string | kWh |
| STAT_TRANSOUT_ASSIST_WERT | real | Energie Getriebeausgang Assist |
| STAT_TRANSOUT_ASSIST_EINH | string | kWh |
| STAT_TRANSOUT_MSA_WERT | real | Energie Getriebeausgang MSA |
| STAT_TRANSOUT_MSA_EINH | string | kWh |
| STAT_TRANSOUT_STANDLADEN_WERT | real | Energie Getriebeausgang Standladen |
| STAT_TRANSOUT_STANDLADEN_EINH | string | kWh |
| STAT_TRANSOUT_VM_WERT | real | Energie Getriebeausgang Verbrennungsmotor |
| STAT_TRANSOUT_VM_EINH | string | kWh |
| STAT_TRANSOUT_GEAMT_WERT | real | Energie Getriebeausgang Gesamt (kein Reset) |
| STAT_TRANSOUT_GEAMT_EINH | string | MWh |
| STAT_ZEIT_SCHUB_REKU_WERT | real | Zeit Schubrekuperation |
| STAT_ZEIT_SCHUB_REKU_EINH | string | min |
| STAT_ZEIT_BREMS_REKU_WERT | real | Zeit Bremsrekuperation |
| STAT_ZEIT_BREMS_REKU_EINH | string | min |
| STAT_ZEIT_LPA_WERT | real | Zeit Lastpunktanhebung |
| STAT_ZEIT_LPA_EINH | string | min |
| STAT_ZEIT_E_FAHREN_WERT | real | Zeit E-Fahren |
| STAT_ZEIT_E_FAHREN_EINH | string | min |
| STAT_ZEIT_BOOST_WERT | real | Zeit Boost |
| STAT_ZEIT_BOOST_EINH | string | min |
| STAT_ZEIT_ASSIST_WERT | real | Zeit Assist |
| STAT_ZEIT_ASSIST_EINH | string | min |
| STAT_ZEIT_MSA_WERT | real | Zeit MSA |
| STAT_ZEIT_MSA_EINH | string | min |
| STAT_ZEIT_STANDLADEN_WERT | real | Zeit Standladen |
| STAT_ZEIT_STANDLADEN_EINH | string | min |
| STAT_ZEIT_VM_WERT | real | Zeit Verbrennungsmotor |
| STAT_ZEIT_VM_EINH | string | min |
| STAT_ZEIT_GESAMT_WERT | real | Zeit Gesamt (kein Reset) |
| STAT_ZEIT_GESAMT_EINH | string | h |
| STAT_ZEIT_MANUAL_WERT | real | Zeit Gear Mode Manual |
| STAT_ZEIT_MANUAL_EINH | string | min |
| STAT_ZEIT_SPORT_WERT | real | Zeit Gear Mode Sport |
| STAT_ZEIT_SPORT_EINH | string | min |
| STAT_ZEIT_DRIVE_WERT | real | Zeit Gear Mode Drive |
| STAT_ZEIT_DRIVE_EINH | string | min |
| STAT_ZEIT_NEUTRAL_WERT | real | Zeit Gear Mode Neutral |
| STAT_ZEIT_NEUTRAL_EINH | string | min |
| STAT_ZEIT_PARK_WERT | real | Zeit Gear Mode Park |
| STAT_ZEIT_PARK_EINH | string | min |
| STAT_ZEIT_REVERSE_WERT | real | Zeit Gear Mode Reverse |
| STAT_ZEIT_REVERSE_EINH | string | min |
| STAT_KM_STAND_RESET_WERT | real | Kilometerstand beim Reset des HISR |
| STAT_KM_STAND_RESET_EINH | string | km |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-hisr-auslesen-02"></a>
### STATUS_HISR_AUSLESEN_02

HISR Werte02 auslesen (Zeitangaben)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZEIT_KF_GESCHW_01_TORQ_01_WERT | real | Zeit Geschwindigkeitsbereich 1 Drehmomentbereich 1 |
| STAT_ZEIT_KF_GESCHW_01_TORQ_01_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_01_TORQ_02_WERT | real | Zeit Geschwindigkeitsbereich 1 Drehmomentbereich  2 |
| STAT_ZEIT_KF_GESCHW_01_TORQ_02_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_01_TORQ_03_WERT | real | Zeit Geschwindigkeitsbereich 1 Drehmomentbereich  3 |
| STAT_ZEIT_KF_GESCHW_01_TORQ_03_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_01_TORQ_04_WERT | real | Zeit Geschwindigkeitsbereich 1 Drehmomentbereich  4 |
| STAT_ZEIT_KF_GESCHW_01_TORQ_04_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_01_TORQ_05_WERT | real | Zeit Geschwindigkeitsbereich 1 Drehmomentbereich  5 |
| STAT_ZEIT_KF_GESCHW_01_TORQ_05_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_01_TORQ_06_WERT | real | Zeit Geschwindigkeitsbereich 1 Drehmomentbereich  6 |
| STAT_ZEIT_KF_GESCHW_01_TORQ_06_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_01_TORQ_07_WERT | real | Zeit Geschwindigkeitsbereich 1 Drehmomentbereich  7 |
| STAT_ZEIT_KF_GESCHW_01_TORQ_07_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_01_TORQ_08_WERT | real | Zeit Geschwindigkeitsbereich 1 Drehmomentbereich 8 |
| STAT_ZEIT_KF_GESCHW_01_TORQ_08_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_01_TORQ_09_WERT | real | Zeit Geschwindigkeitsbereich 1 Drehmomentbereich  9 |
| STAT_ZEIT_KF_GESCHW_01_TORQ_09_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_02_TORQ_01_WERT | real | Zeit Geschwindigkeitsbereich 2 Drehmomentbereich  1 |
| STAT_ZEIT_KF_GESCHW_02_TORQ_01_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_02_TORQ_02_WERT | real | Zeit Geschwindigkeitsbereich 2 Drehmomentbereich 2 |
| STAT_ZEIT_KF_GESCHW_02_TORQ_02_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_02_TORQ_03_WERT | real | Zeit Geschwindigkeitsbereich 2 Drehmomentbereich  3 |
| STAT_ZEIT_KF_GESCHW_02_TORQ_03_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_02_TORQ_04_WERT | real | Zeit Geschwindigkeitsbereich 2 Drehmomentbereich  4 |
| STAT_ZEIT_KF_GESCHW_02_TORQ_04_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_02_TORQ_05_WERT | real | Zeit Geschwindigkeitsbereich 2 Drehmomentbereich  5 |
| STAT_ZEIT_KF_GESCHW_02_TORQ_05_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_02_TORQ_06_WERT | real | Zeit Geschwindigkeitsbereich 2 Drehmomentbereich  6 |
| STAT_ZEIT_KF_GESCHW_02_TORQ_06_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_02_TORQ_07_WERT | real | Zeit Geschwindigkeitsbereich 2 Drehmomentbereich  7 |
| STAT_ZEIT_KF_GESCHW_02_TORQ_07_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_02_TORQ_08_WERT | real | Zeit Geschwindigkeitsbereich 2 Drehmomentbereich  8 |
| STAT_ZEIT_KF_GESCHW_02_TORQ_08_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_02_TORQ_09_WERT | real | Zeit Geschwindigkeitsbereich 2 Drehmomentbereich  9 |
| STAT_ZEIT_KF_GESCHW_02_TORQ_09_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_03_TORQ_01_WERT | real | Zeit Geschwindigkeitsbereich 3 Drehmomentbereich  1 |
| STAT_ZEIT_KF_GESCHW_03_TORQ_01_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_03_TORQ_02_WERT | real | Zeit Geschwindigkeitsbereich 3 Drehmomentbereich  2 |
| STAT_ZEIT_KF_GESCHW_03_TORQ_02_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_03_TORQ_03_WERT | real | Zeit Geschwindigkeitsbereich 3 Drehmomentbereich  3 |
| STAT_ZEIT_KF_GESCHW_03_TORQ_03_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_03_TORQ_04_WERT | real | Zeit Geschwindigkeitsbereich 3 Drehmomentbereich  4 |
| STAT_ZEIT_KF_GESCHW_03_TORQ_04_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_03_TORQ_05_WERT | real | Zeit Geschwindigkeitsbereich 3 Drehmomentbereich  5 |
| STAT_ZEIT_KF_GESCHW_03_TORQ_05_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_03_TORQ_06_WERT | real | Zeit Geschwindigkeitsbereich 3 Drehmomentbereich  6 |
| STAT_ZEIT_KF_GESCHW_03_TORQ_06_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_03_TORQ_07_WERT | real | Zeit Geschwindigkeitsbereich 3 Drehmomentbereich  7 |
| STAT_ZEIT_KF_GESCHW_03_TORQ_07_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_03_TORQ_08_WERT | real | Zeit Geschwindigkeitsbereich 3 Drehmomentbereich  8 |
| STAT_ZEIT_KF_GESCHW_03_TORQ_08_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_03_TORQ_09_WERT | real | Zeit Geschwindigkeitsbereich 3 Drehmomentbereich  9 |
| STAT_ZEIT_KF_GESCHW_03_TORQ_09_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_04_TORQ_01_WERT | real | Zeit Geschwindigkeitsbereich 4 Drehmomentbereich  1 |
| STAT_ZEIT_KF_GESCHW_04_TORQ_01_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_04_TORQ_02_WERT | real | Zeit Geschwindigkeitsbereich 4 Drehmomentbereich  2 |
| STAT_ZEIT_KF_GESCHW_04_TORQ_02_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_04_TORQ_03_WERT | real | Zeit Geschwindigkeitsbereich 4 Drehmomentbereich  3 |
| STAT_ZEIT_KF_GESCHW_04_TORQ_03_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_04_TORQ_04_WERT | real | Zeit Geschwindigkeitsbereich 4 Drehmomentbereich  4 |
| STAT_ZEIT_KF_GESCHW_04_TORQ_04_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_04_TORQ_05_WERT | real | Zeit Geschwindigkeitsbereich 4 Drehmomentbereich  5 |
| STAT_ZEIT_KF_GESCHW_04_TORQ_05_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_04_TORQ_06_WERT | real | Zeit Geschwindigkeitsbereich 4 Drehmomentbereich  6 |
| STAT_ZEIT_KF_GESCHW_04_TORQ_06_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_04_TORQ_07_WERT | real | Zeit Geschwindigkeitsbereich 4 Drehmomentbereich  7 |
| STAT_ZEIT_KF_GESCHW_04_TORQ_07_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_04_TORQ_08_WERT | real | Zeit Geschwindigkeitsbereich 4 Drehmomentbereich  8 |
| STAT_ZEIT_KF_GESCHW_04_TORQ_08_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_04_TORQ_09_WERT | real | Zeit Geschwindigkeitsbereich 4 Drehmomentbereich  9 |
| STAT_ZEIT_KF_GESCHW_04_TORQ_09_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_05_TORQ_01_WERT | real | Zeit Geschwindigkeitsbereich 5 Drehmomentbereich  1 |
| STAT_ZEIT_KF_GESCHW_05_TORQ_01_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_05_TORQ_02_WERT | real | Zeit Geschwindigkeitsbereich 5 Drehmomentbereich  2 |
| STAT_ZEIT_KF_GESCHW_05_TORQ_02_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_05_TORQ_03_WERT | real | Zeit Geschwindigkeitsbereich 5 Drehmomentbereich  3 |
| STAT_ZEIT_KF_GESCHW_05_TORQ_03_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_05_TORQ_04_WERT | real | Zeit Geschwindigkeitsbereich 5 Drehmomentbereich  4 |
| STAT_ZEIT_KF_GESCHW_05_TORQ_04_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_05_TORQ_05_WERT | real | Zeit Geschwindigkeitsbereich 5 Drehmomentbereich  5 |
| STAT_ZEIT_KF_GESCHW_05_TORQ_05_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_05_TORQ_06_WERT | real | Zeit Geschwindigkeitsbereich 5 Drehmomentbereich  6 |
| STAT_ZEIT_KF_GESCHW_05_TORQ_06_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_05_TORQ_07_WERT | real | Zeit Geschwindigkeitsbereich 5 Drehmomentbereich  7 |
| STAT_ZEIT_KF_GESCHW_05_TORQ_07_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_05_TORQ_08_WERT | real | Zeit Geschwindigkeitsbereich 5 Drehmomentbereich  8 |
| STAT_ZEIT_KF_GESCHW_05_TORQ_08_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_05_TORQ_09_WERT | real | Zeit Geschwindigkeitsbereich 5 Drehmomentbereich  9 |
| STAT_ZEIT_KF_GESCHW_05_TORQ_09_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_06_TORQ_01_WERT | real | Zeit Geschwindigkeitsbereich 6 Drehmomentbereich  1 |
| STAT_ZEIT_KF_GESCHW_06_TORQ_01_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_06_TORQ_02_WERT | real | Zeit Geschwindigkeitsbereich 6 Drehmomentbereich  2 |
| STAT_ZEIT_KF_GESCHW_06_TORQ_02_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_06_TORQ_03_WERT | real | Zeit Geschwindigkeitsbereich 6 Drehmomentbereich  3 |
| STAT_ZEIT_KF_GESCHW_06_TORQ_03_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_06_TORQ_04_WERT | real | Zeit Geschwindigkeitsbereich 6 Drehmomentbereich  4 |
| STAT_ZEIT_KF_GESCHW_06_TORQ_04_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_06_TORQ_05_WERT | real | Zeit Geschwindigkeitsbereich 6 Drehmomentbereich  5 |
| STAT_ZEIT_KF_GESCHW_06_TORQ_05_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_06_TORQ_06_WERT | real | Zeit Geschwindigkeitsbereich 6 Drehmomentbereich  6 |
| STAT_ZEIT_KF_GESCHW_06_TORQ_06_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_06_TORQ_07_WERT | real | Zeit Geschwindigkeitsbereich 6 Drehmomentbereich  7 |
| STAT_ZEIT_KF_GESCHW_06_TORQ_07_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_06_TORQ_08_WERT | real | Zeit Geschwindigkeitsbereich 6 Drehmomentbereich  8 |
| STAT_ZEIT_KF_GESCHW_06_TORQ_08_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_06_TORQ_09_WERT | real | Zeit Geschwindigkeitsbereich 6 Drehmomentbereich  9 |
| STAT_ZEIT_KF_GESCHW_06_TORQ_09_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_07_TORQ_01_WERT | real | Zeit Geschwindigkeitsbereich 7 Drehmomentbereich  1 |
| STAT_ZEIT_KF_GESCHW_07_TORQ_01_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_07_TORQ_02_WERT | real | Zeit Geschwindigkeitsbereich 7 Drehmomentbereich  2 |
| STAT_ZEIT_KF_GESCHW_07_TORQ_02_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_07_TORQ_03_WERT | real | Zeit Geschwindigkeitsbereich 7 Drehmomentbereich  3 |
| STAT_ZEIT_KF_GESCHW_07_TORQ_03_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_07_TORQ_04_WERT | real | Zeit Geschwindigkeitsbereich 7 Drehmomentbereich  4 |
| STAT_ZEIT_KF_GESCHW_07_TORQ_04_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_07_TORQ_05_WERT | real | Zeit Geschwindigkeitsbereich 7 Drehmomentbereich  5 |
| STAT_ZEIT_KF_GESCHW_07_TORQ_05_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_07_TORQ_06_WERT | real | Zeit Geschwindigkeitsbereich 7 Drehmomentbereich  6 |
| STAT_ZEIT_KF_GESCHW_07_TORQ_06_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_07_TORQ_07_WERT | real | Zeit Geschwindigkeitsbereich 7 Drehmomentbereich  7 |
| STAT_ZEIT_KF_GESCHW_07_TORQ_07_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_07_TORQ_08_WERT | real | Zeit Geschwindigkeitsbereich 7 Drehmomentbereich  8 |
| STAT_ZEIT_KF_GESCHW_07_TORQ_08_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_07_TORQ_09_WERT | real | Zeit Geschwindigkeitsbereich 7 Drehmomentbereich  9 |
| STAT_ZEIT_KF_GESCHW_07_TORQ_09_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_08_TORQ_01_WERT | real | Zeit Geschwindigkeitsbereich 8 Drehmomentbereich  1 |
| STAT_ZEIT_KF_GESCHW_08_TORQ_01_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_08_TORQ_02_WERT | real | Zeit Geschwindigkeitsbereich 8 Drehmomentbereich  2 |
| STAT_ZEIT_KF_GESCHW_08_TORQ_02_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_08_TORQ_03_WERT | real | Zeit Geschwindigkeitsbereich 8 Drehmomentbereich  3 |
| STAT_ZEIT_KF_GESCHW_08_TORQ_03_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_08_TORQ_04_WERT | real | Zeit Geschwindigkeitsbereich 8 Drehmomentbereich  4 |
| STAT_ZEIT_KF_GESCHW_08_TORQ_04_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_08_TORQ_05_WERT | real | Zeit Geschwindigkeitsbereich 8 Drehmomentbereich  5 |
| STAT_ZEIT_KF_GESCHW_08_TORQ_05_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_08_TORQ_06_WERT | real | Zeit Geschwindigkeitsbereich 8 Drehmomentbereich  6 |
| STAT_ZEIT_KF_GESCHW_08_TORQ_06_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_08_TORQ_07_WERT | real | Zeit Geschwindigkeitsbereich 8 Drehmomentbereich  7 |
| STAT_ZEIT_KF_GESCHW_08_TORQ_07_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_08_TORQ_08_WERT | real | Zeit Geschwindigkeitsbereich 8 Drehmomentbereich  8 |
| STAT_ZEIT_KF_GESCHW_08_TORQ_08_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_08_TORQ_09_WERT | real | Zeit Geschwindigkeitsbereich 8 Drehmomentbereich  9 |
| STAT_ZEIT_KF_GESCHW_08_TORQ_09_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_09_TORQ_01_WERT | real | Zeit Geschwindigkeitsbereich 9 Drehmomentbereich  1 |
| STAT_ZEIT_KF_GESCHW_09_TORQ_01_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_09_TORQ_02_WERT | real | Zeit Geschwindigkeitsbereich 9 Drehmomentbereich  2 |
| STAT_ZEIT_KF_GESCHW_09_TORQ_02_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_09_TORQ_03_WERT | real | Zeit Geschwindigkeitsbereich 9 Drehmomentbereich  3 |
| STAT_ZEIT_KF_GESCHW_09_TORQ_03_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_09_TORQ_04_WERT | real | Zeit Geschwindigkeitsbereich 9 Drehmomentbereich  4 |
| STAT_ZEIT_KF_GESCHW_09_TORQ_04_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_09_TORQ_05_WERT | real | Zeit Geschwindigkeitsbereich 9 Drehmomentbereich  5 |
| STAT_ZEIT_KF_GESCHW_09_TORQ_05_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_09_TORQ_06_WERT | real | Zeit Geschwindigkeitsbereich 9 Drehmomentbereich  6 |
| STAT_ZEIT_KF_GESCHW_09_TORQ_06_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_09_TORQ_07_WERT | real | Zeit Geschwindigkeitsbereich 9 Drehmomentbereich  7 |
| STAT_ZEIT_KF_GESCHW_09_TORQ_07_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_09_TORQ_08_WERT | real | Zeit Geschwindigkeitsbereich 9 Drehmomentbereich  8 |
| STAT_ZEIT_KF_GESCHW_09_TORQ_08_EINH | string | min |
| STAT_ZEIT_KF_GESCHW_09_TORQ_09_WERT | real | Zeit Geschwindigkeitsbereich 9 Drehmomentbereich  9 |
| STAT_ZEIT_KF_GESCHW_09_TORQ_09_EINH | string | min |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-hisr-auslesen-03"></a>
### STATUS_HISR_AUSLESEN_03

HISR Werte03 auslesen (Counter)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_START_STOP_KEYCRNKNORMAL_WERT | real | Motor Start Stopp-Typ KeyCrnkNormal |
| STAT_START_STOP_KEYCRNKNORMAL_EINH | string | - |
| STAT_START_STOP_KEYCRNKLOWPOW_WERT | real | Motor Start Stopp-Typ KeyCrnkLowPower |
| STAT_START_STOP_KEYCRNKLOWPOW_EINH | string | - |
| STAT_START_STOP_ASTRTSMOOTH_WERT | real | Motor Start Stopp-Typ AStrtSmooth |
| STAT_START_STOP_ASTRTSMOOTH_EINH | string | - |
| STAT_START_STOP_ASTRTNORMAL_WERT | real | Motor Start Stopp-Typ AstrtNormal |
| STAT_START_STOP_ASTRTNORMAL_EINH | string | - |
| STAT_START_STOP_ASTRTAGGRSV_WERT | real | Motor Start Stopp-Typ AstrtAggrsv |
| STAT_START_STOP_ASTRTAGGRSV_EINH | string | - |
| STAT_START_STOP_COMPRESSTEST_WERT | real | Motor Start Stopp-Typ CompressTest |
| STAT_START_STOP_COMPRESSTEST_EINH | string | - |
| STAT_START_STOP_STOPCTRLD_WERT | real | Motor Start Stopp-Typ StopCtrld |
| STAT_START_STOP_STOPCTRLD_EINH | string | - |
| STAT_START_STOP_STOPIMMED_WERT | real | Motor Start Stopp-Typ StopImmed |
| STAT_START_STOP_STOPIMMED_EINH | string | - |
| STAT_SILENT_START_COUNTER_WERT | real | Silent Start Zähler |
| STAT_SILENT_START_COUNTER_EINH | string | - |
| STAT_A_STRT_GESCHW_BER_01_WERT | real | Auto Start Zähler Geschwindigkeitsbereich 1 |
| STAT_A_STRT_GESCHW_BER_01_EINH | string | - |
| STAT_A_STRT_GESCHW_BER_02_WERT | real | Auto Start Zähler Geschwindigkeitsbereich 2 |
| STAT_A_STRT_GESCHW_BER_02_EINH | string | - |
| STAT_A_STRT_GESCHW_BER_03_WERT | real | Auto Start Zähler Geschwindigkeitsbereich 3 |
| STAT_A_STRT_GESCHW_BER_03_EINH | string | - |
| STAT_A_STRT_GESCHW_BER_04_WERT | real | Auto Start Zähler Geschwindigkeitsbereich 4 |
| STAT_A_STRT_GESCHW_BER_04_EINH | string | - |
| STAT_A_STRT_GESCHW_BER_05_WERT | real | Auto Start Zähler Geschwindigkeitsbereich 5 |
| STAT_A_STRT_GESCHW_BER_05_EINH | string | - |
| STAT_A_STRT_GESCHW_BER_06_WERT | real | Auto Start Zähler Geschwindigkeitsbereich 6 |
| STAT_A_STRT_GESCHW_BER_06_EINH | string | - |
| STAT_A_STRT_GESCHW_BER_07_WERT | real | Auto Start Zähler Geschwindigkeitsbereich 7 |
| STAT_A_STRT_GESCHW_BER_07_EINH | string | - |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-hisr-auslesen-04"></a>
### STATUS_HISR_AUSLESEN_04

HISR Werte04 auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STRCK_E_FAHR_GESCHW_BER_01_WERT | real | Kilometer E-Fahren Geschwindigkeitsbereich 1 |
| STAT_STRCK_E_FAHR_GESCHW_BER_01_EINH | string | km |
| STAT_STRCK_E_FAHR_GESCHW_BER_02_WERT | real | Kilometer E-Fahren Geschwindigkeitsbereich 2 |
| STAT_STRCK_E_FAHR_GESCHW_BER_02_EINH | string | km |
| STAT_STRCK_E_FAHR_GESCHW_BER_03_WERT | real | Kilometer E-Fahren Geschwindigkeitsbereich 3 |
| STAT_STRCK_E_FAHR_GESCHW_BER_03_EINH | string | km |
| STAT_STRCK_E_FAHR_GESCHW_BER_04_WERT | real | Kilometer E-Fahren Geschwindigkeitsbereich 4 |
| STAT_STRCK_E_FAHR_GESCHW_BER_04_EINH | string | km |
| STAT_STRCK_E_FAHR_GESCHW_BER_05_WERT | real | Kilometer E-Fahren Geschwindigkeitsbereich 5 |
| STAT_STRCK_E_FAHR_GESCHW_BER_05_EINH | string | km |
| STAT_STRCK_E_FAHR_GESCHW_BER_06_WERT | real | Kilometer E-Fahren Geschwindigkeitsbereich 6 |
| STAT_STRCK_E_FAHR_GESCHW_BER_06_EINH | string | km |
| STAT_STRCK_E_FAHR_GESCHW_BER_07_WERT | real | Kilometer E-Fahren Geschwindigkeitsbereich 7 |
| STAT_STRCK_E_FAHR_GESCHW_BER_07_EINH | string | km |
| STAT_ZEIT_E_FAHR_GESCHW_BER_01_WERT | real | Zeit E-Fahren Geschwindigkeitsbereich 1 |
| STAT_ZEIT_E_FAHR_GESCHW_BER_01_EINH | string | min |
| STAT_ZEIT_E_FAHR_GESCHW_BER_02_WERT | real | Kilometer E-Fahren Geschwindigkeitsbereich 2 |
| STAT_ZEIT_E_FAHR_GESCHW_BER_02_EINH | string | min |
| STAT_ZEIT_E_FAHR_GESCHW_BER_03_WERT | real | Zeit E-Fahren Geschwindigkeitsbereich 3 |
| STAT_ZEIT_E_FAHR_GESCHW_BER_03_EINH | string | min |
| STAT_ZEIT_E_FAHR_GESCHW_BER_04_WERT | real | Zeit E-Fahren Geschwindigkeitsbereich 4 |
| STAT_ZEIT_E_FAHR_GESCHW_BER_04_EINH | string | min |
| STAT_ZEIT_E_FAHR_GESCHW_BER_05_WERT | real | Zeit E-Fahren Geschwindigkeitsbereich 5 |
| STAT_ZEIT_E_FAHR_GESCHW_BER_05_EINH | string | min |
| STAT_ZEIT_E_FAHR_GESCHW_BER_06_WERT | real | Zeit E-Fahren Geschwindigkeitsbereich 6 |
| STAT_ZEIT_E_FAHR_GESCHW_BER_06_EINH | string | min |
| STAT_ZEIT_E_FAHR_GESCHW_BER_07_WERT | real | Zeit E-Fahren Geschwindigkeitsbereich 7 |
| STAT_ZEIT_E_FAHR_GESCHW_BER_07_EINH | string | min |
| STAT_STRECKE_VM_AUS_BER_01_WERT | real | Fahren mit VM aus Streckenbereich 1 |
| STAT_STRECKE_VM_AUS_BER_01_EINH | string | - |
| STAT_STRECKE_VM_AUS_BER_02_WERT | real | Fahren mit VM aus Streckenbereich 2 |
| STAT_STRECKE_VM_AUS_BER_02_EINH | string | - |
| STAT_STRECKE_VM_AUS_BER_03_WERT | real | Fahren mit VM aus Streckenbereich 3 |
| STAT_STRECKE_VM_AUS_BER_03_EINH | string | - |
| STAT_STRECKE_VM_AUS_BER_04_WERT | real | Fahren mit VM aus Streckenbereich 4 |
| STAT_STRECKE_VM_AUS_BER_04_EINH | string | - |
| STAT_STRECKE_VM_AUS_BER_05_WERT | real | Fahren mit VM aus Streckenbereich 5 |
| STAT_STRECKE_VM_AUS_BER_05_EINH | string | - |
| STAT_STRECKE_VM_AUS_BER_06_WERT | real | Fahren mit VM aus Streckenbereich 6 |
| STAT_STRECKE_VM_AUS_BER_06_EINH | string | - |
| STAT_ZEIT_VM_AUS_BER_01_WERT | real | Fahren mit VM aus Zeitbereich 1 |
| STAT_ZEIT_VM_AUS_BER_01_EINH | string | - |
| STAT_ZEIT_VM_AUS_BER_02_WERT | real | Fahren mit VM aus Zeitbereich  2 |
| STAT_ZEIT_VM_AUS_BER_02_EINH | string | - |
| STAT_ZEIT_VM_AUS_BER_03_WERT | real | Fahren mit VM aus Zeitbereich 3 |
| STAT_ZEIT_VM_AUS_BER_03_EINH | string | - |
| STAT_ZEIT_VM_AUS_BER_04_WERT | real | Fahren mit VM aus Zeitbereich 4 |
| STAT_ZEIT_VM_AUS_BER_04_EINH | string | - |
| STAT_ZEIT_VM_AUS_BER_05_WERT | real | Fahren mit VM aus Zeitbereich 5 |
| STAT_ZEIT_VM_AUS_BER_05_EINH | string | - |
| STAT_ZEIT_VM_AUS_BER_06_WERT | real | Fahren mit VM aus Zeitbereich 6 |
| STAT_ZEIT_VM_AUS_BER_06_EINH | string | - |
| STAT_ZEIT_GESCHW_BEREICH_01_WERT | real | Zeit Geschwindigkeitsbereich 1 |
| STAT_ZEIT_GESCHW_BEREICH_01_EINH | string | min |
| STAT_ZEIT_GESCHW_BEREICH_02_WERT | real | Zeit Geschwindigkeitsbereich 2 |
| STAT_ZEIT_GESCHW_BEREICH_02_EINH | string | min |
| STAT_ZEIT_GESCHW_BEREICH_03_WERT | real | Zeit Geschwindigkeitsbereich 3 |
| STAT_ZEIT_GESCHW_BEREICH_03_EINH | string | min |
| STAT_ZEIT_GESCHW_BEREICH_04_WERT | real | Zeit Geschwindigkeitsbereich 4 |
| STAT_ZEIT_GESCHW_BEREICH_04_EINH | string | min |
| STAT_ZEIT_GESCHW_BEREICH_05_WERT | real | Zeit Geschwindigkeitsbereich 5 |
| STAT_ZEIT_GESCHW_BEREICH_05_EINH | string | min |
| STAT_ZEIT_GESCHW_BEREICH_06_WERT | real | Zeit Geschwindigkeitsbereich 6 |
| STAT_ZEIT_GESCHW_BEREICH_06_EINH | string | min |
| STAT_ZEIT_GESCHW_BEREICH_07_WERT | real | Zeit Geschwindigkeitsbereich 7 |
| STAT_ZEIT_GESCHW_BEREICH_07_EINH | string | min |
| STAT_ZEIT_GESCHW_BEREICH_08_WERT | real | Zeit Geschwindigkeitsbereich 8 |
| STAT_ZEIT_GESCHW_BEREICH_08_EINH | string | min |
| STAT_ZEIT_GESCHW_BEREICH_09_WERT | real | Zeit Geschwindigkeitsbereich 9 |
| STAT_ZEIT_GESCHW_BEREICH_09_EINH | string | min |
| STAT_ZEIT_GESCHW_BEREICH_10_WERT | real | Zeit Geschwindigkeitsbereich 10 |
| STAT_ZEIT_GESCHW_BEREICH_10_EINH | string | min |
| STAT_ZEIT_GESCHW_BEREICH_11_WERT | real | Zeit Geschwindigkeitsbereich 11 |
| STAT_ZEIT_GESCHW_BEREICH_11_EINH | string | min |
| STAT_ZEIT_GESCHW_BEREICH_12_WERT | real | Zeit Geschwindigkeitsbereich 12 |
| STAT_ZEIT_GESCHW_BEREICH_12_EINH | string | min |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-hisr-av-reset-haeufigkeit"></a>
### STEUERN_HISR_AV_RESET_HAEUFIGKEIT

Löscht die Häufigkeit des Ausschaltverhinderer (AV) Historienspeicher

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-hisr-av-reset-km-und-aktiv"></a>
### STEUERN_HISR_AV_RESET_KM_UND_AKTIV

Löscht beide Kilometerstände und Aktiv-Status des Ausschaltverhinderer (AV) Historienspeicher

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-soc-stimul"></a>
### STEUERN_SOC_STIMUL

Job schaltet die SOC Stimmulierung ein. Batterie wird entladen und gelanden um den SOC-Wert zu bestimmen. AUS nach 1200s $2E     SID WriteDataByIdentifier $F2 $14 DID Messwert Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TRIGGER | unsigned char | Werttabelle 0 = Stimmulierung AUS 1 = Stimmulierung EIN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-adaptionswerte-lesen"></a>
### STATUS_ADAPTIONSWERTE_LESEN

Liest die Adaptionswerte von PyroFuse(integriert in der SBK - SicherheitsBatterieKlemme), Batterie, CC-Meldung aus. Siehe Argumente. $22      SID WriteDataByIdentifier $02 $32  DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PYROFUSE_RAPID_SHUTDOWN_AKTIV | unsigned char | Pyrofuse (integriert in der SBK - SicherheitsBatterieKlemme) |
| STAT_PYROFUSE_RAPID_SHUTDOWN_AKTIV_TEXT | string | Shutdown durch die Pyrofuse (integriert in der SBK - SicherheitsBatterieKlemme) hervorgerufen |
| STAT_BATTERIE_NUTZUNG_01_WERT | real | Nutzung der HV-Batterie in Wh per Km. |
| STAT_BATTERIE_NUTZUNG_01_EINH | string | "Wh/km" |
| STAT_BATTERIE_ACK_LADE_AMPERESTUNDEN_WERT | real | Ackumulierte Ladeamperstunden der HV-Batterie |
| STAT_BATTERIE_ACK_LADE_AMPERESTUNDEN_EINH | string | "Ah" |
| STAT_BATTERIE_ACK_ENTLADE_AMPERESTUNDEN_WERT | real | Ackumulierte Entladeamperstunden der HV-Batterie |
| STAT_BATTERIE_ACK_ENTLADE_AMPERESTUNDEN_EINH | string | "Ah" |
| STAT_BATTERIE_NUTZUNG_KM_WERT | real | Nutzung der HV-Batterie in km Auflösung 10 km |
| STAT_BATTERIE_NUTZUNG_KM_EINH | string | "km" |
| STAT_CC_SOC_STIMM_WERT | real | Dieses Result entspricht der HV-Batterie SOC, der an HOS gesendet wird |
| STAT_CC_SOC_STIMM_EINH | string | "%" |
| STAT_CC_SOC_WERT | real | HV-SOC Prozentanzeige |
| STAT_CC_SOC_EINH | string | "%" |
| STAT_CC_E_FAHREN_WERT | real | Zähler Taktzyklen im elektrischen Fahrbetrieb |
| STAT_CC_E_FAHREN_EINH | string | "-" keine Einheit da Zähler |
| STAT_CC_MISCHBETRIEB_WERT | real | Zähler Taktzyklen im hybriden Fahrbetrieb |
| STAT_CC_MISCHBETRIEB_EINH | string | "-" keine Einheit da Zähler |
| STAT_CC_V_BETRIEB_WERT | real | Zähler Taktzyklen im verbrennungsmotorischen Fahrbetrieb |
| STAT_CC_V_BETRIEB_EINH | string | "-" keine Einheit da Zähler |
| STAT_CC_ZEIT_SEIT_RESET_WERT | real | Zeit in Sekunden seit Reset der Hybridnutzenanzeige |
| STAT_CC_ZEIT_SEIT_RESET_EINH | string | "s" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-adaptionswerte-loeschen"></a>
### STEUERN_ADAPTIONSWERTE_LOESCHEN

Löscht die Adaptionswerte. Siehe Argumente. $2E     SID WriteDataByIdentifier $F2 $1A DID Messwert Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION | unsigned char | Löscht die Adaptionswerte Werttabelle 0= alle löschen 1= Pyrofuse (integriert in der SBK - SicherheitsBatterieKlemme) wird zurückgesetzt(Klemme 41) 2= Batterie wird nicht mehr unterstützt - siehe Steuern_Batterie_Adaptionswerte_Loeschen 3= CC-Meldung 4= HISR- Betriebsstrategie-Analyse wir zurückgesetzt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-batterie-adaptionswerte-loeschen"></a>
### STEUERN_BATTERIE_ADAPTIONSWERTE_LOESCHEN

Löscht die Adaptionswerte in der HV-Batterie. Ausschließlich im Werkstattmode möglich. $2E     SID WriteDataByIdentifier $F2 $27 DID Messwert Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION | string | 0= keine Aktion 7= Adaptionswerte der Batterie löschen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-completecontrol-pin"></a>
### STEUERN_COMPLETECONTROL_PIN

Freigabe Code für Steuern Antriebsart Complete Control Es muss der entsprechenden Freigabecode übergeben werden, damit keine Beschädigungen im Getriebe auftreten können. $2E     SID WriteDataByIdentifier $F2 $17 DID Messwert Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FREIGABECODE | unsigned long | Freigabe Code für Steuern Antriebsart Complete Control Darf nicht im Service ausgeführt werden Es muss der entsprechenden Freigabecode übergeben werden, damit keine Beschädigungen im Getriebe auftreten können. Es wird eine 9-stellige Zahl eingegeben! |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-e-motor-control-check"></a>
### STEUERN_E_MOTOR_CONTROL_CHECK

Anstossen des E-Motor Control Check Zur Überprüfung der E-Maschinen. Die E-Maschinen werden für max. 60s gedreht Service Hinweise: Nur in Verbindung mit Energiesparmode Werkstatt. WÄHREND TEST KEINESFALLS START-STOP-TASTER DRÜCKEN!!! BAUTEILSCHÄDIGUNG.  $2E       SID WriteDataByIdentifier $F2 $16   DID Messwert Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MOTOR | unsigned char | Die E-Maschinen werden kurz gedreht bis 0=AUS/OFF bzw. max. 60s Wertetabelle: 0 = AUS/OFF 1 = E-Maschine A 2 = E-Maschine B |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-crash-detection-signal"></a>
### STATUS_CRASH_DETECTION_SIGNAL

Gibt den Status der Crash Detection Leitung aus $22     SID ReadDataByIdentifier $02 $26 DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CRASH_DETECTION_SIGNAL_EIN_TEXT | string | Status der Crash Detektion Leitung 1= Crash dedektiert (EIN) 0= Kein Crash dedektiert (AUS) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-gesamtfzg-degradation"></a>
### STATUS_GESAMTFZG_DEGRADATION

Auslesen der strategischen EM-A Degradation $22     SID ReadDataByIdentifier $02 $0F DID Messwert Auslesen der strategischen EM-B Degradation $22     SID ReadDataByIdentifier $02 $10 DID Messwert Auslesen der strategischen Verbrennungsmotordegradation $22     SID ReadDataByIdentifier $02 $11 DID Messwert Auslesen der strategischen Batterieladedegradation $22     SID ReadDataByIdentifier $02 $0E DID Messwert Auslesen der strategischen Batterieentladedegradation $22     SID ReadDataByIdentifier $02 $0D DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GESAMTFZG_DEGR_EMOT_A_WERT | real | Strategischen EM-A Degradation in Prozent 100 % Vollfunktion, 0% Totaldegradation 0 bis100 Prozent Aufloesung: 1 Prozent |
| STAT_GESAMTFZG_DEGR_EMOT_A_EINH | string | "%" - Einheit der Degradation |
| STAT_GESAMTFZG_DEGR_EMOT_B_WERT | real | Strategischen EM-B Degradation in Prozent 100 % Vollfunktion, 0% Totaldegradation 0 bis100 Prozent Aufloesung: 1 Prozent |
| STAT_GESAMTFZG_DEGR_EMOT_B_EINH | string | "%" - Einheit der Degradation |
| STAT_GESAMTFZG_DEGR_VMOT_GANG01_WERT | real | Strategischen Verbrennungsmotordegradation 100 % Vollfunktion, 0% Totaldegradation 0 bis100 Prozent Aufloesung: 1 Prozent |
| STAT_GESAMTFZG_DEGR_VMOT_GANG01_EINH | string | "%" - Einheit der Degradation |
| STAT_GESAMTFZG_DEGR_VMOT_GANG02_WERT | real | Strategischen Verbrennungsmotordegradation 100 % Vollfunktion, 0% Totaldegradation 0 bis100 Prozent Aufloesung: 1 Prozent |
| STAT_GESAMTFZG_DEGR_VMOT_GANG02_EINH | string | "%" - Einheit der Degradation |
| STAT_GESAMTFZG_DEGR_VMOT_GANG03_WERT | real | Strategischen Verbrennungsmotordegradation 100 % Vollfunktion, 0% Totaldegradation 0 bis100 Prozent Aufloesung: 1 Prozent |
| STAT_GESAMTFZG_DEGR_VMOT_GANG03_EINH | string | "%" - Einheit der Degradation |
| STAT_GESAMTFZG_DEGR_VMOT_GANG04_WERT | real | Strategischen Verbrennungsmotordegradation 100 % Vollfunktion, 0% Totaldegradation 0 bis100 Prozent Aufloesung: 1 Prozent |
| STAT_GESAMTFZG_DEGR_VMOT_GANG04_EINH | string | "%" - Einheit der Degradation |
| STAT_GESAMTFZG_DEGR_VMOT_GANG05_WERT | real | Strategischen Verbrennungsmotordegradation 100 % Vollfunktion, 0% Totaldegradation 0 bis100 Prozent Aufloesung: 1 Prozent |
| STAT_GESAMTFZG_DEGR_VMOT_GANG05_EINH | string | "%" - Einheit der Degradation |
| STAT_GESAMTFZG_DEGR_VMOT_GANG06_WERT | real | Strategischen Verbrennungsmotordegradation 100 % Vollfunktion, 0% Totaldegradation 0 bis100 Prozent Aufloesung: 1 Prozent |
| STAT_GESAMTFZG_DEGR_VMOT_GANG06_EINH | string | "%" - Einheit der Degradation |
| STAT_GESAMTFZG_DEGR_VMOT_GANG07_WERT | real | Strategischen Verbrennungsmotordegradation 100 % Vollfunktion, 0% Totaldegradation 0 bis100 Prozent Aufloesung: 1 Prozent |
| STAT_GESAMTFZG_DEGR_VMOT_GANG07_EINH | string | "%" - Einheit der Degradation |
| STAT_GESAMTFZG_DEGR_VMOT_GANG08_WERT | real | Strategischen Verbrennungsmotordegradation 100 % Vollfunktion, 0% Totaldegradation 0 bis100 Prozent Aufloesung: 1 Prozent |
| STAT_GESAMTFZG_DEGR_VMOT_GANG08_EINH | string | "%" - Einheit der Degradation |
| STAT_GESAMTFZG_DEGR_VMOT_GANG09_WERT | real | Strategischen Verbrennungsmotordegradation 100 % Vollfunktion, 0% Totaldegradation 0 bis100 Prozent Aufloesung: 1 Prozent |
| STAT_GESAMTFZG_DEGR_VMOT_GANG09_EINH | string | "%" - Einheit der Degradation |
| STAT_GESAMTFZG_DEGR_BAT_LADEN_WERT | real | Strategischen Batterieladedegradation in Prozent 100 % Vollfunktion, 0% Totaldegradation 0 bis100 Prozent Aufloesung: 1 Prozent |
| STAT_GESAMTFZG_DEGR_BAT_LADEN_EINH | string | "%" - Einheit der Degradation |
| STAT_GESAMTFZG_DEGR_BAT_ENTLADEN_WERT | real | Strategischen Batterieentladedegradation in Prozent 100 % Vollfunktion, 0% Totaldegradation 0 bis100 Prozent Aufloesung: 1 Prozent |
| STAT_GESAMTFZG_DEGR_BAT_ENTLADEN_EINH | string | "%" - Einheit der Degradation |
| STAT_GESAMTFZG_DEGR_BAT_ENTLADEN_EFAHREN_WERT | real | Strategischen Batterieentladedegradation beim E-Fahren in Prozent 100 % Vollfunktion, 0% Totaldegradation 0 bis100 Prozent Aufloesung: 1 Prozent |
| STAT_GESAMTFZG_DEGR_BAT_ENTLADEN_EFAHREN_EINH | string | "%" - Einheit der Degradation |
| STAT_GESAMTFZG_DEGR_KLIMAKOMPR_WERT | real | Strategischen Degradation des Klimakompressors in Prozent 100 % Vollfunktion, 0% Totaldegradation 0 bis100 Prozent Aufloesung: 1 Prozent |
| STAT_GESAMTFZG_DEGR_KLIMAKOMPR_EINH | string | "%" - Einheit der Degradation |
| STAT_GESAMTFZG_DEGR_REKUPERATION_WERT | real | Strategischen Rekuperations-Degradation in Prozent 100 % Vollfunktion, 0% Totaldegradation 0 bis100 Prozent Aufloesung: 1 Prozent |
| STAT_GESAMTFZG_DEGR_REKUPERATION_EINH | string | "%" - Einheit der Degradation |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST01 | binary | Hex-Auftrag an SG |
| _RESPONSE01 | binary | Hex-Antwort von SG |
| _REQUEST02 | binary | Hex-Auftrag an SG |
| _RESPONSE02 | binary | Hex-Antwort von SG |
| _REQUEST03 | binary | Hex-Auftrag an SG |
| _RESPONSE03 | binary | Hex-Antwort von SG |
| _REQUEST04 | binary | Hex-Auftrag an SG |
| _RESPONSE04 | binary | Hex-Antwort von SG |
| _REQUEST05 | binary | Hex-Auftrag an SG |
| _RESPONSE05 | binary | Hex-Antwort von SG |
| _REQUEST06 | binary | Hex-Auftrag an SG |
| _RESPONSE06 | binary | Hex-Antwort von SG |
| _REQUEST07 | binary | Hex-Auftrag an SG |
| _RESPONSE07 | binary | Hex-Antwort von SG |
| _REQUEST08 | binary | Hex-Auftrag an SG |
| _RESPONSE08 | binary | Hex-Antwort von SG |

<a id="job-status-aktuelle-getriebeposition"></a>
### STATUS_AKTUELLE_GETRIEBEPOSITION

Status der Getriebeposition P / R / N / D $22     SID ReadDataByIdentifier $02 $28 DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ISTPOSITION_NR | unsigned char | Gibt die aktuelle Getriebepostition zurück. 5= Drive 6= Neutral 7= Reverse 8= Park 15= Init |
| STAT_ISTPOSITION_TEXT | string | Gibt die aktuelle Getriebepostition als Text zurück. |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-emf-hilferuf"></a>
### STATUS_EMF_HILFERUF

Lese Anzahl der EMF Hilferufe in D/S/M/R/N

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_REQDRND_DR_WERT | unsigned int | Anzahl der EMF Hilferufe in D/S/M/R |
| STAT_REQDRND_DR_EINH | string | "-" keine Einheite, da Anzahl |
| STAT_REQDRND_N_WERT | unsigned int | Lese Anzahl der EMF Hilferufe in N |
| STAT_REQDRND_N_EINH | string | "-" keine Einheite, da Anzahl |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-voltage-hcp-hv-side"></a>
### STATUS_VOLTAGE_HCP_HV_SIDE

Auslesen der Hochvolt-Spannung und des Interlock Status ACHTUNG: Die Spannungsfreiheit wird nicht durch diesen Aufruf garantiert! Bitte Hochvolt-Sicherheits-Maßnahmen beachten. $22     SID ReadDataByIdentifier $02 $25 DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HV_SPANNUNG_MCPA_WERT | real | Hochvolt Systemspannung der MCPA in Volt. ACHTUNG: Die Spannungsfreiheit wird nicht durch diesen Aufruf garantiert! Bitte Hochvolt-Sicherheits-Maßnahmen beachten. |
| STAT_HV_SPANNUNG_MCPA_EINH | string | Einheit der Hochvolt Systemspannung der MCPA in Volt "V" |
| STAT_HV_SPANNUNG_MCPB_WERT | real | Hochvolt Systemspannung der MCPB in Volt. ACHTUNG: Die Spannungsfreiheit wird nicht durch diesen Aufruf garantiert! Bitte Hochvolt-Sicherheits-Maßnahmen beachten. |
| STAT_HV_SPANNUNG_MCPB_EINH | string | Einheit der Hochvolt Systemspannung der MCPB in Volt "V" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-hcp-teleservice-monitoring"></a>
### STATUS_HCP_TELESERVICE_MONITORING

Results folgender Jobs hintereinander: STATUS_LESEN_PWRLNCH_COUNTER STATUS_ABSCHALTVERHINDERER STATUS_DEGRATIONS_SOURCE STATUS_EMF_HILFERUF STATUS_HCP_RBM_RATIO

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PWRLNCH_CONTIN_CNT | real | Anzahl aller durchgefuehrten PowerLaunche. Beschreibung: 's' |
| STAT_PWRLNCH_CNT | real | Anzahl aller durchgefuehrten PowerLaunches seit Reset |
| STAT_HV_BATTERY_PACK_VOLTAGE_LEVEL_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_HV_BATTERY_PACK_VOLTAGE_LEVEL_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_HV_BATTERY_POWER_LIMITS_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_HV_BATTERY_POWER_LIMITS_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_HV_BATTERY_MODULE_VOLTAGE_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_HV_BATTERY_MODULE_VOLTAGE_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_HV_BATTERY_STATE_OF_CHARGE_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_HV_BATTERY_STATE_OF_CHARGE_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_TRANSMISSION_RANGE_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_TRANSMISSION_RANGE_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_HOOD_OPEN_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_HOOD_OPEN_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_ECM_REQUEST_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_ECM_REQUEST_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_RUNCRANK_NOT_ACTIVE_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_RUNCRANK_NOT_ACTIVE_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_DRIVEABILITY_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_DRIVEABILITY_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_MINIMUM_RUN_TIME_NOT_MET_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_MINIMUM_RUN_TIME_NOT_MET_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_DEVICE_CONTROL_AUTOSTART_OVERRIDE_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_DEVICE_CONTROL_AUTOSTART_OVERRIDE_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_KEY_FORCED_AUTOSTART_REQUEST_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_KEY_FORCED_AUTOSTART_REQUEST_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_AUXILIARY_TRANSMISSION_PUMP_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_AUXILIARY_TRANSMISSION_PUMP_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_ELECTRIC_MOTOR_INVERTER_TEMPERATURE_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_ELECTRIC_MOTOR_INVERTER_TEMPERATURE_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_ELECTRIC_MOTOR_TEMPERATURE_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_ELECTRIC_MOTOR_TEMPERATURE_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_ENGINE_COOLANT_TEMPERATURE_UNDER_MINLIM_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_ENGINE_COOLANT_TEMPERATURE_UNDER_MINLIM_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_REMOTE_START_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_REMOTE_START_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_REVERSE_GRADE_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_REVERSE_GRADE_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_DATA_VALIDITY_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_DATA_VALIDITY_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_VEHICLE_SPEED_TOO_HIGH_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_VEHICLE_SPEED_TOO_HIGH_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_SYSTEM_OPTIMIZATION_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_SYSTEM_OPTIMIZATION_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_SYSTEM_VOLTAGE_LOW_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_SYSTEM_VOLTAGE_LOW_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_TOWHAUL_SWITCH_ON_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_TOWHAUL_SWITCH_ON_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_HV_BATTERY_PACK_TEMPERATURE_UNDER_MINLIM_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_HV_BATTERY_PACK_TEMPERATURE_UNDER_MINLIM_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_ENGINE_COOLANT_TEMPERATURE_OVER_MAXLIM_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_ENGINE_COOLANT_TEMPERATURE_OVER_MAXLIM_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_HV_BATTERY_PACK_TEMPERATURE_OVER_MAXLIM_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_HV_BATTERY_PACK_TEMPERATURE_OVER_MAXLIM_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_ECM_OVERRIDE_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_ECM_OVERRIDE_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_REMEDIAL_ACTIONS_NR | unsigned char | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_REMEDIAL_ACTIONS_TEXT | string | Ursache fuer Abschaltverhinderung aktiv: nein/ja |
| STAT_EOVERDRIVE_NR | unsigned char | veraltete AV-s |
| STAT_EOVERDRIVE_TEXT | string | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_UEBERLADEN_BATTERIE_NR | unsigned char | Verhindern des Ueberladens der Batterie |
| STAT_UEBERLADEN_BATTERIE_TEXT | string | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_S_M_MODE_NR | unsigned char | S/M-Mode |
| STAT_S_M_MODE_TEXT | string | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_PEDAL_BETAETIGUNG_P_N_NR | unsigned char | Gaspedalbetaetigung in P/N |
| STAT_PEDAL_BETAETIGUNG_P_N_TEXT | string | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_PADDEL_TIP_IN_NR | unsigned char | Paddle-TipIn |
| STAT_PADDEL_TIP_IN_TEXT | string | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_E_DRIVE_INEFFITZIENT_NR | unsigned char | eDrive nicht effizient |
| STAT_E_DRIVE_INEFFITZIENT_TEXT | string | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_REMEDIAL_ACTIONS_M1_NR | unsigned char | Remedial Actions erlauben M1 nicht |
| STAT_REMEDIAL_ACTIONS_M1_TEXT | string | Ursache der Abschaltverhinderung 0= nein/1=ja |
| STAT_DEGR_MOMENT_EMOT_A_TEMP_EMOT_A_AKTIV | unsigned char | Degradation Moment E-Maschine A durch Temperatur E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_EMOT_A_TEMP_EMOT_A_AKTIV_TEXT | string | Degradation Moment E-Maschine A durch Temperatur E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_EMOT_A_TEMP_INVERTER_EMOT_A_AKTIV | unsigned char | Degradation Moment E-Maschine A durch Temperatur Inverter E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_EMOT_A_TEMP_INVERTER_EMOT_A_AKTIV_TEXT | string | Degradation Moment E-Maschine A durch Temperatur Inverter E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_EMOT_A_TEMP_GETR_OEL_AKTIV | unsigned char | Degradation Moment E-Maschine A durch Temperatur Getriebeöl 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_EMOT_A_TEMP_GETR_OEL_AKTIV_TEXT | string | Degradation Moment E-Maschine A durch Temperatur Getriebeöl 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_RESERVE_1_3_AKTIV | unsigned char | - - |
| STAT_RESERVE_1_3_AKTIV_TEXT | string | - - |
| STAT_DEGR_MOMENT_EMOT_A_TEMP_APM_AKTIV | unsigned char | Degradation Moment E-Maschine A durch Temperatur APM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_EMOT_A_TEMP_APM_AKTIV_TEXT | string | Degradation Moment E-Maschine A durch Temperatur APM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_EMOT_B_TEMP_EMOT_B_AKTIV | unsigned char | Degradation Moment E-Maschine B durch Temperatur E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_EMOT_B_TEMP_EMOT_B_AKTIV_TEXT | string | Degradation Moment E-Maschine B durch Temperatur E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_EMOT_B_TEMP_INVERTER_EMOT_B_AKTIV | unsigned char | Degradation Moment E-Maschine B durch Temperatur Inverter E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_EMOT_B_TEMP_INVERTER_EMOT_B_AKTIV_TEXT | string | Degradation Moment E-Maschine B durch Temperatur Inverter E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_RESERVE_1_7_AKTIV | unsigned char | - - |
| STAT_RESERVE_1_7_AKTIV_TEXT | string | - - |
| STAT_DEGR_MOMENT_EMOT_B_TEMP_APM_AKTIV | unsigned char | Degradation Moment E-Maschine B durch Temperatur APM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_EMOT_B_TEMP_APM_AKTIV_TEXT | string | Degradation Moment E-Maschine B durch Temperatur APM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_EMOT_B_TEMP_GETR_OEL_AKTIV | unsigned char | Degradation Moment E-Maschine B durch Temperatur Getriebeöl 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_EMOT_B_TEMP_GETR_OEL_AKTIV_TEXT | string | Degradation Moment E-Maschine B durch Temperatur Getriebeöl 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_ENTLADELEISTUNG_FAHRMODUS_AKTIV | unsigned char | Degradation Batterie-Entladeleistung durch Fahrmodus 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_ENTLADELEISTUNG_FAHRMODUS_AKTIV_TEXT | string | Degradation Batterie-Entladeleistung durch Fahrmodus 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_ENTLADELEISTUNG_TEMP_HV_SPEICHER_AKTIV | unsigned char | Degradation Batterie-Entladeleistung durch Temperatur HV-Speicher 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_ENTLADELEISTUNG_TEMP_HV_SPEICHER_AKTIV_TEXT | string | Degradation Batterie-Entladeleistung durch Temperatur HV-Speicher 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_ENTLADELEISTUNG_SOC_AKTIV | unsigned char | Degradation Batterie-Entladeleistung durch SOC 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_ENTLADELEISTUNG_SOC_AKTIV_TEXT | string | Degradation Batterie-Entladeleistung durch SOC 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_ENTLADELEISTUNG_FAHRMODUS_EDRIVE_AKTIV | unsigned char | Degradation Batterie-Entladeleistung durch Fahrmodus bei eDrive 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_ENTLADELEISTUNG_FAHRMODUS_EDRIVE_AKTIV_TEXT | string | Degradation Batterie-Entladeleistung durch Fahrmodus bei eDrive 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_ENTLADELEISTUNG_TMP_HV_SPEICH_EDRIVE_AKTIV | unsigned char | Degradation Batterie-Entladeleistung durch Temperatur HV-Speicher bei eDrive 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_ENTLADELEISTUNG_TMP_HV_SPEICH_EDRIVE_AKTIV_TEXT | string | Degradation Batterie-Entladeleistung durch Temperatur HV-Speicher bei eDrive 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_ENTLADELEISTUNG_SOC_EDRIVE_AKTIV | unsigned char | Degradation Batterie-Entladeleistung durch SOC bei eDrive 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_ENTLADELEISTUNG_SOC_EDRIVE_AKTIV_TEXT | string | Degradation Batterie-Entladeleistung durch SOC bei eDrive 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_LADELEISTUNG_TEMP_HV_SPEICHER_AKTIV | unsigned char | Degradation Batterie-Ladeleistung durch Temperatur HV-Speicher 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_LADELEISTUNG_TEMP_HV_SPEICHER_AKTIV_TEXT | string | Degradation Batterie-Ladeleistung durch Temperatur HV-Speicher 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_LADELEISTUNG_SOC_AKTIV | unsigned char | Degradation Batterie-Ladeleistung durch SOC 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_BAT_LADELEISTUNG_SOC_AKTIV_TEXT | string | Degradation Batterie-Ladeleistung durch SOC 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_VMOT_TEMP_EMOT_A_AKTIV | unsigned char | Degradation Verbrennungsmotormoment durch Temperatur E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_VMOT_TEMP_EMOT_A_AKTIV_TEXT | string | Degradation Verbrennungsmotormoment durch Temperatur E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_VMOT_TEMP_EMOT_B_AKTIV | unsigned char | Degradation Verbrennungsmotormoment durch Temperatur E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_VMOT_TEMP_EMOT_B_AKTIV_TEXT | string | Degradation Verbrennungsmotormoment durch Temperatur E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_RESERVE_1_20_AKTIV | unsigned char | - - |
| STAT_RESERVE_1_20_AKTIV_TEXT | string | - - |
| STAT_DEGR_MOMENT_VMOT_TEMP_INVERTER_EMOT_A_AKTIV | unsigned char | Degradation Verbrennungsmotormoment durch Temperatur Inverter E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_VMOT_TEMP_INVERTER_EMOT_A_AKTIV_TEXT | string | Degradation Verbrennungsmotormoment durch Temperatur Inverter E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_VMOT_TEMP_INVERTER_EMOT_B_AKTIV | unsigned char | Degradation Verbrennungsmotormoment durch Temperatur Inverter E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_VMOT_TEMP_INVERTER_EMOT_B_AKTIV_TEXT | string | Degradation Verbrennungsmotormoment durch Temperatur Inverter E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_VMOT_TEMP_WMK_AKTIV | unsigned char | Degradation Verbrennungsmotormoment durch Temperatur WMK 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_VMOT_TEMP_WMK_AKTIV_TEXT | string | Degradation Verbrennungsmotormoment durch Temperatur WMK 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_EKK_TEMP_WMK_AKTIV | unsigned char | Degradation elektr. Klimakompressor durch Temperatur WMK 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_EKK_TEMP_WMK_AKTIV_TEXT | string | Degradation elektr. Klimakompressor durch Temperatur WMK 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_EKK_TEMP_EMOT_A_AKTIV | unsigned char | Degradation elektr. Klimakompressor durch Temperatur E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_EKK_TEMP_EMOT_A_AKTIV_TEXT | string | Degradation elektr. Klimakompressor durch Temperatur E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_EKK_TEMP_EMOT_B_AKTIV | unsigned char | Degradation elektr. Klimakompressor durch Temperatur E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_EKK_TEMP_EMOT_B_AKTIV_TEXT | string | Degradation elektr. Klimakompressor durch Temperatur E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_EKK_TEMP_GETR_OEL_AKTIV | unsigned char | Degradation elektr. Klimakompressor durch Temperatur Getriebeöl 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_EKK_TEMP_GETR_OEL_AKTIV_TEXT | string | Degradation elektr. Klimakompressor durch Temperatur Getriebeöl 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_EKK_TEMP_VMOT_KUEHLM_AKTIV | unsigned char | Degradation elektr. Klimakompressor durch Temperatur Kühlmittel VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_EKK_TEMP_VMOT_KUEHLM_AKTIV_TEXT | string | Degradation elektr. Klimakompressor durch Temperatur Kühlmittel VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_EKK_TEMP_VMOT_OEL_AKTIV | unsigned char | Degradation elektr. Klimakompressor durch Temperatur Öl VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_EKK_TEMP_VMOT_OEL_AKTIV_TEXT | string | Degradation elektr. Klimakompressor durch Temperatur Öl VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_RESERVE_1_30_AKTIV | unsigned char | - - |
| STAT_RESERVE_1_30_AKTIV_TEXT | string | - - |
| STAT_DEGR_EKK_TEMP_HV_SPEICHER_AKTIV | unsigned char | Degradation elektr. Klimakompressor durch Temperatur HV-Speicher 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_EKK_TEMP_HV_SPEICHER_AKTIV_TEXT | string | Degradation elektr. Klimakompressor durch Temperatur HV-Speicher 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_RESERVE_2_0_AKTIV | unsigned char | - - |
| STAT_RESERVE_2_0_AKTIV_TEXT | string | - - |
| STAT_RESERVE_2_1_AKTIV | unsigned char | - - |
| STAT_RESERVE_2_1_AKTIV_TEXT | string | - - |
| STAT_RESERVE_2_2_AKTIV | unsigned char | - - |
| STAT_RESERVE_2_2_AKTIV_TEXT | string | - - |
| STAT_RESERVE_2_3_AKTIV | unsigned char | - - |
| STAT_RESERVE_2_3_AKTIV_TEXT | string | - - |
| STAT_RESERVE_2_4_AKTIV | unsigned char | - - |
| STAT_RESERVE_2_4_AKTIV_TEXT | string | - - |
| STAT_RESERVE_2_5_AKTIV | unsigned char | - - |
| STAT_RESERVE_2_5_AKTIV_TEXT | string | - - |
| STAT_RESERVE_2_6_AKTIV | unsigned char | - - |
| STAT_RESERVE_2_6_AKTIV_TEXT | string | - - |
| STAT_DEGR_MOMENT_GETR_TEMP_EMOT_A_AKTIV | unsigned char | Degradation Getriebeausgangsmoment durch Temperatur E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_GETR_TEMP_EMOT_A_AKTIV_TEXT | string | Degradation Getriebeausgangsmoment durch Temperatur E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_GETR_TEMP_EMOT_B_AKTIV | unsigned char | Degradation Getriebeausgangsmoment durch Temperatur E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_GETR_TEMP_EMOT_B_AKTIV_TEXT | string | Degradation Getriebeausgangsmoment durch Temperatur E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_GETR_TEMP_GETR_OEL_AKTIV | unsigned char | Degradation Getriebeausgangsmoment durch Temperatur Getriebeöl 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_GETR_TEMP_GETR_OEL_AKTIV_TEXT | string | Degradation Getriebeausgangsmoment durch Temperatur Getriebeöl 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_GETR_TEMP_VMOT_KUEHLM_AKTIV | unsigned char | Degradation Getriebeausgangsmoment durch Temperatur Kühlmittel VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_GETR_TEMP_VMOT_KUEHLM_AKTIV_TEXT | string | Degradation Getriebeausgangsmoment durch Temperatur Kühlmittel VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_GETR_TEMP_VMOT_OEL_AKTIV | unsigned char | Degradation Getriebeausgangsmoment durch Temperatur Öl VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_GETR_TEMP_VMOT_OEL_AKTIV_TEXT | string | Degradation Getriebeausgangsmoment durch Temperatur Öl VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_GETR_TEMP_HV_SPEICHER_AKTIV | unsigned char | Degradation Getriebeausgangsmoment durch Temperatur HV-Speicher 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_MOMENT_GETR_TEMP_HV_SPEICHER_AKTIV_TEXT | string | Degradation Getriebeausgangsmoment durch Temperatur HV-Speicher 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_EMOT_A_AKTIV | unsigned char | Degradation SOCR durch Temperatur E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_EMOT_A_AKTIV_TEXT | string | Degradation SOCR durch Temperatur E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_EMOT_B_AKTIV | unsigned char | Degradation SOCR durch Temperatur E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_EMOT_B_AKTIV_TEXT | string | Degradation SOCR durch Temperatur E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_INVERTER_EMOT_A_AKTIV | unsigned char | Degradation SOCR durch Temperatur Inverter E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_INVERTER_EMOT_A_AKTIV_TEXT | string | Degradation SOCR durch Temperatur Inverter E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_INVERTER_EMOT_B_AKTIV | unsigned char | Degradation SOCR durch Temperatur Inverter E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_INVERTER_EMOT_B_AKTIV_TEXT | string | Degradation SOCR durch Temperatur Inverter E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_VMOT_KUEHLM_AKTIV | unsigned char | Degradation SOCR durch Temperatur Kühlmittel VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_VMOT_KUEHLM_AKTIV_TEXT | string | Degradation SOCR durch Temperatur Kühlmittel VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_VMOT_OEL_AKTIV | unsigned char | Degradation SOCR durch Temperatur Öl VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_VMOT_OEL_AKTIV_TEXT | string | Degradation SOCR durch Temperatur Öl VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_GETR_OEL_AKTIV | unsigned char | Degradation SOCR durch Temperatur Getriebeöl 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_GETR_OEL_AKTIV_TEXT | string | Degradation SOCR durch Temperatur Getriebeöl 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_RESERVE_2_20_AKTIV | unsigned char | - - |
| STAT_RESERVE_2_20_AKTIV_TEXT | string | - - |
| STAT_DEGR_SOCR_TEMP_AMP_AKTIV | unsigned char | Degradation SOCR durch Temperatur APM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_SOCR_TEMP_AMP_AKTIV_TEXT | string | Degradation SOCR durch Temperatur APM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_EMOT_A_AKTIV | unsigned char | Degradation Rekuperation durch Temperatur E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_EMOT_A_AKTIV_TEXT | string | Degradation Rekuperation durch Temperatur E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_EMOT_B_AKTIV | unsigned char | Degradation Rekuperation durch Temperatur E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_EMOT_B_AKTIV_TEXT | string | Degradation Rekuperation durch Temperatur E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_GETR_OEL_AKTIV | unsigned char | Degradation Rekuperation durch Temperatur Getriebeöl 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_GETR_OEL_AKTIV_TEXT | string | Degradation Rekuperation durch Temperatur Getriebeöl 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_VMOT_KUEHLM_AKTIV | unsigned char | Degradation Rekuperation durch Temperatur Kühlmittel VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_VMOT_KUEHLM_AKTIV_TEXT | string | Degradation Rekuperation durch Temperatur Kühlmittel VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_VMOT_OEL_AKTIV | unsigned char | Degradation Rekuperation durch Temperatur Öl VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_VMOT_OEL_AKTIV_TEXT | string | Degradation Rekuperation durch Temperatur Öl VM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_HV_SPEICHER_AKTIV | unsigned char | Degradation Rekuperation durch Temperatur HV-Speicher 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_HV_SPEICHER_AKTIV_TEXT | string | Degradation Rekuperation durch Temperatur HV-Speicher 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_SOC_AKTIV | unsigned char | Degradation Rekuperation durch SOC 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_SOC_AKTIV_TEXT | string | Degradation Rekuperation durch SOC 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_INVERTER_EMOT_A_AKTIV | unsigned char | Degradation Rekuperation durch Temperatur Inverter E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_INVERTER_EMOT_A_AKTIV_TEXT | string | Degradation Rekuperation durch Temperatur Inverter E-Maschine A 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_INVERTER_EMOT_B_AKTIV | unsigned char | Degradation Rekuperation durch Temperatur Inverter E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_INVERTER_EMOT_B_AKTIV_TEXT | string | Degradation Rekuperation durch Temperatur Inverter E-Maschine B 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_APM_AKTIV | unsigned char | Degradation Rekuperation durch Temperatur APM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_DEGR_REKU_TEMP_APM_AKTIV_TEXT | string | Degradation Rekuperation durch Temperatur APM 1=Degradation aktiv /0=Degradation nicht aktiv |
| STAT_REQDRND_DR_NR | real | Lese Anzahl der EMF Hilferufe in D/S/M/R |
| STAT_REQDRND_N_NR | real | Lese Anzahl der EMF Hilferufe in N |
| STAT_DEN_BPCM_01 | real | Nenner BPCM 01 |
| STAT_DEN_BPCM_02 | real | Nenner BPCM 02 |
| STAT_DEN_BPCM_03 | real | Nenner BPCM 03 |
| STAT_DEN_BPCM_04 | real | Nenner BPCM 04 |
| STAT_DEN_BPCM_05 | real | Nenner BPCM 05 |
| STAT_DEN_BPCM_06 | real | Nenner BPCM 06 |
| STAT_DEN_BPCM_07 | real | Nenner BPCM 07 |
| STAT_DEN_BPCM_08 | real | Nenner BPCM 08 |
| STAT_DEN_BPCM_09 | real | Nenner BPCM 09 |
| STAT_DEN_BPCM_10 | real | Nenner BPCM 10 |
| STAT_DEN_BPCM_11 | real | Nenner BPCM 11 |
| STAT_DEN_BPCM_12 | real | Nenner BPCM 12 |
| STAT_DEN_BPCM_13 | real | Nenner BPCM 13 |
| STAT_DEN_BPCM_14 | real | Nenner BPCM 14 |
| STAT_DEN_BPCM_15 | real | Nenner BPCM 15 |
| STAT_DEN_BPCM_16 | real | Nenner BPCM 16 |
| STAT_DEN_BPCM_17 | real | Nenner BPCM 17 |
| STAT_DEN_BPCM_18 | real | Nenner BPCM 18 |
| STAT_DEN_BPCM_19 | real | Nenner BPCM 19 |
| STAT_DEN_BPCM_20 | real | Nenner BPCM 20 |
| STAT_DEN_BPCM_21 | real | Nenner BPCM 21 |
| STAT_DEN_BPCM_22 | real | Nenner BPCM 22 |
| STAT_DEN_BPCM_23 | real | Nenner BPCM 23 |
| STAT_DEN_BPCM_24 | real | Nenner BPCM 24 |
| STAT_DEN_BPCM_25 | real | Nenner BPCM 25 |
| STAT_DEN_BPCM_26 | real | Nenner BPCM 26 |
| STAT_DEN_BPCM_27 | real | Nenner BPCM 27 |
| STAT_DEN_BPCM_28 | real | Nenner BPCM 28 |
| STAT_DEN_BPCM_29 | real | Nenner BPCM 29 |
| STAT_DEN_BPCM_30 | real | Nenner BPCM 30 |
| STAT_DEN_BPCM_31 | real | Nenner BPCM 31 |
| STAT_DEN_BPCM_32 | real | Nenner BPCM 32 |
| STAT_NUM_BPCM_01 | real | @@Zähler@@ BPCM 01 |
| STAT_NUM_BPCM_02 | real | Zähler BPCM 02 |
| STAT_NUM_BPCM_03 | real | Zähler BPCM 03 |
| STAT_NUM_BPCM_04 | real | Zähler BPCM 04 |
| STAT_NUM_BPCM_05 | real | Zähler BPCM 05 |
| STAT_NUM_BPCM_06 | real | Zähler BPCM 06 |
| STAT_NUM_BPCM_07 | real | Zähler BPCM 07 |
| STAT_NUM_BPCM_08 | real | Zähler BPCM 08 |
| STAT_NUM_BPCM_09 | real | Zähler BPCM 09 |
| STAT_NUM_BPCM_10 | real | Zähler BPCM 10 |
| STAT_NUM_BPCM_11 | real | Zähler BPCM 11 |
| STAT_NUM_BPCM_12 | real | Zähler BPCM 12 |
| STAT_NUM_BPCM_13 | real | Zähler BPCM 13 |
| STAT_NUM_BPCM_14 | real | Zähler BPCM 14 |
| STAT_NUM_BPCM_15 | real | Zähler BPCM 15 |
| STAT_NUM_BPCM_16 | real | Zähler BPCM 16 |
| STAT_NUM_BPCM_17 | real | Zähler BPCM 17 |
| STAT_NUM_BPCM_18 | real | Zähler BPCM 18 |
| STAT_NUM_BPCM_19 | real | Zähler BPCM 19 |
| STAT_NUM_BPCM_20 | real | Zähler BPCM 20 |
| STAT_NUM_BPCM_21 | real | Zähler BPCM 21 |
| STAT_NUM_BPCM_22 | real | Zähler BPCM 22 |
| STAT_NUM_BPCM_23 | real | Zähler BPCM 23 |
| STAT_NUM_BPCM_24 | real | Zähler BPCM 24 |
| STAT_NUM_BPCM_25 | real | Zähler BPCM 25 |
| STAT_NUM_BPCM_26 | real | Zähler BPCM 26 |
| STAT_NUM_BPCM_27 | real | Zähler BPCM 27 |
| STAT_NUM_BPCM_28 | real | Zähler BPCM 28 |
| STAT_NUM_BPCM_29 | real | Zähler BPCM 29 |
| STAT_NUM_BPCM_30 | real | Zähler BPCM 30 |
| STAT_NUM_BPCM_31 | real | Zähler BPCM 31 |
| STAT_NUM_BPCM_32 | real | Zähler BPCM 32 |
| STAT_DEN_MCPA_01 | real | Nenner MCPA 01 |
| STAT_DEN_MCPA_02 | real | Nenner MCPA 02 |
| STAT_DEN_MCPA_03 | real | Nenner MCPA 03 |
| STAT_DEN_MCPA_04 | real | Nenner MCPA 04 |
| STAT_DEN_MCPA_05 | real | Nenner MCPA 05 |
| STAT_NUM_MCPA_01 | real | Zähler MCPA 01 |
| STAT_NUM_MCPA_02 | real | Zähler MCPA 02 |
| STAT_NUM_MCPA_03 | real | Zähler MCPA 03 |
| STAT_NUM_MCPA_04 | real | Zähler MCPA 04 |
| STAT_NUM_MCPA_05 | real | Zähler MCPA 05 |
| STAT_DEN_MCPB_01 | real | Nenner MCPB 01 |
| STAT_DEN_MCPB_02 | real | Nenner MCPB 02 |
| STAT_DEN_MCPB_03 | real | Nenner MCPB 03 |
| STAT_DEN_MCPB_04 | real | Nenner MCPB 04 |
| STAT_DEN_MCPB_05 | real | Nenner MCPB 05 |
| STAT_NUM_MCPB_01 | real | Zähler MCPB 01 |
| STAT_NUM_MCPB_02 | real | Zähler MCPB 02 |
| STAT_NUM_MCPB_03 | real | Zähler MCPB 03 |
| STAT_NUM_MCPB_04 | real | Zähler MCPB 04 |
| STAT_NUM_MCPB_05 | real | Zähler MCPB 05 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-batterie-kuehlung"></a>
### STATUS_BATTERIE_KUEHLUNG

Job ließt die Daten der Batteriekühlung aus.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ATEMP_GUELTIG | unsigned char | Außentemperatur gültig. |
| STAT_ATEMP_GUELTIG_TEXT | string | 1= gültig, 0= ungültig |
| STAT_TBATMOD_MAX_FEHLER | unsigned char | Batteriemodultemperatur maximal Fehler. 1= Fehler vorhanden, 0= kein Fehler vorhanden |
| STAT_TBATMOD_MAX_FEHLER_TEXT | string | Batteriemodultemperatur maximal Fehler. 1= Fehler vorhanden, 0= kein Fehler vorhanden |
| STAT_TBATMOD_MIN_FEHLER | unsigned char | Batteriemodultemperatur minimal Fehler. 1= Fehler vorhanden, 0= kein Fehler vorhanden |
| STAT_TBATMOD_MIN_FEHLER_TEXT | string | Batteriemodultemperatur minimal Fehler. 1= Fehler vorhanden, 0= kein Fehler vorhanden |
| STAT_TBATCOOLNT_IN_FEHLER | unsigned char | Kühlmitteltemperatur Einlass Fehler. 1= Fehler vorhanden, 0= kein Fehler vorhanden |
| STAT_TBATCOOLNT_IN_FEHLER_TEXT | string | Kühlmitteltemperatur Einlass Fehler. 1= Fehler vorhanden, 0= kein Fehler vorhanden |
| STAT_TBATCOOLNT_OUT_FEHLER | unsigned char | Kühlmitteltemperatur Auslass Fehler. 1= Fehler vorhanden, 0= kein Fehler vorhanden |
| STAT_TBATCOOLNT_OUT_FEHLER_TEXT | string | Kühlmitteltemperatur Auslass Fehler. 1= Fehler vorhanden, 0= kein Fehler vorhanden |
| STAT_COOLPWR_FEHLER | unsigned char | Fehler Kühlleistung Chiller. 1= Fehler vorhanden, 0= kein Fehler vorhanden |
| STAT_COOLPWR_FEHLER_TEXT | string | Fehler Kühlleistung Chiller. 1= Fehler vorhanden, 0= kein Fehler vorhanden |
| STAT_BATCOOL_NR | unsigned char | Betriebsmodus |
| STAT_BATCOOL_NR_TEXT | string | 0 = Kühlung aus 1 = Zirkulation zur Homogenisierung 3 = Vorkühlung 4 = Kühlung über Radiator 5 = Duplex Kühlung über Radiator und Chiller 6 = Kühlung über Chiller 8 = Vorkühlung Variante 1 9 = Vorkühlung Variante 2 11 = Kühlung über Radiator Variante 1 12 = Kühlung über Radiator Variante 2 14 = Duplex Kühlung Variante 1 15 = Duplex Kühlung Variante 2 17 = Kühlung über Chiller Variante 1 18 = Kühlung über Chiller Variante 2 19 = Kühlung über Chiller Variante 3 21 = Chiller keine Freigabe/defekt, Kühlung über Radiator 22 = Chiller keine Freigabe/defekt, Kühlung über Radiator Variante 1 23 = Chiller keine Freigabe/defekt, Kühlung über Radiator Variante 2 24 = Chiller keine Freigabe/defekt, keine Kühlung über Radiator möglich 25 = Duplexmodus, Chiller keine Freigabe/defekt, Kühlung über Radiator 26 = Duplexmodus, Chiller keine Freigabe/defekt, Kühlung über Radiator Variante 1 27 = Duplexmodus, Chiller keine Freigabe/defekt, Kühlung über Radiator Variante 2 28 = Duplexmodus, Chiller keine Freigabe/defekt, keine Kühlung über Radiator möglich 29 = Zirkulation zur Nachkühlung 30 = Ventil Radiator defekt, keine Kühlung über Chiller möglich 31 = Ventil Radiator defekt, Kühlung über Chiller |
| STAT_LUEFTER_GEFORDERT_NR | unsigned char | Anforderung E-Lüfter |
| STAT_LUEFTER_GEFORDERT_NR_TEXT | string | 0= Stufe 0 1= Stufe 1 2= Stufe 2 3= Stufe 3 4= Stufe 4 5= Stufe 5 6= Stufe 6 7= Stufe 7 8= Stufe 8 9= Stufe 9 10= Stufe 10 11= Stufe 11 12= Stufe 12 13= Stufe 13 14= Stufe 14 15= ungültig |
| STAT_DUOVLVE_CHILL_NR | unsigned char | Anforderung Duoventil Chiller. 1= offen 0= geschlossen |
| STAT_DUOVLVE_CHILL_NR_TEXT | string | Anforderung Duoventil Chiller. 1= offen 0= geschlossen |
| STAT_DUOVLVE_WAERMETAUSCHER_NR | unsigned char | Anforderung Duoventil HeatExchanger (Wärmetauscher) |
| STAT_DUOVLVE_WAERMETAUSCHER_NR_TEXT | string | 1= offen 0= geschlossen |
| STAT_BLCKVLVE_CHILL_NR | unsigned char | Anforderung Kältemittelabsperrventil Chiller, 1= offen 0= geschlossen |
| STAT_BLCKVLVE_CHILL_NR_TEXT | string | Anforderung Kältemittelabsperrventil Chiller, 1= offen 0= geschlossen |
| STAT_COMPRSR_NR | unsigned char | Anforderung Kompressor IHKA. 1= offen 0= geschlossen |
| STAT_COMPRSR_NR_TEXT | string | Anforderung Kompressor IHKA. 1= offen 0= geschlossen |
| STAT_COMPRSR_FREIGABE_NR | unsigned char | Freigabe Kompressor IHKA. 1= freigegeben 0= nicht freigegeben |
| STAT_COMPRSR_FREIGABE_NR_TEXT | string | Freigabe Kompressor IHKA. 1= freigegeben 0= nicht freigegeben |
| STAT_BLCKVLVE_CHILL_ZWANGSANF_NR | unsigned char | Zwangsstellungsanforderung Kältemittelabsperrventil Chiller. 1= gefordert, 0= nicht gefordert |
| STAT_BLCKVLVE_CHILL_ZWANGSANF_NR_TEXT | string | Zwangsstellungsanforderung Kältemittelabsperrventil Chiller. 1= gefordert, 0= nicht gefordert |
| STAT_PUMP_GESCHWINDIGKEIT_SOLL_EINH | string | "%" |
| STAT_PUMP_GESCHWINDIGKEIT_SOLL_WERT | real | Anforderung Pumpengeschwindigkeit. Soll-Wert |
| STAT_PUMP_GESCHWINDIGKEIT_IST_EINH | string | "%" |
| STAT_PUMP_GESCHWINDIGKEIT_IST_WERT | real | Rückmeldung Pumpengeschwindigkeit. IST-Wert |
| STAT_GESCHAETZTE_KUEHLLEITUNG_EINH | string | "%" |
| STAT_GESCHAETZTE_KUEHLLEITUNG_WERT | real | Geschätzte Kühlleistung |
| STAT_ATEMP_EINH | string | "°C" |
| STAT_ATEMP_WERT | real | Außentemperatur |
| STAT_TBATMOD_MAX_EINH | string | "°C" |
| STAT_TBATMOD_MAX_WERT | real | Batteriemodultemperatur maximal |
| STAT_TBATMOD_MIN_EINH | string | "°C" |
| STAT_TBATMOD_MIN_WERT | real | Batteriemodultemperatur minimal |
| STAT_TBATCOOLNT_IN_EINH | string | "°C" |
| STAT_TBATCOOLNT_IN_WERT | real | Kühlmitteltemperatur Einlass |
| STAT_TBATCOOLNT_OUT_EINH | string | "°C" |
| STAT_TBATCOOLNT_OUT_WERT | real | Kühlmitteltemperatur Auslass |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-batterie-kuehlung"></a>
### STEUERN_BATTERIE_KUEHLUNG

Job zum Ansteuern der Kühlsystemkonfiguration

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARGUMENT | string | Werttabelle 0 = Keine Vorgabe Kühlungsmodus 1 = Vorgabe Kühlung im Chillermodus 2 = Vorgabe Kühlung im HeatExchangermodus 3 = Vorgabe Kühlung im Duplexmodus 4 = Vorgabe Befüllung Chillerkreis 5 = Vorgabe Befüllung HeatExchangerkreis 6 = Vorgabe Befüllung beide Kreise 7 = Vorgabe Kühlung aus |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-hcp-rbm-ratios"></a>
### STATUS_HCP_RBM_RATIOS

Auslesen der Ratios vom HCP

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DEN_BPCM_01 | real | Nenner BPCM 01 |
| STAT_DEN_BPCM_02 | real | Nenner BPCM 02 |
| STAT_DEN_BPCM_03 | real | Nenner BPCM 03 |
| STAT_DEN_BPCM_04 | real | Nenner BPCM 04 |
| STAT_DEN_BPCM_05 | real | Nenner BPCM 05 |
| STAT_DEN_BPCM_06 | real | Nenner BPCM 06 |
| STAT_DEN_BPCM_07 | real | Nenner BPCM 07 |
| STAT_DEN_BPCM_08 | real | Nenner BPCM 08 |
| STAT_DEN_BPCM_09 | real | Nenner BPCM 09 |
| STAT_DEN_BPCM_10 | real | Nenner BPCM 10 |
| STAT_DEN_BPCM_11 | real | Nenner BPCM 11 |
| STAT_DEN_BPCM_12 | real | Nenner BPCM 12 |
| STAT_DEN_BPCM_13 | real | Nenner BPCM 13 |
| STAT_DEN_BPCM_14 | real | Nenner BPCM 14 |
| STAT_DEN_BPCM_15 | real | Nenner BPCM 15 |
| STAT_DEN_BPCM_16 | real | Nenner BPCM 16 |
| STAT_DEN_BPCM_17 | real | Nenner BPCM 17 |
| STAT_DEN_BPCM_18 | real | Nenner BPCM 18 |
| STAT_DEN_BPCM_19 | real | Nenner BPCM 19 |
| STAT_DEN_BPCM_20 | real | Nenner BPCM 20 |
| STAT_DEN_BPCM_21 | real | Nenner BPCM 21 |
| STAT_DEN_BPCM_22 | real | Nenner BPCM 22 |
| STAT_DEN_BPCM_23 | real | Nenner BPCM 23 |
| STAT_DEN_BPCM_24 | real | Nenner BPCM 24 |
| STAT_DEN_BPCM_25 | real | Nenner BPCM 25 |
| STAT_DEN_BPCM_26 | real | Nenner BPCM 26 |
| STAT_DEN_BPCM_27 | real | Nenner BPCM 27 |
| STAT_DEN_BPCM_28 | real | Nenner BPCM 28 |
| STAT_DEN_BPCM_29 | real | Nenner BPCM 29 |
| STAT_DEN_BPCM_30 | real | Nenner BPCM 30 |
| STAT_DEN_BPCM_31 | real | Nenner BPCM 31 |
| STAT_DEN_BPCM_32 | real | Nenner BPCM 32 |
| STAT_NUM_BPCM_01 | real | @@Zähler@@ BPCM 01 |
| STAT_NUM_BPCM_02 | real | Zähler BPCM 02 |
| STAT_NUM_BPCM_03 | real | Zähler BPCM 03 |
| STAT_NUM_BPCM_04 | real | Zähler BPCM 04 |
| STAT_NUM_BPCM_05 | real | Zähler BPCM 05 |
| STAT_NUM_BPCM_06 | real | Zähler BPCM 06 |
| STAT_NUM_BPCM_07 | real | Zähler BPCM 07 |
| STAT_NUM_BPCM_08 | real | Zähler BPCM 08 |
| STAT_NUM_BPCM_09 | real | Zähler BPCM 09 |
| STAT_NUM_BPCM_10 | real | Zähler BPCM 10 |
| STAT_NUM_BPCM_11 | real | Zähler BPCM 11 |
| STAT_NUM_BPCM_12 | real | Zähler BPCM 12 |
| STAT_NUM_BPCM_13 | real | Zähler BPCM 13 |
| STAT_NUM_BPCM_14 | real | Zähler BPCM 14 |
| STAT_NUM_BPCM_15 | real | Zähler BPCM 15 |
| STAT_NUM_BPCM_16 | real | Zähler BPCM 16 |
| STAT_NUM_BPCM_17 | real | Zähler BPCM 17 |
| STAT_NUM_BPCM_18 | real | Zähler BPCM 18 |
| STAT_NUM_BPCM_19 | real | Zähler BPCM 19 |
| STAT_NUM_BPCM_20 | real | Zähler BPCM 20 |
| STAT_NUM_BPCM_21 | real | Zähler BPCM 21 |
| STAT_NUM_BPCM_22 | real | Zähler BPCM 22 |
| STAT_NUM_BPCM_23 | real | Zähler BPCM 23 |
| STAT_NUM_BPCM_24 | real | Zähler BPCM 24 |
| STAT_NUM_BPCM_25 | real | Zähler BPCM 25 |
| STAT_NUM_BPCM_26 | real | Zähler BPCM 26 |
| STAT_NUM_BPCM_27 | real | Zähler BPCM 27 |
| STAT_NUM_BPCM_28 | real | Zähler BPCM 28 |
| STAT_NUM_BPCM_29 | real | Zähler BPCM 29 |
| STAT_NUM_BPCM_30 | real | Zähler BPCM 30 |
| STAT_NUM_BPCM_31 | real | Zähler BPCM 31 |
| STAT_NUM_BPCM_32 | real | Zähler BPCM 32 |
| STAT_DEN_MCPA_01 | real | Nenner MCPA 01 |
| STAT_DEN_MCPA_02 | real | Nenner MCPA 02 |
| STAT_DEN_MCPA_03 | real | Nenner MCPA 03 |
| STAT_DEN_MCPA_04 | real | Nenner MCPA 04 |
| STAT_DEN_MCPA_05 | real | Nenner MCPA 05 |
| STAT_NUM_MCPA_01 | real | Zähler MCPA 01 |
| STAT_NUM_MCPA_02 | real | Zähler MCPA 02 |
| STAT_NUM_MCPA_03 | real | Zähler MCPA 03 |
| STAT_NUM_MCPA_04 | real | Zähler MCPA 04 |
| STAT_NUM_MCPA_05 | real | Zähler MCPA 05 |
| STAT_DEN_MCPB_01 | real | Nenner MCPB 01 |
| STAT_DEN_MCPB_02 | real | Nenner MCPB 02 |
| STAT_DEN_MCPB_03 | real | Nenner MCPB 03 |
| STAT_DEN_MCPB_04 | real | Nenner MCPB 04 |
| STAT_DEN_MCPB_05 | real | Nenner MCPB 05 |
| STAT_NUM_MCPB_01 | real | Zähler MCPB 01 |
| STAT_NUM_MCPB_02 | real | Zähler MCPB 02 |
| STAT_NUM_MCPB_03 | real | Zähler MCPB 03 |
| STAT_NUM_MCPB_04 | real | Zähler MCPB 04 |
| STAT_NUM_MCPB_05 | real | Zähler MCPB 05 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-batterie-equilibrierung"></a>
### STATUS_BATTERIE_EQUILIBRIERUNG

Zustand Batterie-Equilibrierung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EQU_PHASE_NR | unsigned char | Aktueller Status der Batterie- Equilibrierungs Routine Wertetabelle: 0= AUS 1= Entladepahse SOC &gt;30% 2= Entladepahse SOC &gt;20% 3= Entladephase SOC &gt;10% 4= Stabilisierungsphase 5= Equlibrierungspahse 6= Erholungsphase 7= Ladephase SOC &lt;20% 8= Ladephase SOC &lt;30% 9= Equilibrierung beendet |
| STAT_EQU_PHASE_NR_TEXT | string | Aktueller Status der Batterie- Equilibrierungs Routine Wertetabelle: 0= AUS 1= Entladepahse SOC &gt;30% 2= Entladepahse SOC &gt;20% 3= Entladephase SOC &gt;10% 4= Stabilisierungsphase 5= Equlibrierungspahse 6= Erholungsphase 7= Ladephase SOC &lt;20% 8= Ladephase SOC &lt;30% 9= Equilibrierung beendet |
| STAT_EQU_SPERR_BED_1_ERFUELLT | unsigned char | Sperrbedingung n.n Wertetabelle: 0= Sperrbed.liegt nicht an 1= Sperrbed.liegt an |
| STAT_EQU_SPERR_BED_1_ERFUELLT_TEXT | string | Sperrbedingung n.n Wertetabelle: 0= Sperrbed.liegt nicht an 1= Sperrbed.liegt an |
| STAT_EQU_SPERR_BED_2_ERFUELLT | unsigned char | Sperrbedingung: SOC niedrig Wertetabelle: 0= Sperrbed.liegt nicht an 1= Sperrbed.liegt an |
| STAT_EQU_SPERR_BED_2_ERFUELLT_TEXT | string | Sperrbedingung: SOC niedrig Wertetabelle: 0= Sperrbed.liegt nicht an 1= Sperrbed.liegt an |
| STAT_EQU_SPERR_BED_3_ERFUELLT | unsigned char | Sperrbedingung: 12-Spannung zu niedrig Wertetabelle: 0= Sperrbed.liegt nicht an 1= Sperrbed.liegt an |
| STAT_EQU_SPERR_BED_3_ERFUELLT_TEXT | string | Sperrbedingung: 12-Spannung zu niedrig Wertetabelle: 0= Sperrbed.liegt nicht an 1= Sperrbed.liegt an |
| STAT_EQU_SPERR_BED_4_ERFUELLT | unsigned char | Sperrbedingung: Verbrennerdrehzahl zu hoch Wertetabelle: 0= Sperrbed.liegt nicht an 1= Sperrbed.liegt an |
| STAT_EQU_SPERR_BED_4_ERFUELLT_TEXT | string | Sperrbedingung: Verbrennerdrehzahl zu hoch Wertetabelle: 0= Sperrbed.liegt nicht an 1= Sperrbed.liegt an |
| STAT_EQU_SPERR_BED_5_ERFUELLT | unsigned char | Sperrbedingung: v zu hoch Wertetabelle: 0= Sperrbed.liegt nicht an 1= Sperrbed.liegt an |
| STAT_EQU_SPERR_BED_5_ERFUELLT_TEXT | string | Sperrbedingung: v zu hoch Wertetabelle: 0= Sperrbed.liegt nicht an 1= Sperrbed.liegt an |
| STAT_EQU_SPERR_BED_6_ERFUELLT | unsigned char | Sperrbedingung: Getriebe nicht in P Wertetabelle: 0= Sperrbed.liegt nicht an 1= Sperrbed.liegt an |
| STAT_EQU_SPERR_BED_6_ERFUELLT_TEXT | string | Sperrbedingung: Getriebe nicht in P Wertetabelle: 0= Sperrbed.liegt nicht an 1= Sperrbed.liegt an |
| STAT_EQU_SPERR_BED_7_ERFUELLT | unsigned char | Sperrbedingung: SOC Güte zu niedrig Wertetabelle: 0= Sperrbed.liegt nicht an 1= Sperrbed.liegt an |
| STAT_EQU_SPERR_BED_7_ERFUELLT_TEXT | string | Sperrbedingung: SOC Güte zu niedrig Wertetabelle: 0= Sperrbed.liegt nicht an 1= Sperrbed.liegt an |
| STAT_EQU_SPERR_BED_8_ERFUELLT | unsigned char | Sperrbedingung: Nicht in Energiesparmode Wertetabelle: 0= Sperrbed.liegt nicht an 1= Sperrbed.liegt an |
| STAT_EQU_SPERR_BED_8_ERFUELLT_TEXT | string | Sperrbedingung: Nicht in Energiesparmode Wertetabelle: 0= Sperrbed.liegt nicht an 1= Sperrbed.liegt an |
| STAT_EQU_SPERR_BED_9_ERFUELLT | unsigned char | Sperrbedingung: Timer abgelaufen Wertetabelle: 0= Sperrbed.liegt nicht an 1= Sperrbed.liegt an |
| STAT_EQU_SPERR_BED_9_ERFUELLT_TEXT | string | Sperrbedingung: Timer abgelaufen Wertetabelle: 0= Sperrbed.liegt nicht an 1= Sperrbed.liegt an |
| STAT_EQU_JOB_ABBRUCH | unsigned char | Equilibrierungsroutine angebrochen Wertetabelle: 0= EQU-Routine nicht beendet 1= EQU-Routine beendet |
| STAT_EQU_JOB_ABBRUCH_TEXT | string | Equilibrierungsroutine angebrochen Wertetabelle: 0= EQU-Routine nicht beendet 1= EQU-Routine beendet |
| STAT_EQU_JOB_AKTIV | unsigned char | Equilibrierungsroutine aktiv Wertetabelle: 0= EQU-Routine nicht aktiv 1= EQU-Routine aktiv |
| STAT_EQU_JOB_AKTIV_TEXT | string | Equilibrierungsroutine aktiv Wertetabelle: 0= EQU-Routine nicht aktiv 1= EQU-Routine aktiv |
| STAT_BATT_EQU_RESTZEIT_EINH | string | "s" |
| STAT_BATT_EQU_RESTZEIT_WERT | real | Gibt die verbleibende Zeit der Batterie- Equilibrierung aus |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-batterie-equilibrierung"></a>
### STEUERN_BATTERIE_EQUILIBRIERUNG

Steuern der Batterie-Equilibrierung.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION | string | Werttabelle 0 = AUS 1 = AKTIV 2 = beendet |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-batterie-nutzung"></a>
### STATUS_BATTERIE_NUTZUNG

Liest die Variablen der Batterienutzung aus.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BATTERIE_LAUFKILOMETER_EINH | string | "km" |
| STAT_BATTERIE_LAUFKILOMETER_WERT | real | Liest die von der Batterie gesehene Laufkilometern in km aus. |
| STAT_BATTERIE_WH_DIST_NORM_EINH | string | "Batterie-Nutzung normiert in Wh/km (temperaturbewertet)" |
| STAT_BATTERIE_WH_DIST_NORM_WERT | real | Liest die Batterie gesehene Wh/Km normiert aus Der Wert wird durch die Batterie-Temperatur beinflusst und entsprechend gewichtet. Bei hoher Temperatur steigt der Gewichtungsfaktor, der dadurch die freigegebene Leistung der Batterie einschränkt. Für eine aussagekräftige normierte Batterie-Nutzung muss die Batterie-Distanz mindestens 5000km betragen. |
| STAT_BATTERIE_WH_EINH | string | "Batterie-Energie in Wh (temperaturbewertet)" |
| STAT_BATTERIE_WH_WERT | real | Liest die Batterie gesehene Wh aus Der Wert wird durch die Batterie-Temperatur beinflusst und entsprechend gewichtet. Bei hoher Temperatur steigt der Gewichtungsfaktor, der dadurch die freigegebene Leistung der Batterie einschränkt. |
| STAT_BATTERIE_WH_DIST_EINH | string | "Batterie-Nutzung in Wh/km (temperaturbewertet)" |
| STAT_BATTERIE_WH_DIST_WERT | real | Liest die Batterie gesehene Wh/Km aus Der Wert wird durch die Batterie-Temperatur beinflusst und entsprechend gewichtet. Bei hoher Temperatur steigt der Gewichtungsfaktor, der dadurch die freigegebene Leistung pro km der Batterie einschränkt. Für eine aussagekräftige Batterie-Nutzung muss die Batterie-Distanz mindestens 5000km betragen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-kurzschluss-uvw-emp"></a>
### STEUERN_KURZSCHLUSS_UVW_EMP

Steuert aktiven Kurzschluss an EMP

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION | string | 0 = inaktiv (Kurzschluss UVW gegen DC-Minus inaktiv) 1 = aktiv (Kurzschluss UVW gegen DC-Minus aktiv) 2 = beendet (Kurzschluss UVW gegen DC-Minus von Benutzer beendet) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-timer-batterie-kuehlung"></a>
### STEUERN_TIMER_BATTERIE_KUEHLUNG

Job zum Vorgeben der maximalen Laufzeit des JOBS STEUERN_BATTERIE_KUEHLUNG

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LAUFZEIT | unsigned long | maximalen Laufzeit fuer den Job STEUERN_BATTERIE_KUEHLUNG Bereich: 0-65000s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-batterie-adaptionswerte-lesen"></a>
### STATUS_BATTERIE_ADAPTIONSWERTE_LESEN

Batterie Adaptionswert lesen Daten muessen vor dem Flashen gesichert werden.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BATTERIE_ACK_LADE_AMPERESTUNDEN_EINH | string | Einheit der ackumulieren Leistung "Ah" |
| STAT_BATTERIE_ACK_LADE_AMPERESTUNDEN_WERT | real | Ackumulierte Ladeamperstunden der HV-Batterie |
| STAT_BATTERIE_ACK_ENTLADE_AMPERESTUNDEN_EINH | string | Einheit der ackumulieren Leistung "Ah" |
| STAT_BATTERIE_ACK_ENTLADE_AMPERESTUNDEN_WERT | real | Ackumulierte Entladeamperstunden der HV-Batterie |
| STAT_BATTERIE_WH_EINH | string | "Wh" |
| STAT_BATTERIE_WH_WERT | real | Liest die Variablen der Batterienutzung in Wh aus |
| STAT_BATTERIE_KM_STAND_AUSTAUSCH_EINH | string | "km" |
| STAT_BATTERIE_KM_STAND_AUSTAUSCH_WERT | real | Kilometerstand des Fahrzeuges beim Batterietausch |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-batterie-adaptionswerte-geschrieben"></a>
### STATUS_BATTERIE_ADAPTIONSWERTE_GESCHRIEBEN

Ließt den Status nach dem Adaptionswerte schreiben aus.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BATT_ADAPTIONSWERTE_OKAY | unsigned char | Ließt den Status nach dem Adaptionswerte schreiben aus. |
| STAT_BATT_ADAPTIONSWERTE_OKAY_TEXT | string | WerteTabelle: 0 = nicht OK 1 = OK |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-batterie-adaptionswerte-schreiben"></a>
### STEUERN_BATTERIE_ADAPTIONSWERTE_SCHREIBEN

Daten muessen nach dem Flashen geschrieben werden. SG muss vorher in Werkstattmode gesetzt werden

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BATTERIE_ACK_LADE_AMPERESTUNDEN | real | Ackumulierte Ladeamperstunden der HV-Batterie in Ah Auflösung=1 |
| BATTERIE_ACK_ENTLADE_AMPERESTUNDEN | real | Ackumulierte Entladeamperstunden der HV-Batterie in Ah Auflösung=1 |
| BATTERIE_WH | string | Batterienutzung in Wh Auflösung=0,1 |
| BATTERIE_KM_STAND_AUSTAUSCH | string | Kilometerstand des Fahrzeuges beim Batterietausch in km Auflösung=0,1 |
| SOC_STIMM_WERT | real | HV-Batterie SOC der an HOS gesendet wird in % Auflösung 1 |
| BATTERIE_ADAPT_RUECKSCHREIBEN_IO | string | Werttabelle 0 = Rueckschreiben nicht erlaubt 1 = Rueckschreiben erlaubt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-vm-leistungsmessung"></a>
### STATUS_VM_LEISTUNGSMESSUNG

Rückmeldung des Status Motorleistungstest

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VM_LEISTUNGSMESSUNG_NR | unsigned char | Rückmeldung des Status Motorleistungstest |
| STAT_VM_LEISTUNGSMESSUNG_NR_TEXT | string | WerteTabelle 0= aus 1= an 2= gesperrt 3= Testzeitraum abgelaufen 4= kein Wert |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-vm-leistung-lesen"></a>
### STATUS_VM_LEISTUNG_LESEN

Rückgabe der VM-Werte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VM_LEISTUNG_01_EINH | string | "kW" |
| STAT_VM_LEISTUNG_01_WERT | real | Rückgabe der VM-Leistung in kW |
| STAT_VM_MOMENT_02_EINH | string | "Nm" |
| STAT_VM_MOMENT_02_WERT | real | Rückgabe des VM-Momentes in Nm |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-vm-leistungsmessung"></a>
### STEUERN_VM_LEISTUNGSMESSUNG

Für Motorleistungstest müssen elektrische Antriebskomponenten neutralisiert werden. Fzg. fährt rein verbrennungsmotorisch. 1= nur Verbrennungsmotor 0= VM und E-Motor ENERGIEPARMODE muss an sein Job ist 10 Minuten aktiv und kann nicht ausgeschalten werden!

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION | string | Werttabelle 0 = AUS 1 = EIN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-batterie-equil-historie"></a>
### STATUS_BATTERIE_EQUIL_HISTORIE

Historie der Batterie Equilibrierung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BATT_EQU_BETRIEBSSTUNDE_LAST_EQU_EINH | string | Letzte Batterie Equilibrierung durchgeführt bei Betriebsstunde "h" |
| STAT_BATT_EQU_BETRIEBSSTUNDE_LAST_EQU_WERT | real | Gibt die Betriebstunde der letzten durchführten Batt-Equlibrierung an |
| STAT_BATT_EQU_KM_LAST_EQU_EINH | string | Letzte Batterie Equilibrierung durchgeführt bei km-Stand "km" |
| STAT_BATT_EQU_KM_LAST_EQU_WERT | real | Gibt den Kilometerstand der letzten durchführten Batt-Equlibrierung an |
| STAT_BATT_EQU_ANZAHL | real | Gibt die Anzahl der bereits durchgeführten Batt-Equlibrierungen an Bislang druchgeführte Batterieequlibrierungen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-hisr-hos-reset"></a>
### STEUERN_HISR_HOS_RESET

Erwirkt einen Reset der Betriebsstrategieanalyse ENERGIEPARMODE muss an sein

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION | string | Werttabelle 0 = AUS 1 = RESET |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-vital-variables-drehzahlen"></a>
### STATUS_VITAL_VARIABLES_DREHZAHLEN

Liest die Werte von charakteristischen Drehzahlen und Geschwindigkeiten aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SPEED_MTRA_EINH | string | "1/min" |
| STAT_SPEED_MTRA_WERT | real | Liest die Drehzahl vom E-Motor A aus |
| STAT_SPEED_MTRB_EINH | string | "1/min" |
| STAT_SPEED_MTRB_WERT | real | Liest die Drehzahl vom E-Motor B aus |
| STAT_SPEED_VM_EINH | string | "1/min" |
| STAT_SPEED_VM_WERT | real | Liest die Drehzahl des Verbrennungsmotors aus |
| STAT_SPEED_ABTRIEB_EINH | string | "1/min" |
| STAT_SPEED_ABTRIEB_WERT | real | Liest die Drehzahl des Abtriebsstrangs aus |
| STAT_SPEED_FZG_EINH | string | "km/h" |
| STAT_SPEED_FZG_WERT | real | Liest die Fahrzeuggeschwindigkeit aus |
| STAT_SPEED_EMPI_EINH | string | "1/min" |
| STAT_SPEED_EMPI_WERT | real | Liest die EMPI Drehzahl aus |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-vital-variables-leistungen"></a>
### STATUS_VITAL_VARIABLES_LEISTUNGEN

Liest die Werte von charakteristischen Leistungen, Spannungen, Stroemen und Ladezustaenden aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PWR_ACC_EINH | string | "kW" |
| STAT_PWR_ACC_WERT | real | Liest die von Sekundaerverbrauchern genutze Leistung aus |
| STAT_PWR_HV_BAT_EINH | string | "kW" |
| STAT_PWR_HV_BAT_WERT | real | Liest die Leistung der HV Batterie aus |
| STAT_SOC_HV_BAT_EINH | string | "%" |
| STAT_SOC_HV_BAT_WERT | real | Liest den Ladezustand der HV Batterie aus |
| STAT_U_APM_EINH | string | "V" |
| STAT_U_APM_WERT | real | Liest die Spannung des Niederspannungsbordnetzes aus |
| STAT_U_HV_BAT_EINH | string | "V" |
| STAT_U_HV_BAT_WERT | real | Liest die Spannung der Hochvoltbatterie aus |
| STAT_PCT_SOC_ACC_EINH | string | "%" |
| STAT_PCT_SOC_ACC_WERT | real | Liest die Genauigkeit der Ladungsanzeige der Hochvoltbatterie aus |
| STAT_P_LT_LIM_MAX_EINH | string | "kW" |
| STAT_P_LT_LIM_MAX_WERT | real | Liest das maximale long-term Leistungslimit der Batterie aus |
| STAT_P_LT_LIM_MIN_EINH | string | "kW" |
| STAT_P_LT_LIM_MIN_WERT | real | Liest das minimale long-term Leistungslimit der Batterie aus |
| STAT_P_PRED_LIM_MAX_EINH | string | "kW" |
| STAT_P_PRED_LIM_MAX_WERT | real | Liest das maximale predicted Leistungslimit der Batterie aus |
| STAT_P_PRED_LIM_MIN_EINH | string | "kW" |
| STAT_P_PRED_LIM_MIN_WERT | real | Liest das minimale predicted Leistungslimit der Batterie aus |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-vital-variables-momente"></a>
### STATUS_VITAL_VARIABLES_MOMENTE

Liest die Werte von charakteristischen Momenten aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TORQUE_PWG_SOLL_EINH | string | "Nm" |
| STAT_TORQUE_PWG_SOLL_WERT | real | Liest das vom Fahrer geforderte To aus |
| STAT_TORQUE_VM_SOLL_EINH | string | "Nm" |
| STAT_TORQUE_VM_SOLL_WERT | real | Liest das vom Verbrenner geforderte Ti aus |
| STAT_TORQUE_VM_IST_MEAS_EINH | string | "Nm" |
| STAT_TORQUE_VM_IST_MEAS_WERT | real | Liest das gemessene Ti aus |
| STAT_TORQUE_VM_IST_PRED_EINH | string | "Nm" |
| STAT_TORQUE_VM_IST_PRED_WERT | real | Liest das von der DME geschaetzte Ti aus |
| STAT_TORQUE_BREAK_SOLL_EINH | string | "Nm" |
| STAT_TORQUE_BREAK_SOLL_WERT | real | Liest das geforderte Verzögerungsmoment aus |
| STAT_TORQUE_OPT_TI_EINH | string | "Nm" |
| STAT_TORQUE_OPT_TI_WERT | real | Liest das verbrauchsguenstigste Verbrennermoment aus |
| STAT_TORQUE_BREAK_REGEN_EINH | string | "Nm" |
| STAT_TORQUE_BREAK_REGEN_WERT | real | Liest das rekuperationsfaehige Verzoegerungsmoment aus |
| STAT_TORQUE_OUT_EINH | string | "Nm" |
| STAT_TORQUE_OUT_WERT | real | Liest das Antriebsstrangmoment aus |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-vital-variables-status"></a>
### STATUS_VITAL_VARIABLES_STATUS

Liest die Werte von charakteristischen Status aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KUPP_1_NR | unsigned char | Liest den Status von Kupplung 1 aus |
| STAT_KUPP_1_TEXT | string | Wertetabelle 0 = Ungueltig 1 = Offen 2 = Betaetigt 3 = Fast Synchronisiert 4 = Synchronisiert 5 = Gesperrt |
| STAT_KUPP_2_NR | unsigned char | Liest den Status von Kupplung 2 aus |
| STAT_KUPP_2_TEXT | string | Wertetabelle 0 = Ungueltig 1 = Offen 2 = Betaetigt 3 = Fast Synchronisiert 4 = Synchronisiert 5 = Gesperrt |
| STAT_KUPP_3_NR | unsigned char | Liest den Status von Kupplung 3 aus |
| STAT_KUPP_3_TEXT | string | Wertetabelle 0 = Ungueltig 1 = Offen 2 = Betaetigt 3 = Fast Synchronisiert 4 = Synchronisiert 5 = Gesperrt |
| STAT_KUPP_4_NR | unsigned char | Liest den Status von Kupplung 4 aus |
| STAT_KUPP_4_TEXT | string | Wertetabelle 0 = Ungueltig 1 = Offen 2 = Betaetigt 3 = Fast Synchronisiert 4 = Synchronisiert 5 = Gesperrt |
| STAT_VM_AKTIV | unsigned char | Liest aus, ob Laufen des Verbrennungsmotors gefordert ist |
| STAT_VM_AKTIV_TEXT | string | Wertetabelle 0 = nicht gefordert 1 = Gefordert |
| STAT_RNG_DSRD_NR | unsigned char | Liest den Zielgetrieberange aus |
| STAT_RNG_DSRD_TEXT | string | Wertetabelle 0= POWERUP 1= EVAL_BP_CLOSE (Evaluation Batteriepack Contactors Close) 2= DET_BP_CLOSED (Determine Batteriepack Contactors Closed) 3= EVAL_INV_ENABLE (Evaluation Inverter Enable) 4= DET_INV_ENABLED (Determine Inverter Enabled) 5= EVAL_ENG_SYS (Evaluation Engine System) 6= EVAL_REKEY_ALLOWED (Evaluatio Rekey Allowed) 7= OPERATIONAL 8= DET_ENG_STOPPED (Determine Engine Stopped) 9= DET_INV_DISABLED (Determine Inverter Disabled) 10=  EVAL_BP_OPEN (Evaluation Batteripack Open) 11=  DET_BP_OPENED (Determine Batteripack Opened) 12=  DET_BUS_DISCHARGED (Determine Highvoltage Bus Discharged) 13=  SHUTDOWN 14=  JUMP_ASSIST |
| STAT_USECASE_NR | unsigned char | Liest den SOCR Usecase aus |
| STAT_USECASE_TEXT | string | Wertetabelle 1 = Batterie zu heiss 2 = Batterie Equilibrierung 3 = Standladen 4 = Kat-heiz-modus 5 = Batterieheizen (laden) 6 = Batterieheizen (entladen) 7 = Produktionsmodus 8 = Sportmodus 9 = Rückwärts 10 = Neutral 11 = Park 12 = Drive 13 = Produktionsmodus ohne Ladeunterdrückung 14 = Warmlauf 15 = Batteriestimulus (laden) 16 = Batteriestimulus (entladen) 17 = SOC Overwrite Tester 18 = Limiterbetrieb 19 = Efficient Drive 20 = SOC SFA 21 = Default |
| STAT_RNGST_NR | unsigned char | Liest den RangeState aus |
| STAT_RNGST_TEXT | string | Wertetabelle 0 = Init 1 = Neutral 2 = Mode 1 3 = Mode 2 4 = Gear 1 5 = Gear 2 6 = Gear 3 7 = Gear 4 8 = G1 zu G2 (Drehzahl) 9 = G1 zu G2 (Drehmoment) 10 = G2 zu G1 (Drehzahl) 11 = G2 zu G1 (Drehmoment) 12 = G2 zu G3 (Drehzahl) 13 = G2 zu G3 (Drehmoment) 14 = G3 zu G2 (Drehzahl) 15 = G3 zu G2 (Drehmoment) 16 = G3 zu G4 (Drehzahl) 17 = G3 zu G4 (Drehmoment) 18 = G4 zu G3 (Drehzahl) 19 = G4 zu G3 (Drehmoment) 20 = M1 zu G1 21 = M1 zu G2 22 = M2 zu G2 23 = M2 zu G3 24 = M2 zu G4 25 = N zu M1 26 = N zu M2 27 = Neutralschaltung 28 = M1 zu M2 wenig Drehmoment 29 = M2 zu M1 wenig Drehmoment 30 = M1 Abbruch 31 = M2 Abbruch 32 = G1 Abbruch 33 = G2 Abbruch 34 = G3 Abbruch 35 = G2 Abbruch 36 = G3 Abbruch 37 = G4 Abbruch |
| STAT_MAN_SPORT_NR | unsigned char | Liest das Fahrprogramm in Automatic und Sport aus |
| STAT_MAN_SPORT_TEXT | string | Wertetabelle 0 = AUTOMATIC 1 = SPORT 2 = MAN 4 = LIMIT 8 = CITY 15 = INVALID |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-vital-variables-temperaturen"></a>
### STATUS_VITAL_VARIABLES_TEMPERATUREN

Liest die Werte von charakteristischen Temperaturen aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEMP_INVTR_A_EINH | string | "°C" |
| STAT_TEMP_INVTR_A_WERT | real | Liest die Temperatur des Inverters Motor A aus |
| STAT_TEMP_MTR_A_EINH | string | "°C" |
| STAT_TEMP_MTR_A_WERT | real | Liest die Temperatur von Motor A aus |
| STAT_TEMP_INVTR_B_EINH | string | "°C" |
| STAT_TEMP_INVTR_B_WERT | real | Liest die Temperatur des Inverters Motor B aus |
| STAT_TEMP_MTR_B_EINH | string | "°C" |
| STAT_TEMP_MTR_B_WERT | real | Liest die Temperatur von Motor B aus |
| STAT_TEMP_TRNS_OEL_EINH | string | "°C" |
| STAT_TEMP_TRNS_OEL_WERT | real | Liest die Getriebeoeltemperatur aus |
| STAT_TEMP_BATT_MOD_EINH | string | "°C" |
| STAT_TEMP_BATT_MOD_WERT | real | Liest die Batteriemodultemperatur aus |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-lesen-individualdata-liste"></a>
### LESEN_INDIVIDUALDATA_LISTE

Lesen eines Listeneintrags der Individualisierungsdaten KWP2000: $21 ReadDataByLocalIdentifier (not used) $01 recordLocalIdentifier (not used)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_LISTENTRY | unsigned int | Nummer des angeforderten Listenelements (0,1,2,...) 0x0000 = Anforderung, das 1. Listelement zu senden 0x0001 = Anforderung, das 2. Listelement zu senden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RET_ENTRYNR | unsigned int | Nummer des zurückgegebenen Listenelements (0,1,2,...) |
| RET_STATUS | unsigned char | Information ob aktuelles Listenelement das Letzte ist 0xFF    letztes Listenelement 0xFE    Listenelement nicht gefunden 0x00    nicht letztes Listenelement |
| RET_FROMWHERE | unsigned char | Strategienummer 0x01    via 22 5F 8B |
| RET_DATA | binary | Listentry zur Individualdaten-Abfrage 1.Byte, Diagnoseadresse (for future use), diese gibt Auskunft von welchem SG die Individualdaten verwaltet werden. z.B. 0x63  2.Byte: Sind die Daten Car- oder Key- Memory relevant? 0x01    CarMemory relevant 0x02    KeyMemory relevant 0x03    CarMemory relevant und KeyMemory relevant  3.Byte:  Strategienummer 0x01    via 22 5F 8B  4.Byte und Folgende siehe Spec Datenrettung  |
| RET_COMMENT | string | Kommentarspalte des Entries |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-lese-individualdata"></a>
### LESE_INDIVIDUALDATA

Lesen von Individualisierungsdaten Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_KEYID | unsigned char | 0x00       CarMemory 0x01..0x04 Schlüsselnummer dem der RET_DATA zugeordnet ist 0xFF       Aktuell gesteckter Schlüssel ist RET_DATA zugeordnet (not used) |
| ARG_BLOCKNR | unsigned long | Zu übertragende Blocknummer (Zähler) bei langen Datenstreams z.B. 0x01020304 (4 Bytes) falls nicht verwendet als Dummy mitschleifen |
| ARG_FROMWHERE | unsigned char | Strategienummer 0x01    = Batterie Recovery |
| ARG_INQY_LEN | unsigned char | Länge des folgenden Anfragedatenstreams (not used) z.B. 0x02 für 2 Byte |
| ARG_INQY_DATA | string | ASCII-codiert Anfrage Individualdatenstream (not used) |
| ARG_RESP_LEN | unsigned char | Länge der folgenden Information wie die Antwort erhalten wird. Also ein Antwortfilter bzw. -hinweis (not used) |
| ARG_RESP_DATA | string | ASCII-codiert Information wie die Antwort erhalten wird: Also ein Antwortfilter bzw. -hinweis (not used) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RET_STATUS | unsigned char | 0xFF letztes oder einziges element des Datenstreams 0x00 es folgen weitere Datenstreamstücke |
| RET_BLOCKNR | unsigned long | Übertragende Blocknummer (Zähler) bei langen Datenstreams z.B. 0x01020304 falls nicht verwendet als Dummy mitschleifen |
| RET_LEN | int | Länge des Individualisierungs Datenstream oder -streamstücks |
| RET_DATA | binary | Individualisierungs Datenstream |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-schreiben-individualdata"></a>
### SCHREIBEN_INDIVIDUALDATA

Schreiben von Individualisierungsdaten Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_KEYID | unsigned char | 0x00       CarMemory 0x01..0x04 Schlüsselnummer dem der ARG_DATA zugeordnet ist 0xFF       Aktuell gesteckter Schlüssel ist ARG_DATA zugeordnet (not used) |
| ARG_BLOCKNR | unsigned long | Zu übertragende Blocknummer (Zähler) bei langen Datenstreams z.B. 0x01020304 (4 Bytes) falls nicht verwendet als Dummy mitschleifen |
| ARG_FROMWHERE | unsigned char | Strategienummer 0x01    = Batterie Recovery |
| ARG_STATUS | unsigned char | 0xFF letztes oder einziges element des Datenstreams 0x00 es folgen weitere Datenstreamstücke |
| ARG_WRITE_LEN | unsigned char | Länge des folgenden Schreibauftrags z.B. 0x02 für 2 Byte |
| ARG_WRITE_DATA | string | ASCII-codiert Schreibauftrag für Individualdatenstream (not used) |
| ARG_W_RESP_LEN | unsigned char | Optional, Laenge des folgenden Antwortfilters  (not used) z.B. 0x02 für 2 Byte |
| ARG_W_RESP_DATA | string | ASCII-codiert, Optional, Antwortfilter des Schreibauftrags (not used) |
| ARG_LEN | int | Länge des Individualisierungs Datenstream oder -streamstücks |
| ARG_DATA | string | ASCII-codiert Datenstream |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RET_STATUS | unsigned char | Rückmeldungen, Fehlercodes z.B. OK 0x00 oder NOTOK 0x01 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-flashprog-precondition-lesen"></a>
### _STATUS_FLASHPROG_PRECONDITION_LESEN

Status der Vorbedingungen fuer das Flashen ueber WinKFP $22     SID ReadDataByIdentifier $03 $01 DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SPERRE_VERBRENNER_AKTIV | string | Pruefung beim Anforderung der Busruhe Sperre aktiv, wenn Verbrenner aktiviert (Drehzahl, Start/Stopp-Mode) 0 = Keine Sperrung 1 = Sperre aktiv |
| STAT_SPERRE_EWS_AKTIV | string | Pruefung beim Anforderung der Busruhe Sperre aktiv, wegen aktiver EWS-Sperre 0 = Keine Sperrung 1 = Sperre aktiv |
| STAT_SPERRE_KLEMME_15_AKTIV | string | Pruefung beim Anforderung der Busruhe Sperre aktive, wenn Kl.15 nicht eingeschaltet 0 = Keine Sperrung 1 = Sperre aktiv |
| STAT_SPERRE_TEMPERATUR_AKTIV | string | Pruefung beim Anforderung der Busruhe Sperre aktiv, wenn Steuergeraete-UEbertemperatur 0 = Keine Sperrung 1 = Sperre aktiv |
| STAT_SPERRE_PARK_NEUTRAL_AKTIV | string | Pruefung beim Anforderung der Busruhe Sperre aktiv, wenn Getriebe nicht in Parkstellung oder nicht in Neutral 0 = Keine Sperrung 1 = Sperre aktiv |
| STAT_SPERRE_HOCHVOLT_AKTIV | string | Pruefung beim Anforderung der Busruhe Sperre aktiv, wenn Hochvolt aktiv ist 0 = Keine Sperrung 1 = Sperre aktiv |
| STAT_SPERRE_FSP_AKTIV | string | Pruefung beim Uebergang von der Extended zur Programming Session Sperre aktiv, wenn Fehlerspeichereintrag aktiv 0 = Keine Sperrung 1 = Sperre aktiv |
| STAT_SPERRE_BUSRUHE_AKTIV | string | Pruefung beim Uebergang von der Extended zur Programming Session Sperre aktiv, wenn Busruhe nicht aktiviert 0 = Keine Sperrung 1 = Sperre aktiv |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-prozessor-lesen-jobs"></a>
### _STATUS_PROZESSOR_LESEN_JOBS

Reset-Statistik, Resetursachen, Resetadressen Status der Level 3-Tests, NVM-Status/Checksummen Hoechste erreichte Anzahl von(Running-)Resets zwischen 2 PowerUp-Resets PowerUp-Reset setzt Wert zurueck Wert wird bei Klemme15- und Batteriewechsel nicht zurueckgesetzt $22     SID ReadDataByIdentifier $20 $4B DID Messwert Anzahl der Resets seit der letzten Neuprogrammierung Powerup-Resets(Watchdog) werden nicht erfasst Klemme15- und Batteriewechsel haben auf den Wert keinen Einfluss $22     SID ReadDataByIdentifier $20 $4A DID Messwert Ursache des letzten Resets $22     SID ReadDataByIdentifier $12 $DE DID Messwert Adresse, an der der letzte Resets aufgetreten  ist $22     SID ReadDataByIdentifier $12 $E7 DID Messwert Adresse, an der vom RAM-Test eine Fehler festgestellt wurde $22     SID ReadDataByIdentifier $20 $34 DID Messwert Status der Processorueberwachung FUSI-Level 3 $22     SID ReadDataByIdentifier $20 $39 DID Messwert Status der Checksummen- und Lesepruefung aller NVM-RAM Bereiche $22     SID ReadDataByIdentifier $20 $33 DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MAX_ANZAHL_RESETS_WERT | unsigned int | Groesste erreichte Anzahl von Resets zwischen seit dem letzten Klemme30 - Wechsel 0 bis 655535 |
| STAT_ANZAHL_RESETS_TOTAL_WERT | unsigned int | Anzahl der Resets seit der letzten Neuprogrammierung |
| STAT_RESETGRUND_NR | unsigned char | Ursache des letzten Resets 0 = Power Up / Klemme30-Wechsel 2 = Externer Watchdog 3 = Interner Watchdog 4 = Unhandled Exception 5 = MCPA/MCPB hat  Reset angefordert 6-255 = CPU spezifische Resets |
| STAT_RESETGRUND_TEXT | string | Ursache des letzten Resets |
| STAT_RESET_ADRESSE_WERT | unsigned long | Adresse an der der letzte Reset aufgetreten  ist |
| STAT_RAM_FEHLER_ADRESSE_WERT | unsigned long | Adresse, an der vom RAM-Test eine Fehler festgestellt wurde |
| STAT_CPU_FEHLER_NR | unsigned char | Status des Prozessors |
| STAT_CPU_FEHLER_TEXT | string | Status des Prozessors |
| STAT_STATIC_NVM_LESEN_TEXT | string | Lesestatus des NVM-Ram im STATIC-Bereich |
| STAT_ADAPTABLE_NVM_LESEN_TEXT | string | Lesestatus des NVM-Ram im ADAPTABLE -Bereich |
| STAT_CUMULATIVE_NVM_LESEN_TEXT | string | Lesestatus des NVM-Ram im CUMULATIVE -Bereich |
| STAT_STATIC_NVM_CHECKSUMME_TEXT | string | Status der Checksummenpruefung des NVM-Ram im STATIC-Bereich |
| STAT_ADAPTABLE_NVM_CHECKSUMME_TEXT | string | Status der Checksummenpruefung des NVM-Ram im ADAPTABLE-Bereich |
| STAT_CUMULATIVE_NVM_CHECKSUMME_TEXT | string | Status der Checksummenpruefung des NVM-Ram im CUMULATIVE-Bereich |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST01 | binary | Hex-Auftrag an SG |
| _RESPONSE01 | binary | Hex-Antwort von SG |
| _REQUEST02 | binary | Hex-Auftrag an SG |
| _RESPONSE02 | binary | Hex-Antwort von SG |
| _REQUEST03 | binary | Hex-Auftrag an SG |
| _RESPONSE03 | binary | Hex-Antwort von SG |
| _REQUEST04 | binary | Hex-Auftrag an SG |
| _RESPONSE04 | binary | Hex-Antwort von SG |
| _REQUEST05 | binary | Hex-Auftrag an SG |
| _RESPONSE05 | binary | Hex-Antwort von SG |
| _REQUEST06 | binary | Hex-Auftrag an SG |
| _RESPONSE06 | binary | Hex-Antwort von SG |
| _REQUEST07 | binary | Hex-Auftrag an SG |
| _RESPONSE07 | binary | Hex-Antwort von SG |

<a id="job-status-remedial-action-history"></a>
### _STATUS_REMEDIAL_ACTION_HISTORY

Gibt den Fehler bitkodiert zurück

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_REMEDIAL_ACTION_NR | unsigned int | Bit0: Keine Bremsenergierückgewinnung Bit1: Getriebelistung reduziert Bit2: Antrieb kann nur kriechen Bit3: Getriebe-Gangwahl eingeschränkt Bit4: V-Motor aus und bleibt abgestellt Bit5: V-Motor läuft immer und wird nicht abgestellt Bit6: System Shutdown verzögert Bit7: System Shutdown mit HV-Schütze zu Bit8: System Shutdown mit HV-Schütze auf |
| STAT_REMEDIAL_ACTION_NR_TEXT | string | 0 = nicht gesetzt 1 = gesetzt |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-remedial-action"></a>
### _STATUS_REMEDIAL_ACTION

Gibt die letzten Fehler bitcodiert zurueck $22     SID ReadDataByIdentifier $03 $02 DID Messwert Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_REMEDIAL_ACTION_NR | unsigned int | Gibt den letzten Fehler bitkodiert zurück |
| STAT_REMEDIAL_ACTION_NR_TEXT | string | Gibt den letzten Fehler bitkodiert zurück Bit0: Keine Bremsenergierückgewinnung Bit1: Getriebelistung reduziert Bit2: Antrieb kann nur kriechen Bit3: Getriebe-Gangwahl eingeschränkt Bit4: V-Motor aus und bleibt abgestellt Bit5: V-Motor läuft immer und wird nicht abgestellt Bit6: System Shutdown verzögert Bit7: System Shutdown mit HV-Schütze zu Bit8: System Shutdown mit HV-Schütze auf FehlerX = gesetzt bzw. nicht gesetzt |
| STAT_REMEDIAL_ACTION_INPUT1 | unsigned long | Gibt die letzte(n) aktiven SRAR-Diagnosen1 bitkodiert zurück |
| STAT_REMEDIAL_ACTION_INPUT11_TEXT | string | SRAR-Diagnosen1 von 1-15 DiagX = gesetzt bzw. nicht gesetzt |
| STAT_REMEDIAL_ACTION_INPUT12_TEXT | string | SRAR-Diagnosen1 von 16-32 DiagX = gesetzt bzw. nicht gesetzt |
| STAT_REMEDIAL_ACTION_INPUT2 | unsigned long | Gibt die letzte(n) aktiven SRAR-Diagnosen2 bitkodiert zurück |
| STAT_REMEDIAL_ACTION_INPUT21_TEXT | string | SRAR-Diagnosen2 von 1-15 DiagX = gesetzt bzw. nicht gesetzt |
| STAT_REMEDIAL_ACTION_INPUT22_TEXT | string | SRAR-Diagnosen2 von 16-29 DiagX = gesetzt bzw. nicht gesetzt |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-remedial-action-reset"></a>
### _STEUERN_REMEDIAL_ACTION_RESET

Löschen des Historienspeichers RA Energiesparmode Werkstatt muss gesetzt sein

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-build-ident-lesen"></a>
### _BUILD_IDENT_LESEN

Auslesen der Build Informations Felder Standard Flashjob Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BUILD_ONAME | string | Buildname,wird beim Make vergeben |
| BUILD_USER | string | BUILD-USER |
| JAHR | unsigned char | Jahr des Build |
| WOCHE | unsigned char | Woche des Build |
| BUILD_NR | unsigned char | Nummer des Build in der Woche |
| _REQUEST01 | binary | Hex-Auftrag an SG |
| _RESPONSE01 | binary | Hex-Antwort von SG |
| _REQUEST02 | binary | Hex-Auftrag an SG |
| _RESPONSE02 | binary | Hex-Antwort von SG |
| _REQUEST03 | binary | Hex-Auftrag an SG |
| _RESPONSE03 | binary | Hex-Antwort von SG |

<a id="job-steuern-standload-verfuegbar"></a>
### _STEUERN_STANDLOAD_VERFUEGBAR

Entwicklerjob zur Bereitstellung der Standloadfunktion mit Gas&Bremspedal

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STANDLOAD_AVAIL | string | Werttabelle 0 = AUS 1 = EIN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-batterie-aktive-leistung"></a>
### _STATUS_BATTERIE_AKTIVE_LEISTUNG

Liest Status der Batterieleistung aus. Gibt an von welchem Kriterium die Leistung im Moment begrenzt ist.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ENTL_LEISTUNG_BE_NR | unsigned char | Liest die Art des Begrenzers von Battery Estimated Entladeleistung aus |
| STAT_ENTL_LEISTUNG_BE_NR_TEXT | string | 0 = Leistung wird von maximaler Grenze begrenzt 1 = Leistung wird von BPCM begrenzt 2 = Leistung wird von Remedial Action begrenzt 3 = Leistung wird von minimaler Grenze begrenzt 4 = Leistung wird von mismatch begrenzt 5 = Leistung wird vom Applikationswert vorgegeben 6 = Leistung wird vom Powerlaunch vorgegeben |
| STAT_LADE_LEISTUNG_BE_NR | unsigned char | Liest die Art des Begrenzers von Battery Estimated Ladeleistung aus |
| STAT_LADE_LEISTUNG_BE_NR_TEXT | string | 0 = Leistung wird von minimaler Grenze begrenzt 1 = Leistung wird von BPCM begrenzt 2 = Leistung wird von Remedial Action begrenzt 3 = Leistung wird von maximaler Grenze begrenzt 4 = Leistung wird von mismatch begrenzt 5 = Leistung wird vom Applikationswert vorgegeben |
| STAT_ENTL_LEISTUNG_ST_NR | unsigned char | Liest die Art des Begrenzers von Short Term Entladeleistung aus |
| STAT_ENTL_LEISTUNG_ST_NR_TEXT | string | 0 = Leistung wird von maximaler Grenze begrenzt 1 = Leistung wird von BPCM begrenzt 2 = Leistung wird von Remedial Action begrenzt 3 = Leistung wird von SOC begrenzt 4 = Leistung wird von Batt. Nutzung begrenzt 5 = Leistung wird von minimaler Grenze begrenzt 6 = Leistung wird von Unterspannung begrenzt 7 = Leistung wird von mismatch begrenzt 8 = Leistung wird von Battery Estimated Leistung begrenzt 9 = Leistung wird vom Applikationswert vorgegeben 10 = Leistung wird von Rev Grade begrenzt 11 = Leistung wird von Power Launch begrenzt |
| STAT_LADE_LEISTUNG_ST_NR | unsigned char | Liest die Art des Begrenzers von Short Term Ladeleistung aus |
| STAT_LADE_LEISTUNG_ST_NR_TEXT | string | 0 = Leistung wird von minimaler Grenze begrenzt 1 = Leistung wird von BPCM begrenzt 2 = Leistung wird von Remedial Action begrenzt 3 = Leistung wird von SOC begrenzt 4 = Leistung wird von Batt. Nutzung begrenzt 5 = Leistung wird von maximaler Grenze begrenzt 6 = Leistung wird von Überspannung begrenzt 7 = Leistung wird von mismatch begrenzt 8 = Leistung wird von Battery Estimated Leistung begrenzt 9 = Leistung wird vom Applikationswert vorgegeben |
| STAT_ENTL_LEISTUNG_LT_NR | unsigned char | Liest die Art des Begrenzers von Long Term Entladeleistung aus |
| STAT_ENTL_LEISTUNG_LT_NR_TEXT | string | 0 = Leistung wird von maximaler Grenze begrenzt 1 = Leistung wird von BPCM begrenzt 2 = Leistung wird von Remedial Action begrenzt 3 = Leistung wird von SOC begrenzt 4 = Leistung wird von Batt. Nutzung begrenzt 5 = Leistung wird von minimaler Grenze begrenzt 6 = Leistung wird von Unterspannung begrenzt 7 = Leistung wird von mismatch begrenzt 8 = Leistung wird von Short Term Leistung begrenzt 9 = Leistung wird vom Applikationswert vorgegeben 10 = Leistung wird von Rev Grade begrenzt 11 = Leistung wird von Power Launch begrenzt |
| STAT_LADE_LEISTUNG_LT_NR | unsigned char | Liest die Art des Begrenzers von Long Term Ladeleistung aus |
| STAT_LADE_LEISTUNG_LT_NR_TEXT | string | 0 = Leistung wird von minimaler Grenze begrenzt 1 = Leistung wird von BPCM begrenzt 2 = Leistung wird von Remedial Action begrenzt 3 = Leistung wird von SOC begrenzt 4 = Leistung wird von Batt. Nutzung begrenzt 5 = Leistung wird von maximaler Grenze begrenzt 6 = Leistung wird von Überspannung begrenzt 7 = Leistung wird von mismatch begrenzt 8 = Leistung wird von Short Term Leistung begrenzt 9 = Leistung wird vom Applikationswert vorgegeben |
| STAT_ENTL_LEISTUNG_BP_NR | unsigned char | Liest die Art des Begrenzers von Battery Predicted Entladeleistung aus |
| STAT_ENTL_LEISTUNG_BP_NR_TEXT | string | 0 = Leistung wird von maximaler Grenze begrenzt 1 = Leistung wird von BPCM begrenzt 2 = Leistung wird von Remedial Action begrenzt 3 = Leistung wird von SOC begrenzt 4 = Leistung wird von Batt. Nutzung begrenzt 5 = Leistung wird von minimaler Grenze begrenzt 6 = Leistung wird von mismatch begrenzt 7 = Leistung wird von Long Term Leistung begrenzt 8 = Leistung wird vom Applikationswert vorgegeben |
| STAT_LADE_LEISTUNG_BP_NR | unsigned char | Liest die Art des Begrenzers von Battery Predicted Ladeleistung aus |
| STAT_LADE_LEISTUNG_BP_NR_TEXT | string | 0 = Leistung wird von minimaler Grenze begrenzt 1 = Leistung wird von BPCM begrenzt 2 = Leistung wird von Remedial Action begrenzt 3 = Leistung wird von SOC begrenzt 4 = Leistung wird von Batt. Nutzung begrenzt 5 = Leistung wird von maximaler Grenze begrenzt 6 = Leistung wird von mismatch begrenzt 7 = Leistung wird von Long Term Leistung begrenzt 8 = Leistung wird vom Applikationswert vorgegeben |
| STAT_ENTL_LEISTUNG_BE_EINH | string | "kW" |
| STAT_ENTL_LEISTUNG_BE_WERT | real | Liest den Wert des Begrenzers von Battery Estimated Entladeleistung aus |
| STAT_LADE_LEISTUNG_BE_EINH | string | "kW" |
| STAT_LADE_LEISTUNG_BE_WERT | real | Liest den Wert des Begrenzers von Battery Estimated Ladeleistung aus |
| STAT_ENTL_LEISTUNG_ST_EINH | string | "kW" |
| STAT_ENTL_LEISTUNG_ST_WERT | real | Liest den Wert des Begrenzers von Short Term Entladeleistung aus |
| STAT_LADE_LEISTUNG_ST_EINH | string | "kW" |
| STAT_LADE_LEISTUNG_ST_WERT | real | Liest den Wert des Begrenzers von Short Term Ladeleistung aus |
| STAT_ENTL_LEISTUNG_LT_EINH | string | "kW" |
| STAT_ENTL_LEISTUNG_LT_WERT | real | Liest den Wert des Begrenzers von Long Term Entladeleistung aus |
| STAT_LADE_LEISTUNG_LT_EINH | string | "kW" |
| STAT_LADE_LEISTUNG_LT_WERT | real | Liest den Wert des Begrenzers von Long Term Ladeleistung aus |
| STAT_ENTL_LEISTUNG_BP_EINH | string | "kW" |
| STAT_ENTL_LEISTUNG_BP_WERT | real | Liest den Wert des Begrenzers von Battery Predicted Entladeleistung aus |
| STAT_LADE_LEISTUNG_BP_EINH | string | "kW" |
| STAT_LADE_LEISTUNG_BP_WERT | real | Liest den Wert des Begrenzers von Battery Predicted Ladeleistung aus |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-socr-usecase"></a>
### _STATUS_SOCR_USECASE

Rückgabe des aktuellen Betriebszustandes der HV-Speicherladestrategie

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SOCR_USECASE_NR | unsigned char | Rückgabe des aktuellen Betriebszustandes der HV-Speicherladestrategie |
| STAT_SOCR_USECASE_NR_TEXT | string | 1 = Batterie zu heiss 2 = Batterie Equilibrierung 3 = Standladen 4 = Kat-heiz-modus 5 = Batterieheizen (laden) 6 = Batterieheizen (entladen) 7 = Produktionsmodus 8 = Sportmodus 9 = Rückwärts 10 = Neutral 11 = Park 12 = Drive 13 = Produktionsmodus ohne Ladeunterdrückung 14 = Warmlauf 15 = Batteriestimulus (laden) 16 = Batteriestimulus (entladen) 17 = SOC Overwrite Tester 18 = Limiterbetrieb 19 = Efficient Drive 20 = SOC SFA 21 = Default |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-reset-ursache"></a>
### _STATUS_RESET_URSACHE

Auslesen der Reset Ursache Es werden 6 Pakete zurückgeliefert  1 Paket: Reset der nicht durch einen PowerUp Reset verursacht wurde. 5 Pakete: Alle zuletzt aufgetretenen Resets Inhalt eines Pakets: - SOC der HV-Batterie - Spannung RunCrank - Background-LoopMax Wert - PLD Feedback-Wert - Sammelfehler für Processorhardware - E-MotorA Temperatur - E-MotorA-Inverter Temperatur - km-Stand - ResetSourceAddress - ResetSource - Program/Datenstand  Beschreibung der Results wird hier nur an Hand des 1.Paket gemacht. Die anderen Pakete sind analog zu betrachten.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RST_NOPWRUP_HV_BAT_SOC_EINH | string | "%" |
| STAT_RST_NOPWRUP_HV_BAT_SOC_WERT | real | SOC der HV-Batterie(none powerup reset) |
| STAT_RST_NOPWRUP_RUN_CRANK_EINH | string | "V" |
| STAT_RST_NOPWRUP_RUN_CRANK_WERT | real | Spannung RunCrank(none powerup reset) |
| STAT_RST_NOPWRUP_BG_LOOPMAX_EINH | string | "s" |
| STAT_RST_NOPWRUP_BG_LOOPMAX_WERT | real | Background-LoopMax Wert(none powerup reset) |
| STAT_RST_NOPWRUP_FDBCK_PLD | unsigned char | PLD Feedback-Wert(none powerup reset) |
| STAT_RST_NOPWRUP_FDBCK_PLD_TEXT | string | PLD Feedback-Wert(OK=1/Not OK=0) |
| STAT_RST_NOPWRUP_MP_FAULT | unsigned char | Sammelfehler für Prozessorhardware (z.B. RAM/ROM, Stackoverflow etc.) |
| STAT_RST_NOPWRUP_MP_FAULT_TEXT | string | 0 = nicht aktiv, 1 = aktiv |
| STAT_RST_NOPWRUP_MTRA_TMP_EINH | string | "°C" |
| STAT_RST_NOPWRUP_MTRA_TMP_WERT | real | E-MotorA Temperatur(none powerup reset) |
| STAT_RST_NOPWRUP_MTRA_INVTRTMP_EINH | string | "°C" |
| STAT_RST_NOPWRUP_MTRA_INVTRTMP_WERT | real | E-MotorA-Inverter Temperatur(none powerup reset) |
| STAT_RST_NOPWRUP_KM_EINH | string | "km" |
| STAT_RST_NOPWRUP_KM_WERT | real | km-Stand(none powerup reset) |
| STAT_RST_NOPWRUP_RSTSRCADDR | unsigned long | ResetSourceAddress(none powerup reset) |
| STAT_RST_NOPWRUP_RSTSRC | unsigned char | ResetSource(none powerup reset) |
| STAT_RST_NOPWRUP_RSTSRC_TEXT | string | Wertetabelle: 0 = CeHWIO_e_PwrUpRstIgn 1 = CeHWIO_e_PwrUpRstSerial 2 = CeHWIO_e_RunRstExtWDT 3 = CeHWIO_e_RunRstIntWDT3 4 = CeHWIO_e_RunRstUnhndldExcptn 5 = CeHWIO_e_RstBattConnect 6 = CeHWIO_e_RstUnident |
| STAT_RST_NOPWRUP_BMW_DATA_REF | string | Program/Datenstand (BMW_DATA_REF - die letzten 10 Zeichen reichen) |
| STAT_RST01_HV_BAT_SOC_EINH | string | "%" |
| STAT_RST01_HV_BAT_SOC_WERT | real |  |
| STAT_RST01_RUN_CRANK_EINH | string | "V" |
| STAT_RST01_RUN_CRANK_WERT | real |  |
| STAT_RST01_BG_LOOPMAX_EINH | string | "s" |
| STAT_RST01_BG_LOOPMAX_WERT | real |  |
| STAT_RST01_FDBCK_PLD | unsigned char |  |
| STAT_RST01_FDBCK_PLD_TEXT | string |  |
| STAT_RST01_MP_FAULT | unsigned char |  |
| STAT_RST01_MP_FAULT_TEXT | string |  |
| STAT_RST01_MTRA_TMP_EINH | string | "°C" |
| STAT_RST01_MTRA_TMP_WERT | real |  |
| STAT_RST01_MTRA_INVTRTMP_EINH | string | "°C" |
| STAT_RST01_MTRA_INVTRTMP_WERT | real |  |
| STAT_RST01_KM_EINH | string | "km" |
| STAT_RST01_KM_WERT | real |  |
| STAT_RST01_RSTSRCADDR | unsigned long |  |
| STAT_RST01_RSTSRC | unsigned char |  |
| STAT_RST01_RSTSRC_TEXT | string |  |
| STAT_RST01_BMW_DATA_REF | string |  |
| STAT_RST02_HV_BAT_SOC_EINH | string | "%" |
| STAT_RST02_HV_BAT_SOC_WERT | real |  |
| STAT_RST02_RUN_CRANK_EINH | string | "V" |
| STAT_RST02_RUN_CRANK_WERT | real |  |
| STAT_RST02_BG_LOOPMAX_EINH | string | "s" |
| STAT_RST02_BG_LOOPMAX_WERT | real |  |
| STAT_RST02_FDBCK_PLD | unsigned char |  |
| STAT_RST02_FDBCK_PLD_TEXT | string |  |
| STAT_RST02_MP_FAULT | unsigned char |  |
| STAT_RST02_MP_FAULT_TEXT | string |  |
| STAT_RST02_MTRA_TMP_EINH | string | "°C" |
| STAT_RST02_MTRA_TMP_WERT | real |  |
| STAT_RST02_MTRA_INVTRTMP_EINH | string | "°C" |
| STAT_RST02_MTRA_INVTRTMP_WERT | real |  |
| STAT_RST02_KM_EINH | string | "km" |
| STAT_RST02_KM_WERT | real |  |
| STAT_RST02_RSTSRCADDR | unsigned long |  |
| STAT_RST02_RSTSRC | unsigned char |  |
| STAT_RST02_RSTSRC_TEXT | string |  |
| STAT_RST02_BMW_DATA_REF | string |  |
| STAT_RST03_HV_BAT_SOC_EINH | string | "%" |
| STAT_RST03_HV_BAT_SOC_WERT | real |  |
| STAT_RST03_RUN_CRANK_EINH | string | "V" |
| STAT_RST03_RUN_CRANK_WERT | real |  |
| STAT_RST03_BG_LOOPMAX_EINH | string | "s" |
| STAT_RST03_BG_LOOPMAX_WERT | real |  |
| STAT_RST03_FDBCK_PLD | unsigned char |  |
| STAT_RST03_FDBCK_PLD_TEXT | string |  |
| STAT_RST03_MP_FAULT | unsigned char |  |
| STAT_RST03_MP_FAULT_TEXT | string |  |
| STAT_RST03_MTRA_TMP_EINH | string | "°C" |
| STAT_RST03_MTRA_TMP_WERT | real |  |
| STAT_RST03_MTRA_INVTRTMP_EINH | string | "°C" |
| STAT_RST03_MTRA_INVTRTMP_WERT | real |  |
| STAT_RST03_KM_EINH | string | "km" |
| STAT_RST03_KM_WERT | real |  |
| STAT_RST03_RSTSRCADDR | unsigned long |  |
| STAT_RST03_RSTSRC | unsigned char |  |
| STAT_RST03_RSTSRC_TEXT | string |  |
| STAT_RST03_BMW_DATA_REF | string |  |
| STAT_RST04_HV_BAT_SOC_EINH | string | "%" |
| STAT_RST04_HV_BAT_SOC_WERT | real |  |
| STAT_RST04_RUN_CRANK_EINH | string | "V" |
| STAT_RST04_RUN_CRANK_WERT | real |  |
| STAT_RST04_BG_LOOPMAX_EINH | string | "s" |
| STAT_RST04_BG_LOOPMAX_WERT | real |  |
| STAT_RST04_FDBCK_PLD | unsigned char |  |
| STAT_RST04_FDBCK_PLD_TEXT | string |  |
| STAT_RST04_MP_FAULT | unsigned char |  |
| STAT_RST04_MP_FAULT_TEXT | string |  |
| STAT_RST04_MTRA_TMP_EINH | string | "°C" |
| STAT_RST04_MTRA_TMP_WERT | real |  |
| STAT_RST04_MTRA_INVTRTMP_EINH | string | "°C" |
| STAT_RST04_MTRA_INVTRTMP_WERT | real |  |
| STAT_RST04_KM_EINH | string | "km" |
| STAT_RST04_KM_WERT | real |  |
| STAT_RST04_RSTSRCADDR | unsigned long |  |
| STAT_RST04_RSTSRC | unsigned char |  |
| STAT_RST04_RSTSRC_TEXT | string |  |
| STAT_RST04_BMW_DATA_REF | string |  |
| STAT_RST05_HV_BAT_SOC_EINH | string | "%" |
| STAT_RST05_HV_BAT_SOC_WERT | real |  |
| STAT_RST05_RUN_CRANK_EINH | string | "V" |
| STAT_RST05_RUN_CRANK_WERT | real |  |
| STAT_RST05_BG_LOOPMAX_EINH | string | "s" |
| STAT_RST05_BG_LOOPMAX_WERT | real |  |
| STAT_RST05_FDBCK_PLD | unsigned char |  |
| STAT_RST05_FDBCK_PLD_TEXT | string |  |
| STAT_RST05_MP_FAULT | unsigned char |  |
| STAT_RST05_MP_FAULT_TEXT | string |  |
| STAT_RST05_MTRA_TMP_EINH | string | "°C" |
| STAT_RST05_MTRA_TMP_WERT | real |  |
| STAT_RST05_MTRA_INVTRTMP_EINH | string | "°C" |
| STAT_RST05_MTRA_INVTRTMP_WERT | real |  |
| STAT_RST05_KM_EINH | string | "km" |
| STAT_RST05_KM_WERT | real |  |
| STAT_RST05_RSTSRCADDR | unsigned long |  |
| STAT_RST05_RSTSRC | unsigned char |  |
| STAT_RST05_RSTSRC_TEXT | string |  |
| STAT_RST05_BMW_DATA_REF | string |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (66 × 2)
- [LIEFERANTEN](#table-lieferanten) (118 × 2)
- [FARTTEXTE](#table-farttexte) (19 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [PROZESSKLASSEN](#table-prozessklassen) (24 × 3)
- [SVK_ID](#table-svk-id) (65 × 2)
- [DTCEXTENDEDDATARECORDNUMBER](#table-dtcextendeddatarecordnumber) (5 × 3)
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (5 × 9)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [DIAGMODE](#table-diagmode) (11 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [BETRIEBSMODE](#table-betriebsmode) (2 × 3)
- [FORTTEXTE](#table-forttexte) (456 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 3)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [T_SUPPLIERLIST_3_8](#table-t-supplierlist-3-8) (140 × 2)
- [T_NEIN_JA_1BIT](#table-t-nein-ja-1bit) (2 × 2)
- [T_NICHT_AKTIV_AKTIV_1BYTE](#table-t-nicht-aktiv-aktiv-1byte) (2 × 2)
- [T_JUMP_ASSIST_STATE](#table-t-jump-assist-state) (6 × 2)
- [T_APM_LADEMODUS_TEXT](#table-t-apm-lademodus-text) (6 × 2)
- [T_DEGRADATION_TEXT](#table-t-degradation-text) (11 × 2)
- [T_HCP_ANTRIEBSART_TEXT](#table-t-hcp-antriebsart-text) (9 × 2)
- [T_HPMR_STATE_TEXT](#table-t-hpmr-state-text) (15 × 2)
- [T_HVIL_GESAMT](#table-t-hvil-gesamt) (3 × 2)
- [T_HVIL_MCPA_B](#table-t-hvil-mcpa-b) (2 × 2)
- [T_HVIL_BATTERIE](#table-t-hvil-batterie) (3 × 2)
- [T_STATUS_ISOL_BATTERIE](#table-t-status-isol-batterie) (4 × 2)
- [T_LADEN_HV_BATTERIE](#table-t-laden-hv-batterie) (5 × 2)
- [T_STATUS_ISOL_PEB](#table-t-status-isol-peb) (3 × 2)
- [T_STEUERN_ANTRIEBSART_TEXT](#table-t-steuern-antriebsart-text) (3 × 2)
- [T_INAKTIV_AKTIV_1BYTE](#table-t-inaktiv-aktiv-1byte) (2 × 2)
- [T_EMPI_MODE_TEXT](#table-t-empi-mode-text) (8 × 2)
- [T_VOLTAGE_HV_SIDE_TEXT](#table-t-voltage-hv-side-text) (2 × 2)
- [T_RESET_SOURCE](#table-t-reset-source) (6 × 2)
- [T_PASS_FAIL_INDETERMINATE](#table-t-pass-fail-indeterminate) (3 × 2)
- [T_TEXTAKTUELLEGETRIEBEPOSITION](#table-t-textaktuellegetriebeposition) (5 × 2)
- [T_TEXTANTRIEBSARTZUGRIFF](#table-t-textantriebsartzugriff) (4 × 2)
- [T_TEXTBATTCONN](#table-t-textbattconn) (7 × 2)
- [T_TEXTCRASHDETECTIONSIGNAL](#table-t-textcrashdetectionsignal) (2 × 2)
- [T_TEXTENERGIESPARMODE](#table-t-textenergiesparmode) (9 × 2)
- [T_TEXTLLREGELUNG](#table-t-textllregelung) (4 × 2)
- [T_TEXTPARKSENSOREN](#table-t-textparksensoren) (4 × 2)
- [T_TEXTREMEDIALACTIONHISTROY](#table-t-textremedialactionhistroy) (10 × 2)
- [T_TEXTDEGRADATIONSOURCE2](#table-t-textdegradationsource2) (33 × 2)
- [T_TEXTDEGRADATIONSOURCE1](#table-t-textdegradationsource1) (33 × 2)
- [T_DEGRADATION_AKT_TEXT](#table-t-degradation-akt-text) (2 × 2)
- [T_TEXTSOCSTIMUL](#table-t-textsocstimul) (2 × 2)
- [T_NOT_AKTIV_AKTIV](#table-t-not-aktiv-aktiv) (2 × 2)
- [T_TRUE_FALSE](#table-t-true-false) (2 × 2)
- [T_TEXTADAPTIONSWERTELESENPYRO](#table-t-textadaptionswertelesenpyro) (2 × 2)
- [T_TEXTLASTSTARTTYPE](#table-t-textlaststarttype) (11 × 2)
- [T_TEXTLASTSTOPTYPE](#table-t-textlaststoptype) (3 × 2)
- [T_TEXTSTEUERNKURZSCHLUVWEMP](#table-t-textsteuernkurzschluvwemp) (3 × 2)
- [T_TEXTDEGRADATIONBIT](#table-t-textdegradationbit) (2 × 2)
- [T_LUEFTERSTUFEN_1_15](#table-t-luefterstufen-1-15) (16 × 2)
- [T_EIN_AUSSCHALTANFORDERUNG](#table-t-ein-ausschaltanforderung) (4 × 2)
- [T_FEHLERVORHANDEN_KEINFEHLERVORHANDEN](#table-t-fehlervorhanden-keinfehlervorhanden) (2 × 2)
- [T_OK_NICHTOK](#table-t-ok-nichtok) (2 × 2)
- [T_GESCHLOSSEN_OFFEN](#table-t-geschlossen-offen) (2 × 2)
- [T_FREIGABE](#table-t-freigabe) (4 × 2)
- [T_GUELTIG_UNGUELTIG](#table-t-gueltig-ungueltig) (2 × 2)
- [T_TEXTSTEUERNBATTKUEHL](#table-t-textsteuernbattkuehl) (8 × 2)
- [T_AUS_ACTIVE_BEENDET](#table-t-aus-active-beendet) (3 × 2)
- [T_TEXTBATTLADELEISTBE](#table-t-textbattladeleistbe) (6 × 2)
- [T_TEXTBATTENTLLEISTST](#table-t-textbattentlleistst) (12 × 2)
- [T_TEXTBATTLADELEISTLT](#table-t-textbattladeleistlt) (10 × 2)
- [T_TEXTBATTLADELEISTBP](#table-t-textbattladeleistbp) (9 × 2)
- [T_TEXTBATTENTLLEISTBP](#table-t-textbattentlleistbp) (9 × 2)
- [T_TEXTBATTLADELEISTST](#table-t-textbattladeleistst) (10 × 2)
- [T_TEXTBATTENTLLEISTBE](#table-t-textbattentlleistbe) (7 × 2)
- [T_TEXTBATTENTLLEISTLT](#table-t-textbattentlleistlt) (12 × 2)
- [T_TEXTFLASHPRECONDITION](#table-t-textflashprecondition) (2 × 2)
- [FORTUMWELTNR](#table-fortumweltnr) (447 × 36)
- [FORTUMWELTTEXTE](#table-fortumwelttexte) (35 × 7)
- [T_TEXTISTRANGE](#table-t-textistrange) (38 × 2)
- [T_TEXTREMEDIALACTIONINPUT2](#table-t-textremedialactioninput2) (32 × 2)
- [T_TEXTREMEDIALACTION](#table-t-textremedialaction) (10 × 2)
- [T_TEXTREMEDIALACTIONINPUT1](#table-t-textremedialactioninput1) (32 × 2)
- [T_TEXTRUECKSCHREIBENIO](#table-t-textrueckschreibenio) (2 × 2)
- [T_NICHTOK_OK](#table-t-nichtok-ok) (2 × 2)
- [T_TEXTMOTORLEISTUNGSMESSUNG](#table-t-textmotorleistungsmessung) (5 × 2)
- [T_EIN_AUS](#table-t-ein-aus) (2 × 2)
- [T_TEXTSTATUSKUPPLUNG](#table-t-textstatuskupplung) (6 × 2)
- [T_TEXT_GEFORDERTNICHTGEFORDERT](#table-t-text-gefordertnichtgefordert) (2 × 2)
- [T_TEXTRANGESTATE](#table-t-textrangestate) (38 × 2)
- [T_TEXTUSECASES](#table-t-textusecases) (22 × 2)
- [T_TEXTGETRIEBERANGE](#table-t-textgetrieberange) (15 × 2)
- [T_TEXTRESETURSACHE](#table-t-textresetursache) (7 × 2)
- [T_OK_NICHT_OK](#table-t-ok-nicht-ok) (2 × 2)
- [T_TEXTSTATEQUROUTINEAKTIV](#table-t-textstatequroutineaktiv) (2 × 2)
- [T_TEXTSTATEQUROUTINEABBRUCH](#table-t-textstatequroutineabbruch) (2 × 2)
- [T_TEXTSTATSPERRBED](#table-t-textstatsperrbed) (2 × 2)
- [T_TEXTSTATBATTEQUIL](#table-t-textstatbattequil) (10 × 2)
- [T_TEXTSOCRUSECASE](#table-t-textsocrusecase) (22 × 2)
- [T_TEXTADAPTIONSWERTELOESCHEN](#table-t-textadaptionswerteloeschen) (4 × 2)
- [T_TEXTBATTLOESCHEN](#table-t-textbattloeschen) (2 × 2)
- [T_GEAR](#table-t-gear) (12 × 2)
- [T_AUS_RESET](#table-t-aus-reset) (2 × 2)
- [T_TEXTAV](#table-t-textav) (40 × 2)
- [T_UNGUELTIG1_GUELTIG0](#table-t-ungueltig1-gueltig0) (2 × 2)
- [T_TEXTBATTKUEHLBETRIEBSMODUS](#table-t-textbattkuehlbetriebsmodus) (26 × 2)
- [T_TEXTDRRMODE](#table-t-textdrrmode) (10 × 2)
- [TINDIVIDUALDATALISTE](#table-tindividualdataliste) (1 × 17)
- [T_TEXTIONIO](#table-t-textionio) (3 × 2)
- [HYBRID_LIEF](#table-hybrid-lief) (6 × 2)
- [DATUM_MONAT](#table-datum-monat) (53 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 66 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x10 | ERROR_ECU_GENERAL_REJECT |
| 0x11 | ERROR_ECU_SERVICE_NOT_SUPPORTED |
| 0x12 | ERROR_ECU_SUB_FUNCTION_NOT_SUPPORTED |
| 0x13 | ERROR_ECU_INCORRECT_MESSAGE_LENGTH_OR_INVALID_FORMAT |
| 0x14 | ERROR_ECU_RESPONSE_TOO_LONG |
| 0x21 | ERROR_ECU_BUSY_REPEAT_REQUEST |
| 0x22 | ERROR_ECU_CONDITIONS_NOT_CORRECT |
| 0x24 | ERROR_ECU_REQUEST_SEQUENCE_ERROR |
| 0x25 | ERROR_ECU_NO_RESPONSE_FROM_SUBNET_COMPONENT |
| 0x26 | ERROR_ECU_FAILURE_PREVENTS_EXECUTION_OF_REQUESTED_ACTION |
| 0x31 | ERROR_ECU_REQUEST_OUT_OF_RANGE |
| 0x33 | ERROR_ECU_SECURITY_ACCESS_DENIED |
| 0x35 | ERROR_ECU_INVALID_KEY |
| 0x36 | ERROR_ECU_EXCEED_NUMBER_OF_ATTEMPTS |
| 0x37 | ERROR_ECU_REQUIRED_TIME_DELAY_NOT_EXPIRED |
| 0x70 | ERROR_ECU_UPLOAD_DOWNLOAD_NOT_ACCEPTED |
| 0x71 | ERROR_ECU_TRANSFER_DATA_SUSPENDED |
| 0x72 | ERROR_ECU_GENERAL_PROGRAMMING_FAILURE |
| 0x73 | ERROR_ECU_WRONG_BLOCK_SEQUENCE_COUNTER |
| 0x78 | ERROR_ECU_REQUEST_CORRECTLY_RECEIVED__RESPONSE_PENDING |
| 0x7E | ERROR_ECU_SUB_FUNCTION_NOT_SUPPORTED_IN_ACTIVE_SESSION |
| 0x7F | ERROR_ECU_SERVICE_NOT_SUPPORTED_IN_ACTIVE_SESSION |
| 0x81 | ERROR_ECU_RPM_TOO_HIGH |
| 0x82 | ERROR_ECU_RPM_TOO_LOW |
| 0x83 | ERROR_ECU_ENGINE_IS_RUNNING |
| 0x84 | ERROR_ECU_ENGINE_IS_NOT_RUNNING |
| 0x85 | ERROR_ECU_ENGINE_RUN_TIME_TOO_LOW |
| 0x86 | ERROR_ECU_TEMPERATURE_TOO_HIGH |
| 0x87 | ERROR_ECU_TEMPERATURE_TOO_LOW |
| 0x88 | ERROR_ECU_VEHICLE_SPEED_TOO_HIGH |
| 0x89 | ERROR_ECU_VEHICLE_SPEED_TOO_LOW |
| 0x8A | ERROR_ECU_THROTTLE_PEDAL_TOO_HIGH |
| 0x8B | ERROR_ECU_THROTTLE_PEDAL_TOO_LOW |
| 0x8C | ERROR_ECU_TRANSMISSION_RANGE_NOT_IN_NEUTRAL |
| 0x8D | ERROR_ECU_TRANSMISSION_RANGE_NOT_IN_GEAR |
| 0x8F | ERROR_ECU_BRAKE_SWITCH_NOT_CLOSED |
| 0x90 | ERROR_ECU_SHIFTER_LEVER_NOT_IN_PARK |
| 0x91 | ERROR_ECU_TORQUE_CONVERTER_CLUTCH_LOCKED |
| 0x92 | ERROR_ECU_VOLTAGE_TOO_HIGH |
| 0x93 | ERROR_ECU_VOLTAGE_TOO_LOW |
| ?00? | OKAY |
| ?01? | ERROR_ECU_NO_RESPONSE |
| ?02? | ERROR_ECU_INCORRECT_LEN |
| ?03? | ERROR_ECU_INCORRECT_RESPONSE_ID |
| ?04? | ERROR_ECU_TA_RESPONSE_NOT_SA_REQUEST |
| ?05? | ERROR_ECU_SA_RESPONSE_NOT_TA_REQUEST |
| ?06? | ERROR_ECU_RESPONSE_INCORRECT_DATA_IDENTIFIER |
| ?07? | ERROR_ECU_RESPONSE_TOO_MUCH_DATA |
| ?08? | ERROR_ECU_RESPONSE_TOO_LESS_DATA |
| ?09? | ERROR_ECU_RESPONSE_VALUE_OUT_OF_RANGE |
| ?0A? | ERROR_TABLE |
| ?10? | ERROR_F_CODE |
| ?12? | ERROR_INTERPRETATION |
| ?13? | ERROR_F_POS |
| ?14? | ERROR_ECU_RESPONSE_INCORRECT_IO_CONTROL_PARAMETER |
| ?15? | ERROR_ECU_RESPONSE_INCORRECT_ROUTINE_CONTROL_TYPE |
| ?16? | ERROR_ECU_RESPONSE_INCORRECT_SUB_FUNCTION |
| ?17? | ERROR_ECU_RESPONSE_INCORRECT_DYNAMICALLY_DEFINED_DATA_IDENTIFIER |
| ?18? | ERROR_ECU_RESPONSE_NO_STRING_END_CHAR |
| ?50? | ERROR_BYTE1 |
| ?51? | ERROR_BYTE2 |
| ?52? | ERROR_BYTE3 |
| ?80? | ERROR_SVK_INCORRECT_LEN |
| ?81? | ERROR_SVK_INCORRECT_FINGERPRINT |
| ?F0? | ERROR_ARGUMENT |
| 0xXY | ERROR_ECU_UNKNOWN_NEGATIVE_RESPONSE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 118 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x000001 | Reinshagen =&gt; Delphi |
| 0x000002 | Kostal |
| 0x000003 | Hella |
| 0x000004 | Siemens |
| 0x000005 | Eaton |
| 0x000006 | UTA |
| 0x000007 | Helbako |
| 0x000008 | Bosch |
| 0x000009 | Loewe =&gt; Lear |
| 0x000010 | VDO |
| 0x000011 | Valeo |
| 0x000012 | MBB |
| 0x000013 | Kammerer |
| 0x000014 | SWF |
| 0x000015 | Blaupunkt |
| 0x000016 | Philips |
| 0x000017 | Alpine |
| 0x000018 | Continental Teves |
| 0x000019 | Elektromatik Suedafrika |
| 0x000020 | Becker |
| 0x000021 | Preh |
| 0x000022 | Alps |
| 0x000023 | Motorola |
| 0x000024 | Temic |
| 0x000025 | Webasto |
| 0x000026 | MotoMeter |
| 0x000027 | Delphi PHI |
| 0x000028 | DODUCO =&gt; BERU |
| 0x000029 | DENSO |
| 0x000030 | NEC |
| 0x000031 | DASA |
| 0x000032 | Pioneer |
| 0x000033 | Jatco |
| 0x000034 | Fuba |
| 0x000035 | UK-NSI |
| 0x000036 | AABG |
| 0x000037 | Dunlop |
| 0x000038 | Sachs |
| 0x000039 | ITT |
| 0x000040 | FTE |
| 0x000041 | Megamos |
| 0x000042 | TRW |
| 0x000043 | Wabco |
| 0x000044 | ISAD Electronic Systems |
| 0x000045 | HEC (Hella Electronics Corporation) |
| 0x000046 | Gemel |
| 0x000047 | ZF |
| 0x000048 | GMPT |
| 0x000049 | Harman Kardon |
| 0x000050 | Remes |
| 0x000051 | ZF Lenksysteme |
| 0x000052 | Magneti Marelli |
| 0x000053 | Borg Instruments |
| 0x000054 | GETRAG |
| 0x000055 | BHTC (Behr Hella Thermocontrol) |
| 0x000056 | Siemens VDO Automotive |
| 0x000057 | Visteon |
| 0x000058 | Autoliv |
| 0x000059 | Haberl |
| 0x000060 | Magna Steyr |
| 0x000061 | Marquardt |
| 0x000062 | AB-Elektronik |
| 0x000063 | Siemens VDO Borg |
| 0x000064 | Hirschmann Electronics |
| 0x000065 | Hoerbiger Electronics |
| 0x000066 | Thyssen Krupp Automotive Mechatronics |
| 0x000067 | Gentex GmbH |
| 0x000068 | Atena GmbH |
| 0x000069 | Magna-Donelly |
| 0x000070 | Koyo Steering Europe |
| 0x000071 | NSI B.V |
| 0x000072 | AISIN AW CO.LTD |
| 0x000073 | Shorlock |
| 0x000074 | Schrader |
| 0x000075 | BERU Electronics GmbH |
| 0x000076 | CEL |
| 0x000077 | Audio Mobil |
| 0x000078 | rd electronic |
| 0x000079 | iSYS RTS GmbH |
| 0x000080 | Westfalia Automotive GmbH |
| 0x000081 | Tyco Electronics |
| 0x000082 | Paragon AG |
| 0x000083 | IEE S.A |
| 0x000084 | TEMIC AUTOMOTIVE of NA |
| 0x000085 | AKsys GmbH |
| 0x000086 | META System |
| 0x000087 | Hülsbeck & Fürst GmbH & Co KG |
| 0x000088 | Mann & Hummel Automotive GmbH |
| 0x000089 | Brose Fahrzeugteile GmbH & Co |
| 0x000090 | Keihin |
| 0x000091 | Vimercati S.p.A. |
| 0x000092 | CRH |
| 0x000093 | TPO Display Corp. |
| 0x000094 | KÜSTER Automotive Control |
| 0x000095 | Hitachi Automotive |
| 0x000096 | Continental Automotive |
| 0x000097 | TI-Automotive |
| 0x000098 | Hydro |
| 0x000099 | Johnson Controls |
| 0x00009A | Takata- Petri |
| 0x00009B | Mitsubishi Electric B.V. (Melco) |
| 0x00009C | Autokabel |
| 0x00009D | GKN-Driveline |
| 0x00009E | Zollner Elektronik AG |
| 0x00009F | PEIKER acustics GmbH |
| 0x0000A0 | Bosal-Oris |
| 0x0000A1 | Cobasys |
| 0x0000A2 | Lighting Reutlingen GmbH |
| 0x0000A3 | CONTI VDO |
| 0x0000A4 | ADC Automotive Distance Control Systems GmbH |
| 0x0000A5 | Funkwerk Dabendorf GmbH |
| 0x0000A6 | Lame |
| 0x0000A7 | Magna/Closures |
| 0x0000A8 | Wanyu |
| 0x0000A9 | Thyssen Krupp Presta |
| 0x0000AA | ArvinMeritor |
| 0x0000AB | Kongsberg Automotive GmbH |
| 0xFFFFFF | unbekannter Hersteller |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 19 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | keine Fehlerart verfügbar |
| 0x04 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x05 | Fehler momentan vorhanden und bereits gespeichert |
| 0x08 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x09 | Fehler momentan vorhanden und bereits gespeichert |
| 0x0C | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x0D | Fehler momentan vorhanden und bereits gespeichert |
| 0x40 | unbekannte Fehlerart |
| 0x44 | Fehler gespeichert |
| 0x45 | Fehler gespeichert |
| 0x48 | Fehler gespeichert |
| 0x49 | Fehler gespeichert |
| 0x4C | Fehler gespeichert |
| 0x4D | Fehler gespeichert |
| 0x10 | Testbedingungen erfüllt |
| 0x11 | Testbedingungen noch nicht erfüllt |
| 0x80 | Fehler würde kein Aufleuchten einer Warnlampe verursachen |
| 0x81 | Fehler würde das Aufleuchten einer Warnlampe verursachen |
| 0xFF | unbekannte Fehlerart |

<a id="table-digitalargument"></a>
### DIGITALARGUMENT

Dimensions: 17 rows × 2 columns

| TEXT | WERT |
| --- | --- |
| ein | 1 |
| aus | 0 |
| ja | 1 |
| nein | 0 |
| auf | 1 |
| ab | 0 |
| an | 1 |
| yes | 1 |
| no | 0 |
| on | 1 |
| off | 0 |
| up | 1 |
| down | 0 |
| true | 1 |
| false | 0 |
| 1 | 1 |
| 0 | 0 |

<a id="table-prozessklassen"></a>
### PROZESSKLASSEN

Dimensions: 24 rows × 3 columns

| WERT | PROZESSKLASSE | BEZEICHNUNG |
| --- | --- | --- |
| 0x00 | - | ungueltig |
| 0x01 | HWEL | Hardware (Elektronik) |
| 0x02 | HWAP | Hardwareauspraegung |
| 0x03 | HWFR | Hardwarefarbe |
| 0x05 | CAFD | Codierdaten |
| 0x06 | BTLD | Bootloader |
| 0x08 | SWFL | Software ECU Speicherimage |
| 0x09 | SWFF | Flash File Software |
| 0x0A | SWPF | Pruefsoftware |
| 0x0B | ONPS | Onboard Programmiersystem |
| 0x0F | FAFP | FA2FP |
| 0x1A | TLRT | Temporaere Loeschroutine |
| 0x1B | TPRG | Temporaere Programmierroutine |
| 0x07 | FLSL | Flashloader Slave |
| 0x0C | IBAD | Interaktive Betriebsanleitung Daten |
| 0x10 | FCFA | Freischaltcode Fahrzeug-Auftrag |
| 0x1C | BLUP | Bootloader-Update Applikation |
| 0x1D | FLUP | Flashloader-Update Applikation |
| 0xA0 | ENTD | Entertainment Daten |
| 0xA1 | NAVD | Navigation Daten |
| 0xA2 | FCFN | Freischaltcode Funktion |
| 0xC0 | SWUP | Software-Update Package |
| 0xC1 | SWIP | Index Software-Update Package |
| 0xFF | - | ungueltig |

<a id="table-svk-id"></a>
### SVK_ID

Dimensions: 65 rows × 2 columns

| WERT | BEZEICHNUNG |
| --- | --- |
| 0x01 | SVK_AKTUELL |
| 0x02 | SVK_SUPPLIER |
| 0x03 | SVK_WERK |
| 0x04 | SVK_BACKUP_01 |
| 0x05 | SVK_BACKUP_02 |
| 0x06 | SVK_BACKUP_03 |
| 0x07 | SVK_BACKUP_04 |
| 0x08 | SVK_BACKUP_05 |
| 0x09 | SVK_BACKUP_06 |
| 0x0A | SVK_BACKUP_07 |
| 0x0B | SVK_BACKUP_08 |
| 0x0C | SVK_BACKUP_09 |
| 0x0D | SVK_BACKUP_10 |
| 0x0E | SVK_BACKUP_11 |
| 0x0F | SVK_BACKUP_12 |
| 0x10 | SVK_BACKUP_13 |
| 0x11 | SVK_BACKUP_14 |
| 0x12 | SVK_BACKUP_15 |
| 0x13 | SVK_BACKUP_16 |
| 0x14 | SVK_BACKUP_17 |
| 0x15 | SVK_BACKUP_18 |
| 0x16 | SVK_BACKUP_19 |
| 0x17 | SVK_BACKUP_20 |
| 0x18 | SVK_BACKUP_21 |
| 0x19 | SVK_BACKUP_22 |
| 0x1A | SVK_BACKUP_23 |
| 0x1B | SVK_BACKUP_24 |
| 0x1C | SVK_BACKUP_25 |
| 0x1D | SVK_BACKUP_26 |
| 0x1E | SVK_BACKUP_27 |
| 0x1F | SVK_BACKUP_28 |
| 0x20 | SVK_BACKUP_29 |
| 0x21 | SVK_BACKUP_30 |
| 0x22 | SVK_BACKUP_31 |
| 0x23 | SVK_BACKUP_32 |
| 0x24 | SVK_BACKUP_33 |
| 0x25 | SVK_BACKUP_34 |
| 0x26 | SVK_BACKUP_35 |
| 0x27 | SVK_BACKUP_36 |
| 0x28 | SVK_BACKUP_37 |
| 0x29 | SVK_BACKUP_38 |
| 0x2A | SVK_BACKUP_39 |
| 0x2B | SVK_BACKUP_40 |
| 0x2C | SVK_BACKUP_41 |
| 0x2D | SVK_BACKUP_42 |
| 0x2E | SVK_BACKUP_43 |
| 0x2F | SVK_BACKUP_44 |
| 0x30 | SVK_BACKUP_45 |
| 0x31 | SVK_BACKUP_46 |
| 0x32 | SVK_BACKUP_47 |
| 0x33 | SVK_BACKUP_48 |
| 0x34 | SVK_BACKUP_49 |
| 0x35 | SVK_BACKUP_50 |
| 0x36 | SVK_BACKUP_51 |
| 0x37 | SVK_BACKUP_52 |
| 0x38 | SVK_BACKUP_53 |
| 0x39 | SVK_BACKUP_54 |
| 0x3A | SVK_BACKUP_55 |
| 0x3B | SVK_BACKUP_56 |
| 0x3C | SVK_BACKUP_57 |
| 0x3D | SVK_BACKUP_58 |
| 0x3E | SVK_BACKUP_59 |
| 0x3F | SVK_BACKUP_60 |
| 0x40 | SVK_BACKUP_61 |
| 0xXY | ERROR_UNKNOWN |

<a id="table-dtcextendeddatarecordnumber"></a>
### DTCEXTENDEDDATARECORDNUMBER

Dimensions: 5 rows × 3 columns

| WERT | TEXT | ANZ_BYTE |
| --- | --- | --- |
| 0x00 | ISO_RESERVED | 0 |
| 0x01 | CONDITION_BYTE | 1 |
| 0x02 | HFK | 1 |
| 0x03 | HLZ | 1 |
| 0xFF | RECORD_UNKNOWN | 0 |

<a id="table-dtcsnapshotidentifier"></a>
### DTCSNAPSHOTIDENTIFIER

Dimensions: 5 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x1700 | KM_STAND | 0-n | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1701 | ABS_ZEIT | 0-n | - | 0xFFFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1702 | SAE_CODE | 0-n | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1731 | Fehlerklasse_DTC | - | - | u char | - | 1 | 1 | 0.000000 |
| 0xFFFF | IDENTIFIER_UNKNOWN | - | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |

<a id="table-fehlerklasse"></a>
### FEHLERKLASSE

Dimensions: 5 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0x00 | Keine Fehlerklasse verfuegbar |
| 0x01 | Ueberpruefung bei naechstem Werkstattbesuch |
| 0x02 | Ueberpruefung bei naechstem Halt |
| 0x04 | Ueberpruefung sofort erforderlich ! |
| 0xFF | unbekannte Fehlerklasse |

<a id="table-diagmode"></a>
### DIAGMODE

Dimensions: 11 rows × 3 columns

| NR | MODE | MODE_TEXT |
| --- | --- | --- |
| 0x00 | UNGUELTIG | DefaultMode |
| 0x01 | DEFAULT | DefaultMode |
| 0x02 | ECUPM | ECUProgrammingMode |
| 0x03 | ECUEXTDIAG | ECUExtendedDiagnosticSession |
| 0x04 | ECUSSDS | ECUSafetySystemDiagnosticSession |
| 0x40 | ECUEOL | ECUEndOfLineSession |
| 0x41 | ECUCODE | ECUCodingSession |
| 0x42 | ECUSWT | ECUSwtSession |
| 0x43 | ECUHDD | ECUHDDDownloadSession |
| 0x4F | ECUDEVELOP | ECUDevelopmentSession |
| 0xXY | -- | unbekannter Diagnose-Mode |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-betriebsmode"></a>
### BETRIEBSMODE

Dimensions: 2 rows × 3 columns

| WERT | TEXT | BEDEUTUNG |
| --- | --- | --- |
| 0x00 | kein Betriebsmode gesetzt | kein Betriebsmode |
| 0xFF | ungültiger Betriebsmode | ungültig |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 456 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x010219 | HCP:  Drehzahl Verbrennungsmotor kurzzeitig höher als zulässig.  | 0 |
| 0x010506 | HCP: Leerlaufregelsystem. Drehzahl zu niedrig  | 0 |
| 0x010507 | HCP: Leerlaufregelsystem. Drehzahl zu hoch  | 0 |
| 0x010562 | HCP: Batterie Unterspannung erkannt | 0 |
| 0x010563 | HCP: Batterie Überspannung erkannt | 0 |
| 0x01061A | HCP: Rückmeldung der Momente vom Bremssteuergerät (SBA)  via CAN Bus HCP unplausibel | 0 |
| 0x01061B | HCP: Unplausibilität Drehhmoment Fahranforderung mit HCP-intern berechnetem Moment. | 0 |
| 0x0107A3 | HCP: Getriebe. Kupplung C1 im stufenlosen Getriebesystem unberechtigt geschlossen in Betriebsart EVT2 | 0 |
| 0x0107A5 | HCP: Getriebe. Kupplung C2 im stufenlosen Getriebesystem unberechtigt geschlossen in Betriebsart EVT1 | 0 |
| 0x0107A7 | HCP: Getriebe. Kupplung C3 im stufenlosen Getriebesystem unberechtigt geschlossen in Betriebsart EVT2 | 0 |
| 0x0107A9 | HCP: Getriebe. Kupplung C4 im stufenlosen Getriebesystem unberechtigt geschlossen in Betriebsart EVT2 | 0 |
| 0x010A02 | HIM: Kühlkreislauf PEB, Temperatursensor Kühlmittelaustritt, Kurzschluss nach Masse | 0 |
| 0x010A03 | HIM: Kühlkreislauf PEB, Temperatursensor Kühlmittelaustritt, Kurzschluss nach Plus | 0 |
| 0x010A0C | BPCM: Hochvoltkontaktüberwachung (High Voltage Interlock Loop), Kurzschluss nach Masse oder Leitungsunterbrechung | 0 |
| 0x010A0D | BPCM: Hochvoltkontaktüberwachung (High Voltage Interlock Loop), Kurzschluss nach Plus | 0 |
| 0x010A1B | MCPB: PEB-interner Steuergerätefehler Prozessorhardware. Abschaltung der Elektromaschinen | 0 |
| 0x010A1C | MCPA: PEB-interner Steuergerätefehler Prozessorhardware. Abschaltung der Elektromaschinen | 0 |
| 0x010A1F | BPCM: Steuergerät interner Hardwarefehler (Mikroprozessor) | 0 |
| 0x010A2A | MCPB: Temperatursensor Getriebeinterne Elektromaschine 1  Leitungsunterbrechung oder Untertemperatur   | 0 |
| 0x010A2B | MCPB: Signal Temperatursensor Getriebeinterne Elektromaschine 1  unplausibel/ ausserhalb zulässiger Bereich  | 0 |
| 0x010A2C | MCPB: Temperatursensor Getriebeinterne Elektromaschine 1  Kurzschluss nach Masse oder Übertemperatur.  | 0 |
| 0x010A2F | MCPB: Getriebeinterne Elektromaschine 1  Überhitzungsfehler | 0 |
| 0x010A30 | MCPA: Temperatursensor Getriebeinterne Elektromaschine 2 Leitungsunterbrechung oder Untertemperatur   | 0 |
| 0x010A31 | MCPA: Signal Temperatursensor Getriebeinterne Elektromaschine 2 unplausibel/ ausserhalb zulässiger Bereich  | 0 |
| 0x010A32 | MCPA: Temperatursensor Getriebeinterne Elektromaschine 2 Kurzschluss nach Masse oder Übertemperatur.  | 0 |
| 0x010A35 | MCPA: Getriebeinterne Elektromaschine 2 Überhitzungsfehler | 0 |
| 0x010A3F | MCPB: Getriebeinterne Elektromaschine 1  Verlust/ Störung Positionssignal Resolver. Abschaltung der Elektromaschinen  | 0 |
| 0x010A40 | MCPB: Getriebeinterne Elektromaschine 1  Resolver Toleranzüberschreitung Positionssignal | 0 |
| 0x010A44 | MCPB: Getriebeinterne Elektromaschine 1  Überdrehzahl des Resolvers. Abschaltung der Elektromaschinen | 0 |
| 0x010A45 | MCPA: Getriebeinterne Elektromaschine 2 Verlust/ Störung Positionssignal Resolver. Abschaltung der Elektromaschinen  | 0 |
| 0x010A46 | MCPA: Getriebeinterne Elektromaschine 2 Resolver Toleranzüberschreitung Positionssignal | 0 |
| 0x010A4A | MCPA: Getriebeinterne Elektromaschine 2 Überdrehzahl des Resolvers. Abschaltung der Elektromaschinen | 0 |
| 0x010A7D | HCP: Ladezustand Hochvoltbatterie niedrig.  | 0 |
| 0x010A7E | HCP: Hochvoltbatterie Übertemperatur  erkannt  | 0 |
| 0x010A80 | BPCM: Hochvoltbatterie defekt, Innenwiderstand über Schwellenwert | 0 |
| 0x010A93 | MCPA: PEB-interner Kühlkreislauf Fehler Kühlmittelfluss | 0 |
| 0x010A95 | BPCM: Hochvoltbatterie Sicherung defekt | 0 |
| 0x010A9C | BPCM:Temperatursensor 1, Wert unplausibel | 0 |
| 0x010A9D | BPCM:Temperatursensor 1, Wert unter Sollwert | 0 |
| 0x010A9E | BPCM:Temperatursensor 1, Wert über Sollwert | 0 |
| 0x010AA6 | BPCM: Isolationsüberwachung Fehler | 0 |
| 0x010ABB | BPCM: interne Spannungsmessung, Wert unplausibel | 0 |
| 0x010ABC | BPCM: interne Spannungsmessung, Wert unter Sollwert | 0 |
| 0x010ABD | BPCM: interne Spannungsmessung, Wert über Sollwert | 0 |
| 0x010AC0 | BPCM: interne Strommessung, Wert unplausibel | 0 |
| 0x010AC1 | BPCM: interne Strommessung, Wert unter Sollwert | 0 |
| 0x010AC2 | BPCM: interne Strommessung, Wert über Sollwert | 0 |
| 0x010AC6 | BPCM:Temperatursensor 2, Wert unplausibel | 0 |
| 0x010AC7 | BPCM:Temperatursensor 2, Wert unter Sollwert | 0 |
| 0x010AC8 | BPCM:Temperatursensor 2, Wert über Sollwert | 0 |
| 0x010ACB | BPCM:Temperatursensor 3, Wert unplausibel | 0 |
| 0x010ACC | BPCM:Temperatursensor 3, Wert unter Sollwert | 0 |
| 0x010ACD | BPCM:Temperatursensor 3, Wert über Sollwert | 0 |
| 0x010ADC | BPCM: Hochvoltbatterie Pluspol Schütz, 12-V-Treiber, Kurzschluß nach 12-V-Versorgung | 0 |
| 0x010AE0 | BPCM: Hochvoltbatterie Minuspol Schütz, 12-V-Treiber, Kurzschluß nach 12-V-Versorgung | 0 |
| 0x010AE7 | BPCM: Hochvoltbatterie Vorbelastung Schütz, 12-V-Treiber, Kurzschluß nach 12-V-Versorgung | 0 |
| 0x010AE9 | BPCM:Temperatursensor 4, Wert unplausibel | 0 |
| 0x010AEA | BPCM:Temperatursensor 4, Wert unter Sollwert | 0 |
| 0x010AEB | BPCM:Temperatursensor 4, Wert über Sollwert | 0 |
| 0x010AEE | MCPA: PEB-interner Inverter Phase U Leistungstransistor Temperatur Bereichsunter-/ überschreitung | 0 |
| 0x010AEF | MCPA: PEB-interner Inverter Phase U Leistungstransistor Temperatursensor Kurzschluss nach Masse | 0 |
| 0x010AF0 | MCPA: PEB-interner Inverter Phase U Leistungstransistor Temperatursensor Kurzschluss nach Plus oder Leitungsunterbrechung | 0 |
| 0x010AF3 | MCPB: PEB-interner Inverter Phase U Leistungstransistor Temperatur Bereichsunter-/ überschreitung | 0 |
| 0x010AF4 | MCPB: PEB-interner Inverter Phase U Leistungstransistor Temperatursensor Kurzschluss nach Masse | 0 |
| 0x010AF5 | MCPB: PEB-interner Inverter Phase U Leistungstransistor Temperatursensor Kurzschluss nach Plus oder Leitungsunterbrechung | 0 |
| 0x010AFA | BPCM: Hochvoltbatterie, Unterspannung | 0 |
| 0x010AFB | BPCM: Hochvoltbatterie, Überspannung | 0 |
| 0x010B0A | EMPI: Spannungsversorgung (14V) Spannung zu niedrig.   | 0 |
| 0x010B0B | EMPI: Spannungsversorgung (14V) Spannung zu hoch.  | 0 |
| 0x010B0D | EMPI: PEB-interner Steuergerätefehler Inverter Hardware oder Treiberlogik defekt. | 0 |
| 0x010B15 | BPCM: externe Spannungsmessung, Wert unplausibel | 0 |
| 0x010B16 | BPCM: externe Spannungsmessung, Wert unter Sollwert | 0 |
| 0x010B17 | BPCM: externe Spannungsmessung, Wert über Sollwert | 0 |
| 0x010B3C | BPCM: Hochvoltbatterie Zellenblock 1, Spannungswert unplausibel | 0 |
| 0x010B3D | BPCM: Hochvoltbatterie Zellenblock 1, Spannungswert unter Sollwert | 0 |
| 0x010B3E | BPCM: Hochvoltbatterie Zellenblock 1, Spannungswert über Sollwert | 0 |
| 0x010B41 | BPCM: Hochvoltbatterie Zellenblock 2, Spannungswert unplausibel | 0 |
| 0x010B42 | BPCM: Hochvoltbatterie Zellenblock 2, Spannungswert unter Sollwert | 0 |
| 0x010B43 | BPCM: Hochvoltbatterie Zellenblock 2, Spannungswert über Sollwert | 0 |
| 0x010B46 | BPCM: Hochvoltbatterie Zellenblock 3, Spannungswert unplausibel | 0 |
| 0x010B47 | BPCM: Hochvoltbatterie Zellenblock 3, Spannungswert unter Sollwert | 0 |
| 0x010B48 | BPCM: Hochvoltbatterie Zellenblock 3, Spannungswert über Sollwert | 0 |
| 0x010B4B | BPCM: Hochvoltbatterie Zellenblock 4, Spannungswert unplausibel | 0 |
| 0x010B4C | BPCM: Hochvoltbatterie Zellenblock 4, Spannungswert unter Sollwert | 0 |
| 0x010B4D | BPCM: Hochvoltbatterie Zellenblock 4, Spannungswert über Sollwert | 0 |
| 0x010B50 | BPCM: Hochvoltbatterie Zellenblock 5, Spannungswert unplausibel | 0 |
| 0x010B51 | BPCM: Hochvoltbatterie Zellenblock 5, Spannungswert unter Sollwert | 0 |
| 0x010B52 | BPCM: Hochvoltbatterie Zellenblock 5, Spannungswert über Sollwert | 0 |
| 0x010B55 | BPCM: Hochvoltbatterie Zellenblock 6, Spannungswert unplausibel | 0 |
| 0x010B56 | BPCM: Hochvoltbatterie Zellenblock 6, Spannungswert unter Sollwert | 0 |
| 0x010B57 | BPCM: Hochvoltbatterie Zellenblock 6, Spannungswert über Sollwert | 0 |
| 0x010B5A | BPCM: Hochvoltbatterie Zellenblock 7, Spannungswert unplausibel | 0 |
| 0x010B5B | BPCM: Hochvoltbatterie Zellenblock 7, Spannungswert unter Sollwert | 0 |
| 0x010B5C | BPCM: Hochvoltbatterie Zellenblock 7, Spannungswert über Sollwert | 0 |
| 0x010B5F | BPCM: Hochvoltbatterie Zellenblock 8, Spannungswert unplausibel | 0 |
| 0x010B60 | BPCM: Hochvoltbatterie Zellenblock 8, Spannungswert unter Sollwert | 0 |
| 0x010B61 | BPCM: Hochvoltbatterie Zellenblock 8, Spannungswert über Sollwert | 0 |
| 0x010B64 | BPCM: Hochvoltbatterie Zellenblock 9, Spannungswert unplausibel | 0 |
| 0x010B65 | BPCM: Hochvoltbatterie Zellenblock 9, Spannungswert unter Sollwert | 0 |
| 0x010B66 | BPCM: Hochvoltbatterie Zellenblock 9, Spannungswert über Sollwert | 0 |
| 0x010B69 | BPCM: Hochvoltbatterie Zellenblock 10, Spannungswert unplausibel | 0 |
| 0x010B6A | BPCM: Hochvoltbatterie Zellenblock 10, Spannungswert unter Sollwert | 0 |
| 0x010B6B | BPCM: Hochvoltbatterie Zellenblock 10, Spannungswert über Sollwert | 0 |
| 0x010B6E | BPCM: Hochvoltbatterie Zellenblock 11, Spannungswert unplausibel | 0 |
| 0x010B6F | BPCM: Hochvoltbatterie Zellenblock 11, Spannungswert unter Sollwert | 0 |
| 0x010B70 | BPCM: Hochvoltbatterie Zellenblock 11, Spannungswert über Sollwert | 0 |
| 0x010B73 | BPCM: Hochvoltbatterie Zellenblock 12, Spannungswert unplausibel | 0 |
| 0x010B74 | BPCM: Hochvoltbatterie Zellenblock 12, Spannungswert unter Sollwert | 0 |
| 0x010B75 | BPCM: Hochvoltbatterie Zellenblock 12, Spannungswert über Sollwert | 0 |
| 0x010B78 | BPCM: Hochvoltbatterie Zellenblock 13, Spannungswert unplausibel | 0 |
| 0x010B79 | BPCM: Hochvoltbatterie Zellenblock 13, Spannungswert unter Sollwert | 0 |
| 0x010B7A | BPCM: Hochvoltbatterie Zellenblock 13, Spannungswert über Sollwert | 0 |
| 0x010B7D | BPCM: Hochvoltbatterie Zellenblock 14, Spannungswert unplausibel | 0 |
| 0x010B7E | BPCM: Hochvoltbatterie Zellenblock 14, Spannungswert unter Sollwert | 0 |
| 0x010B7F | BPCM: Hochvoltbatterie Zellenblock 14, Spannungswert über Sollwert | 0 |
| 0x010B82 | BPCM: Hochvoltbatterie Zellenblock 15, Spannungswert unplausibel | 0 |
| 0x010B83 | BPCM: Hochvoltbatterie Zellenblock 15, Spannungswert unter Sollwert | 0 |
| 0x010B84 | BPCM: Hochvoltbatterie Zellenblock 15, Spannungswert über Sollwert | 0 |
| 0x010B87 | BPCM: Hochvoltbatterie Zellenblock 16, Spannungswert unplausibel | 0 |
| 0x010B88 | BPCM: Hochvoltbatterie Zellenblock 16, Spannungswert unter Sollwert | 0 |
| 0x010B89 | BPCM: Hochvoltbatterie Zellenblock 16, Spannungswert über Sollwert | 0 |
| 0x010B8C | BPCM: Hochvoltbatterie Zellenblock 17, Spannungswert unplausibel | 0 |
| 0x010B8D | BPCM: Hochvoltbatterie Zellenblock 17, Spannungswert unter Sollwert | 0 |
| 0x010B8E | BPCM: Hochvoltbatterie Zellenblock 17, Spannungswert über Sollwert | 0 |
| 0x010B91 | BPCM: Hochvoltbatterie Zellenblock 18, Spannungswert unplausibel | 0 |
| 0x010B92 | BPCM: Hochvoltbatterie Zellenblock 18, Spannungswert unter Sollwert | 0 |
| 0x010B93 | BPCM: Hochvoltbatterie Zellenblock 18, Spannungswert über Sollwert | 0 |
| 0x010B96 | BPCM: Hochvoltbatterie Zellenblock 19, Spannungswert unplausibel | 0 |
| 0x010B97 | BPCM: Hochvoltbatterie Zellenblock 19, Spannungswert unter Sollwert | 0 |
| 0x010B98 | BPCM: Hochvoltbatterie Zellenblock 19, Spannungswert über Sollwert | 0 |
| 0x010B9B | BPCM: Hochvoltbatterie Zellenblock 20, Spannungswert unplausibel | 0 |
| 0x010B9C | BPCM: Hochvoltbatterie Zellenblock 20, Spannungswert unter Sollwert | 0 |
| 0x010B9D | BPCM: Hochvoltbatterie Zellenblock 20, Spannungswert über Sollwert | 0 |
| 0x010BA0 | BPCM: Hochvoltbatterie Zellenblock 21, Spannungswert unplausibel | 0 |
| 0x010BA1 | BPCM: Hochvoltbatterie Zellenblock 21, Spannungswert unter Sollwert | 0 |
| 0x010BA2 | BPCM: Hochvoltbatterie Zellenblock 21, Spannungswert über Sollwert | 0 |
| 0x010BA5 | BPCM: Hochvoltbatterie Zellenblock 22, Spannungswert unplausibel | 0 |
| 0x010BA6 | BPCM: Hochvoltbatterie Zellenblock 22, Spannungswert unter Sollwert | 0 |
| 0x010BA7 | BPCM: Hochvoltbatterie Zellenblock 22, Spannungswert über Sollwert | 0 |
| 0x010BAA | BPCM: Hochvoltbatterie Zellenblock 23, Spannungswert unplausibel | 0 |
| 0x010BAB | BPCM: Hochvoltbatterie Zellenblock 23, Spannungswert unter Sollwert | 0 |
| 0x010BAC | BPCM: Hochvoltbatterie Zellenblock 23, Spannungswert über Sollwert | 0 |
| 0x010BAF | BPCM: Hochvoltbatterie Zellenblock 24, Spannungswert unplausibel | 0 |
| 0x010BB0 | BPCM: Hochvoltbatterie Zellenblock 24, Spannungswert unter Sollwert | 0 |
| 0x010BB1 | BPCM: Hochvoltbatterie Zellenblock 24, Spannungswert über Sollwert | 0 |
| 0x010BB4 | BPCM: Hochvoltbatterie Zellenblock 25, Spannungswert unplausibel | 0 |
| 0x010BB5 | BPCM: Hochvoltbatterie Zellenblock 25, Spannungswert unter Sollwert | 0 |
| 0x010BB6 | BPCM: Hochvoltbatterie Zellenblock 25, Spannungswert über Sollwert | 0 |
| 0x010BB9 | BPCM: Hochvoltbatterie Zellenblock 26, Spannungswert unplausibel | 0 |
| 0x010BBA | BPCM: Hochvoltbatterie Zellenblock 26, Spannungswert unter Sollwert | 0 |
| 0x010BBB | BPCM: Hochvoltbatterie Zellenblock 26, Spannungswert über Sollwert | 0 |
| 0x010BBD | BPCM: Hochvoltbatterie, Spannungsabweichung zwischen den Zellenblöcken über Sollwert | 0 |
| 0x010BD2 | MCPA: PEB-interner Inverter Phase V Leistungstransistor Temperatur Bereichsunter-/ überschreitung | 0 |
| 0x010BD3 | MCPA: PEB-interner Inverter Phase V Leistungstransistor Temperatursensor Kurzschluss nach Masse | 0 |
| 0x010BD4 | MCPA: PEB-interner Inverter Phase V Leistungstransistor Temperatursensor Kurzschluss nach Plus oder Leitungsunterbrechung | 0 |
| 0x010BD7 | MCPB: PEB-interner Inverter Phase V Leistungstransistor Temperatur Bereichsunter-/ überschreitung | 0 |
| 0x010BD8 | MCPB: PEB-interner Inverter Phase V Leistungstransistor Temperatursensor Kurzschluss nach Masse | 0 |
| 0x010BD9 | MCPB: PEB-interner Inverter Phase V Leistungstransistor Temperatursensor Kurzschluss nach Plus oder Leitungsunterbrechung | 0 |
| 0x010BDC | MCPA: PEB-interner Inverter Phase W Leistungstransistor Temperatur Bereichsunter-/ überschreitung | 0 |
| 0x010BDD | MCPA: PEB-interner Inverter Phase W Leistungstransistor Temperatursensor Kurzschluss nach Masse | 0 |
| 0x010BDE | MCPA: PEB-interner Inverter Phase W Leistungstransistor Temperatursensor Kurzschluss nach Plus oder Leitungsunterbrechung | 0 |
| 0x010BE1 | MCPB: PEB-interner Inverter Phase W Leistungstransistor Temperatur Bereichsunter-/ überschreitung | 0 |
| 0x010BE2 | MCPB: PEB-interner Inverter Phase W Leistungstransistor Temperatursensor Kurzschluss nach Masse | 0 |
| 0x010BE3 | MCPB: PEB-interner Inverter Phase W Leistungstransistor Temperatursensor Kurzschluss nach Plus oder Leitungsunterbrechung | 0 |
| 0x010BE6 | MCPB: PEB-interner Inverter Phase U Stromsensor unzulässige Grundabweichung | 0 |
| 0x010BE7 | MCPB: PEB-interner Inverter Phase U Stromsensor Kurzschluss nach Masse. Abschaltung der Elektromaschinen | 0 |
| 0x010BE8 | MCPB: PEB-interner Inverter Phase U Stromsensor Kurzschluss nach Plus oder Leitungsunterbrechung. Abschaltung der Elektromaschinen | 0 |
| 0x010BEA | MCPB: PEB-interner Inverter Phase V Stromsensor unzulässige Grundabweichung | 0 |
| 0x010BEB | MCPB: PEB-interner Inverter Phase V Stromsensor Kurzschluss nach Masse. Abschaltung der Elektromaschinen | 0 |
| 0x010BEC | MCPB: PEB-interner Inverter Phase V Stromsensor Kurzschluss nach Plus oder Leitungsunterbrechung. Abschaltung der Elektromaschinen | 0 |
| 0x010BEE | MCPB: PEB-interner Inverter Phase W Stromsensor unzulässige Grundabweichung | 0 |
| 0x010BEF | MCPB: PEB-interner Inverter Phase W Stromsensor Kurzschluss nach Masse. Abschaltung der Elektromaschinen | 0 |
| 0x010BF0 | MCPB: PEB-interner Inverter Phase W Stromsensor Kurzschluss nach Plus oder Leitungsunterbrechung. Abschaltung der Elektromaschinen | 0 |
| 0x010BF2 | MCPA: PEB-interner Inverter Phase U Stromsensor unzulässige Grundabweichung | 0 |
| 0x010BF3 | MCPA: PEB-interner Inverter Phase U Stromsensor Kurzschluss nach Masse. Abschaltung der Elektromaschinen | 0 |
| 0x010BF4 | MCPA: PEB-interner Inverter Phase U Stromsensor Kurzschluss nach Plus oder Leitungsunterbrechung. Abschaltung der Elektromaschinen | 0 |
| 0x010BF6 | MCPA: PEB-interner Inverter Phase V Stromsensor unzulässige Grundabweichung | 0 |
| 0x010BF7 | MCPA: PEB-interner Inverter Phase V Stromsensor Kurzschluss nach Masse. Abschaltung der Elektromaschine | 0 |
| 0x010BF8 | MCPA: PEB-interner Inverter Phase V Stromsensor Kurzschluss nach Plus oder Leitungsunterbrechung. Abschaltung der Elektromaschinen | 0 |
| 0x010BFA | MCPA: PEB-interner Inverter Phase W Stromsensor unzulässige Grundabweichung | 0 |
| 0x010BFB | MCPA: PEB-interner Inverter Phase W Stromsensor Kurzschluss nach Masse. Abschaltung der Elektromaschinen | 0 |
| 0x010BFC | MCPA: PEB-interner Inverter Phase W Stromsensor Kurzschluss nach Plus oder Leitungsunterbrechung. Abschaltung der Elektromaschinen | 0 |
| 0x010BFD | MCPB: Getriebeinterne Elektromaschine 1  Hochvoltleitungen Versorgung Stromsensor Korrelationsfehler. | 0 |
| 0x010BFE | MCPA: Getriebeinterne Elektromaschine 2 Hochvoltleitungen Versorgung Stromsensor Korrelationsfehler. | 0 |
| 0x010BFF | MCPB: Getriebeinterne Elektromaschine 1  Hochvoltleitungen Versorgung Elektromotorströme asymmetrisch. Leitungsfehler, Isolationsfehler, interne Messfehler | 0 |
| 0x010C01 | MCPB: Getriebeinterne Elektromaschine 1  Hochvoltleitungen Versorgung Elektromotorströme Phasenlage falsch oder Leitungen vertauscht. Strom zu hoch Abschaltung der Elektromaschinen | 0 |
| 0x010C02 | MCPA: Getriebeinterne Elektromaschine 2 Hochvoltleitungen Versorgung Elektromotorströme asymmetrisch. Leitungsfehler, Isolationsfehler, interne Messfehler | 0 |
| 0x010C04 | MCPA: Getriebeinterne Elektromaschine 2 Hochvoltleitungen Versorgung Elektromotorströme Phasenlage falsch oder Leitungen vertauscht. Strom zu hoch. Abschaltung der Elektromaschinen | 0 |
| 0x010C05 | MCPB: Getriebeinterne Elektromaschine 1  Hochvoltleitungen Versorgung Elektromotorströme Leitungsunterbrechung. Abschaltung der Elektromaschinen | 0 |
| 0x010C08 | MCPA: Getriebeinterne Elektromaschine 2 Hochvoltleitungen Versorgung Elektromotorströme Leitungsunterbrechung. Abschaltung der Elektromaschinen | 0 |
| 0x010C0B | MCPB: PEB-interner Inverterfehler. Spannungsversorgung Leistungselektronik ausgefallen. Abschaltung der Elektromaschinen | 0 |
| 0x010C0E | MCPA: PEB-interner Inverter fehlerhaft. Spannungsversorgung Leistungselektronik ausgefallen. Abschaltung der Elektromaschinen | 0 |
| 0x010C11 | MCPB: PEB-interner Inverter Phase U Leistungstransistor Übertemperatur | 0 |
| 0x010C12 | MCPB: PEB-interner Inverter Phase V Leistungstransistor Übertemperatur | 0 |
| 0x010C13 | MCPB: PEB-interner Inverter Phase W Leistungstransistor Übertemperatur | 0 |
| 0x010C14 | MCPA: PEB-interner Inverter Phase U Leistungstransistor Übertemperatur | 0 |
| 0x010C15 | MCPA: PEB-interner Inverter Phase V Leistungstransistor Übertemperatur | 0 |
| 0x010C16 | MCPA: PEB-interner Inverter Phase W Leistungstransistor Übertemperatur | 0 |
| 0x010C17 | MCPB: Getriebeinterne Elektromaschine 1  Resolver Grundwerte nicht eingelernt | 0 |
| 0x010C18 | MCPA: Getriebeinterne Elektromaschine 2 Resolver Grundwerte nicht eingelernt | 0 |
| 0x010C1E | EMPI: PEB-interner Steuergerätefehler Bereichsunterschreitung Sensorwert Temperatursensor. Leitungsunterbrechung oder Kurzschluß nach Masse. | 0 |
| 0x010C1F | EMPI: PEB-interner Steuergerätefehler Bereichsüberschreitung Sensorwert Temperatursensor. Leitungsunterbrechung oder Kurzschluss nach Plus. | 0 |
| 0x010C26 | EMPI: Überstrom fließt durch Hybrid-Ölpumpe. Strom (gemessen im Steuergerät) höher als Schwellwert.  | 0 |
| 0x010C2A | EMPI: Hybrid Ölpumpe Motor blockiert | 0 |
| 0x010C2F | HCP: Verbrennungsmotordrehzahl von Kurbelwellensensor und über Motor A Resolver bestimmte Verbrennungsmotordrehzahl weichen voneinander ab | 0 |
| 0x010C30 | HCP: Ladezustand Hochvoltbatterie hoch.  | 0 |
| 0x010C31 | MCPB: PEB-interner Kühlkreislauf Fehler Kühlmittelfluss | 0 |
| 0x010C43 | BPCM: Kühlmitteleintritt, Kühlmitteltemperatursensor, Wert unplausibel | 0 |
| 0x010C44 | BPCM: Kühlmitteleintritt, Kühlmitteltemperatursensor, Wert unter Sollwert | 0 |
| 0x010C45 | BPCM: Kühlmitteleintritt, Kühlmitteltemperatursensor, Wert über Sollwert | 0 |
| 0x010C4C | BPCM: Kühlmittelpumpe Versorgungspannung, Unterspannung | 0 |
| 0x010C4D | BPCM: Kühlmittelpumpe Versorgungspannung, Überspannung | 0 |
| 0x010C4E | MCPB: Getriebeinterne Elektromaschine 1  Resolver Grundwerte einlernen misslungen. Abschaltung der Elektromaschinen | 0 |
| 0x010C4F | MCPA: Getriebeinterne Elektromaschine 2 Resolver Grundwerte einlernen fehlgeschlagen. Abschaltung der Elektromaschinen | 0 |
| 0x010C52 | MCPB: Getriebeinterne Elektromaschine 1  Resolver Spur A Kurzschluss nach Masse | 0 |
| 0x010C53 | MCPB: Getriebeinterne Elektromaschine 1   Resolver Spur A Leitungsunterbrechung oder Kurzschluss nach Plus | 0 |
| 0x010C57 | MCPA: Getriebeinterne Elektromaschine 2 Resolver Spur A Kurzschluss nach Masse | 0 |
| 0x010C58 | MCPA: Getriebeinterne Elektromaschine 2 Resolver Spur A Leitungsunterbrechung oder Kurzschluss nach Plus | 0 |
| 0x010C5C | MCPB: Getriebeinterne Elektromaschine 1  Resolver Spur B Kurzschluss nach Masse  | 0 |
| 0x010C5D | MCPB: Getriebeinterne Elektromaschine 1  Resolver Spur B Leitungsunterbrechung oder Kurzschluss nach Plus  | 0 |
| 0x010C61 | MCPA: Getriebeinterne Elektromaschine 2  Resolver Spur B Kurzschluss nach Masse  | 0 |
| 0x010C62 | MCPA: Getriebeinterne Elektromaschine 2  Resolver Spur B Leitungsunterbrechung oder Kurzschluss nach Plus  | 0 |
| 0x010C76 | BPCM: aktive Entladung zu langsam | 0 |
| 0x010C77 | BPCM: Aktivierung des Hochvoltbordnetzs fehlgeschlagen, Vorbelastung zu schnell | 0 |
| 0x010C78 | HCP: Aktivierung des Hochvoltbordnetzs nach SchLießung der Schütze fehlgeschlagen, Vorbelastung zu langsam | 0 |
| 0x01139F | HCP:  Drehzahl Signal Elektromaschine A: Rückwärtsdrehender Verbrennungsmotor erkannt | 0 |
| 0x0115A9 | Energiesparmodus - Transportmodus | 0 |
| 0x011828 | HCP: Elektronische Drucksteuerventile Sollwerte falsch oder Werte nicht plausibel mit aktuellem Betriebszustand | 0 |
| 0x011829 | HCP: Kupplungs-Ansteuerung Sollwerte falsch oder Werte nicht plausibel mit aktuellem Betriebszustand | 0 |
| 0x011A00 | HCP:  Drehmoment Signal Verbrennungsmotor aktuell geringer als angefordert. Verbrennungsmotor startet trotz Aufforderung nicht. Problemverursachung ggfs. Verbrennungsmotor | 0 |
| 0x011A01 | BPCM: Steuergerät interner Hardwarefehler (EEPROM) | 0 |
| 0x011A02 | HCP: Steckverbindung PEB fehlerhaft. Batteriekontakt offen. Mögliche Ursache Steckerkontakt oder Kabelbaum | 0 |
| 0x011A03 | HCP: Steckverbindung PEB fehlerhaft. Kurzschluss nach Masse festgestellt. Mögliche Ursache Steckerkontakt oder Kabelbaum | 0 |
| 0x011A04 | HCP: Steckverbindung PEB fehlerhaft. Kurzschluss nach Versorgungsspannung festgestellt. Mögliche Ursache Steckerkontakt oder Kabelbaum | 0 |
| 0x011A05 | BPCM: Steuergerät interner Hardwarefehler (RAM) | 0 |
| 0x011A06 | BPCM: Steuergerät interner Hardwarefehler (ROM) | 0 |
| 0x011A07 | BPCM: Stromsensor, Versorgungspannung außerhalb Sollbereich | 0 |
| 0x011A08 | BPCM: Hochvoltbatterie Schütze, Kontakte kleben | 0 |
| 0x011A09 | HCP:  Airbag Auslösung erkannt. Abschaltung der Hochspannung durch Pyrofuse (integriert in der SBK - SicherheitsBatterieKlemme). | 0 |
| 0x011A0A | HCP: Eingangssignal liegt ausserhalb des gültigen Spannungsbereiches | 0 |
| 0x011A0B | BPCM: Hochvoltbatterie, Summe der einzelnen Sensorspannungen unplausibel | 0 |
| 0x011A0C | BPCM: Steuergerät, Versorgungspannung Unterspannung | 0 |
| 0x011A0D | BPCM: Steuergerät, Versorgungspannung Überspannung | 0 |
| 0x011A0E | MCPB: Verifikationsfehler getriebeinterne Elektromaschine 1. Kalibrierdaten für Hochvolt-Sensorik ungültig   | 0 |
| 0x011A0F | MCPA: Verifikationsfehler getriebeinterne Elektromaschine 2. Kalibrierdaten für Hochvolt-Sensorik ungültig   | 0 |
| 0x011A10 | MCPB: Temperatursensorwert Kühlmitteltemperatur PEB unplausibel | 0 |
| 0x011A11 | MCPA: Temperatursensorwert Kühlmitteltemperatur PEB unplausibel   | 0 |
| 0x011A12 | BPCM: Schütze, Versorgungspannung Unterspannung | 0 |
| 0x011A13 | BPCM: Schütze, Versorgungspannung Überspannung | 0 |
| 0x011A19 | BPCM: Hochvoltbatterie, mehrere Temperatursensoren ausgefallen | 0 |
| 0x011A20 | BPCM: Aktivierung des Hochvoltbordnetzs fehlgeschlagen, Vorbelastung zu langsam | 0 |
| 0x011A21 | HCP: Hochvoltbordnetz Schütze unaufgefordert offen erkannt. Betriebsstörung. Kommentar | 0 |
| 0x011A25 | MCPB: PEB-interner Inverterfehler Überstrom am Umrichter. Abschaltung der Elektromaschinen | 0 |
| 0x011A26 | MCPA: PEB-interner Inverter fehlerhaft. Überstrom am Umrichter. Abschaltung der Elektromaschinen | 0 |
| 0x011A2A | MCPA: PEB-interne Logikspannung (5V) zu hoch Ursache im Bordnetz (Niederspannungsseite) | 0 |
| 0x011A2B | MCPA: PEB-interne Logikspannung (5V) zu niedrig Ursache im Bordnetz (Niederspannungsseite) | 0 |
| 0x011A2C | MCPB: PEB-interne Logikspannung (5V) zu hoch Ursache im Bordnetz (Niederspannungsseite) | 0 |
| 0x011A2D | MCPB: PEB-interne Logikspannung (5V) zu niedrig Ursache im Bordnetz (Niederspannungsseite) | 0 |
| 0x011A30 | BPCM: Weckleitung 1, Kurzschluss nach Masse | 0 |
| 0x011A31 | BPCM: Weckleitung 1, Kurzschluss nach Plus | 0 |
| 0x011A32 | BPCM: Weckleitung 2, Kurzschluss nach Plus | 0 |
| 0x011A33 | MCPA: PEB-interne Spannungsversorgung (15V) zu hoch Ursache PEB-intern | 0 |
| 0x011A34 | MCPA: PEB-interne Spannungsversorgung (15V) zu niedrig Ursache PEB-intern | 0 |
| 0x011A35 | MCPB: PEB-interne Spannungsversorgung (15V) zu hoch Ursache PEB-intern | 0 |
| 0x011A36 | MCPB: PEB-interne Spannungsversorgung (15V) zu niedrig Ursache PEB-intern | 0 |
| 0x011A37 | MCPA: PEB-interne Steuerung Drehmomentüberwachung unplausibel | 0 |
| 0x011A38 | MCPB: PEB-interne Steuerung Drehmomentüberwachung unplausibel | 0 |
| 0x011A40 | HCP: HCP-interner Steuergerätefehler ROM-Check fehlerhaft  | 0 |
| 0x011A41 | HCP: HCP-interner Steuergerätefehler RAM-Check fehlerhaft | 0 |
| 0x011A42 | HCP: HCP-interner Steuergerätefehler EEPROM Schreibfehler | 0 |
| 0x011A43 | HCP: HCP-interner Steuergerätefehler Prozessor Hardware: Externer Überwachungsrechner fehlerhaft | 0 |
| 0x011A44 | HCP: HCP-interner Steuergerätefehler Prozessor Hardware. Abschalten im Fehlerfalle nicht gewährleistet  | 0 |
| 0x011A45 | HCP: HCP-interner Steuergerätefehler Steuergerät wurde nicht programmiert  | 0 |
| 0x011A46 | HCP: HCP-interner Steuergerätefehler EEPROM Lesefehler   | 0 |
| 0x011A47 | HCP: HCP-interner Steuergerätefehler Prozessor Leistungsproblem | 0 |
| 0x011A48 | HCP: HCP-interner Steuergerätefehler RAM Datenredundanz Fehler | 0 |
| 0x011A4F | MCPB: PEB-interne Steuerung Softwarefehler oder Steuergerät nicht programmiert. Abschaltung der Elektromaschinen | 0 |
| 0x011A50 | MCPB: PEB-interne Steuerung RAM Arbeitsspeicher Fehler | 0 |
| 0x011A51 | MCPB: PEB-interne Steuerung ROM Lesespeicher Fehler | 0 |
| 0x011A52 | MCPA: PEB-interne Steuerung Softwarefehler oder Steuergerät nicht programmiert. Abschaltung der Elektromaschinen | 0 |
| 0x011A53 | MCPA: PEB-interne Steuerung RAM Arbeitsspeicher Fehler | 0 |
| 0x011A54 | MCPA: PEB-interne Steuerung ROM Lesespeicher Fehler | 0 |
| 0x011A55 | EMPI: PEB-interner Steuergerätefehler Übertemperatur Hybrid-Ölpumpenansteuerung.  | 0 |
| 0x011A5A | BPCM: Hochvoltbatterie, Überwachung Leitungsunterbrechung, Fehlfunktion | 0 |
| 0x011A69 | EMPI: Spannung aus Hochvoltbatterie zu gering. Spannungsschwelle unterschritten. Problemverursachung ggfs. in Hochvoltbatterie | 0 |
| 0x011A6A | EMPI: Spannung aus Hochvoltbatterie zu hoch. Spannungsschwelle überschritten. | 0 |
| 0x011A6B | EMPI: Hochvolt Spannungssensor Phase U allgemeiner Fehler. Sensorbereich unterschritten oder überschritten | 0 |
| 0x011A6C | EMPI: Hochvolt Spannungssensor Phase V allgemeiner Fehler. Sensorbereich unterschritten oder überschritten | 0 |
| 0x011A6D | EMPI: Hochvolt Spannungssensor Phase W allgemeiner Fehler. Sensorbereich unterschritten oder überschritten | 0 |
| 0x011A6E | EMPI: Überdrehzahl Hybrid- Ölpumpe. Drehzahl höher als Schwellenwert.  | 0 |
| 0x011A6F | EMPI: Isolationsfehler Isolationsverlust Elektrische Leitung oder Isolationsverlust Hybrid-Ölpumpe | 0 |
| 0x011A70 | EMPI: PEB-interner Steuergerätefehler Bereichsunterschreitung Sensorwert Stromsensor. Leitungsunterbrechung oder Kurzschluss nach Masse. | 0 |
| 0x011A71 | EMPI: PEB-interner Steuergerätefehler Bereichsüberschreitung Sensorwert Stromsensor. Leitungsunterbrechung oder Kurzschluss nach Plus. | 0 |
| 0x011A74 | EMPI: PEB-interner Steuergerätefehler Bereichsunterschreitung Sensorwert Spannungssensor. Leitungsunterbrechung oder Kurzschluß nach Masse. | 0 |
| 0x011A75 | EMPI: PEB-interner Steuergerätefehler Bereichsüberschreitung Sensorwert Spannungssensor. Leitungsunterbrechung oder Kurzschluss nach Plus. | 0 |
| 0x011ABE | BPCM: Übertemperatur, 2. Schwellenwert überschritten | 0 |
| 0x011AC6 | MCPA: Verlust Drehzahlsignal des Kurbelwellensensor im Verbrennungsmotor (Signal benötigt von Komfortfunktion Aufstartverhalten) | 0 |
| 0x011AC7 | MCPA:  Unplausibilität Drehzahlsignal des Kurbelwellensensor im Verbrennungsmotor (Signal benötigt von Komfortfunktion Aufstartverhalten) | 0 |
| 0x011ADC | MCPB: PEB-interne Steuerung EEPROM Fehler | 0 |
| 0x011ADD | MCPA: PEB-interne Steuerung EEPROM Fehler | 0 |
| 0x011ADE | MCPA: PEB-interne Steuerung Spannungsversorgung (14V) Spannung zu niedrig. Ursache im Bordnetz. Abschaltung der Elektromaschinen | 0 |
| 0x011ADF | MCPA: PEB-interne Steuerung Spannungsversorgung (14V) Spannung zu hoch. Ursache im Bordnetz. Abschaltung der Elektromaschinen | 0 |
| 0x011AE0 | MCPB: PEB-interne Steuerung Spannungsversorgung (14V) Spannung zu niedrig. Ursache im Bordnetz. Abschaltung der Elektromaschinen | 0 |
| 0x011AE1 | MCPB: PEB-interne Steuerung Spannungsversorgung (14V) Spannung zu hoch. Ursache im Bordnetz. Abschaltung der Elektromaschinen | 0 |
| 0x011AE5 | BPCM: Schützsteuerung, Signal von HCP unplausibel | 0 |
| 0x011AE7 | BPCM: Hochvoltbatterie, interner Isolationswiderstand unter 2. Schwellenwert | 0 |
| 0x011AE8 | MCPB: PEB-interne Steuerung getriebeinterne Elektromaschine 1  Hochvolt Spannungssensor Kurzschluss nach Masse | 0 |
| 0x011AE9 | MCPB: PEB-interne Steuerung getriebeinterne Elektromaschine 1  Hochvolt Spannungssensor Kurzschluss nach Plus oder Leitungsunterbrechung | 0 |
| 0x011AEA | MCPA: PEB-interne Steuerung getriebeinterne Elektromaschine 2 Hochvolt Spannungssensor Kurzschluss nach Masse | 0 |
| 0x011AEB | MCPA: PEB-interne Steuerung getriebeinterne Elektromaschine 2 Hochvolt Spannungssensor Kurzschluss nach Plus oder Leitungsunterbrechung | 0 |
| 0x011AEC | MCPB: PEB-interne Steuerung getriebeinterne Elektromaschine 1 Hochvolt Spannungssensoren Plausibilitätsfehler. Abschaltung der Elektromaschinen  | 0 |
| 0x011AED | MCPA: PEB-interne Steuerung getriebeinterne Elektromaschine 2 Hochvolt Spannungssensoren Plausibilitätsfehler. Abschaltung der Elektromaschinen  | 0 |
| 0x011AEE | MCPB: PEB-interne Steuerung getriebeinterne Elektromaschine 1 Bereichsüberschreitung Hochvoltspannung aus Hochvoltbatterie zu hoch | 0 |
| 0x011AEF | MCPA: PEB-interne Steuerung getriebeinterne Elektromaschine 2 Bereichsüberschreitung Hochvoltspannung aus Hochvoltbatterie zu hoch | 0 |
| 0x011AF0 | MCPB: PEB-interne Steuerung getriebeinterne Elektromaschine 1  Versorgung Hochvoltleitungen Fehler Isolationswiderstand zu gering | 0 |
| 0x011AF1 | MCPB: PEB-interne Steuerung getriebeinterne Elektromaschine 1 Versorgung Hochvoltleitungen Warnung Isolationswiderstand zu gering | 0 |
| 0x011AF2 | MCPA: PEB-interne Steuerung getriebeinterne Elektromaschine 2 Versorgung Hochvoltleitungen Fehler Isolationswiderstand zu gering | 0 |
| 0x011AF3 | MCPA: PEB-interne Steuerung getriebeinterne Elektromaschine 2 Versorgung Hochvoltleitungen Warnung Isolationswiderstand zu gering | 0 |
| 0x011AF4 | MCPB: PEB-interne Steuerung getriebeinterne Elektromaschine 1 Isolationsüberwachung Kurzschluss nach Masse | 0 |
| 0x011AF5 | MCPB: PEB-interne Steuerung getriebeinterne Elektromaschine 1  Isolationsüberwachung Kurzschluss nach Plus oder Leitungsunterbrechung | 0 |
| 0x011AF6 | MCPA: PEB-interne Steuerung getriebeinterne Elektromaschine 2 Isolationsüberwachung Kurzschluss nach Masse | 0 |
| 0x011AF7 | MCPA: PEB-interne Steuerung getriebeinterne Elektromaschine 2 Isolationsüberwachung Kurzschluss nach Plus oder Leitungsunterbrechung | 0 |
| 0x011AF8 | MCPB: PEB-interner Inverter fehlerhaft Störung Steuerung Elektromaschine 1, Abschaltpfadtest | 0 |
| 0x011AF9 | MCPB: PEB-interner Inverter fehlerhaft Störung Steuerung Elektromaschine 1, Einschaltvorgang | 0 |
| 0x011AFA | MCPA: PEB-interner Steuergerätefehler Programmierung Initialisierung ungültig. Abschaltung der Elektromaschinen | 0 |
| 0x011AFB | MCPB: PEB-interner Softwarefehler, Programmablaufkontrolle ungültig. Abschaltung der Leitsungselektronik. | 0 |
| 0x011AFE | MCPA: PEB-interner Inverter fehlerhaft Störung Steuerung Elektromaschine 2, Abschaltpfadtest | 0 |
| 0x011AFF | MCPA: PEB-interner Inverter fehlerhaft Störung Steuerung Elektromaschine 2, Einschaltvorgang | 0 |
| 0x011B01 | MCPA: PEB-interner Softwarefehler, Programmablaufkontrolle ungültig. Abschaltung der Leistungselektronik | 0 |
| 0x011B03 | MCPB: Getriebeinterne Elektromaschine 1  Verlust/ Störung Spurinformation Resolver. Abschaltung der Elektromaschinen | 0 |
| 0x011B04 | MCPA: Getriebeinterne Elektromaschine 2 Verlust/ Störung Spurinformation Resolver. Abschaltung der Elektromaschinen | 0 |
| 0x011B05 | MCPA: PEB-externer Fehler getriebeinterne Elektromaschine 1 High Voltage Interlock Loop betätigt/ Hochvoltkontaktüberwachung unterbrochen.  | 0 |
| 0x011B06 | MCPA: PEB-externer Fehler getriebeinterne Elektromaschine 2 High Voltage Interlock Loop betätigt/ Hochvoltkontaktüberwachung unterbrochen.  | 0 |
| 0x011B07 | MCPB: PEB-interne Steuerung getriebeinterne Elektromaschine 1 Bereichsüberschreitung Hochvoltspannung aus Hochvoltbatterie zu niedrig | 0 |
| 0x011B08 | MCPA: PEB-interne Steuerung getriebeinterne Elektromaschine 2 Bereichsüberschreitung Hochvoltspannung aus Hochvoltbatterie zu niedrig | 0 |
| 0x011B09 | MCPB: PEB-interne Steuerung: Spannungsversorgung (14V) zu gering für Betrieb des Steuergerätes | 0 |
| 0x011B0A | MCPA: PEB-interne Steuerung: Spannungsversorgung (14V) zu gering für Betrieb des Steuergerätes | 0 |
| 0x011B0F | MCPB: Getriebeinterne Elektromaschine 1  Fehler Resolver einlernen mislungen. Abschaltung der Elektromaschinen | 0 |
| 0x011B10 | MCPA: Getriebeinterne Elektromaschine 2 Fehler Resolver einlernen fehlgeschlagen. Abschaltung der Elektromaschinen | 0 |
| 0x011B11 | HCP: Unplausibilität Drehmomenterfassung. Gemessener Wert geringer als berechnetes Moment. | 0 |
| 0x011B12 | HCP: Unplausibilität Drehmomenterfassung. Gemessener Wert höher als berechnetes Moment. | 0 |
| 0x011B18 | HCP: Hybrid Ölpumpe Regelzustand fehlerhaft festgestellt | 0 |
| 0x011B20 | BPCM: Authentifizierung der Kühlpumpe noch gesperrt durch Batterie-Control-Modul | 0 |
| 0x011B21 | HCP: Unplausibilität zwischen Dynamisches Verlustmoment und HCP-intern berechnetem Verlustmoment | 0 |
| 0x011B22 | BPCM: Hochvoltbatterie, interner  Isolationswiderstand unter 1. Schwellenwert | 0 |
| 0x011B27 |  HCP: Kühlung Hochvoltbatterie,  Kühlleistung Kühlaggregat unzureichend | 0 |
| 0x011B28 | BPCM: Kühlmittelpumpe eingeschränkter Betrieb | 0 |
| 0x011B29 | BPCM: Kühlmittelpumpe, Betrieb ohne Kühlmittel | 0 |
| 0x011B2A | BPCM: Kühlmittelpumpe, Überspannung oder Überstrom | 0 |
| 0x011B2B | BPCM: Kühlmittelpumpe defekt | 0 |
| 0x011B2D | BPCM: Leitungsanschluss Hochvoltbordnetz, Leitungsunterbrechung | 0 |
| 0x011B2F | BPCM: Aktivierung Hochvoltbordnetz fehlgeschlagen, Schütze offen | 0 |
| 0x011B30 | HCP: HCP-interne Getriebeüberwachung. Parkposition aktuell eingelegt. Aktuell kein Fahrerwunsch Parken vorhanden. | 0 |
| 0x011B31 | HCP: HCP-interne Getriebeüberwachung. Parkposition aktuell nicht eingelegt. Aktuell Fahrerwunsch Parken vorhanden. | 0 |
| 0x011B32 | HCP: HCP-interne Getriebeüberwachung. Aktuelle Parkposition nicht detektierbar. | 0 |
| 0x011B33 | HCP: HCP-interne Getriebeüberwachung. Aktuelle Parkposition nicht detektierbar oder unplausibel. | 0 |
| 0x011B34 | HIM: Kühlkreislauf Hochvoltbatterie, Duo-Wasserventil zum Wärmetauscher Leitung Kurzschluss nach Plus | 0 |
| 0x011B35 | HIM: Kühlkreislauf Hochvoltbatterie, Duo-Wasserventil zum Wärmetauscher, Leitung Kurzschluss nach Masse | 0 |
| 0x011B36 | HIM: Kühlkreislauf Hochvoltbatterie, Duo-Wasserventil zum Wärmetauscher, Leitungsunterbrechung | 0 |
| 0x011B37 | HIM: Kühlkreislauf Hochvoltbatterie, Duo-Wasserventil zum Kühlaggregat, Leitung Kurzschluss nach Plus | 0 |
| 0x011B38 | HIM: Kühlkreislauf Hochvoltbatterie, Duo-Wasserventil zum Kühlaggregat, Leitung Kurzschluss nach Masse | 0 |
| 0x011B39 | HIM: Kühlkreislauf Hochvoltbatterie, Duo-Wasserventil zum Kühlaggregat, Leitungsunterbrechung | 0 |
| 0x011B3F | BPCM: Hochvoltbordnetz, Überstrom | 0 |
| 0x011B40 | BPCM: Hochvoltsicherheitsschalter (Service Disconnect) abgezogen | 0 |
| 0x011B41 | BPCM: Schütze wegen internes Fehlers oder Kommunikationsfehler geöffnet | 0 |
| 0x011B42 | BPCM: Vorbelastungswiderstand, Überhitzungsschutz aktiv | 0 |
| 0x011B43 | BPCM: Hochvoltbordnetz, Isolationswiderstand unter 2. Schwellwert | 0 |
| 0x011B44 | BPCM: Hochvoltbordnetz, Isolationswiderstand unter 1. Schwellwert | 0 |
| 0x011B45 | BPCM: Hochvoltbatterie Pluspol- und Vorbelastungs-Schütz, Kontakte kleben | 0 |
| 0x011B46 | BPCM: Hochvoltbatterie Minuspol Schütz, Kontakt klebt  | 0 |
| 0x011B47 | BPCM: Hochvoltsicherheit, Diagnosefunktion deaktiviert  | 0 |
| 0x011B48 | BPCM: Kühlmittelpumpe, Drehzahl unplausibel | 0 |
| 0x011B4A | HCP: Hybridantriebs-Steuergerät, interner Fehler Shift by Wire Überwachung | 0 |
| 0x011B4B | HCP: Unterspannung Hochvoltbordnetz erkannt. Mögliche Ursache in Hochvoltbatterie   | 0 |
| 0x011B4C | HCP: Überspannung Hochvoltbordnetz erkannt. Mögliche Ursache in Hochvoltbatterie  | 0 |
| 0x011B4D | HCP: Hybridantriebs-Steuergeraet, interne Getriebeueberwachung - falsche Anweisung | 0 |
| 0x011B4E | HCP: Hybridantriebs-Steuergeraet, interne Getriebeueberwachung - Signalfehler Getriebeposition | 0 |
| 0x011B4F | HCP: Hybridantriebs-Steuergeraet, interne Getriebeueberwachung - falsche Getriebeposition | 0 |
| 0x011B50 | HCP: Hybridantriebs-Steuergeraet, interne Getriebeueberwachung - Fahrzeuggeschwindigkeit | 0 |
| 0x011B51 | HCP: HCP-interne Getriebeüberwachung Unplausibilität Fahrzeug Geschwindigkeit mit aktuellem Gang. | 0 |
| 0x011B5F | HCP: Unplausibilität zwischen berechnetem Istmoment Ebene1 und Istmoment Ebene2 | 0 |
| 0x011B71 | HCP: System-Shutdown durch Batteriesteuerung verursacht | 0 |
| 0x011B72 | HCP: System-Shutdown durch E-Maschinensteuerung verursacht | 0 |
| 0x011B73 | HCP: System-Shutdown durch fehlerhafte Sensorik verursacht | 0 |
| 0x011B74 | HCP: System-Shutdown durch Notlauf-Ersatzreaktion verursacht | 0 |
| 0x011C43 | BPCM: Kühlmittelaustritt, Kühlmitteltemperatursensor, Wert unplausibel | 0 |
| 0x011C44 | BPCM: Kühlmittelaustritt, Kühlmitteltemperatursensor, Wert unter Sollwert | 0 |
| 0x011C45 | BPCM: Kühlmittelaustritt, Kühlmitteltemperatursensor, Wert über Sollwert | 0 |
| 0x01215C | HCP: Getriebe Ausgangsdrehzahl unplausibel mit Raddrehzahl | 0 |
| 0x012533 | HCP: Eingangssignal Zündung offen | 0 |
| 0x012797 | HCP: Hybrid Ölpumpe Abweichung zur Solldrehzahl festgestellt | 0 |
| 0x015001 | SBA: Bremskraftverstärker Druck Plausibilität | 0 |
| 0x015002 | SBA: Bremskraftverstärker Spule Fehler elektrisch | 0 |
| 0x015003 | SBA: Bremskraftverstaerker  Unterdruck Versorgung | 0 |
| 0x015010 | SBA: Tandemhauptzylinder Druck Sensor 1 Signal Offset, Plausibilität | 0 |
| 0x015011 | SBA: Tandemhauptzylinder Druck Sensor 2 Signal Offset, Plausibilität | 0 |
| 0x015012 | SBA: Tandemhauptzylinder Druck Sensor 1 Fehler elektrisch | 0 |
| 0x015013 | SBA: Tandemhauptzylinder Druck Sensor 2 Fehler elektrisch | 0 |
| 0x015016 | SBA: Tandemhauptzylinder Bremsdrucksensoren Initialisierung | 0 |
| 0x015020 | SBA: Bremskraftverstärker Wegsensor Signal Plausibilitaet | 0 |
| 0x015021 | SBA: Bremskraftverstärker Wegsensor Fehler elektrisch  | 0 |
| 0x015030 | SBA: Unterdrucksensor Fehler elektrisch Kanal1 | 0 |
| 0x015031 | SBA: Unterdrucksensor Fehler elektrisch Kanal 2 | 0 |
| 0x015032 | SBA Unterdrucksensor Signalwerte Plausibilität | 0 |
| 0x01503F | SBA: Sensoren Versorgungsspannung | 0 |
| 0x015040 | SBA: Vakuum Pumpe Fehler elektrisch | 0 |
| 0x015050 | SBA: Bremssystem Simulator Einheit - elektrischer Fehler des Drucksensors | 0 |
| 0x015051 | SBA: Bremssystem Simulator Einheit - elektrischer Fehler des Ventils | 0 |
| 0x015052 | SBA: Bremssystem Simulator Einheit - allgemeiner Fehler | 0 |
| 0x015062 | SBA: Bremspedalwinkelsensor - Kurzschluss nach Masse | 0 |
| 0x015063 | SBA: Bremspedalwinkelsensor, Kurzschluss nach Plus  | 0 |
| 0x015067 | SBA: Bremspedalwinkelsensor  Überspannung   | 0 |
| 0x015068 | SBA: Bremspedalwinkelsensor  Unterspannung  | 0 |
| 0x015069 | SBA: Bremspedalwinkelsensor Initialisierung | 0 |
| 0x015070 | SBA: Bandendetest Initialisierung  | 0 |
| 0x015071 | SBA: Rekuperatives Bremsen Bremsmomente Plausibilität | 0 |
| 0x015072 | SBA: Überwachung DSC | 0 |
| 0x015073 | SBA: Fahrgestellnummer ungültig  | 0 |
| 0x015080 | SBA: Steuergerät Unterspannung  | 0 |
| 0x015081 | SBA: Steuergerät Überspannung | 0 |
| 0x015082 | SBA: Steuergerät: Interner Fehler (Hardware) | 0 |
| 0x01C073 | HCP: HL-CAN Bus Leitungsfehler | 0 |
| 0x01C074 | HCP: HS-CAN Bus Leitungsfehler  | 0 |
| 0x01D800 | BPCM: Kühlmittelpumpe, Kommunikationsverlust | 0 |
| 0x01D801 | HCP:  Botschaft vom Steuergerät DME über HL-CAN fehlt | 0 |
| 0x01D802 | HCP:  Botschaft vom Steuergerät TCM  (Hybrid-Getriebesteuerung) fehlt | 0 |
| 0x01D803 | HCP:  Botschaft vom Steuergerät BPCM (Hybrid-Hochvoltbatterie) fehlt | 0 |
| 0x01D804 | HCP:  Botschaft vom Steuergerät HIM  (Hybrid-Interface-Modul) über HL-CAN fehlt | 0 |
| 0x01D805 | HCP:  Botschaft vom Steuergerät EMPI (Hybrid-Ölpumpenansteuerung) fehlt | 0 |
| 0x01D806 | HCP:  Botschaft vom Steuergerät DSM  (Hybrid-Parksperre) fehlt | 0 |
| 0x01D807 | HCP:  Botschaft vom Steuergerät HIM  (Hybrid-Interface-Modul) über HS-CAN fehlt | 0 |
| 0x01D808 | HCP:  Botschaft vom Steuergerät APM (Hybrid-DC/DC-Wandler) fehlt | 0 |
| 0x01D80A | SBA: Kommunikation mit DSC fehlerhaft | 0 |
| 0x01D80B | SBA: Kommunikation mit HCP-Prozessor fehlerhaft | 0 |
| 0x01D80C | SBA: PT-Can Bus Off Fehler | 0 |
| 0x01D80D | SBA: HS-Can Bus Off Fehler | 0 |
| 0x01D80E | SBA: Kommunikation mit Steuergerät DME fehlerhaft | 0 |
| 0x01D815 | HCP:  Kommunikationsfehler mit MCPA oder MCPB (Hybrid-Elektromotorsteuerung 1 oder 2)  | 0 |
| 0x01D818 | HCP: HS-CAN Bus Kommunikationsfehler mit DME-Steuergerät   | 0 |
| 0x01D820 | HCP: HS-CAN Bus Kommunikationsfehler mit SBA-Steuergerät (Hybrid-Bremsbetätigungsumschaltung)    | 0 |
| 0x01D870 | MCPB: Botschaft vom Steuergerät DME über HS-CAN-Bus fehlt.  | 0 |
| 0x01D871 | MCPA: Botschaft vom Steuergerät DME über HS-CAN-Bus fehlt | 0 |
| 0x01D872 | MCPA: Botschaft vom Steuergerät MCPB (Hybrid-Elektromotorsteuerung 2) über PEB-interne Busverbindung fehlt | 0 |
| 0x01D875 | MCPB: Botschaft vom Steuergerät BPCM (Hybrid-Hochvoltbatterie) über CAN-Bus fehlt | 0 |
| 0x01D876 | MCPB: Botschaft vom Steuergerät DME über HL-CAN-Bus fehlt  | 0 |
| 0x01D878 | MCPA: Botschaft vom Steuergerät BPCM (Hybrid-Hochvoltbatterie) über CAN-Bus fehlt  | 0 |
| 0x01D879 | MCPA: Botschaft vom Steuergerät DME über HL-CAN-Bus fehlt  | 0 |
| 0x01D880 | MCPB: Botschaft vom Steuergerät HCP (Hybrid-Master-Steuergerät) über PEB-interne Busverbindung fehlt  | 0 |
| 0x01D881 | MCPA: Botschaft vom Steuergerät HCP (Hybrid-Master-Steuergerät) über PEB-interne Busverbindung fehlt  | 0 |
| 0x01D885 | BPCM: Kommunikationsverlust mit HCP | 0 |
| 0x01D886 | BPCM: Kommunikationsverlust mit HIM | 0 |
| 0x01D891 | EMPI: Botschaft vom Steuergerät HCP (Hybrid-Master-Steuergerät) auf HL-CAN fehlt    | 0 |
| 0x01D892 | EMPI: Botschaft vom Steuergerät TCM  (Hybrid-Getriebesteuerung) auf HL-CAN fehlt  | 0 |
| 0x01D89B | MCPB: Botschaft vom Steuergerät TCM (Hybrid-Getriebesteuerung) über CAN-Bus fehlt | 0 |
| 0x01D89C | MCPA: Botschaft vom Steuergerät TCM (Hybrid-Getriebesteuerung) über CAN-Bus fehlt   | 0 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 6 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | nein |
| SAE_CODE | nein |
| F_HLZ | nein |
| F_SEVERITY | nein |
| F_UWB_SATZ | 24 |
| F_HLZ_VIEW | - |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 1 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | nein |
| SAE_CODE | nein |
| F_HLZ | nein |
| F_SEVERITY | nein |

<a id="table-t-supplierlist-3-8"></a>
### T_SUPPLIERLIST_3_8

Dimensions: 140 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | * |
| 1 | Becker |
| 2 | Blaupunkt |
| 3 | Bosch |
| 4 | MB |
| 5 | HuF |
| 6 | Kammerer |
| 7 | Kostal |
| 8 | Siemens |
| 9 | Stribel |
| 10 | MicroHeat |
| 11 | JATCO |
| 16 | SWF |
| 17 | VDO |
| 18 | Webasto |
| 19 | Dornier |
| 20 | TEG |
| 21 | Hella |
| 22 | Lucas |
| 23 | GKR |
| 24 | MBB |
| 25 | Motometer |
| 32 | Borg |
| 33 | Temic |
| 34 | Teves |
| 35 | Borg Warner |
| 36 | MED S.P.A |
| 37 | DENSO |
| 38 | ZF |
| 39 | TRW |
| 40 | Dunlop |
| 41 | LUK |
| 48 | Magneti Marelli |
| 49 | DODUCO |
| 50 | Alpine |
| 51 | AMC (AEG Mobile Com.) |
| 52 | Bose |
| 53 | Dasa |
| 54 | Motorola |
| 55 | Nokia |
| 56 | Panasonic |
| 57 | APAG |
| 58 | Rialtosoft |
| 59 | Applicom |
| 60 | Conti Temic |
| 61 | Cherry |
| 62 | TI Automotive |
| 63 | Kongsberg Automotive |
| 64 | Delphi |
| 65 | Alfmeier |
| 66 | Sidler |
| 67 | Marquardt |
| 68 | Wehrle |
| 69 | megamos |
| 70 | ADC |
| 71 | BERU |
| 72 | Valeo |
| 73 | Magna |
| 74 | Allison |
| 75 | Isringhausen |
| 76 | Grammer |
| 77 | Funkwerk Dabendorf |
| 78 | Hella-Behr |
| 79 | Pollak |
| 80 | AKG |
| 81 | Automotive Lighting |
| 82 | TAG |
| 83 | UNITED PARTS |
| 84 | catem |
| 85 | Alge |
| 86 | Pierburg |
| 87 | Brusa |
| 88 | Ecostar |
| 89 | Xcellsis |
| 90 | Wabco Automotive |
| 91 | Voith |
| 92 | Knorr |
| 93 | TVI |
| 94 | Stoneridge |
| 95 | Telma |
| 96 | STW |
| 97 | Koyo |
| 98 | Eberspächer |
| 99 | ADVICS |
| 100 | OMRON |
| 101 | Mitsubishi Heavy Industry |
| 102 | Methode |
| 103 | UNISIAJECS |
| 104 | UNISIA JKC Steering Systems |
| 105 | AISIN |
| 106 | Zexel Valeo |
| 107 | Schrader |
| 108 | Ballard |
| 109 | Alcoa Fujikura |
| 110 | Transtron |
| 111 | Iteris |
| 112 | SFT |
| 113 | Kieckert AG |
| 114 | Behr |
| 115 | MB Lenkungen |
| 117 | Sachs Automotive |
| 118 | Petri |
| 119 | Autoliv |
| 120 | Thien Electronic |
| 121 | Siemens VDO |
| 122 | Dornier Consulting GmbH |
| 123 | Alps |
| 124 | PREH |
| 125 | Hitachi Unisia |
| 126 | Hitachi |
| 128 | Huntsville |
| 129 | Yazaki |
| 130 | Lear |
| 131 | Johnson Controls |
| 132 | Harman / Becker |
| 133 | Mitsubishi Electric |
| 134 | Tokico USA Inc. |
| 135 | Nippon Seiki (NS Intl) |
| 136 | Inalfa |
| 137 | Nippon Seiki (UK) |
| 138 | GHSP |
| 139 | Vector |
| 140 | Gentex |
| 141 | Visteon |
| 142 | Tochigi Fuji |
| 143 | DCA |
| 144 | May and Scofield |
| 145 | DaimlerChrysler Hamburg Plant |
| 146 | AISIN AW |
| 147 | TOYODA MACHINE WORKS |
| 148 | Solectron-Invotronics |
| 149 | Kicker |
| 150 | American Axle Company |
| 151 | GETRAG |
| 152 | Promate |
| 153 | ArvinMeritor |
| 160 | Reserviert für MMC |
| 161 | Reserviert für MCC-SMART |
| 254 | Nachrüstungs Lieferant |
| 255 | Unidentifiziert |

<a id="table-t-nein-ja-1bit"></a>
### T_NEIN_JA_1BIT

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nein |
| 1 | ja |

<a id="table-t-nicht-aktiv-aktiv-1byte"></a>
### T_NICHT_AKTIV_AKTIV_1BYTE

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht aktiv |
| 1 | aktiv |

<a id="table-t-jump-assist-state"></a>
### T_JUMP_ASSIST_STATE

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Funktion nicht verfügbar oder angefordert |
| 1 | Funktion angefordert |
| 2 | KL15 geschaltet/ Ladegerät auf 12V Seite angeschlossen Ladespannung &gt;13,2V |
| 3 | Ladung der HV Batterie läuft |
| 4 | Ladung abgeschlossen |
| 5 | Abgebrochen weil Netztteil zu klein/ Klemmenzustand geändert |

<a id="table-t-apm-lademodus-text"></a>
### T_APM_LADEMODUS_TEXT

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | KEIN_BOOSTMODE (Laden von 12V nach 300V aktiviert) |
| 1 | KEIN_BUCKMODE (Laden von 300V nach 12V aktiviert |
| 2 | KEIN_LADUNG (HV Batterie wird nicht geladen) |
| 3 | GEREGELT |
| 4 | Buckmode (Laden von 300V nach 12V) |
| 5 | Boostmode (Laden von 12V nach 300V) |

<a id="table-t-degradation-text"></a>
### T_DEGRADATION_TEXT

Dimensions: 11 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | novalue |
| 1 | no_degrad (keine Degardation) |
| 2 | Batt_hot  (HV-Batterie zu heiss) |
| 3 | Batt_cold (HV-Batterie zu kalt) |
| 4 | EM_hot    (E-Maschinen zu heiss) |
| 5 | CE_hot    (Combustion Engine-Verbrennungsmotor zu heiss) |
| 6 | SOC_low   (SOC: Ladezustand-HV-Speicher zu gering) |
| 7 | SOC_high  (SOC: Ladezustand-HV-Speicher zu hoch) |
| 8 | HV_low    (HV-Unterspannung) |
| 9 | HV_high   (HV-Überspannung) |
| 10 | SOH_high  (SOH-HV-Speicher überaltert) |

<a id="table-t-hcp-antriebsart-text"></a>
### T_HCP_ANTRIEBSART_TEXT

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | kein Wert |
| 2 | Energierückgewinnung durch Rekuperation |
| 3 | Lastpunktanhebung |
| 4 | Elektrisches Fahren |
| 5 | Elektrisches Boosten |
| 6 | Lastpunktabsenkung |
| 7 | Motorstopautomatik |
| 8 | Batteriestandladen |
| 9 | Regeneratives Bremsen |

<a id="table-t-hpmr-state-text"></a>
### T_HPMR_STATE_TEXT

Dimensions: 15 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | POWERUP |
| 1 | EVAL_BP_CLOSE (Evaluation Batteriepack Contactors Close) |
| 2 | DET_BP_CLOSED (Determine Batteriepack Contactors Closed) |
| 3 | EVAL_INV_ENABLE (Evaluation Inverter Enable) |
| 4 | DET_INV_ENABLED (Determine Inverter Enabled) |
| 5 | EVAL_ENG_SYS (Evaluation Engine System) |
| 6 | EVAL_REKEY_ALLOWED (Evaluatio Rekey Allowed) |
| 7 | OPERATIONAL |
| 8 | DET_ENG_STOPPED  (Determine Engine Stopped) |
| 9 | DET_INV_DISABLED (Determine Inverter Disabled) |
| 10 | EVAL_BP_OPEN (Evaluation Batteripack Open) |
| 11 | DET_BP_OPENED  (Determine Batteripack Opened) |
| 12 | DET_BUS_DISCHARGED (Determine Highvoltage Bus Discharged) |
| 13 | SHUTDOWN |
| 14 | JUMP_ASSIST |

<a id="table-t-hvil-gesamt"></a>
### T_HVIL_GESAMT

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | HVIL wird nicht bestromt oder initialer Zustand des BPCM (HV Zustand unklar) |
| 1 | HVIL ist geschlossen (HV kann aktiv sein) |
| 2 | HVIL ist offen (Service kann an HV Arbeiten wenn Service Disconnect entfernt und gegen Widereinschalten gesichert ist |

<a id="table-t-hvil-mcpa-b"></a>
### T_HVIL_MCPA_B

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | HVIL ist aus Sicht PEB geschlossen |
| 1 | HVIL ist aus Sicht PEB offen |

<a id="table-t-hvil-batterie"></a>
### T_HVIL_BATTERIE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | HVIL wird aus Sicht der Batterie nicht bestromt |
| 1 | HVIL ist aus Sicht der Batterie geschlossen (HV kann aktiv sein) |
| 2 | HVIL ist aus Sicht der Batterie offen (Service kann an HV Arbeiten wenn Service Disconnect entfernt und gegen widereinschalten gesichert ist |

<a id="table-t-status-isol-batterie"></a>
### T_STATUS_ISOL_BATTERIE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Initialer Zustand der Batterie Zustand unklar |
| 1 | Kein Isolationsfehler aus Sicht der Batterie |
| 2 | Isolationsfehler aus Sicht der Batterie |
| 255 | Undefinierter Wert |

<a id="table-t-laden-hv-batterie"></a>
### T_LADEN_HV_BATTERIE

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 5 | D |
| 6 | N |
| 7 | R |
| 8 | P |
| 15 | init |

<a id="table-t-status-isol-peb"></a>
### T_STATUS_ISOL_PEB

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Initialer Zustand der PEB, d.h. Zustand unklar |
| 1 | Kein Isolationsfehler aus Sicht der PEB  |
| 2 | Isolationsfehler aus Sicht der PEB |

<a id="table-t-steuern-antriebsart-text"></a>
### T_STEUERN_ANTRIEBSART_TEXT

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | geregelte Einstellung |
| 1 | Nur elektrisches Fahren |
| 2 | Nur mit Verbrennungsmotor fahren |

<a id="table-t-inaktiv-aktiv-1byte"></a>
### T_INAKTIV_AKTIV_1BYTE

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | inaktiv |
| 1 | aktiv |

<a id="table-t-empi-mode-text"></a>
### T_EMPI_MODE_TEXT

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Off mode |
| 1 | Speed control mode |
| 2 | Standby mode |
| 3 | Fault mode |
| 4 | Not Used |
| 5 | Not Used |
| 6 | Not Used |
| 7 | Signal Not Available |

<a id="table-t-voltage-hv-side-text"></a>
### T_VOLTAGE_HV_SIDE_TEXT

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Spannungsfreiheit nicht diagnostizierbar (Spannungsfreiheit ist vom Fachmann zu prüfen oder Diagnosefähigkeit ist herzustellen) |
| 1 | Spannungsfreiheit |

<a id="table-t-reset-source"></a>
### T_RESET_SOURCE

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Power Up |
| 2 | External Watchdog |
| 3 | Internal Watchdog |
| 4 | Unhandled Exception |
| 5 | Secondary forced a main running reset |
| 6 | Controller Specific Exceptions |

<a id="table-t-pass-fail-indeterminate"></a>
### T_PASS_FAIL_INDETERMINATE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Fehler |
| 1 | Unbestimmt |
| 3 | Durchgeführt |

<a id="table-t-textaktuellegetriebeposition"></a>
### T_TEXTAKTUELLEGETRIEBEPOSITION

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 5 | D |
| 6 | N |
| 7 | R |
| 8 | P |
| 15 | init |

<a id="table-t-textantriebsartzugriff"></a>
### T_TEXTANTRIEBSARTZUGRIFF

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | kein Wert |
| 1 | Sicher AUS/OFF |
| 2 | Vollzugriff |
| 3 | exclusiv E-Fahren bzw. Verbrennen |

<a id="table-t-textbattconn"></a>
### T_TEXTBATTCONN

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Schütz offen |
| 1 | Vorladung aktiv |
| 2 | geschlossen |
| 3 | Vorladung fehlgeschlagen |
| 4 | Vorladung verboten |
| 7 | Signal nicht vorhanden |
| 255 | Ungültig |

<a id="table-t-textcrashdetectionsignal"></a>
### T_TEXTCRASHDETECTIONSIGNAL

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | kein Crash detektiert (AUS) |
| 1 | Crash detektiert (EIN) |

<a id="table-t-textenergiesparmode"></a>
### T_TEXTENERGIESPARMODE

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | inaktiv |
| 1 | Fertigungsmode |
| 2 | Transportmode |
| 3 | FE+TRA |
| 4 | Werkstattmode |
| 5 | FE+WE |
| 6 | WE+TRA |
| 7 | FE+TRA+W |
| 255 | Ungültig |

<a id="table-t-textllregelung"></a>
### T_TEXTLLREGELUNG

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Diagnose noch nicht abgeschlossen |
| 1 | LL-Drehzahl zu hoch |
| 2 | LL-Drehzahl zu niedrig |
| 3 | Diagnose i.O. abgeschlossen |

<a id="table-t-textparksensoren"></a>
### T_TEXTPARKSENSOREN

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Zustand unbestimmt |
| 1 | Park eingelegt |
| 2 | Park ausgelegt |
| 3 | Ungültig |

<a id="table-t-textremedialactionhistroy"></a>
### T_TEXTREMEDIALACTIONHISTROY

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | Keine Bremsenergierückgewinnung |
| 2 | Getriebelistung reduziert |
| 4 | Antrieb kann nur kriechen |
| 8 | Getriebe-Gangwahl eingeschränkt |
| 16 | V-Motor aus und bleibt abgestellt |
| 32 | V-Motor läuft immer und wird nicht abgestellt |
| 64 | System Shutdown verzögert |
| 128 | System Shutdown mit HV-Schütze zu |
| 256 | System Shutdown mit HV-Schütze auf |
| 65535 | undefinierter Wert |

<a id="table-t-textdegradationsource2"></a>
### T_TEXTDEGRADATIONSOURCE2

Dimensions: 33 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | STAT_RESERVE_2_0_AKTIV |
| 2 | STAT_RESERVE_2_1_AKTIV |
| 4 | STAT_RESERVE_2_2_AKTIV |
| 8 | STAT_RESERVE_2_3_AKTIV |
| 16 | STAT_RESERVE_2_4_AKTIV |
| 32 | STAT_RESERVE_2_5_AKTIV |
| 64 | STAT_RESERVE_2_6_AKTIV |
| 128 | STAT_DEGR_MOMENT_GETR_TEMP_EMOT_A_AKTIV |
| 256 | STAT_DEGR_MOMENT_GETR_TEMP_EMOT_B_AKTIV |
| 512 | STAT_DEGR_MOMENT_GETR_TEMP_GETR_OEL_AKTIV |
| 1024 | STAT_DEGR_MOMENT_GETR_TEMP_VMOT_KUEHLM_AKTIV |
| 2048 | STAT_DEGR_MOMENT_GETR_TEMP_VMOT_OEL_AKTIV |
| 4096 | STAT_DEGR_MOMENT_GETR_TEMP_HV_SPEICHER_AKTIV |
| 8192 | STAT_DEGR_SOCR_TEMP_EMOT_A_AKTIV |
| 16384 | STAT_DEGR_SOCR_TEMP_EMOT_B_AKTIV |
| 32768 | STAT_DEGR_SOCR_TEMP_INVERTER_EMOT_A_AKTIV |
| 65536 | STAT_DEGR_SOCR_TEMP_INVERTER_EMOT_B_AKTIV |
| 131072 | STAT_DEGR_SOCR_TEMP_VMOT_KUEHLM_AKTIV |
| 262144 | STAT_DEGR_SOCR_TEMP_VMOT_OEL_AKTIV |
| 524288 | STAT_DEGR_SOCR_TEMP_GETR_OEL_AKTIV |
| 1048576 | STAT_RESERVE_2_20_AKTIV |
| 2097152 | STAT_DEGR_SOCR_TEMP_AMP_AKTIV |
| 4194304 | STAT_DEGR_REKU_TEMP_EMOT_A_AKTIV |
| 8388608 | STAT_DEGR_REKU_TEMP_EMOT_B_AKTIV |
| 16777216 | STAT_DEGR_REKU_TEMP_GETR_OEL_AKTIV |
| 33554432 | STAT_DEGR_REKU_TEMP_VMOT_KUEHLM_AKTIV |
| 67108864 | STAT_DEGR_REKU_TEMP_VMOT_OEL_AKTIV |
| 134217728 | STAT_DEGR_REKU_TEMP_HV_SPEICHER_AKTIV |
| 268435456 | STAT_DEGR_REKU_SOC_AKTIV |
| 536870912 | STAT_DEGR_REKU_TEMP_INVERTER_EMOT_A_AKTIV |
| 1073741824 | STAT_DEGR_REKU_TEMP_INVERTER_EMOT_B_AKTIV |
| 2147483648 | STAT_DEGR_REKU_TEMP_APM_AKTIV |
| 4294967295 | ungültiger Wert |

<a id="table-t-textdegradationsource1"></a>
### T_TEXTDEGRADATIONSOURCE1

Dimensions: 33 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | STAT_DEGR_MOMENT_EMOT_A_TEMP_EMOT_A_AKTIV |
| 2 | STAT_DEGR_MOMENT_EMOT_A_TEMP_INVERTER_EMOT_A_AKTIV |
| 4 | STAT_DEGR_MOMENT_EMOT_A_TEMP_GETR_OEL_AKTIV |
| 8 | STAT_RESERVE_1_3_AKTIV |
| 16 | STAT_DEGR_MOMENT_EMOT_A_TEMP_APM_AKTIV |
| 32 | STAT_DEGR_MOMENT_EMOT_B_TEMP_EMOT_B_AKTIV |
| 64 | STAT_DEGR_MOMENT_EMOT_B_TEMP_INVERTER_EMOT_B_AKTIV |
| 128 | STAT_RESERVE_1_7_AKTIV |
| 256 | STAT_DEGR_MOMENT_EMOT_B_TEMP_APM_AKTIV |
| 512 | STAT_DEGR_MOMENT_EMOT_B_TEMP_GETR_OEL_AKTIV |
| 1024 | STAT_DEGR_BAT_ENTLADELEISTUNG_FAHRMODUS_AKTIV |
| 2048 | STAT_DEGR_BAT_ENTLADELEISTUNG_TEMP_HV_SPEICHER_AKTIV |
| 4096 | STAT_DEGR_BAT_ENTLADELEISTUNG_SOC_AKTIV |
| 8192 | STAT_DEGR_BAT_ENTLADELEISTUNG_FAHRMODUS_AKTIV |
| 16384 | STAT_DEGR_BAT_ENTLADELEISTUNG_TEMP_HV_SPEICHER_E_DRIVE_AKTIV |
| 32768 | STAT_DEGR_BAT_ENTLADELEISTUNG_SOC_E_DRIVE_AKTIV |
| 65536 | STAT_DEGR_BAT_LADELEISTUNG_TEMP_HV_SPEICHER_AKTIV |
| 131072 | STAT_DEGR_BAT_LADELEISTUNG_SOC_AKTIV |
| 262144 | STAT_DEGR_MOMENT_VMOT_TEMP_EMOT_A_AKTIV |
| 524288 | STAT_DEGR_MOMENT_VMOT_TEMP_EMOT_B_AKTIV |
| 1048576 | STAT_RESERVE_1_20_AKTIV |
| 2097152 | STAT_DEGR_MOMENT_VMOT_TEMP_INVERTER_EMOT_A_AKTIV |
| 4194304 | STAT_DEGR_MOMENT_VMOT_TEMP_INVERTER_EMOT_B_AKTIV |
| 8388608 | STAT_DEGR_MOMENT_VMOT_TEMP_WMK_AKTIV |
| 16777216 | STAT_DEGR_EKK_TEMP_WMK_AKTIV |
| 33554432 | STAT_DEGR_EKK_TEMP_EMOT_A_AKTIV |
| 67108864 | STAT_DEGR_EKK_TEMP_EMOT_B_AKTIV |
| 134217728 | STAT_DEGR_EKK_TEMP_GETR_OEL_AKTIV |
| 268435456 | STAT_DEGR_EKK_TEMP_VMOT_KUEHLM_AKTIV |
| 536870912 | STAT_DEGR_EKK_TEMP_VMOT_OEL_AKTIV |
| 1073741824 | STAT_RESERVE_1_30_AKTIV |
| 2147483648 | STAT_DEGR_EKK_TEMP_HV_SPEICHER_AKTIV |
| 4294967295 | ungültiger Wert |

<a id="table-t-degradation-akt-text"></a>
### T_DEGRADATION_AKT_TEXT

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Degradation nicht aktiv |
| 1 | Degradation aktiv |

<a id="table-t-textsocstimul"></a>
### T_TEXTSOCSTIMUL

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Stimmulierung AUS |
| 1 | Stimmulierung EIN |

<a id="table-t-not-aktiv-aktiv"></a>
### T_NOT_AKTIV_AKTIV

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht aktiv |
| 1 | aktiv |

<a id="table-t-true-false"></a>
### T_TRUE_FALSE

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | False |
| 1 | True |

<a id="table-t-textadaptionswertelesenpyro"></a>
### T_TEXTADAPTIONSWERTELESENPYRO

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Kein HV Shutdown |
| 1 | HV Shutdown |

<a id="table-t-textlaststarttype"></a>
### T_TEXTLASTSTARTTYPE

Dimensions: 11 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Kein Wert |
| 1 | Schlüsselstart normal |
| 2 | Schlüsselstart geringe Batterieleistung |
| 3 | Schlüsselstart geringe Batterieleistung (Applikation B) |
| 4 | Jungfernstart (Werk) |
| 5 | Schlüsselstart Typ Vorhalt |
| 6 | Autostart sanft |
| 7 | Autostart normal |
| 8 | Autostart aggressiv |
| 9 | Autostart vorhalt |
| 10 | Motorstart Kompressionstest |

<a id="table-t-textlaststoptype"></a>
### T_TEXTLASTSTOPTYPE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Kein Wert |
| 11 | Geregelter Stop |
| 12 | Schlüssel- oder Notstop |

<a id="table-t-textsteuernkurzschluvwemp"></a>
### T_TEXTSTEUERNKURZSCHLUVWEMP

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | inaktiv |
| 1 | aktiv |
| 2 | beendet |

<a id="table-t-textdegradationbit"></a>
### T_TEXTDEGRADATIONBIT

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Degradation nicht aktiv |
| 1 | Degradation aktiv |

<a id="table-t-luefterstufen-1-15"></a>
### T_LUEFTERSTUFEN_1_15

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Stufe 0 |
| 1 | Stufe 1 |
| 2 | Stufe 2 |
| 3 | Stufe 3 |
| 4 | Stufe 4 |
| 5 | Stufe 5 |
| 6 | Stufe 6 |
| 7 | Stufe 7 |
| 8 | Stufe 8 |
| 9 | Stufe 9 |
| 10 | Stufe 10 |
| 11 | Stufe 11 |
| 12 | Stufe 12 |
| 13 | Stufe 13 |
| 14 | Stufe 14 |
| 15 | ungültig |

<a id="table-t-ein-ausschaltanforderung"></a>
### T_EIN_AUSSCHALTANFORDERUNG

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | keine Anforderung |
| 1 | Einschaltaufforderung |
| 2 | Ausschaltaufforderung |
| 3 | ungültig |

<a id="table-t-fehlervorhanden-keinfehlervorhanden"></a>
### T_FEHLERVORHANDEN_KEINFEHLERVORHANDEN

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | kein Fehler vorhanden |
| 1 | Fehler vorhanden |

<a id="table-t-ok-nichtok"></a>
### T_OK_NICHTOK

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | OK |
| 1 | nicht OK |

<a id="table-t-geschlossen-offen"></a>
### T_GESCHLOSSEN_OFFEN

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | geschlossen |
| 1 | offen |

<a id="table-t-freigabe"></a>
### T_FREIGABE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | keine Freigabe |
| 1 | Freigabe |
| 2 | Systemfehler erkannt |
| 3 | ungültig |

<a id="table-t-gueltig-ungueltig"></a>
### T_GUELTIG_UNGUELTIG

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | ungültig |
| 1 | gültig |

<a id="table-t-textsteuernbattkuehl"></a>
### T_TEXTSTEUERNBATTKUEHL

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Keine Vorgabe Kühlungsmodus |
| 1 | Vorgabe Kühlung im Chillermodus |
| 2 | Vorgabe Kühlung im HeatExchangermodus |
| 3 | Vorgabe Kühlung im Duplexmodus |
| 4 | Vorgabe Befüllung Chillerkreis |
| 5 | Vorgabe Befüllung HeatExchangerkreis |
| 6 | Vorgabe Befüllung beide Kreise |
| 7 | Vorgabe Kühlung aus |

<a id="table-t-aus-active-beendet"></a>
### T_AUS_ACTIVE_BEENDET

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | AUS |
| 1 | AKTIV |
| 2 | beendet |

<a id="table-t-textbattladeleistbe"></a>
### T_TEXTBATTLADELEISTBE

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Leistung wird von minimaler Grenze begrenzt |
| 1 | Leistung wird von BPCM begrenzt |
| 2 | Leistung wird von Remedial Action begrenzt |
| 3 | Leistung wird von maximaler Grenze begrenzt |
| 4 | Leistung wird von mismatch begrenzt |
| 5 | Leistung wird vom Applikationswert vorgegeben |

<a id="table-t-textbattentlleistst"></a>
### T_TEXTBATTENTLLEISTST

Dimensions: 12 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Leistung wird von maximaler Grenze begrenzt |
| 1 | Leistung wird von BPCM begrenzt |
| 2 | Leistung wird von Remedial Action begrenzt |
| 3 | Leistung wird von SOC begrenzt |
| 4 | Leistung wird von Batt. Nutzung begrenzt |
| 5 | Leistung wird von minimaler Grenze begrenzt |
| 6 | Leistung wird von Unterspannung begrenzt |
| 7 | Leistung wird von mismatch begrenzt |
| 8 | Leistung wird von Battery Estimated Leistung begrenzt |
| 9 | Leistung wird vom Applikationswert vorgegeben |
| 10 | Leistung wird von Rev Grade begrenzt |
| 11 | Leistung wird von Power Launch begrenzt |

<a id="table-t-textbattladeleistlt"></a>
### T_TEXTBATTLADELEISTLT

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Leistung wird von minimaler Grenze begrenzt |
| 1 | Leistung wird von BPCM begrenzt |
| 2 | Leistung wird von Remedial Action begrenzt |
| 3 | Leistung wird von SOC begrenzt |
| 4 | Leistung wird von Batt. Nutzung begrenzt |
| 5 | Leistung wird von maximaler Grenze begrenzt |
| 6 | Leistung wird von Überspannung begrenzt |
| 7 | Leistung wird von mismatch begrenzt |
| 8 | Leistung wird von Short Term Leistung begrenzt |
| 9 | Leistung wird vom Applikationswert vorgegeben |

<a id="table-t-textbattladeleistbp"></a>
### T_TEXTBATTLADELEISTBP

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Leistung wird von minimaler Grenze begrenzt |
| 1 | Leistung wird von BPCM begrenzt |
| 2 | Leistung wird von Remedial Action begrenzt |
| 3 | Leistung wird von SOC begrenzt |
| 4 | Leistung wird von Batt. Nutzung begrenzt |
| 5 | Leistung wird von maximaler Grenze begrenzt |
| 6 | Leistung wird von mismatch begrenzt |
| 7 | Leistung wird von Long Term Leistung begrenzt |
| 8 | Leistung wird vom Applikationswert vorgegeben |

<a id="table-t-textbattentlleistbp"></a>
### T_TEXTBATTENTLLEISTBP

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Leistung wird von maximaler Grenze begrenzt |
| 1 | Leistung wird von BPCM begrenzt |
| 2 | Leistung wird von Remedial Action begrenzt |
| 3 | Leistung wird von SOC begrenzt |
| 4 | Leistung wird von Batt. Nutzung begrenzt |
| 5 | Leistung wird von minimaler Grenze begrenzt |
| 6 | Leistung wird von mismatch begrenzt |
| 7 | Leistung wird von Long Term Leistung begrenzt |
| 8 | Leistung wird vom Applikationswert vorgegeben |

<a id="table-t-textbattladeleistst"></a>
### T_TEXTBATTLADELEISTST

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Leistung wird von minimaler Grenze begrenzt |
| 1 | Leistung wird von BPCM begrenzt |
| 2 | Leistung wird von Remedial Action begrenzt |
| 3 | Leistung wird von SOC begrenzt |
| 4 | Leistung wird von Batt. Nutzung begrenzt |
| 5 | Leistung wird von maximaler Grenze begrenzt |
| 6 | Leistung wird von Überspannung begrenzt |
| 7 | Leistung wird von mismatch begrenzt |
| 8 | Leistung wird von Battery Estimated Leistung begrenzt |
| 9 | Leistung wird vom Applikationswert vorgegeben |

<a id="table-t-textbattentlleistbe"></a>
### T_TEXTBATTENTLLEISTBE

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Leistung wird von maximaler Grenze begrenzt |
| 1 | Leistung wird von BPCM begrenzt |
| 2 | Leistung wird von Remedial Action begrenzt |
| 3 | Leistung wird von minimaler Grenze begrenzt |
| 4 | Leistung wird von mismatch begrenzt |
| 5 | Leistung wird vom Applikationswert vorgegeben |
| 6 | Leistung wird vom Powerlaunch vorgegeben |

<a id="table-t-textbattentlleistlt"></a>
### T_TEXTBATTENTLLEISTLT

Dimensions: 12 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Leistung wird von maximaler Grenze begrenzt |
| 1 | Leistung wird von BPCM begrenzt |
| 2 | Leistung wird von Remedial Action begrenzt |
| 3 | Leistung wird von SOC begrenzt |
| 4 | Leistung wird von Batt. Nutzung begrenzt |
| 5 | Leistung wird von minimaler Grenze begrenzt |
| 6 | Leistung wird von Unterspannung begrenzt |
| 7 | Leistung wird von mismatch begrenzt |
| 8 | Leistung wird von Short Term Leistung begrenzt |
| 9 | Leistung wird vom Applikationswert vorgegeben |
| 10 | Leistung wird von Rev Grade begrenzt |
| 11 | Leistung wird von Power Launch begrenzt |

<a id="table-t-textflashprecondition"></a>
### T_TEXTFLASHPRECONDITION

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Keine Sperrung |
| 1 | Sperre aktiv |

<a id="table-fortumweltnr"></a>
### FORTUMWELTNR

Dimensions: 447 rows × 36 columns

| ORT | F_UW1_NR | F_UW2_NR | F_UW3_NR | F_UW4_NR | F_UW5_NR | F_UW6_NR | F_UW7_NR | F_UW8_NR | F_UW9_NR | F_UW10_NR | F_UW11_NR | F_UW12_NR | F_UW13_NR | F_UW14_NR | F_UW15_NR | F_UW16_NR | F_UW17_NR | F_UW18_NR | F_UW19_NR | F_UW20_NR | F_UW21_NR | F_UW22_NR | F_UW23_NR | F_UW24_NR | F_UW25_NR | F_UW26_NR | F_UW27_NR | F_UW28_NR | F_UW29_NR | F_UW30_NR | F_UW31_NR | F_UW32_NR | F_UW33_NR | F_UW34_NR | F_UW35_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x010219 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010506 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010507 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010562 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010563 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01061A | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01061B | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x0107A3 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x0107A5 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x0107A7 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x0107A9 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A02 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A03 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A0C | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A0D | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A1B | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A1C | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A1F | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A2A | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A2B | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A2C | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A2F | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A30 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A31 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A32 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A35 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A3F | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A40 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A44 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A45 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A46 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A4A | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A7D | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A7E | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A80 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A93 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A95 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A9C | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A9D | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010A9E | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010AA6 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010ABB | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010ABC | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010ABD | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010AC0 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010AC1 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010AC2 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010AC6 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010AC7 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010AC8 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010ACB | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010ACC | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010ACD | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010ADC | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010AE0 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010AE7 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010AE9 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010AEA | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010AEB | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010AEE | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010AEF | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010AF0 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010AF3 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010AF4 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010AF5 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010AFA | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010AFB | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B0D | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B15 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B16 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B17 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B3C | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B3D | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B3E | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B41 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B42 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B43 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B46 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B47 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B48 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B4B | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B4C | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B4D | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B50 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B51 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B52 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B55 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B56 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B57 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B5A | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B5B | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B5C | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B5F | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B60 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B61 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B64 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B65 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B66 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B69 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B6A | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B6B | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B6E | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B6F | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B70 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B73 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B74 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B75 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B78 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B79 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B7A | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B7D | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B7E | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B7F | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B82 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B83 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B84 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B87 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B88 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B89 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B8C | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B8D | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B8E | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B91 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B92 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B93 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B96 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B97 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B98 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B9B | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B9C | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010B9D | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BA0 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BA1 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BA2 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BA5 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BA6 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BA7 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BAA | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BAB | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BAC | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BAF | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BB0 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BB1 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BB4 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BB5 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BB6 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BB9 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BBA | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BBB | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BBD | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BD2 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BD3 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BD4 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BD7 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BD8 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BD9 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BDC | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BDD | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BDE | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BE1 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BE2 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BE3 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BE6 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BE7 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BE8 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BEA | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BEB | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BEC | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BEE | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BEF | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BF0 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BF2 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BF3 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BF4 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BF6 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BF7 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BF8 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BFA | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BFB | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BFC | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BFD | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BFE | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010BFF | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C01 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C02 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C04 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C05 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C08 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C0B | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C0E | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C11 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C12 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C13 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C14 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C15 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C16 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C17 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C18 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C1E | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C1F | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C26 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C2F | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C30 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C31 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C43 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C44 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C45 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C4C | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C4D | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C4E | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C4F | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C52 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C53 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C57 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C58 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C5C | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C5D | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C61 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C62 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C76 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C77 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x010C78 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01139F | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x0115A9 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011828 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011829 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A00 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A01 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A02 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A03 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A04 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A05 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A06 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A07 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A08 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A09 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A0A | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A0C | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A0D | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A0E | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A0F | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A10 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A11 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A12 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A13 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A20 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A21 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A25 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A26 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A2A | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A2B | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A2C | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A2D | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A30 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A31 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A32 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A33 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A34 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A35 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A36 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A37 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A38 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A40 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A41 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A42 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A43 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A44 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A45 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A46 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A47 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A48 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A4F | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A50 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A51 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A52 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A53 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A54 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A55 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A5A | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A69 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A6A | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A6B | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A6C | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A6D | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A6E | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A6F | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A70 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A71 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A74 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011A75 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011ABE | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AC6 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AC7 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011ADC | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011ADD | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011ADE | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011ADF | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AE0 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AE1 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AE5 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AE7 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AE8 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AE9 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AEA | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AEB | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AEC | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AED | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AEE | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AEF | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AF0 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AF1 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AF2 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AF3 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AF4 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AF5 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AF6 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AF7 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AF8 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AF9 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AFA | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AFB | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AFE | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011AFF | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B01 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B03 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B04 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B05 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B06 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B07 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B08 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B09 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B0A | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B0F | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B10 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B11 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B12 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B18 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B20 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B21 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B22 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B27 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B28 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B29 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B2A | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B2B | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B2D | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B2F | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B30 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B31 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B32 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B33 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B34 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B35 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B36 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B37 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B38 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B39 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B3F | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B40 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B41 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B42 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B43 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B44 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B45 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B46 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B47 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B48 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B4A | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B4B | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B4C | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B51 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B5F | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B71 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B72 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B73 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011B74 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011C43 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011C44 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x011C45 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01215C | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x012533 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x012797 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015001 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015002 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015003 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015010 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015011 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015012 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015013 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015016 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015020 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015021 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015030 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015031 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015032 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01503F | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015040 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015050 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015051 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015052 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015062 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015063 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015067 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015068 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015069 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015070 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015071 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015072 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015073 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015080 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015081 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x015082 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01C073 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01C074 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D800 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D801 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D802 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D803 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D804 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D805 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D806 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D807 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D808 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D80A | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D80B | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D80C | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D80D | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D80E | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D815 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D818 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D820 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D870 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D871 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D872 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D875 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D876 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D878 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D879 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D880 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D881 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D885 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D886 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D891 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D892 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D89B | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0x01D89C | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 0xFFFFFF | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 |

<a id="table-fortumwelttexte"></a>
### FORTUMWELTTEXTE

Dimensions: 35 rows × 7 columns

| UWNR | UW_EINH | MUL | DIV | ADD | UWTEXT | UW_LENGTH |
| --- | --- | --- | --- | --- | --- | --- |
| 01 | - | 1 | 1 | 0 | Diagnose Fehler Code | 2 |
| 02 | km | 16 | 1 | 0 | Kilometerstand beim ersten Fehlerauftritt | 2 |
| 03 | km | 16 | 1 | 0 | Kilometerstand beim letzten Fehlerauftritt | 2 |
| 04 | - | 1 | 1 | 0 | Anzahl Fehler aufgetreten | 1 |
| 05 | - | 1 | 1 | 0 | Anzahl Fehler nicht aufgetreten | 1 |
| 06 | - | 1 | 1 | 0 | Anzahl Fehler nicht abgelaufen | 1 |
| 07 | % | 100 | 256 | 0 | Berechneter Lastwert - OBD | 1 |
| 08 | °C | 1 | 1 | -40 | Kuehlmitteltemperatur | 1 |
| 09 | U/min | 1 | 4 | 0 | Motordrehzahl | 2 |
| 10 | km/h | 1 | 1 | 0 | Fahrzeuggeschwindigkeit | 1 |
| 11 | °C | 1 | 1 | -40 | Ansauglufttemperatur | 1 |
| 12 | % | 100 | 256 | 0 | Absolute Drosselklappenposition | 1 |
| 13 | ? | 1 | 1 | 0 | Kraftuebertragungs Status | 1 |
| 14 | - | 1 | 1 | 0 | Anzahl der Aufwaermzyklen seit letzten Fehlerspeicher loeschen | 1 |
| 15 | km | 1 | 1 | 0 | km seit letzten Fehlerspeicher loeschen | 2 |
| 16 | kPa | 1 | 1 | 0 | Lufdruck in kPa | 1 |
| 17 | V | 1 | 1000 | 0 | Spannung Steuergeraet | 2 |
| 18 | °C | 1 | 1 | -40 | Umgebungstemperatur | 1 |
| 19 | % | 100 | 256 | 0 | Relative Gaspedalposition | 1 |
| 20 | s | 1 | 1 | 0 | Motorlaufzeit in s | 2 |
| 21 | U/min | 1 | 8 | 0 | Getriebeausgangsdrehzahl | 2 |
| 22 | - | 1 | 64 | 0 | Berechnetes Getriebeuebersetzungsverhaeltnis | 1 |
| 23 | Nm | 1 | 4 | 0 | Aktuell eingestelltes Motormoment | 2 |
| 24 | % | 100 | 256 | 0 | Aktuelle Gaspedalpostion | 1 |
| 25 | - | 1 | 1 | 0 | Status der TISS/TOSS Spannungsversorgung | 1 |
| 26 | % | 1 | 2 | 0 | SOC | 1 |
| 27 | % | 1 | 2 | 0 | SOC Genauigkeit | 1 |
| 28 | kW | 1 | 1 | -127 | ST Ladeleistungsgrenzen | 1 |
| 29 | kW | 1 | 1 | -127 | LT Ladeleistungsgrenzen | 1 |
| 30 | kW | 1 | 1 | -127 | ST Entladeleistungsgrenzen | 1 |
| 31 | kW | 1 | 1 | -127 | LT Entladeleistungsgrenzen | 1 |
| 32 | V | 2 | 1 | 0 | HV Spannung | 1 |
| 33 | kW | 1 | 10 | -3277 | Momentane HV Leistung | 2 |
| 34 | Nm | 1 | 1 | -32767 | Getriebeausgangsmoment | 2 |
| 35 | % | 1 | 2 | 0 | Aktuelle Gaspedalposition | 1 |

<a id="table-t-textistrange"></a>
### T_TEXTISTRANGE

Dimensions: 38 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Init |
| 1 | Neutral |
| 2 | Mode 1 |
| 3 | Mode 2 |
| 4 | Gang 1 |
| 5 | Gang 2 |
| 6 | Gang 3 |
| 7 | Gang 4 |
| 8 | G1 zu G2 (Drehzahl) |
| 9 | G1 zu G2 (Drehmoment) |
| 10 | G2 zu G1 (Drehzahl) |
| 11 | G2 zu G1 (Drehmoment) |
| 12 | G2 zu G3 (Drehzahl) |
| 13 | G2 zu G3 (Drehmoment) |
| 14 | G3 zu G2 (Drehzahl) |
| 15 | G3 zu G2 (Drehmoment) |
| 16 | G3 zu G4 (Drehzahl) |
| 17 | G3 zu G4 (Drehmoment) |
| 18 | G4 zu G3 (Drehzahl) |
| 19 | G4 zu G3 (Drehmoment) |
| 20 | M1 zu G1 |
| 21 | M1 zu G2 |
| 22 | M2 zu G2 |
| 23 | M2 zu G3 |
| 24 | M2 zu G4 |
| 25 | N zu M1 |
| 26 | N zu M2 |
| 27 | Neutralschaltung |
| 28 | M1 zu M2 wenig Drehmoment |
| 29 | M2 zu M1 wenig Drehmoment |
| 30 | M1 Abbruch |
| 31 | M2 Abbruch |
| 32 | G1 Abbruch |
| 33 | G2 Abbruch |
| 34 | G3 Abbruch |
| 35 | G2 Abbruch |
| 36 | G3 Abbruch |
| 37 | G4 Abbruch |

<a id="table-t-textremedialactioninput2"></a>
### T_TEXTREMEDIALACTIONINPUT2

Dimensions: 32 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | VeESMR_b_HV_BatMaxModTmpSFA |
| 2 | VeESMR_b_HV_BatPackSOC_SFA |
| 4 | VeESMR_b_HV_BatCurrSFA |
| 8 | VeESMR_b_HV_BatVoltModMaxSFA |
| 16 | VeINVR_b_MtrA_TempFA |
| 32 | VeMSPR_b_MtrB_SpdFA |
| 64 | VeMTQR_b_MtrA_TorqAchievedFA |
| 128 | VeETQR_b_EngActualTorqSS_Flt |
| 256 | VeEPCR_b_TransInAng720EstErr |
| 512 | VeCCMR_b_Clch1To4CmdFlt |
| 1024 | VeSRAR_b_Inhibit_Mode1 |
| 2048 | VeSRAR_b_Inhibit_Mode2 |
| 4096 | VeSRAR_b_Inhibit_Gear1 |
| 8192 | VeSRAR_b_Inhibit_Gear2 |
| 16384 | VeSRAR_b_Inhibit_Gear3 |
| 32768 | VeSRAR_b_Inhibit_Gear4 |
| 65536 | VeECMR_b_AxleTorqReqImmedFA |
| 131072 | VeAXLR_b_CmndPrdtAxleTorqFA |
| 262144 | VeTOSR_e_OutputSpdDfltSource |
| 524288 | VeTOSR_e_TOS_Direction |
| 1048576 | VeSRAR_b_EngOnReqBrk |
| 2097152 | VeTFTR_b_TransOilFA |
| 4194304 | VeSRAR_b_EngSysLowFuel |
| 8388608 | VeEPSR_e_EngSpdStat |
| 16777216 | VeTITR_b_EngTrqHVBattLoFA |
| 33554432 | VeTITR_b_EngTrqHVBattHiFA |
| 67108864 | VeBPCR_b_BPCMOverCurrentDTC |
| 134217728 | VeSRAR_b_ECM_LAN_CommFltSum |
| 268435456 | VeSRAR_b_ECM_DPT_CommFltSum |
| 536870912 | VeSRAR_b_HIM_CommFltSum |
| 1073741824 | VeSRAR_b_EMPI_CommFltSum |
| 2147483648 | VeSRAR_b_EngineRAModeFlt |

<a id="table-t-textremedialaction"></a>
### T_TEXTREMEDIALACTION

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Kein Fehler |
| 1 | Keine Bremsenergierückgewinnung |
| 2 | Getriebelistung reduziert |
| 4 | Antrieb kann nur kriechen |
| 8 | Getriebe-Gangwahl eingeschränkt |
| 16 | V-Motor aus und bleibt abgestellt |
| 32 | V-Motor läuft immer und wird nicht abgestellt |
| 64 | System Shutdown verzögert |
| 128 | System Shutdown mit HV-Schütze zu |
| 256 | System Shutdown mit HV-Schütze auf |

<a id="table-t-textremedialactioninput1"></a>
### T_TEXTREMEDIALACTIONINPUT1

Dimensions: 32 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | VeSSRR_b_EngOvrSpdFltDtct |
| 2 | VeHVTR_b_HVOverVoltFltDtct |
| 4 | VeHVTR_b_HVUnderVoltFltDtct |
| 8 | VeESMR_b_SOCHighFltDtct |
| 16 | VeESMR_b_SOCLowFltDtct |
| 32 | VeESMR_b_BattOverTempFltDtct |
| 64 | VeSSRR_b_EngNegSpdFltDtct |
| 128 | VeSPCR_b_SerialCommFlt |
| 256 | VePMDR_b_SysVoltHighFA |
| 512 | VePMDR_b_SysVoltLowFA |
| 1024 | VeMEMR_b_MainProcessorFlt |
| 2048 | VeSTMR_b_TransOutTrqCmdFlt |
| 4096 | VeTRMR_b_PRNDL_MontrFlt |
| 8192 | VeSSRR_b_SpdRatlFlt_FltDtct |
| 16384 | VeMPMR_b_CPU_MntrFailed |
| 32768 | VeSTMR_b_RgnEstMntrFlt |
| 65536 | VeSRAR_b_RBS_CommFltSum |
| 131072 | VeSRAR_b_TCM_CommFltSum |
| 262144 | VeSRAR_b_BPCM_CommFltSum |
| 524288 | VeSRAR_b_EngSysDsbld |
| 1048576 | VeSRAR_b_ShutDown |
| 2097152 | VeSRAR_b_TransCritFltRdcSpd |
| 4194304 | VeINVR_b_MtrA_DC_CrntFA |
| 8388608 | VeINVR_b_MtrA_DC_VoltFA |
| 16777216 | VeINVR_b_MtrA_InvrtrTempFA |
| 33554432 | VeMSPR_b_MtrA_SpdFA |
| 67108864 | VeINVR_b_MtrB_DC_CrntFA |
| 134217728 | VeINVR_b_MtrB_DC_VoltFA |
| 268435456 | VeINVR_b_MtrB_InvrtrTempFA |
| 536870912 | VeINVR_b_MtrB_TempFA |
| 1073741824 | VeMTQR_b_MtrB_TorqAchievedFA |
| 2147483648 | VeSTMR_b_RngStValidationFlt |

<a id="table-t-textrueckschreibenio"></a>
### T_TEXTRUECKSCHREIBENIO

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Rueckschreiben nicht erlaubt |
| 1 | Rueckschreiben erlaubt |

<a id="table-t-nichtok-ok"></a>
### T_NICHTOK_OK

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht OK |
| 1 | OK |

<a id="table-t-textmotorleistungsmessung"></a>
### T_TEXTMOTORLEISTUNGSMESSUNG

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | aus |
| 1 | an |
| 2 | gesperrt |
| 3 | Testzeitraum abgelaufen |
| 4 | kein Wert |

<a id="table-t-ein-aus"></a>
### T_EIN_AUS

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | AUS |
| 1 | EIN |

<a id="table-t-textstatuskupplung"></a>
### T_TEXTSTATUSKUPPLUNG

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Ungueltig |
| 1 | Offen |
| 2 | Betaetigt |
| 3 | Fast Synchronisiert |
| 4 | Synchronisiert |
| 5 | Gesperrt |

<a id="table-t-text-gefordertnichtgefordert"></a>
### T_TEXT_GEFORDERTNICHTGEFORDERT

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Nicht gefordert |
| 1 | Gefordert |

<a id="table-t-textrangestate"></a>
### T_TEXTRANGESTATE

Dimensions: 38 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Init |
| 1 | Neutral |
| 2 | Mode 1 |
| 3 | Mode 2 |
| 4 | Gear 1 |
| 5 | Gear 2 |
| 6 | Gear 3 |
| 7 | Gear 4 |
| 8 | G1 zu G2 (Drehzahl) |
| 9 | G1 zu G2 (Drehmoment) |
| 10 | G2 zu G1 (Drehzahl) |
| 11 | G2 zu G1 (Drehmoment) |
| 12 | G2 zu G3 (Drehzahl) |
| 13 | G2 zu G3 (Drehmoment) |
| 14 | G3 zu G2 (Drehzahl) |
| 15 | G3 zu G2 (Drehmoment) |
| 16 | G3 zu G4 (Drehzahl) |
| 17 | G3 zu G4 (Drehmoment) |
| 18 | G4 zu G3 (Drehzahl) |
| 19 | G4 zu G3 (Drehmoment) |
| 20 | M1 zu G1 |
| 21 | M1 zu G2 |
| 22 | M2 zu G2 |
| 23 | M2 zu G3 |
| 24 | M2 zu G4 |
| 25 | N zu M1 |
| 26 | N zu M2 |
| 27 | Neutralschaltung |
| 28 | M1 zu M2 wenig Drehmoment |
| 29 | M2 zu M1 wenig Drehmoment |
| 30 | M1 Abbruch |
| 31 | M2 Abbruch |
| 32 | G1 Abbruch |
| 33 | G2 Abbruch |
| 34 | G3 Abbruch |
| 35 | G2 Abbruch |
| 36 | G3 Abbruch |
| 37 | G4 Abbruch |

<a id="table-t-textusecases"></a>
### T_TEXTUSECASES

Dimensions: 22 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht definiert |
| 1 | Battery zu heiss |
| 2 | Battery Equilibrierung |
| 3 | Standladen |
| 4 | Kat-heiz-modus |
| 5 | Batterieheizen laden |
| 6 | Batterieheizen entladen |
| 7 | Produktionsmodus |
| 8 | Sportmodus |
| 9 | Rückwärts |
| 10 | Neutral |
| 11 | Park |
| 12 | Drive |
| 13 | Produktionsmodus ohne Ladeunterdrückung |
| 14 | Warmlauf |
| 15 | Batterie Stimulus Laden |
| 16 | Batterie Stimulus Entladen |
| 17 | SOC Overwrite Tester |
| 18 | Limiterbetrieb |
| 19 | Efficient Drive |
| 20 | SOC SFA |
| 21 | Default |

<a id="table-t-textgetrieberange"></a>
### T_TEXTGETRIEBERANGE

Dimensions: 15 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | POWERUP |
| 1 | EVAL_BP_CLOSE (Evaluation Batteriepack Contactors Close) |
| 2 | DET_BP_CLOSED (Determine Batteriepack Contactors Closed) |
| 3 | EVAL_INV_ENABLE (Evaluation Inverter Enable) |
| 4 | DET_INV_ENABLED (Determine Inverter Enabled) |
| 5 | EVAL_ENG_SYS (Evaluation Engine System) |
| 6 | EVAL_REKEY_ALLOWED (Evaluatio Rekey Allowed) |
| 7 | OPERATIONAL |
| 8 | DET_ENG_STOPPED (Determine Engine Stopped) |
| 9 | DET_INV_DISABLED (Determine Inverter Disabled) |
| 10 | EVAL_BP_OPEN (Evaluation Batteripack Open) |
| 11 | DET_BP_OPENED (Determine Batteripack Opened) |
| 12 | DET_BUS_DISCHARGED (Determine Highvoltage Bus Discharged) |
| 13 | SHUTDOWN |
| 14 | JUMP_ASSIST |

<a id="table-t-textresetursache"></a>
### T_TEXTRESETURSACHE

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | CeHWIO_e_PwrUpRstIgn |
| 1 | CeHWIO_e_PwrUpRstSerial |
| 2 | CeHWIO_e_RunRstExtWDT |
| 3 | CeHWIO_e_RunRstIntWDT |
| 4 | CeHWIO_e_RunRstUnhndldExcptn |
| 5 | CeHWIO_e_RstBattConnect |
| 6 | CeHWIO_e_RstUnident |

<a id="table-t-ok-nicht-ok"></a>
### T_OK_NICHT_OK

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht OK |
| 1 | OK |

<a id="table-t-textstatequroutineaktiv"></a>
### T_TEXTSTATEQUROUTINEAKTIV

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | EQU-Routine nicht aktiv |
| 1 | EQU-Routine aktiv |

<a id="table-t-textstatequroutineabbruch"></a>
### T_TEXTSTATEQUROUTINEABBRUCH

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | EQU-Routine nicht abgebrochen |
| 1 | EQU-Routine abgebrochen |

<a id="table-t-textstatsperrbed"></a>
### T_TEXTSTATSPERRBED

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Sperrbed.liegt nicht an |
| 1 | Sperrbed.liegt an |

<a id="table-t-textstatbattequil"></a>
### T_TEXTSTATBATTEQUIL

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | AUS |
| 1 | Entladepahse SOC &gt;30% |
| 2 | Entladepahse SOC &gt;20% |
| 3 | Entladephase SOC &gt;10% |
| 4 | Stabilisierungsphase |
| 5 | Equlibrierungspahse |
| 6 | Erholungsphase |
| 7 | Ladephase SOC &lt;20% |
| 8 | Ladephase SOC &lt;30% |
| 9 | Equilibrierung beendet |

<a id="table-t-textsocrusecase"></a>
### T_TEXTSOCRUSECASE

Dimensions: 22 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht definiert |
| 1 | Battery zu heiss |
| 2 | Battery Equilibrierung |
| 3 | Standladen |
| 4 | Kat-heiz-modus |
| 5 | Batterieheizen laden |
| 6 | Batterieheizen entladen |
| 7 | Produktionsmodus |
| 8 | Sportmodus |
| 9 | Rückwärts |
| 10 | Neutral |
| 11 | Park |
| 12 | Drive |
| 13 | Produktionsmodus ohne Ladeunterdrückung |
| 14 | Warmlauf |
| 15 | Batterie Stimulus Laden |
| 16 | Batterie Stimulus Entladen |
| 17 | SOC Overwrite Tester |
| 18 | Limiterbetrieb |
| 19 | Efficient Drive |
| 20 | SOC SFA |
| 21 | Default |

<a id="table-t-textadaptionswerteloeschen"></a>
### T_TEXTADAPTIONSWERTELOESCHEN

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | alle löschen |
| 1 | Pyrofuse wird zurückgesetzt (Klemme 41) |
| 3 | CC-Meldung |
| 4 | HISR- Betriebsstrategie-Analyse wir zurückgesetzt |

<a id="table-t-textbattloeschen"></a>
### T_TEXTBATTLOESCHEN

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | keine Aktion |
| 7 | Adaptionswerte der Batterie löschen |

<a id="table-t-gear"></a>
### T_GEAR

Dimensions: 12 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | ungueltig |
| 1 | 1.Gang |
| 2 | 2.Gang |
| 3 | 3.Gang |
| 4 | 4.Gang |
| 5 | 5.Gang |
| 6 | 6.Gang |
| 7 | 7.Gang |
| 60 | Neutral |
| 70 | Rueckwaerts |
| 80 | Park |
| 255 | unbekannter Gang |

<a id="table-t-aus-reset"></a>
### T_AUS_RESET

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | AUS |
| 1 | RESET |

<a id="table-t-textav"></a>
### T_TEXTAV

Dimensions: 40 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | VM läuft wegen Batterieladezustand |
| 2 | VM läuft wegen geringer Temperatur Hochvoltbatterie |
| 3 | VM läuft systembedingt |
| 4 | VM läuft wegen Batterieladezustand |
| 5 | keine Anzeige (nicht BMW relevant) |
| 6 | keine Anzeige (nicht BMW relevant) |
| 7 | wird auf DME definiert |
| 8 | VM läuft wegen Batterieladezustand |
| 9 | VM läuft systembedingt |
| 10 | VM läuft systembedingt |
| 11 | VM läuft systembedingt |
| 12 | keine Anzeige (nicht BMW relevant) |
| 13 | VM läuft systembedingt |
| 14 | VM läuft wegen hoher Temperatur im Hybridsystem |
| 15 | VM läuft wegen hoher Temperatur im Hybridsystem |
| 16 | VM läuft wegen niedriger Motortemperatur |
| 17 | VM läuft systembedingt |
| 18 | VM läuft systembedingt |
| 19 | VM läuft systembedingt |
| 20 | VM läuft systembedingt |
| 21 | VM läuft systembedingt |
| 22 | VM läuft wegen Komfortanforderung |
| 23 | keine Anzeige (nicht BMW relevant) |
| 24 | VM läuft wegen geringer Temperatur Hochvoltbatterie  |
| 25 | VM läuft systembedingt |
| 26 | VM läuft wegen hoher Motortemperatur |
| 27 | - |
| 28 | VM läuft wegen geringer Temperatur Hochvoltbatterie  |
| 29 | VM läuft wegen hoher Motortemperatur |
| 30 | VM läuft wegen hoher Temperatur im Hybridsystem |
| 31 | VM läuft wegen niedriger Motortemperatur |
| 32 | VM läuft systembedingt |
| 33 | keine Anzeige |
| 34 | VM läuft wegen Batterieladezustand |
| 35 | Motorstart wurde durch Fahrer erzwungen |
| 36 | Motorstart wurde durch Fahrer erzwungen |
| 37 | Motorstart wurde durch Fahrer erzwungen |
| 38 | VM läuft wegen Batterieladezustand |
| 39 | VM läuft systembedingt |
| 40 | VM läuft wg.Steigung/Gefälle |

<a id="table-t-ungueltig1-gueltig0"></a>
### T_UNGUELTIG1_GUELTIG0

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | gültig |
| 1 | ungültig |

<a id="table-t-textbattkuehlbetriebsmodus"></a>
### T_TEXTBATTKUEHLBETRIEBSMODUS

Dimensions: 26 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Kühlung aus |
| 1 | Zirkulation zur Homogenisierung |
| 3 | Vorkühlung |
| 4 | Kühlung über Radiator |
| 5 | Duplex Kühlung über Radiator und Chiller |
| 6 | Kühlung über Chiller |
| 8 | Vorkühlung Variante 1 |
| 9 | Vorkühlung Variante 2 |
| 11 | Kühlung über Radiator Variante 1 |
| 12 | Kühlung über Radiator Variante 2 |
| 14 | Duplex Kühlung Variante 1 |
| 15 | Duplex Kühlung Variante 2 |
| 17 | Kühlung über Chiller Variante 1 |
| 18 | Kühlung über Chiller Variante 2 |
| 19 | Kühlung über Chiller Variante 3 |
| 21 | Chiller keine Freigabe/defekt, Kühlung über Radiator |
| 22 | Chiller keine Freigabe/defekt, Kühlung über Radiator Variante 1 |
| 23 | Chiller keine Freigabe/defekt, Kühlung über Radiator Variante 2 |
| 24 | Chiller keine Freigabe/defekt, keine Kühlung über Radiator möglich |
| 25 | Duplexmodus, Chiller keine Freigabe/defekt, Kühlung über Radiator |
| 26 | Duplexmodus, Chiller keine Freigabe/defekt, Kühlung über Radiator Variante 1 |
| 27 | Duplexmodus, Chiller keine Freigabe/defekt, Kühlung über Radiator Variante 2 |
| 28 | Duplexmodus, Chiller keine Freigabe/defekt, keine Kühlung über Radiator möglich |
| 29 | Zirkulation zur Nachkühlung |
| 30 | Ventil Radiator defekt, keine Kühlung über Chiller möglich |
| 31 | Ventil Radiator defekt, Kühlung über Chiller |

<a id="table-t-textdrrmode"></a>
### T_TEXTDRRMODE

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | AUTOMATIC |
| 1 | SPORT |
| 2 | MAN |
| 3 | INVALID |
| 4 | LIMIT |
| 5 | INVALID |
| 6 | INVALID |
| 7 | INVALID |
| 8 | CITY |
| 15 | INVALID |

<a id="table-tindividualdataliste"></a>
### TINDIVIDUALDATALISTE

Dimensions: 1 rows × 17 columns

| ENTRYNR | ISLAST | FROMWHERE | DIAG | CARORKEY | USECASE | TESTER_ALGO | RESERVED | INQY_LEN | INQY_DATA | RESP_LEN | RESP_DATA | WRITE_LEN | WRITE_DATA | W_RESP_LEN | W_RESP_DATA | COMMENT |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x0000 | 0xFF | 01 | 1A | 02 | 000F | 01 | 00 | 00 | - | 00 | - | 00 | - | 00 | - | Batterie.Recovery |

<a id="table-t-textionio"></a>
### T_TEXTIONIO

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Kein Ergebnis |
| 1 | i.O |
| 2 | n.i.O |

<a id="table-hybrid-lief"></a>
### HYBRID_LIEF

Dimensions: 6 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0003 | Bosch |
| 0040 | Delphi |
| 007E | Hitachi |
| 009C | Cobasys |
| 0008 | Siemens |
| FFFF | undefinierter Lieferant |

<a id="table-datum-monat"></a>
### DATUM_MONAT

Dimensions: 53 rows × 2 columns

| KW | MON |
| --- | --- |
| 0x01 | 0x01 |
| 0x02 | 0x01 |
| 0x03 | 0x01 |
| 0x04 | 0x01 |
| 0x05 | 0x01 |
| 0x06 | 0x02 |
| 0x07 | 0x02 |
| 0x08 | 0x02 |
| 0x09 | 0x02 |
| 0x0A | 0x03 |
| 0x0B | 0x03 |
| 0x0C | 0x03 |
| 0x0D | 0x03 |
| 0x0E | 0x04 |
| 0x0F | 0x04 |
| 0x10 | 0x04 |
| 0x11 | 0x04 |
| 0x12 | 0x04 |
| 0x13 | 0x05 |
| 0x14 | 0x05 |
| 0x15 | 0x05 |
| 0x16 | 0x05 |
| 0x17 | 0x06 |
| 0x18 | 0x06 |
| 0x19 | 0x06 |
| 0x1A | 0x06 |
| 0x1B | 0x07 |
| 0x1C | 0x07 |
| 0x1D | 0x07 |
| 0x1E | 0x07 |
| 0x1F | 0x07 |
| 0x20 | 0x08 |
| 0x21 | 0x08 |
| 0x22 | 0x08 |
| 0x23 | 0x08 |
| 0x24 | 0x09 |
| 0x25 | 0x09 |
| 0x26 | 0x09 |
| 0x27 | 0x09 |
| 0x28 | 0x0A |
| 0x29 | 0x0A |
| 0x2A | 0x0A |
| 0x2B | 0x0A |
| 0x2C | 0x0A |
| 0x2D | 0x0B |
| 0x2E | 0x0B |
| 0x2F | 0x0B |
| 0x30 | 0x0B |
| 0x31 | 0x0C |
| 0x32 | 0x0C |
| 0x33 | 0x0C |
| 0x34 | 0x0C |
| 0xFF | 0x00 |
