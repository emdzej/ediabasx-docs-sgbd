# FZD_70.prg

- Jobs: [114](#jobs)
- Tables: [48](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | FZD E70 |
| ORIGIN | BMW EI-61 Herter |
| REVISION | 2.000 |
| AUTHOR | Hella_Micron_Engineering Software_Development Peter_Schmidt, Hella_KGaA EE_313 Dieter_Schnelle |
| COMMENT | N/A |
| PACKAGE | 1.30 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [INFO](#job-info) - Information SGBD
- [DIAGNOSEPROTOKOLL_LESEN](#job-diagnoseprotokoll-lesen) - Gibt die möglichen Diagnoseprotokolle für eine Auswahl an den Aufrufer zurück
- [DIAGNOSEPROTOKOLL_SETZEN](#job-diagnoseprotokoll-setzen) - Wählt ein Diagnoseprotokoll aus
- [IDENT](#job-ident) - Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default
- [FS_LESEN_DETAIL](#job-fs-lesen-detail) - Fehlerspeicher lesen (ein Fehler / alle Details) KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus: Default
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : Default
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels KWP2000: $22 ReadDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [NORMALER_DATENVERKEHR](#job-normaler-datenverkehr) - Sperren bzw. Freigeben des normalen Datenverkehrs KWP2000: $28 DisableNormalMessageTransmission KWP2000: $29 EnableNormalMessageTransmission Modus  : Default
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode des SG aufrecht erhalten KWP2000: $3E TesterPresent Modus  : Default
- [FS_SPERREN](#job-fs-sperren) - Sperren bzw. Freigeben des Fehlerspeichers KWP2000: $85 ControlDTCSetting Modus  : Default
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry Modus: Default
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [HS_LESEN](#job-hs-lesen) - Historyspeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2100 HistoryMemory Modus  : Default
- [HS_LESEN_DETAIL](#job-hs-lesen-detail) - Historypeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2101 - $21FF HistoryMemoryEntry Modus: Default
- [HS_LOESCHEN](#job-hs-loeschen) - Historyspeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $03 ClearHistoryMemory Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
- [C_CI_LESEN](#job-c-ci-lesen) - Codierindex lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $9B Vehicle Manufacturer Coding Index oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [C_FG_LESEN](#job-c-fg-lesen) - Fahrgestellnummer lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default
- [C_FG_SCHREIBEN](#job-c-fg-schreiben) - Fahrgestellnummer schreiben Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $90 Vehicle Identification Number Modus  : Default
- [C_FG_AUFTRAG](#job-c-fg-auftrag) - Fahrgestellnummer schreiben und ruecklesen Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $90 Vehicle Identification Number KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default
- [C_AEI_LESEN](#job-c-aei-lesen) - Aenderungsindex der Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default
- [C_AEI_SCHREIBEN](#job-c-aei-schreiben) - Aenderungsindex der Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default
- [C_AEI_AUFTRAG](#job-c-aei-auftrag) - Aenderungsindex der Codierdaten schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3FFF ChangeIndexOfCodingData KWP2000: $22   ReadDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default
- [C_C_LESEN](#job-c-c-lesen) - Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [C_C_SCHREIBEN](#job-c-c-schreiben) - Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [SERIENNUMMER_LESEN](#job-seriennummer-lesen) - Hersteller Seriennummer lesen KWP2000: $1A ReadECUIdentification $89 SystemSupplierECUSerialNumber oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [ZIF_LESEN](#job-zif-lesen) - Auslesen des Zulieferinfofeldes KWP2000: $22   ReadDataByCommonIdentifier $2503 ProgrammReferenz und KWP2000: $1A   ReadECUIdentification $91   VehicleManufacturerECUHardware*Number oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [ZIF_BACKUP_LESEN](#job-zif-backup-lesen) - Auslesen des Backups des Zulieferinfofeldes ProgrammReferenzBackup         PRGREFB vehicleManufECUHW*NumberBackup VMECUH*NB KWP2000: $22   ReadDataByCommonIdentifier $2500 PRBHW*B oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [PHYSIKALISCHE_HW_NR_LESEN](#job-physikalische-hw-nr-lesen) - Auslesen der physikalischen Hardwarenummer KWP2000: $1A ReadECUIdentification $87 physicalECUHardwareNumber (PECUHN) oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [HARDWARE_REFERENZ_LESEN](#job-hardware-referenz-lesen) - Auslesen der Hardware Referenz KWP2000: $22   ReadDataByCommonIdentifier $2502 HWREF oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [DATEN_REFERENZ_LESEN](#job-daten-referenz-lesen) - Auslesen der Daten Referenz KWP2000: $22   ReadDataByCommonIdentifier $2504 DREF Modus  : Default
- [FLASH_ZEITEN_LESEN](#job-flash-zeiten-lesen) - Auslesen der Flash Loeschzeit, Signaturtestzeit, Authentisierberechnungszeit und Resetzeit KWP2000: $22   ReadDataByCommonIdentifier $2501 Zeiten Modus  : Default
- [FLASH_BLOCKLAENGE_LESEN](#job-flash-blocklaenge-lesen) - Auslesen des maximalen Blocklaenge beim Flashen KWP2000: $22   ReadDataByCommonIdentifier $2506 MaximaleBlockLaenge Modus  : Default
- [AUTHENTISIERUNG_ZUFALLSZAHL_LESEN](#job-authentisierung-zufallszahl-lesen) - Authentisierung Zufallszahl des SG lesen KWP2000: $31 StartRoutineByLocalIdentifier $07 RequestForAuthentication Modus  : Default
- [AUTHENTISIERUNG_START](#job-authentisierung-start) - Authentisierung pruefen KWP2000: $31 StartRoutineByLocalIdentifier $08 ReleaseAuthentication Modus  : Default
- [FLASH_PROGRAMMIER_STATUS_LESEN](#job-flash-programmier-status-lesen) - Programmierstatus des SG lesen KWP2000: $31 StartRoutineByLocalIdentifier $0A CheckProgrammingStatus Modus  : Default
- [FLASH_SIGNATUR_PRUEFEN](#job-flash-signatur-pruefen) - Flash Signatur pruefen KWP2000: $31 StartRoutineByLocalIdentifier $09 CheckSignature Modus  : Default
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Steuergeraete reset ausloesen KWP2000: $11 ECUReset $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [FLASH_LOESCHEN](#job-flash-loeschen) - Flash loeschen Standard Flashjob KWP2000: $31 StartRoutineByLocalIdentifier $02 ClearMemory Modus  : Default
- [FLASH_SCHREIBEN_ADRESSE](#job-flash-schreiben-adresse) - Vorbereitung fuer Flash schreiben Standard Flashjob KWP2000: $34 RequestDownload Modus  : Default
- [FLASH_SCHREIBEN](#job-flash-schreiben) - Flash Daten schreiben Standard Flashjob KWP2000: $36 TransferData Modus  : Default
- [FLASH_SCHREIBEN_ENDE](#job-flash-schreiben-ende) - Flashprogrammierung abschliessen Standard Flashjob KWP2000: $37 RequestTransferExit Modus  : Default
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender Informations Feldes Standard Flashjob KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [AIF_SCHREIBEN](#job-aif-schreiben) - Schreiben des Anwender Informations Feldes Standard Flashjob KWP 2000: $3D WriteMemoryByAddress Modus   : Default
- [STATUS_BATTERIESPANNUNG](#job-status-batteriespannung) - Versorgungsspannungsspannung auslesen Ergebnis in mV
- [STATUS_TEMPERATUR_FZD](#job-status-temperatur-fzd) - Auslesen der Temperatur an folgenden Punkten: - direkt auf der FZD Platine - im Innenraum (via CAN )
- [STATUS_ENERGIESPARMODE](#job-status-energiesparmode) - aktuellen Energiesparmode-Lesen (FeTraWe)
- [_STATUS_RESETZAEHLER](#job-status-resetzaehler) - Gibt den aktuellen Wert der Resetzähler zurück
- [_STEUERN_RESETZAEHLER_LOESCHEN](#job-steuern-resetzaehler-loeschen) - Zurücksetzen der Resetzaehler
- [_STATUS_STACKCHECK](#job-status-stackcheck) - gibt die Anzahl der unbenutzten Bytes in den Task- und ISR-Stacks zurück
- [_STEUERN_STACKCHECK_LOESCHEN](#job-steuern-stackcheck-loeschen) - Setzt die Stackcheckcounter zurueck
- [_STATUS_USIS_VERSIONINFO](#job-status-usis-versioninfo) - Auslesen der Versionsinformation fuer USIS
- [_SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [_SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default
- [STEUERN_SHD_EINLERNEN](#job-steuern-shd-einlernen) - Einlernen des Schiebedachs Einlernvorgang per Diagnose muss ohne Randbedingungen ausgefuehrt werden koennen Zu Beginn eines Einlernvorgangs wird STAT_SHD_EINGELERNT zurueckgesetzt Der Job fuehrt die Normierung und die Initialsierung des Schiebedachs bzw. der Schiebedächer durch
- [STATUS_MDS_DATEN](#job-status-mds-daten) - Auslesen der Bedienkonzept-Daten
- [STATUS_TASTER_SHD](#job-status-taster-shd) - Auslesen der Stati von Schalterleitungen Fuer den MDS-Bedienkonzept-Schalter Werte bei Results: 0: Taster nicht betaetigt 1: Taster betaetigt
- [STEUERN_TASTER_SHD](#job-steuern-taster-shd) - Steuert den Zustand des Bedienkonzept-Schalters Nach Ausführung des Jobs geht die Kontrolle automatisch an das SG zurück Bei jeder Tasterbetätigung (über Diagnose) muß eine "0x00: Nichts gedrückt" gesendet werden, damit der Folgezustand des Tasters erkannt werden kann.
- [STATUS_SHD](#job-status-shd) - Abfrage der Schiebedach Stati In welchem Zustand befindet sich das Schiebdach? Wertezuordnung bei Results: 0: nicht aktiv bzw nicht eingelernt 1: aktiv bzw eingelernt
- [STATUS_ESH](#job-status-esh) - Abfrage der Stati des Elektrischen SchiebeHimmels (ESH) In welchem Zusatnd befindet sich der elektrische Schiebehimmel Wertezuordnung bei Results: 0: nicht aktiv bzw nicht eingelernt 1: aktiv bzw eingelernt
- [STATUS_MDS_BEDIENSTATISTIK](#job-status-mds-bedienstatistik) - Bedienkonzept-Statistik auslesen
- [STEUERN_DIGITAL_OUTPUT](#job-steuern-digital-output) - Ansteuerung der Ausgaenge
- [STEUERN_SHD](#job-steuern-shd) - Verfahren des Schiebedachs per Diagnose Ansteuerung bezieht sich auf die Eingangsseite
- [STEUERN_ESH](#job-steuern-esh) - Verfahren des elektrischen Schiebehimmels per Diagnose Ansteuerung bezieht sich auf die Eingangsseite
- [STEUERN_MDS_STANDALONE](#job-steuern-mds-standalone) - Stand-Alone Version des MDS aktivieren / Deaktivieren Bei aktiver Stand-Alone-Version ist keine Freigabe der Dachbewegung über CAN erforderlich nach ECU-Reset ist codierter Zustand wiederhergestellt
- [STEUERN_EKS_SHD](#job-steuern-eks-shd) - Aktivieren oder deaktivieren des Einklemmschutzes fuer den Motor SHD Nach ECU-Reset ist der codierte Zustand wiederhergestellt
- [STEUERN_EKS_ESH](#job-steuern-eks-esh) - Aktivieren oder deaktivieren des Einklemmschutzes uer den Motor ESH nach ECU-Reset ist codierter Zustand wiederhergestellt
- [STATUS_TEMPERATURMONITOR_MDS](#job-status-temperaturmonitor-mds) - Gibt den Status des Temperaturmonitors des MDS zurueck Wertezuordnung bei Results: 0: nicht aktiv 1: aktiv
- [STATUS_EKS](#job-status-eks) - Gibt Anzahl der Klemmungen und die letzte Klemmposition zurueck
- [STEUERN_THERMO_SHD](#job-steuern-thermo-shd) - Aktivieren oder deaktivieren des Thermoschutzes fuer den Motor SHD nach ECU-Reset ist codierter Zustand wiederhergestellt
- [STEUERN_THERMO_ESH](#job-steuern-thermo-esh) - Aktivieren oder deaktivieren des Thermoschutzes fuer den Motor ESH nach ECU-Reset ist codierter Zustand wiederhergestellt
- [STEUERN_COMFORT_POS](#job-steuern-comfort-pos) - Aktivieren oder deaktivieren des Anfahrens der Komfortposition nach ECU-Reset ist codierter Zustand wiederhergestellt
- [STEUERN_WINDABWEISER](#job-steuern-windabweiser) - Ausfahren bzw. Einfahren des Windabweisers unabhängig von der Fahrzeuggeschwindigkeit nach ECU-Reset ist codierter Zustand wiederhergestellt
- [STATUS_EKS_KENNLINIEN](#job-status-eks-kennlinien) - Auslesen der gespeicherten Kennlinien fuer den Einklemmschutz  Bemerkungen: - Jeder "STAT_INKREMENT"-ten Motorposition wird ein 8Bit Stromsample zugeordnet. - Der erste Stromwert bezieht sich auf die "STAT_STARTPOS"-Position. - Aufloesung: 0 ... 15.9375 A in 62,5 mA Schritten. Jedes Datenbyte muss durch 16 dividiert werden, um eine Anzeige in Ampere zu bekommen.
- [STATUS_BEDIENKONZEPT](#job-status-bedienkonzept) - Job liefert Aussage, welche Schiebedachvariante verbaut ist Benoetigt fuer HELLA Prueflabor
- [_STATUS_DWA](#job-status-dwa) - Auslesen des DWA-Status Wertezuordnung bei Results: 0: nicht aktiv 1: aktiv
- [STATUS_DWA_LED](#job-status-dwa-led) - Auslesen des Status der DWA-LED
- [STATUS_CAR_KEY_MEMORY](#job-status-car-key-memory) - Auslesen der CKM-Parameter
- [STATUS_DWA_ALARMTRIGGER](#job-status-dwa-alarmtrigger) - Auslesen des Status der Alarmtrigger Wertezuordnung bei Results: 0: nicht ausgeloest 1: ausgeloest
- [STATUS_DWA_INTERN](#job-status-dwa-intern) - Auslesen des Status der DWA-Applikation 0x00:  DWA entschärft 0x01:  DWA in Schärfung 0x02:  DWA geschärft 0x03:  DWA wird entschärft (not supported) 0x04:  DWA Alarm 0x05:  DWA Pause nach Alarm 0x06:  DWA Transport Mode 0x07:  DWA Werkstattmode 0x09:  DWA geschärft - IRS und Neigungssensor durch Benutzer deaktiviert 0x0A:  DWA geschärft - Distributionsmodus (not supported) 0x0B:  DWA Energiesparmode wird beendet (not supported) 0x0C:  DWA Powerdown Mode (not supported) 0x0D:  DWA Panik Alarm Mode 0x0E:  DWA geschärft - Hotelstellung aktiv 0x0F:  DWA geschärft - IRS & Neigungssensor nicht aktiv 0x10:  DWA geschärft - IRS nicht aktiv 0x11:  DWA geschärft - Neigungssensor nicht aktiv 0x12:  DWA Schnelltest aktiv
- [STEUERN_DWA_LED](#job-steuern-dwa-led) - Setzen des Status der DWA-LED Voraussetzung: DWA ungeschärft Beendigungmöglichkeiten des Jobs: - Automatisch nach 2 Minuten - Schärfen der DWA - Parameter = 0
- [STEUERN_DWA_SCHAERFEN](#job-steuern-dwa-schaerfen) - Setzen des Status der DWA Ein Entschaerfen der DWA, die ueber CAN geschaerft wurde, ist nicht moeglich
- [STEUERN_SIRENE_EIN_AUS](#job-steuern-sirene-ein-aus) - Setzen des Status der DWA-SINE
- [STEUERN_DWA_SELFTEST](#job-steuern-dwa-selftest) - Perform an hardware selftest of the DWA
- [STEUERN_DWA_SCHNELLTEST](#job-steuern-dwa-schnelltest) - Aktiviert den DWA-Schnelltest Modus Sensoren werden geschaerft Nach der Referenzierung kann ein Alarm ausgelöst werden Tritt ein Alarm auf, so wird 2s lang ein Alarmton erzeugt Abbrechkriterien: - Ausführen dieses Jobs mit "0", "aus" oder "off" - Schärfen oder Entschärfen der DWa über CAN - Timeout von 5 Minuten Startkriterien: Ausführen des Jobs mit "1", "ein", "on" oder ohne Argument
- [STEUERN_DWA_SCHNELLTEST_LEISE](#job-steuern-dwa-schnelltest-leise) - Aktiviert den DWA-Schnelltest Modus Sensoren werden geschaerft Nach der Referenzierung kann ein Alarm ausgelöst werden Tritt ein Alarm auf, so wird 2s lang ein Alarmton mit verringerter Lautstärke erzeugt Abbrechkriterien: - Ausführen dieses Jobs mit "0", "aus" oder "off" - Schärfen oder Entschärfen der DWa über CAN - Timeout von 5 Minuten Startkriterien: Ausführen des Jobs mit "1", "ein", "on" oder ohne Argument
- [STEUERN_K_BUS_TEST](#job-steuern-k-bus-test) - Prüft die Kommunikation zur SINE
- [STATUS_INNENLICHT_LEUCHTEN](#job-status-innenlicht-leuchten) - gibt den Status der Innenlicht-Leuchten zurück Wertezuordnung bei Results: 0: Leuchte aus 1: Leuchte ein
- [STATUS_INNENLICHT_TASTER](#job-status-innenlicht-taster) - gibt den Status der Innenlicht-Taster zurück Wertezuordnung bei Results: 0: Taster nicht gedrückt 1: Taster gedrückt
- [_STEUERN_INNENLICHT_LEUCHTEN](#job-steuern-innenlicht-leuchten) - Steuert den Zustand der Innenlicht-Leuchten
- [STEUERN_INNENLICHT_TASTER](#job-steuern-innenlicht-taster) - Steuert den Zustand der Innenlicht-Taster Job stellt Tastimpuls auf der Leitung per CAN nach
- [STEUERN_DIGITAL_LICHT](#job-steuern-digital-licht) - Ansteuerung der Innenlicht-Leuchten Verwendet Tabelle für ELEMENT: STEUERN_DIGITAL_LICHT Verwendete Tabelle für AKTION: DIGITAL_ARGUMENT Folgende Lichter werden gemeinsam geschaltet: Alle Innenlichter Die Makeup-Spiegelleuchten-Freigabe Diese Einschränkung ist Hardware-Abhängig
- [_FS_LESEN_PARAMETRIERT](#job-fs-lesen-parametriert) - parametrierte Version des FS_LESEN
- [_FS_LOESCHEN_PARAMETRIERT](#job-fs-loeschen-parametriert) - Parametrierte Version des Jobs FS_LOESCHEN
- [_IS_LOESCHEN_PARAMETRIERT](#job-is-loeschen-parametriert) - Parametrierte Version des Jobs IS_LOESCHEN
- [_MDS_TEST](#job-mds-test) - Jobvorlage
- [STATUS_IRS_ALARMCOUNTER](#job-status-irs-alarmcounter) - Auslesen der Stati der Innenraum-Sensoren Ausgegeben werden die Anzahl der intern gespeicherten Alarme Das Zurücksetzen der Werte erfolgt über den Job STEUERN_IRS_ALARM_LEVELS_RESET
- [STATUS_IRS_ALARM_LEVELS](#job-status-irs-alarm-levels) - Auslesen der letzten 10 Alarm-Levels Der ALARM_LEVEL_ARRAY_xxx identifiziert dabei einen Parameter Set Dieser Set wird von der Doppler-Erkennung zur Alarmerkennung genutzt Der Wert '0' bedeutet: Kein Alarm an dieser Stelle gespeichert Das Zurücksetzen der Werte erfolgt über den Job STEUERN_IRS_ALARM_LEVELS_RESET Mögliche Werte des jeweiligen Alarm-Level Eintrags sind: ALARM_LEVEL_ARRAY IRS inaktiv Normal Fenster / Dach offen Klimaanlage an Mögliche Werte des Alarm-Levels sind: Thermal levels VL = 0 -&gt; -40°C .. -15°C L  = 1 -&gt; -15°C .. + 5°C M  = 2 -&gt;  +5°C .. +45°C H  = 3 -&gt; +45°C .. +65°C VH = 4 -&gt; +65°C .. +85°C Hardware gain level _LO_GAIN = 0 -&gt; low _ML_GAIN = 1 -&gt; medium low _MH_GAIN = 2 -&gt; medium high _HI_GAIN = 3 -&gt; high Sensitivity
- [STATUS_IRS_FALSE_WAKEUP_LEVELS](#job-status-irs-false-wakeup-levels) - Auslesen der letzten 10 Wakeup-Levels ohne Alarmauslösung D.h. der Doppler-Mode wurde aktiviviert ohne Alarm auszulösen Der Werte '0' bedeutet: Kein Alarm an dieser Stelle gespeichert Das Zurücksetzen der Werte erfolgt über den Job STEUERN_IRS_FALSE_WAKEUP_LEVELS_RESET
- [STATUS_IRS_NOISE](#job-status-irs-noise) - Gibt Maßzahl für das Störrauschen an Wird erreichnet aus dem Verhältnis Anzahl Echo mode / Anzahl Doppler Mode Berechnet als gleitender Mittelwert in Anzahl/Minute Das Zurücksetzen der Werte erfolgt über den Job STEUERN_IRS_NOISE_RESET
- [STATUS_SENSOR_EMPFINDLICHKEIT](#job-status-sensor-empfindlichkeit) - Liest die Empfindlichkeit der Innenraumsensoren aus 0x00:   Normal mode 0x01:   Window opened 0x02:   Roof opened 0x03:   Air condition/heater on
- [STEUERN_SENSOR_EMPFINDLICHKEIT](#job-steuern-sensor-empfindlichkeit) - Stellt die Empfindlichkeit der Innenraumsensoren ein Eingestellte Werte werden mit Entschärfen der DWA automatisch zurückgesetzt 0x00:   Normal mode 0x01:   Window opened 0x02:   Roof opened 0x03:   Air condition/heater on
- [STEUERN_IRS_SELFTEST](#job-steuern-irs-selftest) - Selbsttest der Innenraumschutz-Sensoren Dieser Job ist nur im ungeschärften Zustand der IRS ausführbar Es wird ein statischer Fehlercode zurückgegeben: 8:  defect detected - both channels 9:  defect detected - Channel Front(A) 10: defect detected - Channel Rear(B) 11: the internal usis selftest has passed, no defect detected
- [STEUERN_IRS_NOISE_RESET](#job-steuern-irs-noise-reset) - Noise-Level löschen
- [STEUERN_IRS_ALARM_LEVELS_RESET](#job-steuern-irs-alarm-levels-reset) - Löschen der letzten 10 Alarm-Level
- [STEUERN_IRS_FALSE_WAKEUP_LEVELS_RESET](#job-steuern-irs-false-wakeup-levels-reset) - Löschen der letzen 10 False-Wakeup Level

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

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

<a id="job-diagnoseprotokoll-lesen"></a>
### DIAGNOSEPROTOKOLL_LESEN

Gibt die möglichen Diagnoseprotokolle für eine Auswahl an den Aufrufer zurück

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY oder ERROR_DIAG_PROT |
| DIAG_PROT_IST | string | Gibt das aktuelle gewählte Protokoll aus table KONZEPT_TABELLE KONZEPT_TEXT |
| DIAG_PROT_ANZAHL | int | Anzahl der Diagnoseprotokolle |
| DIAG_PROT_NR1 | string | Alle möglichen Diagnose-Protokolle Falls mehrere Protokolle möglich sind werden die entsprechenden Results DIAG_PROT_NRx dynamisch erzeugt |

<a id="job-diagnoseprotokoll-setzen"></a>
### DIAGNOSEPROTOKOLL_SETZEN

Wählt ein Diagnoseprotokoll aus

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DIAG_PROT | string | Diagnoseprotokoll table KONZEPT_TABELLE KONZEPT_TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |

<a id="job-ident"></a>
### IDENT

Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | string | BMW-Hardware-Versionsindex |
| ID_COD_INDEX | int | Codier-Index |
| ID_DIAG_INDEX | int | Diagnose-Index |
| ID_VAR_INDEX | int | Varianten-Index |
| ID_DATUM_JAHR | int | Herstelldatum (Jahr) |
| ID_DATUM_MONAT | int | Herstelldatum (Monat) |
| ID_DATUM_TAG | int | Herstelldatum (Tag) |
| ID_DATUM | string | Herstelldatum (TT.MM.JJJJ) |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Text table Lieferanten LIEF_TEXT |
| ID_SW_NR_MCV | string | Softwarenummer (message catalogue version) |
| ID_SW_NR_FSV | string | Softwarenummer (functional software version) |
| ID_SW_NR_OSV | string | Softwarenummer (operating system version) |
| ID_SW_NR_RES | string | Softwarenummer (reserved - currently unused) |
| ID_SG_ADR | long | Steuergeraeteadresse bzw. LIN Master Steuergeraeteadresse |
| ID_LIN_SLAVE_ADR | long | LIN Slave Steuergeraeteadresse |
| ID_EWS_SS | int | Identifikation EWS-Schnittstelle Nur fuer DS2-Bordnetz benoetigt Fuer EWS-DME/DDE Abgleich |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen-detail"></a>
### FS_LESEN_DETAIL

Fehlerspeicher lesen (ein Fehler / alle Details) KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | gewaehlter Fehlercode |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_PCODE | unsigned int | optional / Pflicht fuer abgasrelevante SG Wertebereich 0x0000 - 0xFFFF 0x0000: wenn nicht belegt |
| F_PCODE_STRING | string | 5 stelliger Text in der Form 'Pxxxx' '--': wenn nicht belegt '??': wenn nicht bekannt |
| F_PCODE_TEXT | string | Fehler als Klartext '': wenn nicht belegt table PCodeTexte TEXT |
| F_PCODE7 | unsigned int | optional / fuer abgasrelevante SG Wertebereich 0x0000 - 0xFFFF 0x0000: wenn nicht belegt |
| F_PCODE7_STRING | string | 5 stelliger Text in der Form 'Pxxxx' '--': wenn nicht belegt '??': wenn nicht bekannt |
| F_PCODE7_TEXT | string | Fehler als Klartext '': wenn nicht belegt table PCodeTexte TEXT |
| F_HFK | int | Haufigkeitszaehler als Zahl Wertebereich 0 - 255 -1: ohne Haufigkeitszaehler |
| F_LZ | int | Logistikzaehler als Zahl Wertebereich 0 - 255 -1: ohne Logistikzaehler |
| F_ART_ANZ | int | Anzahl der zusaetzlichen Fehlerarten Je nach dieser Anzahl i (i = 1, 2, ...) existieren i mal folgende Results: (long)   F_ARTi_NR   Index der i. Fehlerart (string) F_ARTi_TEXT Text  zur i. Fehlerart |
| F_UW_KM | long | Umweltbedingung Kilometerstand Wertebereich: 0 - 524280 km |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Je nach dieser Anzahl i (i = 1, 2, ...) existieren i mal folgende Results: (long)   F_UWi_NR   Index   der i. Umweltbedingung (string) F_UWi_TEXT Text    zur i. Umweltbedingung (real)   F_Uwi_WERT Wert    der i. Umweltbedingung (string) F_UWi_EINH Einheit der i. Umweltbedingung |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | 0x????: Angabe eines einzelnen Fehlers 0xFFFB: alle Antriebsfehler 0xFFFC: alle Fahrwerkfehler 0xFFFD: alle Karosseriefehler 0xFFFE: alle Netzwerkfehler Default: 0xFFFF: alle Fehler |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels KWP2000: $22 ReadDataByCommonIdentifier $1000 TestStamp Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default

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
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-normaler-datenverkehr"></a>
### NORMALER_DATENVERKEHR

Sperren bzw. Freigeben des normalen Datenverkehrs KWP2000: $28 DisableNormalMessageTransmission KWP2000: $29 EnableNormalMessageTransmission Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FREIGEBEN | string | "ja"   -&gt; normalen Datenverkehr freigeben "nein" -&gt; normalen Datenverkehr sperren table DigitalArgument TEXT |
| SG_ANTWORT | string | "ja"   -&gt; SG soll antworten "nein" -&gt; SG soll nicht antworten table DigitalArgument TEXT Default:  SG soll antworten |
| FUNKTIONAL | string | "ja"   -&gt; Funktionale Adresse 0xEF wird benutzt nur in Verbindung mit SG_ANTWORT="nein" "nein" -&gt; SG Adresse wird benutzt table DigitalArgument TEXT Default:  SG Adresse wird benutzt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Diagnosemode des SG aufrecht erhalten KWP2000: $3E TesterPresent Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SG_ANTWORT | string | "ja"   -&gt; SG soll antworten "nein" -&gt; SG soll nicht antworten table DigitalArgument TEXT Default:  SG soll antworten |
| FUNKTIONAL | string | "ja"   -&gt; Funktionale Adresse 0xEF wird benutzt nur in Verbindung mit SG_ANTWORT="nein" "nein" -&gt; SG Adresse wird benutzt table DigitalArgument TEXT Default:  SG Adresse wird benutzt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-sperren"></a>
### FS_SPERREN

Sperren bzw. Freigeben des Fehlerspeichers KWP2000: $85 ControlDTCSetting Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPERREN | string | "ja"   -&gt; Fehlerspeicher sperren "nein" -&gt; Fehlerspeicher freigeben table DigitalArgument TEXT |
| SG_ANTWORT | string | "ja"   -&gt; SG soll antworten "nein" -&gt; SG soll nicht antworten table DigitalArgument TEXT Default:  SG soll antworten |
| FUNKTIONAL | string | "ja"   -&gt; Funktionale Adresse 0xEF wird benutzt nur in Verbindung mit SG_ANTWORT="nein" "nein" -&gt; SG Adresse wird benutzt table DigitalArgument TEXT Default:  SG Adresse wird benutzt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-lesen"></a>
### IS_LESEN

Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table IOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-lesen-detail"></a>
### IS_LESEN_DETAIL

Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | gewaehlter Infocode Wenn dieser Parameter angegeben wird, wird die Position automatisch ermittelt. Es darf dann nicht argument F_POS angegeben werden |
| F_POS | int | gewaehlter Eintrag Wenn dieser Parameter angegeben wird, wird die Position benutzt. Wertebereich 1 - 255 Es darf dann nicht argument F_CODE angegeben werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table IOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table IArtTexte ARTTEXT |
| F_PCODE | unsigned int | optional / Pflicht fuer abgasrelevante SG Wertebereich 0x0000 - 0xFFFF 0x0000: wenn nicht belegt |
| F_PCODE_STRING | string | 5 stelliger Text in der Form 'Pxxxx' '--': wenn nicht belegt '??': wenn nicht bekannt |
| F_PCODE_TEXT | string | Fehler als Klartext '': wenn nicht belegt table PCodeTexte TEXT |
| F_PCODE7 | unsigned int | optional / fuer abgasrelevante SG Wertebereich 0x0000 - 0xFFFF 0x0000: wenn nicht belegt |
| F_PCODE7_STRING | string | 5 stelliger Text in der Form 'Pxxxx' '--': wenn nicht belegt '??': wenn nicht bekannt |
| F_PCODE7_TEXT | string | Fehler als Klartext '': wenn nicht belegt table PCodeTexte TEXT |
| F_HFK | int | Haufigkeitszaehler als Zahl Wertebereich 0 - 255 -1: ohne Haufigkeitszaehler |
| F_LZ | int | Logistikzaehler als Zahl Wertebereich 0 - 255 -1: ohne Logistikzaehler |
| F_ART_ANZ | int | Anzahl der zusaetzlichen Fehlerarten Je nach dieser Anzahl i (i = 1, 2, ...) existieren i mal folgende Results: (long)   F_ARTi_NR   Index der i. Fehlerart (string) F_ARTi_TEXT Text  zur i. Fehlerart |
| F_UW_KM | long | Umweltbedingung Kilometerstand Wertebereich: 0 - 524280 km |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Je nach dieser Anzahl i (i = 1, 2, ...) existieren i mal folgende Results: (long)   F_UWi_NR   Index   der i. Umweltbedingung (string) F_UWi_TEXT Text    zur i. Umweltbedingung (real)   F_Uwi_WERT Wert    der i. Umweltbedingung (string) F_UWi_EINH Einheit der i. Umweltbedingung |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-loeschen"></a>
### IS_LOESCHEN

Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-hs-lesen"></a>
### HS_LESEN

Historyspeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2100 HistoryMemory Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table HOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-hs-lesen-detail"></a>
### HS_LESEN_DETAIL

Historypeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2101 - $21FF HistoryMemoryEntry Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | gewaehlter Historycode Wenn dieser Parameter angegeben wird, wird die Position automatisch ermittelt. Es darf dann nicht argument F_POS angegeben werden |
| F_POS | int | gewaehlter Eintrag Wenn dieser Parameter angegeben wird, wird die Position benutzt. Wertebereich 1 - 255 Es darf dann nicht argument F_CODE angegeben werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table HOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_PCODE | unsigned int | optional / Pflicht fuer abgasrelevante SG Wertebereich 0x0000 - 0xFFFF 0x0000: wenn nicht belegt |
| F_PCODE_STRING | string | 5 stelliger Text in der Form 'Pxxxx' '--': wenn nicht belegt '??': wenn nicht bekannt |
| F_PCODE_TEXT | string | Fehler als Klartext '': wenn nicht belegt table PCodeTexte TEXT |
| F_PCODE7 | unsigned int | optional / fuer abgasrelevante SG Wertebereich 0x0000 - 0xFFFF 0x0000: wenn nicht belegt |
| F_PCODE7_STRING | string | 5 stelliger Text in der Form 'Pxxxx' '--': wenn nicht belegt '??': wenn nicht bekannt |
| F_PCODE7_TEXT | string | Fehler als Klartext '': wenn nicht belegt table PCodeTexte TEXT |
| F_HFK | int | Haufigkeitszaehler als Zahl Wertebereich 0 - 255 -1: ohne Haufigkeitszaehler |
| F_LZ | int | Logistikzaehler als Zahl Wertebereich 0 - 255 -1: ohne Logistikzaehler |
| F_ART_ANZ | int | Anzahl der zusaetzlichen Fehlerarten Je nach dieser Anzahl i (i = 1, 2, ...) existieren i mal folgende Results: (long)   F_ARTi_NR   Index der i. Fehlerart (string) F_ARTi_TEXT Text  zur i. Fehlerart |
| F_UW_KM | long | Umweltbedingung Kilometerstand Wertebereich: 0 - 524280 km |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Je nach dieser Anzahl i (i = 1, 2, ...) existieren i mal folgende Results: (long)   F_UWi_NR   Index   der i. Umweltbedingung (string) F_UWi_TEXT Text    zur i. Umweltbedingung (real)   F_Uwi_WERT Wert    der i. Umweltbedingung (string) F_UWi_EINH Einheit der i. Umweltbedingung |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-hs-loeschen"></a>
### HS_LOESCHEN

Historyspeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $03 ClearHistoryMemory Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagnose-mode"></a>
### DIAGNOSE_MODE

SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | gewuenschter Diagnose-Modus table DiagMode MODE MODE_TEXT Defaultwert: DEFAULT (DefaultMode) |
| BAUDRATE | string | optionaler Parameter fuer die gewuenschte Baudrate table BaudRate BAUD |
| SPEZIFISCHE_BAUDRATE_WERT | long | Parameter nur fuer BAUDRATE = 'SB' ( spezifische Baudrate ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEIT | real | a) Zeit nach der das Steuergerät einschläft Bereich   : 0.5 bis 20.0 [Sekunden] Auflösung : 0.5 [Sekunden] =&gt; zeitgesteuerter Power-Down (0x0E) wird aktiviert b) Default: (Es wird kein Argument übergeben!) =&gt; normaler Power-Down (0x05) wird aktiviert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-energiesparmode"></a>
### ENERGIESPARMODE

Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PRODUKTIONSMODE | string | "ein" -&gt; Produktions Mode ein "aus" -&gt; Produktions Mode aus table DigitalArgument TEXT Default: "aus" |
| TRANSPORTMODE | string | "ein" -&gt; Transport Mode ein "aus" -&gt; Transport Mode aus table DigitalArgument TEXT Default: "aus" |
| WERKSTATTMODE | string | "ein" -&gt; Werkstatt Mode ein "aus" -&gt; Werkstatt Mode aus table DigitalArgument TEXT Default: "aus" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-ci-lesen"></a>
### C_CI_LESEN

Codierindex lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $9B Vehicle Manufacturer Coding Index oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_COD_INDEX | int | Codier-Index |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Fahrgestellnummer lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FG_NR | string | Fahrgestellnummer 7-stellig |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fg-schreiben"></a>
### C_FG_SCHREIBEN

Fahrgestellnummer schreiben Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $90 Vehicle Identification Number Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fg-auftrag"></a>
### C_FG_AUFTRAG

Fahrgestellnummer schreiben und ruecklesen Standard Codierjob KWP2000: $3B WriteDataByLocalIdentifier $90 Vehicle Identification Number KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (18-stellig) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-c-aei-lesen"></a>
### C_AEI_LESEN

Aenderungsindex der Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| COD_AE_INDEX | string | Aenderungsindex max. 2-stellig ASCII inkl. Ziffern 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-aei-schreiben"></a>
### C_AEI_SCHREIBEN

Aenderungsindex der Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| COD_AE_INDEX | string | Aenderungsindex max. 2-stellig ASCII inkl. Ziffern 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-aei-auftrag"></a>
### C_AEI_AUFTRAG

Aenderungsindex der Codierdaten schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3FFF ChangeIndexOfCodingData KWP2000: $22   ReadDataByCommonIdentifier $3FFF ChangeIndexOfCodingData Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| COD_AE_INDEX | string | Aenderungsindex max. 2-stellig ASCII inkl. Ziffern 'a', 'b', .., 'y', 'z', 'aa', 'ab', .., 'zy', 'zz' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-c-c-lesen"></a>
### C_C_LESEN

Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : Codierdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIER_DATEN | binary | Codierdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-c-schreiben"></a>
### C_C_SCHREIBEN

Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : Codierdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-c-auftrag"></a>
### C_C_AUFTRAG

Codierdaten schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : Codierdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-seriennummer-lesen"></a>
### SERIENNUMMER_LESEN

Hersteller Seriennummer lesen KWP2000: $1A ReadECUIdentification $89 SystemSupplierECUSerialNumber oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SERIENNUMMER | string | Seriennummer des Steuergeraets |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-zif-lesen"></a>
### ZIF_LESEN

Auslesen des Zulieferinfofeldes KWP2000: $22   ReadDataByCommonIdentifier $2503 ProgrammReferenz und KWP2000: $1A   ReadECUIdentification $91   VehicleManufacturerECUHardware*Number oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ZIF_PROGRAMM_REFERENZ | string | PRGREF ProgrammReferenz letzter lauffaehiger Programmstand Format: ZZZPPPxVBBxh 12 Byte ASCII ZZZ   : Hardwarelieferant PPP   : Hardwarerelevanz zum Programmstand x     : nicht programmrelevante Varianten der Hardware V     : Projektvariante BB    : Programmstand x     : nicht datenrelevanter Änderungsindex h     : Programmstandersteller |
| ZIF_SG_KENNUNG | string | ZZZ |
| ZIF_PROJEKT | string | PPPxV |
| ZIF_PROGRAMM_STAND | string | BBxh |
| ZIF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |
| ZIF_BMW_HW | string | VMECUH*N vehicleManufacturerECUHardware*Number BMW Hardware Nummer |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_3 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_3 | binary | Hex-Antwort von SG |

<a id="job-zif-backup-lesen"></a>
### ZIF_BACKUP_LESEN

Auslesen des Backups des Zulieferinfofeldes ProgrammReferenzBackup         PRGREFB vehicleManufECUHW*NumberBackup VMECUH*NB KWP2000: $22   ReadDataByCommonIdentifier $2500 PRBHW*B oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ZIF_BACKUP_PROGRAMM_REFERENZ | string | PRGREFB ProgrammReferenzBackup letzter lauffaehiger Programmstand Format: ZZZPPPxVBBxh 12 Byte ASCII ZZZ   : Hardwarelieferant PPP   : Hardwarerelevanz zum Programmstand x     : nicht programmrelevante Varianten der Hardware V     : Projektvariante BB    : Programmstand x     : nicht datenrelevanter Änderungsindex h     : Programmstandersteller |
| ZIF_BACKUP_SG_KENNUNG | string | ZZZ |
| ZIF_BACKUP_PROJEKT | string | PPPxV |
| ZIF_BACKUP_PROGRAMM_STAND | string | BBxh |
| ZIF_BACKUP_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |
| ZIF_BACKUP_BMW_HW | string | VMECUH*NB vehicleManufECUHW*NumberBackup BMW Hardware* Nummer |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-physikalische-hw-nr-lesen"></a>
### PHYSIKALISCHE_HW_NR_LESEN

Auslesen der physikalischen Hardwarenummer KWP2000: $1A ReadECUIdentification $87 physicalECUHardwareNumber (PECUHN) oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PHYSIKALISCHE_HW_NR | string | Physikalische Hardware-Nummer |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-hardware-referenz-lesen"></a>
### HARDWARE_REFERENZ_LESEN

Auslesen der Hardware Referenz KWP2000: $22   ReadDataByCommonIdentifier $2502 HWREF oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| HARDWARE_REFERENZ | string | Hardware Referenz Format: ZZZPPPx 7 Byte ASCII ZZZ   : Hardwarelieferant PPP   : Hardwarerelevanz zum Programmstand x     : nicht programmrelevante Varianten der Hardware |
| HW_REF_SG_KENNUNG | string | ZZZ |
| HW_REF_PROJEKT | string | PPPx |
| HW_REF_STATUS | int | Dateninhalt bei FF noch nicht beschrieben |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

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

<a id="job-flash-zeiten-lesen"></a>
### FLASH_ZEITEN_LESEN

Auslesen der Flash Loeschzeit, Signaturtestzeit, Authentisierberechnungszeit und Resetzeit KWP2000: $22   ReadDataByCommonIdentifier $2501 Zeiten Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FLASH_LOESCHZEIT | int | Flash Loeschzeit in Sekunden |
| FLASH_SIGNATURTESTZEIT | int | Flash Signaturtestzeit in Sekunden |
| FLASH_RESETZEIT | int | Flash Resetzeit in Sekunden |
| FLASH_AUTHENTISIERZEIT | int | Flash Authentisierberechnungszeit in Sekunden |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-blocklaenge-lesen"></a>
### FLASH_BLOCKLAENGE_LESEN

Auslesen des maximalen Blocklaenge beim Flashen KWP2000: $22   ReadDataByCommonIdentifier $2506 MaximaleBlockLaenge Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FLASH_BLOCKLAENGE_GESAMT | unsigned int | Flash Blocklaenge inclusive SID |
| FLASH_BLOCKLAENGE_DATEN | int | Flash Datenlaenge |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-authentisierung-zufallszahl-lesen"></a>
### AUTHENTISIERUNG_ZUFALLSZAHL_LESEN

Authentisierung Zufallszahl des SG lesen KWP2000: $31 StartRoutineByLocalIdentifier $07 RequestForAuthentication Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LEVEL | int |  |
| USER_ID | long | optional |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ZUFALLSZAHL | binary | Zufallszahl |
| AUTHENTISIERUNG | string | Authentisierungsart table Authentisierung AUTHG_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-authentisierung-start"></a>
### AUTHENTISIERUNG_START

Authentisierung pruefen KWP2000: $31 StartRoutineByLocalIdentifier $08 ReleaseAuthentication Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : (unbenutzt) Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : Authentisierungszeit in Sekunden Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : (unbenutzt) Wortadresse (low/highbyte, low/highword) Byte 21,....        : Schluesseldaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-programmier-status-lesen"></a>
### FLASH_PROGRAMMIER_STATUS_LESEN

Programmierstatus des SG lesen KWP2000: $31 StartRoutineByLocalIdentifier $0A CheckProgrammingStatus Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FLASH_PROGRAMMIER_STATUS_TEXT | string | table ProgrammierStatus STATUS_TEXT |
| FLASH_PROGRAMMIER_STATUS | int | ProgrammierStatus 0 - 255 |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-signatur-pruefen"></a>
### FLASH_SIGNATUR_PRUEFEN

Flash Signatur pruefen KWP2000: $31 StartRoutineByLocalIdentifier $09 CheckSignature Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BEREICH | string | 'Programm' 'Daten' |
| SIGNATURTESTZEIT | int | Zeit in Sekunden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuergeraete-reset"></a>
### STEUERGERAETE_RESET

Steuergeraete reset ausloesen KWP2000: $11 ECUReset $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-loeschen"></a>
### FLASH_LOESCHEN

Flash loeschen Standard Flashjob KWP2000: $31 StartRoutineByLocalIdentifier $02 ClearMemory Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : Loeschzeit in Sekunden (Byteparameter 1) Byte 5,6            : Loeschzeit in Sekunden (WordParameter 1 (low/high)) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : (unbenutzt) Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_LOESCHEN_STATUS | int | Loeschstatus 1 = Speicher geloescht 2 = Speicher nicht geloescht 5 = Signaturpruefung PAF nicht durchgefuehrt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-schreiben-adresse"></a>
### FLASH_SCHREIBEN_ADRESSE

Vorbereitung fuer Flash schreiben Standard Flashjob KWP2000: $34 RequestDownload Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : (unbenutzt) Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_BLOCKLAENGE_DATEN | int | Flash Datenlaenge ohne Telegramm-Overhead |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-schreiben"></a>
### FLASH_SCHREIBEN

Flash Daten schreiben Standard Flashjob KWP2000: $36 TransferData Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : (unbenutzt) Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : (unbenutzt) Wortadresse (low/highbyte, low/highword) Byte 21,....        : Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_SCHREIBEN_ANZAHL | unsigned int | Anzahl FLASH_SCHREIBEN seit letztem FLASH_SCHREIBEN_ADRESSE |
| FLASH_SCHREIBEN_STATUS | int | Programmierstatus 1 = Programmierung in Ordnung 2 = Programmierung nicht in Ordnung |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-schreiben-ende"></a>
### FLASH_SCHREIBEN_ENDE

Flashprogrammierung abschliessen Standard Flashjob KWP2000: $37 RequestTransferExit Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : (unbenutzt) Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-aif-lesen"></a>
### AIF_LESEN

Auslesen des Anwender Informations Feldes Standard Flashjob KWP 2000: $23 ReadMemoryByAddress Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AIF_NUMMER | int | ==0 : aktuelles AIF &gt; 0 : Nummer des zu lesenden AIF default = 0 : aktuelles AIF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| AIF_ADRESSE_HIGH | int | AIF Adresse des AIF, High-Word |
| AIF_ADRESSE_LOW | int | AIF Adresse des AIF, Low-Word |
| AIF_FG_NR | string | Fahrgestellnummer 7-stellig |
| AIF_FG_NR_LANG | string | Fahrgestellnummer 17-stellig falls vorhanden, sonst 7-stellig |
| AIF_DATUM | string | Datum der SG-Programmierung in der Form TT.MM.JJJJ |
| AIF_ZB_NR | string | BMW/Rover Zusammenbaunummer |
| AIF_SW_NR | string | BMW/Rover Datensatznummer - Softwarenummer |
| AIF_BEHOERDEN_NR | string | BMW/Rover Behoerdennummer |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_SERIEN_NR | string | Tester Seriennummer |
| AIF_KM | long | km-Stand bei der Programmierung |
| AIF_PROG_NR | string | Programmstandsnummer |
| AIF_ANZ_FREI | int | Anzahl noch vorhandener AIF-Eintraege |
| AIF_ANZAHL_PROG | int | Anzahl Programmiervorgaenge |
| AIF_ANZ_DATEN | int | Groesse des AIF-Eintrags |
| AIF_GROESSE | int | Groesse des AIF |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-aif-schreiben"></a>
### AIF_SCHREIBEN

Schreiben des Anwender Informations Feldes Standard Flashjob KWP 2000: $3D WriteMemoryByAddress Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AIF_FG_NR | string | Fahrgestellnummer 7-stellig oder 17-stellig |
| AIF_DATUM | string | Datum der SG-Programmierung in der Form TT.MM.JJJJ oder TTMMJJ |
| AIF_ZB_NR | string | BMW/Rover Zusammenbaunummer |
| AIF_SW_NR | string | BMW/Rover Datensatznummer - Softwarenummer |
| AIF_BEHOERDEN_NR | string | BMW/Rover Behoerdennummer |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_SERIEN_NR | string | Tester Seriennummer |
| AIF_KM | long | km-Stand bei der Programmierung |
| AIF_PROG_NR | string | Programmstandsnummer |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| AIF_NUMMER | int | Nummer des geschreibenen AIF |
| AIF_DATEN | binary | AIF Hex-Daten |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG AIF lesen |
| _TEL_ANTWORT | binary | Hex-Antwort von SG AIF lesen |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG AIF schreiben |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG AIF schreiben |

<a id="job-status-batteriespannung"></a>
### STATUS_BATTERIESPANNUNG

Versorgungsspannungsspannung auslesen Ergebnis in mV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KL30_WERT | int | Wert der Batteriespannung in mV |
| STAT_KL30_WERT_EINH | string | "mV" |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-temperatur-fzd"></a>
### STATUS_TEMPERATUR_FZD

Auslesen der Temperatur an folgenden Punkten: - direkt auf der FZD Platine - im Innenraum (via CAN )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FZD_TEMP_WERT | real | Temperatur der FZD Platine in Grad C |
| STAT_TEMP_INTERIOR | real | Temperatur des Innenraums in Grad C |
| STAT_FZD_TEMP_EINH | string | Einheit der Temperaturwerte const "Grad C" |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-energiesparmode"></a>
### STATUS_ENERGIESPARMODE

aktuellen Energiesparmode-Lesen (FeTraWe)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FETRAWE_WERT | int | Status FeTraWe |
| STAT_FETRAWE_TEXT | string | textuelle Ausgabe des aktuellen FetraWeModes siehe Tabelle STATUS_FETRAWE_TAB |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-resetzaehler"></a>
### _STATUS_RESETZAEHLER

Gibt den aktuellen Wert der Resetzähler zurück

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RESETZAEHLER_HW_RESET | int | anzahl Resets Resetzähler Hardware Reset |
| STAT_RESETZAEHLER_WATCHDOG_RESET | int | anzahl Resets Resetzähler µC Watchdog |
| STAT_RESETZAEHLER_SOFTWARE_TASK_WATCHDOG_RESET | int | anzahl Resets Resetzähler Software Task Watchdog |
| STAT_RESETZAEHLER_SOFTWARE_RESET_REQUEST | int | anzahl Resets Resetzähler Software Reset Request |
| STAT_RESETZAEHLER_STACK_WATCHDOG_RESET | int | anzahl Resets Resetzähler Stack Watchdog |
| STAT_RESETGRUND_WERT | int | Grund des letzten Resets |
| STAT_RESETGRUND_TEXT | string | Grund des letzten Resets |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-resetzaehler-loeschen"></a>
### _STEUERN_RESETZAEHLER_LOESCHEN

Zurücksetzen der Resetzaehler

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERN_LOESCHE_RESETZAEHLER_1 | int | 0: nicht loeschen 1: loeschen |
| STEUERN_LOESCHE_RESETZAEHLER_2 | int | 0: nicht loeschen 1: loeschen |
| STEUERN_LOESCHE_RESETZAEHLER_3 | int | 0: nicht loeschen 1: loeschen |
| STEUERN_LOESCHE_RESETZAEHLER_4 | int | 0: nicht loeschen 1: loeschen |
| STEUERN_LOESCHE_RESETZAEHLER_5 | int | 0: nicht loeschen 1: loeschen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-stackcheck"></a>
### _STATUS_STACKCHECK

gibt die Anzahl der unbenutzten Bytes in den Task- und ISR-Stacks zurück

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_UNUSED_STACK_OPM | int | Anzahl unbenutzte Bytes im Stackbereich OPM |
| STAT_UNUSED_STACK_DWA | int | Anzahl unbenutzte Bytes im Stackbereich DWA |
| STAT_UNUSED_STACK_DST | int | Anzahl unbenutzte Bytes im Stackbereich DST |
| STAT_UNUSED_STACK_HPC | int | Anzahl unbenutzte Bytes im Stackbereich HPC |
| STAT_UNUSED_STACK_DAS | int | Anzahl unbenutzte Bytes im Stackbereich DAS |
| STAT_UNUSED_STACK_FLT | int | Anzahl unbenutzte Bytes im Stackbereich FLT |
| STAT_UNUSED_STACK_NVM | int | Anzahl unbenutzte Bytes im Stackbereich NVM |
| STAT_UNUSED_STACK_ISR | int | Anzahl unbenutzte Bytes im Stackbereich ISR |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-stackcheck-loeschen"></a>
### _STEUERN_STACKCHECK_LOESCHEN

Setzt die Stackcheckcounter zurueck

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERN_LOESCHE_STACKCHECK_OPM | int | 0: nicht loeschen 1: loeschen |
| STEUERN_LOESCHE_STACKCHECK_DWA | int | 0: nicht loeschen 1: loeschen |
| STEUERN_LOESCHE_STACKCHECK_DST | int | 0: nicht loeschen 1: loeschen |
| STEUERN_LOESCHE_STACKCHECK_HPC | int | 0: nicht loeschen 1: loeschen |
| STEUERN_LOESCHE_STACKCHECK_DAS | int | 0: nicht loeschen 1: loeschen |
| STEUERN_LOESCHE_STACKCHECK_FLT | int | 0: nicht loeschen 1: loeschen |
| STEUERN_LOESCHE_STACKCHECK_NVM | int | 0: nicht loeschen 1: loeschen |
| STEUERN_LOESCHE_STACKCHECK_ISR | int | 0: nicht loeschen 1: loeschen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-usis-versioninfo"></a>
### _STATUS_USIS_VERSIONINFO

Auslesen der Versionsinformation fuer USIS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VERSINFO_BYTE_1 | int | Byte 1 der Versionsinformation |
| STAT_VERSINFO_BYTE_2 | int | Byte 2 der Versionsinformation |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-speicher-lesen"></a>
### _SPEICHER_LESEN

Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT | string | table SpeicherSegment SEG_NAME SEG_TEXT |
| ADRESSE | long | 0x000000 - 0xFFFFFF |
| ANZAHL | int | 1 - n ( 254 ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | ausgelesene Daten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-speicher-schreiben"></a>
### _SPEICHER_SCHREIBEN

Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT | string | table SpeicherSegment SEG_NAME SEG_TEXT |
| ADRESSE | long | 0x000000 - 0xFFFFFF |
| ANZAHL | int | 1 - n ( max. 249 ) |
| DATEN | string | zu schreibende Daten (Anzahl siehe oben) z.B. 1,2,03,0x04,0x05... |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-shd-einlernen"></a>
### STEUERN_SHD_EINLERNEN

Einlernen des Schiebedachs Einlernvorgang per Diagnose muss ohne Randbedingungen ausgefuehrt werden koennen Zu Beginn eines Einlernvorgangs wird STAT_SHD_EINGELERNT zurueckgesetzt Der Job fuehrt die Normierung und die Initialsierung des Schiebedachs bzw. der Schiebedächer durch

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_SHD | int | 0x00: Vorgang abbrechen 0x01: Einlernvorgang starten Kein Argument uebergeben wird wie 0x00 behandelt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STATUS_VORGANG_GESTARTET_EIN | int | 0: Einlernvorgang konnte nicht gestartet werden 1: Einlernvorgang gestartet |
| STATUS_VORGANG_GESTARTET_DEZIMAL | int | Zuordnung siehe CODE aus table SHD_EINLERNEN  CODE BESCHREIBUNG siehe STATUS_VORGANG_GESTARTET_TEXT |
| STATUS_VORGANG_GESTARTET_TEXT | string | Zuordnung siehe BESCHREIBUNG aus table SHD_EINLERNEN  CODE BESCHREIBUNG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mds-daten"></a>
### STATUS_MDS_DATEN

Auslesen der Bedienkonzept-Daten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TARGETPOS_MOTOR1 | int | Zielposition SHD  |
| STAT_TARGETPOS_MOTOR2 | int | Zielposition ESH  |
| STAT_ACTPOS_MOTOR1 | int | Position SHD (PosZaehler Dach)  |
| STAT_ACTPOS_MOTOR2 | int | Position SHD (PosZaehler Himmel)  |
| STAT_STOREDPOSITION_MOTOR2 | int | gespeicherte Himmelposition  |
| STAT_VEHICLE_SPEED | int | Fahrzeuggeschwindigkeit  |
| STAT_H2_CONTROL | int | Codierung Wasserstoff - Fahrzeug  |
| STAT_SAVESTATE_WINDSCHOTT_ST | int | Windschott SM-Zustand  |
| STAT_SAVESTATE_SHD_ST | int | SHD SM-Zustand  |
| STAT_SAVESTATE_KEYST_ST | int | Schalter SM-Zustand  |
| STAT_SAVESTATE_PAN_ST | int | Panoramadach SM-Zustand  |
| STAT_SAVESTATE_GHD_ST | int | Glashubdach SM-Zustand  |
| STAT_SAVESTATE_POS_ST2 | int | Himmelpositions SM-Zustand  |
| STAT_SAVESTATE_INIT_ST | int | Initialisierungs SM-Zustand  |
| STAT_SAVESTATE_POS_ST1 | int | Deckelpositions SM_Zustand  |
| STAT_STOREPOSITION_MOTOR2 | int | Himmelposition schreiben wenn FZG gesichert  |
| STAT_KEYSTATE_1 | int | Input Schalterbetätigung  |
| STAT_RAIN_INTENSITY | int | Regenintensität  |
| STAT_COMFORT_MOVE | int | Komfortfunktion CAS (Funktschlüssel)  |
| STAT_INIT_ACTIVE | int | ACK Auto Init (AcknowlegeSignal)  |
| STAT_WINDSCHOTT_ACTIVE | int | Diagnose: Windschott ausgefahren  |
| STAT_STARTSTOP_MOTOR1 | int | SHD Steuerung Start-Stop  |
| STAT_STARTSTOP_MOTOR2 | int | ESH Steuerung Start-Stop - Bit  |
| STAT_DISABLE_CFL_MOTOR1 | int | EKS SHD wird ignoriert  |
| STAT_BBSHORT_MOTOR1 | int | SHD: Kurzer Reversierweg 2cm  |
| STAT_BBNOTBEFORSTART_MOTOR1 | int | SHD: Bei Regenschliessen, Reversierung nur bis Motorstart  |
| STAT_TMONDISABLE_MOTOR1 | int | SHD: Temperatur Monitor ignorieren und trotzdem fahren  |
| STAT_DISABLE_CFL_MOTOR2 | int | ESH: EKS wird ignoriert  |
| STAT_BBSHORT_MOTOR2 | int | ESH: Kurzer Reversierweg 2cm  |
| STAT_BBNOTBEFORESTART_MOTOR2 | int | ESH: Bei Regenschliessen, Reversierung nur bis Motorstart  |
| STAT_TMONDISABLE_MOTOR2 | int | ESH: Temperatur Monitor ignorieren und trotzdem fahren  |
| STAT_PARAM_CHANGED_1 | int | alle Parameter einlesen, nur wenn Bit true ist  |
| STAT_PANIC_ENABLED_1 | int | Panic-Mode Freigabe vom CAS  |
| STAT_EBA_MODE | int | EBA - Modus  |
| STAT_RF_MAX_VALID_MOTOR1 | int | SHD Kennlinie Max erkannt  |
| STAT_RF_MIN_VALID_MOTOR1 | int | SHD Kennlinie Min erkannt  |
| STAT_NORMED_MOTOR1 | int | SHD Normiert  |
| STAT_RF_MAX_VALID_MOTOR2 | int | ESH Kennlinie Max erkannt  |
| STAT_RF_MIN_VALID_MOTOR2 | int | ESH Kennlinie Min erkannt  |
| STAT_NORMED_MOTOR2 | int | ESH Normiert  |
| STAT_AUTO_INIT_CAN | int | Input Automatische Inititalisierung  |
| STAT_KL50 | int | Input Klemme 50 ( Anlasser )  |
| STAT_SHD_ENABLED | int | Tastenfreigabe vom CAS  |
| STAT_KL15 | int | Zustand Klemme 15  |
| STAT_MOVING_MOTOR1 | int | SHD läuft / steht  |
| STAT_MOVING_MOTOR2 | int | ESH läuft / steht  |
| STAT_BOUNCEBACK_MOTOR1 | int | SHD Reversiert  |
| STAT_BOUNCEBACK_MOTOR2 | int | ESH Reversiert  |
| STAT_START_STOP_PREV_MOTOR1 | int | StartStop SHD  |
| STAT_START_STOP_PREV_MOTOR2 | int | StartStop ESH  |
| STAT_PINCHINGDETECTED_MOTOR1 | int | Kraftzuwachs des SHD erkannt, oder blockiert  |
| STAT_PINCHINGDETECTED_MOTOR2 | int | Kraftzuwachs des ESH erkannt, oder blockiert  |
| STAT_LOWPOWER | int | Unterspannung erkannt  |
| STAT_HIGHPOWER | int | Überspannung erkannt  |
| STAT_CARSECURED | int | FZG ZV gesichert bzw. entriegelt  |
| STAT_FORCE_WINDSCHOTT | int | Windschott ausfahren ohne Gewschindigkeitsüberwachung  |
| STAT_SECURITY_ALARM | int | Sicherheitsfahrzeug Alarm  |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-taster-shd"></a>
### STATUS_TASTER_SHD

Auslesen der Stati von Schalterleitungen Fuer den MDS-Bedienkonzept-Schalter Werte bei Results: 0: Taster nicht betaetigt 1: Taster betaetigt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TASTER_SHD_MAUT_ZU | int | 0: Taster Schiebedach schliessen Maut nicht betaetigt 1: Taster Schiebedach schliessen Maut betaetigt |
| STAT_TASTER_SHD_ZU | int | 0: Taster Schiebedach schliessen nicht betaetigt 1: Taster Schiebedach schliessen betaetigt |
| STAT_TASTER_SHD_MAUT_AUF | int | 0: Taster Schiebedach oeffnen Maut nicht betaetigt 1: Taster Schiebedach oeffnen Maut betaetigt |
| STAT_TASTER_SHD_AUF | int | 0: Taster Schiebedach oeffnen nicht betaetigt 1: Taster Schiebedach oeffnen betaetigt |
| STAT_TASTER_SHD_HEBEN | int | 0: Taster Schiebedach heben nicht betaetigt 1: Taster Schiebedach heben betaetigt |
| STAT_TASTER_SHD_WERT | int | 0x00 = Schalter nicht betaetigt 0x01 = Zu (Tipp) 0x02 = Zu (Maut) 0x03 = Auf (Tipp) 0x04 = Auf (Maut) 0x05 = Heben |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-taster-shd"></a>
### STEUERN_TASTER_SHD

Steuert den Zustand des Bedienkonzept-Schalters Nach Ausführung des Jobs geht die Kontrolle automatisch an das SG zurück Bei jeder Tasterbetätigung (über Diagnose) muß eine "0x00: Nichts gedrückt" gesendet werden, damit der Folgezustand des Tasters erkannt werden kann.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_SCHALTER | int | Zuordnung siehe Tabelle STATUS_MDS_BK_SCHALTER_TAB 0x00: Nichts gedrückt - Kontrolle geht an das SG zurück 0x01: MDS auf 0x02: MDS zu 0x04: MDS heben 0x11: MAUT auf 0x12: MAUT zu |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SCHALTER_SHD_TEXT | string | Zuordnung siehe Tabelle STATUS_MDS_BK_SCHALTER_TAB |
| STAT_SCHALTER_SHD_WERT | int | identisch mit STEUERN_BK_SCHALTER_WERT eingepflegt nach IM-Meldung 6420 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-shd"></a>
### STATUS_SHD

Abfrage der Schiebedach Stati In welchem Zustand befindet sich das Schiebdach? Wertezuordnung bei Results: 0: nicht aktiv bzw nicht eingelernt 1: aktiv bzw eingelernt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SHD_EINGELERNT | int | 0: Schiebedach nicht eingelernt 1: Schiebedach eingelernt |
| STAT_SHD_EINLERNVORGANG_AKTIV | int | 0: Einlernvorgang nicht aktiv 1: Einlernvorgang aktiv |
| STAT_SHD_KENNLINIE_SCHLIESSEN_EIN | int | 0: Kennlinie Schiebedach schliessen nicht eingelernt 1: Kennlinie Schiebedach schliessen eingelernt |
| STAT_SHD_KENNLINIE_HEBEN_EIN | int | 0: Kennlinie Schiebedach heben nicht eingelernt 1: Kennlinie Schiebedach heben eingelernt |
| STAT_SHD_MAUT_ZU | int | 0: Schiebedach schliessen Maut nicht aktiv 1: Schiebedach schliessen Maut aktiv |
| STAT_SHD_ZU | int | 0: Schiebedach schliessen nicht aktiv 1: Schiebedach schliessen aktiv |
| STAT_SHD_MAUT_AUF | int | 0: Schiebedach oeffnen Maut nicht aktiv 1: Schiebedach oeffnen Maut aktiv |
| STAT_SHD_AUF | int | 0: Schiebedach oeffnen nicht aktiv 1: Schiebedach oeffnen aktiv |
| STAT_SHD_HEBEN | int | 0: Schiebedach heben nicht aktiv 1: Schiebedach heben aktiv |
| STAT_SHD_WERT | int | 0: Keine Bewegung 1: Zu (Tipp) 2: Zu (Maut) 3: Auf (Tipp) 4: Auf (Maut) 5: Heben |
| STAT_SHD_OFFEN_KOMPLETT | int | 0: Schiebedach nicht vollstaendig geoeffnet 1: Schiebedach vollstaendig geoeffnet |
| STAT_SHD_GESCHLOSSEN_KOMPLETT | int | 0: Schiebedach nicht vollstaendig geschlossen 1: Schiebedach vollstaendig geschlossen |
| STAT_SHD_GEHOBEN | int | 0: Schiebedach nicht in Position gehoben 1: Schiebedach in Position gehoben |
| STAT_SHD_POSITION_HORIZONTAL_WERT | int | Angabe der Position des Schiebedachs in Prozent 0% bis 100% 0%:   Schiebedach offen 100%: Schiebedach geschlossen 0xFF: Ungültig |
| STAT_SHD_POSITION_HORIZONTAL_EINH | string | Einheit zu STAT_SHD_POSITION_HORIZONTAL_WERT |
| STAT_SHD_POSITION_HEBEN_WERT | int | Angabe der Position Heben des Schiebedachs in Prozent 0% bis 100% 0%:   Schiebedach gehoben 100%: Schiebedach geschlossen 0xFF: Ungültig |
| STAT_SHD_POSITION_HEBEN_EINH | string | Einheit zu STAT_SHD_POSITION_HEBEN_WERT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-esh"></a>
### STATUS_ESH

Abfrage der Stati des Elektrischen SchiebeHimmels (ESH) In welchem Zusatnd befindet sich der elektrische Schiebehimmel Wertezuordnung bei Results: 0: nicht aktiv bzw nicht eingelernt 1: aktiv bzw eingelernt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ESH_EINGELERNT | int | 0: Elektrischer Schiebehimmel nicht eingelernt 1: Elektrischer Schiebehimmel eingelernt |
| STAT_ESH_EINLERNVORGANG_AKTIV | int | 0: Einlernvorgang nicht aktiv 1: Einlernvorgang aktiv |
| STAT_ESH_KENNLINIE_SCHLIESSEN_EIN | int | 0: Kennlinie elektrischer Schiebehimmel schliessen nicht eingelernt 1: Kennlinie elektrischer Schiebehimmel schliessen eingelernt |
| STAT_ESH_KENNLINIE_HEBEN_EIN | int | 0: Kennlinie elektrischer Schiebehimmel heben nicht eingelernt 1: Kennlinie elektrischer Schiebehimmel heben eingelernt |
| STAT_ESH_MAUT_ZU | int | 0: elektrischer Schiebehimmel schliessen Maut nicht aktiv 1: elektrischer Schiebehimmel schliessen Maut aktiv |
| STAT_ESH_ZU | int | 0: elektrischer Schiebehimmel schliessen nicht aktiv 1: elektrischer Schiebehimmel schliessen aktiv |
| STAT_ESH_MAUT_AUF | int | 0: elektrischer Schiebehimmel oeffnen Maut nicht aktiv 1: elektrischer Schiebehimmel oeffnen Maut aktiv |
| STAT_ESH_AUF | int | 0: elektrischer Schiebehimmel oeffnen nicht aktiv 1: elektrischer Schiebehimmel oeffnen aktiv |
| STAT_ESH_HEBEN | int | 0: elektrischer Schiebehimmel heben nicht aktiv 1: elektrischer Schiebehimmel heben aktiv |
| STAT_ESH_WERT | int | 0: Keine Bewegung 1: Zu (Tipp) 2: Zu (Maut) 3: Auf (Tipp) 4: Auf (Maut) 5: Heben |
| STAT_ESH_OFFEN_KOMPLETT | int | 0: elektrischer Schiebehimmel nicht vollstaendig geoeffnet 1: elektrischer Schiebehimmel vollstaendig geoeffnet |
| STAT_ESH_GESCHLOSSEN_KOMPLETT | int | 0: elektrischer Schiebehimmel nicht vollstaendig geschlossen 1: elektrischer Schiebehimmel vollstaendig geschlossen |
| STAT_ESH_GEHOBEN | int | 0: elektrischer Schiebehimmel nicht in Position gehoben 1: elektrischer Schiebehimmel in Position gehoben |
| STAT_ESH_POSITION_HORIZONTAL_WERT | int | Angabe der Position des elektrischen Schiebehimmels in Prozent 0% bis 100% 0%:   Elektrischer Schiebehimmel offen 100%: Elektrischer Schiebehimmel geschlossen 0xFF: Ungültig |
| STAT_ESH_POSITION_HORIZONTAL_EINH | string | Einheit zu STAT_ESH_POSITION_HORIZONTAL_WERT |
| STAT_ESH_POSITION_HEBEN_WERT | int | Angabe der Position Heben des elektrischen Schiebehimmels in Prozent 0% bis 100% 0%:   Elektrischer Schiebehimmel gehoben 100%: Elektrischer Schiebehimmel geschlossen 0xFF: Ungültig |
| STAT_ESH_POSITION_HEBEN_EINH | string | Einheit zu STAT_ESH_POSITION_HEBEN_WERT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mds-bedienstatistik"></a>
### STATUS_MDS_BEDIENSTATISTIK

Bedienkonzept-Statistik auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_COUNT_CAS_OPEN | int | Zähler Komfort_Auf 0...65536 |
| STAT_COUNT_CAS_CLOSE | int | Zähler Komfort_Zu 0...65536 |
| STAT_COUNT_KEY_STOP | int | Zähler Schalterstopp 0...65536 |
| STAT_COUNT_OPEN_1 | int | Zähler Taster Auf 0...65536 |
| STAT_COUNT_DBL_OPEN | int | Zähler Taster Auf Doppelklick 0...65536 |
| STAT_COUNT_OPEN_2 | int | Zähler Taster Auf überdrückt 0...65536 |
| STAT_COUNT_TILT | int | Zähler Taster Heben 0...65536 |
| STAT_COUNT_DBL_TILT | int | Zähler Taster Heben Doppelklick 0...65536 |
| STAT_COUNT_CLOSE_1 | int | Zähler Taster Zu 0...65536 |
| STAT_COUNT_DBL_CLOSE | int | Zähler Taster Zu Doppelklick 0...65536 |
| STAT_COUNT_CLOSE_2 | int | Zähler Taster Zu überdrückt 0...65536 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-digital-output"></a>
### STEUERN_DIGITAL_OUTPUT

Ansteuerung der Ausgaenge

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL | int | 0x00: Ansteuerung aller Ausgaenge stoppen 0x8A: Schiebedach verfahren 0x8B: Schiebedach heben 0x8C: Elektrischer Schiebehimmel verfahren 0x8D: Elektrischer Schiebehimmel heben Tabelle mit diesen un allen weiteren Werten anlegen |
| AKTION | int | 0: Vorgang abbrechen Bei 0x8A - 0x8D: 0% bis 100 % 0: vollstaendig offen 100: vollstaendig geschlossen Bitte Werte in Tabelle einpflegen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-shd"></a>
### STEUERN_SHD

Verfahren des Schiebedachs per Diagnose Ansteuerung bezieht sich auf die Eingangsseite

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_RICHTUNG | int | ARGUMENT aus table STEUERN_DIGITAL_VERFAHREN   ARGUMENT NAME BESCHREIBUNG 0x00: Alles abbrechen 0x80: SHD MAUT auf 0x81: SHD auf 0x82: SHD MAUT zu 0x83: SHD zu 0x84: SHD heben |
| AKTION | int | 0: Vorgang abbrechen Bei Maut schliessen, Maut oeffnen und heben 1: Vorgang starten Bei oeffnen und schliessen 1-xxxx: Ansteuerzeit in s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-esh"></a>
### STEUERN_ESH

Verfahren des elektrischen Schiebehimmels per Diagnose Ansteuerung bezieht sich auf die Eingangsseite

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_RICHTUNG | int | ARGUMENT aus table STEUERN_DIGITAL_VERFAHREN   ARGUMENT NAME BESCHREIBUNG 0x00: Alles Abbrechen 0x85: ESH MAUT auf 0x86: ESH auf 0x87: ESH MAUT zu 0x88: ESH zu 0x89: ESH heben |
| AKTION | int | 0: Vorgang abbrechen Bei Maut schliessen, Maut oeffnen und heben 1: Vorgang starten Bei oeffnen und schliessen 1-xxxx: Ansteuerzeit in s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mds-standalone"></a>
### STEUERN_MDS_STANDALONE

Stand-Alone Version des MDS aktivieren / Deaktivieren Bei aktiver Stand-Alone-Version ist keine Freigabe der Dachbewegung über CAN erforderlich nach ECU-Reset ist codierter Zustand wiederhergestellt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAND_ALONE_AKTIV | int | Steuert die StandAlone Version 0: StandAlone Version des MDS deaktivieren 1: StandAlone Version des MDS aktivieren |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-eks-shd"></a>
### STEUERN_EKS_SHD

Aktivieren oder deaktivieren des Einklemmschutzes fuer den Motor SHD Nach ECU-Reset ist der codierte Zustand wiederhergestellt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EKS_SHD_AKTIV | int | 0: Einklemmschutz des SHD deaktivieren 1: Einklemmschutz des SHD aktivieren |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-eks-esh"></a>
### STEUERN_EKS_ESH

Aktivieren oder deaktivieren des Einklemmschutzes uer den Motor ESH nach ECU-Reset ist codierter Zustand wiederhergestellt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EKS_SHD_AKTIV | int | 0: Einklemmschutz des ESH deaktivieren 1: Einklemmschutz des ESH aktivieren |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-temperaturmonitor-mds"></a>
### STATUS_TEMPERATURMONITOR_MDS

Gibt den Status des Temperaturmonitors des MDS zurueck Wertezuordnung bei Results: 0: nicht aktiv 1: aktiv

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEMPMON_SHD | int | Temperaturmonitor des SHD 0: nicht aktiv 1: aktiv |
| STAT_TEMPMON_ESH | int | Temperaturmonitor des ESH 0: nicht aktiv 1: aktiv |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-eks"></a>
### STATUS_EKS

Gibt Anzahl der Klemmungen und die letzte Klemmposition zurueck

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EKS_ZAEHL_SHD | int | Anzahl der Klemmungen fuer Motor SHD |
| STAT_EKS_POS_SHD | int | Position der letzten Klemmung fuer Motor SHD |
| STAT_EKS_ZAEHL_ESH | int | Anzahl der Klemmungen fuer Motor ESH |
| STAT_EKS_POS_ESH | int | Position der letzten Klemmung fuer Motor ESH |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-thermo-shd"></a>
### STEUERN_THERMO_SHD

Aktivieren oder deaktivieren des Thermoschutzes fuer den Motor SHD nach ECU-Reset ist codierter Zustand wiederhergestellt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| THERMO_SHD_AKTIV | int | 0: Thermoschutz des SHD deaktivieren 1: Thermoschutz des SHD aktivieren |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-thermo-esh"></a>
### STEUERN_THERMO_ESH

Aktivieren oder deaktivieren des Thermoschutzes fuer den Motor ESH nach ECU-Reset ist codierter Zustand wiederhergestellt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| THERMO_ESH_AKTIV | int | 0: Thermoschutz des ESH deaktivieren 1: Thermoschutz des ESH aktivieren |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-comfort-pos"></a>
### STEUERN_COMFORT_POS

Aktivieren oder deaktivieren des Anfahrens der Komfortposition nach ECU-Reset ist codierter Zustand wiederhergestellt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| COMFORTPOS_AKTIV | int | 0: Anfahren der Komfort-Position deaktivieren 1: Anfahren der Komfort-Position aktivieren |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-windabweiser"></a>
### STEUERN_WINDABWEISER

Ausfahren bzw. Einfahren des Windabweisers unabhängig von der Fahrzeuggeschwindigkeit nach ECU-Reset ist codierter Zustand wiederhergestellt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANTIWUMMER_AKTIV | int | 0: Ausfahren des Windabweisers deaktivieren 1: Ausfahren des Windabweisers aktivieren |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-eks-kennlinien"></a>
### STATUS_EKS_KENNLINIEN

Auslesen der gespeicherten Kennlinien fuer den Einklemmschutz  Bemerkungen: - Jeder "STAT_INKREMENT"-ten Motorposition wird ein 8Bit Stromsample zugeordnet. - Der erste Stromwert bezieht sich auf die "STAT_STARTPOS"-Position. - Aufloesung: 0 ... 15.9375 A in 62,5 mA Schritten. Jedes Datenbyte muss durch 16 dividiert werden, um eine Anzeige in Ampere zu bekommen.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MOTOR_ID | int | 0: Motor SHD 1: Motor ESH |
| KENNLINIEN_ID | int | Auswahl der Kennlinie 1: SchiebenSchließen 2: SchiebenÖffnen 3: Hubschließen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STARTPOS | int | u16 Startposisition der Kennlinie |
| STAT_INKREMENT | int | u8 Inkrement der Kennlinie |
| STAT_KENNLINIE_GROESSE | int | u16 Größe der Kennlinie in Byte |
| STAT_ANZ_SEGMENTE | int | Anzahl der Kennliniensegmente |
| STAT_KENNLINIE | binary | Kennliniendaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bedienkonzept"></a>
### STATUS_BEDIENKONZEPT

Job liefert Aussage, welche Schiebedachvariante verbaut ist Benoetigt fuer HELLA Prueflabor

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MDS_BEDIENKONZEPT_WERT | int | Art des verbauten Dachs 0: Panoramadach 1: Glashubdach 2: SchiebeHebeDach siehe auch Tabelle STAT_BEDIENKONZEPT_TAB |
| STAT_MDS_BEDIENKONZEPT_TEXT | string | siehe Tabelle STAT_BEDIENKONZEPT_TAB |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dwa"></a>
### _STATUS_DWA

Auslesen des DWA-Status Wertezuordnung bei Results: 0: nicht aktiv 1: aktiv

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DWA_WERT | int | StatusByte |
| STAT_DWA_TEXT | string | Zuordnung siehe Tabelle STATUS_DWA_TEXT  |
| STAT_DWA_ALARM | int | 0: Alarm inaktiv 1: Alarm aktiv |
| STAT_OPTISCHER_ALARM | int | 0: optischer Alarm inaktiv 1: optischer Alarm aktiv |
| STAT_AKUSTISCHER_ALARM | int | 0: akustischer Alarm inaktiv 1: akustischer Alarm aktiv |
| STAT_INNENRAUMSENSOR | int | 0: Innenraumsensor inaktiv 1: Innenraumsensor aktiv |
| STAT_NEIGUNGSSENSOR | int | 0: Neigungssensor inaktiv 1: Neigungssensor aktiv |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dwa-led"></a>
### STATUS_DWA_LED

Auslesen des Status der DWA-LED

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DWA_LED_WERT | int | 0: LED aus 1: LED ein 2: LED blinkt 3: LED blitzt |
| STAT_DWA_LED_TEXT | string | Zuordnung siehe Tabelle "STATUS_DWA_LED_STATE" |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-car-key-memory"></a>
### STATUS_CAR_KEY_MEMORY

Auslesen der CKM-Parameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_QUIT_OPTIC_ENTSCHAERFEN | int |  |
| STAT_QUIT_OPTIC_SCHAERFEN | int |  |
| STAT_QUIT_OPTIC_SCHAERFEN_KLAPPE | int |  |
| STAT_QUIT_AKUSTIC_ENTSCHAERFEN | int |  |
| STAT_QUIT_AKUSTIC_SCHAERFEN | int |  |
| STAT_QUIT_AKUSTIC_SCHAERFEN_KLAPPE | int |  |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dwa-alarmtrigger"></a>
### STATUS_DWA_ALARMTRIGGER

Auslesen des Status der Alarmtrigger Wertezuordnung bei Results: 0: nicht ausgeloest 1: ausgeloest

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FAT_AUSGEL | int | Status Alarmtrigger Fahrertür 0: nicht ausgeloest 1: ausgeloest |
| STAT_BFT_AUSGEL | int | Status Alarmtrigger Beifahrertür 0: nicht ausgeloest 1: ausgeloest |
| STAT_FATH_AUSGEL | int | Status Alarmtrigger Fahrertür hinten 0: nicht ausgeloest 1: ausgeloest |
| STAT_BFTH_AUSGEL | int | Status Alarmtrigger Beifahrertür hinten 0: nicht ausgeloest 1: ausgeloest |
| STAT_HK_AUSGEL | int | Status Alarmtrigger Heckklappe 0: nicht ausgeloest 1: ausgeloest |
| STAT_HS_AUSGEL | int | Status Alarmtrigger Heckscheibe 0: nicht ausgeloest 1: ausgeloest |
| STAT_MH_AUSGEL | int | Status Alarmtrigger Motorhaube 0: nicht ausgeloest 1: ausgeloest |
| STAT_NG_AUSGEL | int | Status Alarmtrigger Neigungsgeber 0: nicht ausgeloest 1: ausgeloest |
| STAT_IRS_AUSGEL | int | Status Alarmtrigger Ultraschall-Innenraumschutz 0: nicht ausgeloest 1: ausgeloest |
| STAT_KBUS_AUSGEL | int | Status Alarmtrigger KBUS-Manipulationsalarm 0: nicht ausgeloest 1: ausgeloest |
| STAT_DISTRIBUTION_AUSGEL | int | Status Alarmtrigger Distribution 0: nicht ausgeloest 1: ausgeloest |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dwa-intern"></a>
### STATUS_DWA_INTERN

Auslesen des Status der DWA-Applikation 0x00:  DWA entschärft 0x01:  DWA in Schärfung 0x02:  DWA geschärft 0x03:  DWA wird entschärft (not supported) 0x04:  DWA Alarm 0x05:  DWA Pause nach Alarm 0x06:  DWA Transport Mode 0x07:  DWA Werkstattmode 0x09:  DWA geschärft - IRS und Neigungssensor durch Benutzer deaktiviert 0x0A:  DWA geschärft - Distributionsmodus (not supported) 0x0B:  DWA Energiesparmode wird beendet (not supported) 0x0C:  DWA Powerdown Mode (not supported) 0x0D:  DWA Panik Alarm Mode 0x0E:  DWA geschärft - Hotelstellung aktiv 0x0F:  DWA geschärft - IRS & Neigungssensor nicht aktiv 0x10:  DWA geschärft - IRS nicht aktiv 0x11:  DWA geschärft - Neigungssensor nicht aktiv 0x12:  DWA Schnelltest aktiv

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DWA_INTERN_WERT | int | Status der DWA-Applikation Werte siehe Tabelle DWA_STATUS_INTERN_TAB |
| STAT_DWA_INTERN_TEXT | string | Status der DWA-Applikation Werte siehe Tabelle DWA_STATUS_INTERN_TAB |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-led"></a>
### STEUERN_DWA_LED

Setzen des Status der DWA-LED Voraussetzung: DWA ungeschärft Beendigungmöglichkeiten des Jobs: - Automatisch nach 2 Minuten - Schärfen der DWA - Parameter = 0

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERN_DWA_LED_WERT | int | 0: LED aus 1: LED ein 2: LED blinkt 3: LED blitzt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-schaerfen"></a>
### STEUERN_DWA_SCHAERFEN

Setzen des Status der DWA Ein Entschaerfen der DWA, die ueber CAN geschaerft wurde, ist nicht moeglich

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERN_DWA_WERT | int | 0: DWA entschärft 1: DWA geschärft |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sirene-ein-aus"></a>
### STEUERN_SIRENE_EIN_AUS

Setzen des Status der DWA-SINE

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERN_DWA_SINE_WERT | int | 0: SINE inaktiv 1: SINE aktiv |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-selftest"></a>
### STEUERN_DWA_SELFTEST

Perform an hardware selftest of the DWA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DWA_SELFTEST_GENERAL_WERT | int | 0: dwa ok (alle folgenden Tests ok) 1: dwa not ok (mindestens ein Test nich ok) |
| STAT_DWA_EXT_V_LEV_WERT | int | 0: DWA ext. V. level ok 15: Externe Batteriespannung &lt; 9V 19: Externe Batteriespannung &gt; 16V |
| STAT_DWA_LED_WERT | int | 0: DWA LED ok 13: DWA LED defekt |
| STAT_DWA_SELFTEST_GENERAL_TEXT | string | DWA Selftest Gesamtstatus |
| STAT_DWA_EXT_V_LEV_TEXT | string | 0: DWA ext. V. level ok 15: External Battery voltage &lt; 9V 19: External Battery voltage &gt; 16V |
| STAT_DWA_LED_TEXT | string | 0: DWA LED ok 13: DWA LED failure |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-schnelltest"></a>
### STEUERN_DWA_SCHNELLTEST

Aktiviert den DWA-Schnelltest Modus Sensoren werden geschaerft Nach der Referenzierung kann ein Alarm ausgelöst werden Tritt ein Alarm auf, so wird 2s lang ein Alarmton erzeugt Abbrechkriterien: - Ausführen dieses Jobs mit "0", "aus" oder "off" - Schärfen oder Entschärfen der DWa über CAN - Timeout von 5 Minuten Startkriterien: Ausführen des Jobs mit "1", "ein", "on" oder ohne Argument

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION | string | aus Tabelle DIGITAL_ARGUMENT wenn dieses Argument fehlt, wird der Job gestartet "ein", "on", "1", "": Job wird gestartet "aus", "off", "0": Job wird abgebrochen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dwa-schnelltest-leise"></a>
### STEUERN_DWA_SCHNELLTEST_LEISE

Aktiviert den DWA-Schnelltest Modus Sensoren werden geschaerft Nach der Referenzierung kann ein Alarm ausgelöst werden Tritt ein Alarm auf, so wird 2s lang ein Alarmton mit verringerter Lautstärke erzeugt Abbrechkriterien: - Ausführen dieses Jobs mit "0", "aus" oder "off" - Schärfen oder Entschärfen der DWa über CAN - Timeout von 5 Minuten Startkriterien: Ausführen des Jobs mit "1", "ein", "on" oder ohne Argument

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AKTION | string | aus Tabelle DIGITAL_ARGUMENT wenn dieses Argument fehlt, wird der Job gestartet "ein", "on", "1", "": Job wird gestartet "aus", "off", "0": Job wird abgebrochen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-k-bus-test"></a>
### STEUERN_K_BUS_TEST

Prüft die Kommunikation zur SINE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DWABUS_TEST_RESULT_WERT | int | 0: OK 1: Not OK |
| DWABUS_TEST_RESULT_TEXT | string | OK / Not OK |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG Testing communication to SINE Sensor |

<a id="job-status-innenlicht-leuchten"></a>
### STATUS_INNENLICHT_LEUCHTEN

gibt den Status der Innenlicht-Leuchten zurück Wertezuordnung bei Results: 0: Leuchte aus 1: Leuchte ein

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_INNENLICHT_WERT | int | zusammengefasster Status aller Leuchten |
| STAT_LESELICHT_RECHTS_VORNE | int | 0:	Leuchte aus 1:	Leuchte ein |
| STAT_LESELICHT_LINKS_VORNE | int | 0:	Leuchte aus 1:	Leuchte ein |
| STAT_INNENLICHT_VORNE | int | 0:	Leuchte aus 1:	Leuchte ein |
| STAT_LESELICHT_RECHTS_HINTEN | int | 0:	Leuchte aus 1:	Leuchte ein |
| STAT_LESELICHT_LINKS_HINTEN | int | 0:	Leuchte aus 1:	Leuchte ein |
| STAT_INNENLICHT_RECHTS_HINTEN | int | 0:	Leuchte aus 1:	Leuchte ein |
| STAT_INNENLICHT_LINKS_HINTEN | int | 0:	Leuchte aus 1:	Leuchte ein |
| STAT_MAKEUP_SPIEGELEUCHTEN_FREIGABE | int | 0:	Leuchte aus 1:	Leuchte ein |
| STAT_DIMMUNG_BACKLIGHTING | int | 0:	Leuchten aus 1-199:	Leuchten an, gedimmt 0.5%-Schritten 200:	Leuchten an, voll |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-innenlicht-taster"></a>
### STATUS_INNENLICHT_TASTER

gibt den Status der Innenlicht-Taster zurück Wertezuordnung bei Results: 0: Taster nicht gedrückt 1: Taster gedrückt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_IL_TASTER_WERT | int | zusammengefasster Status der Innenlicht-Taster Auswertung im Folgenden |
| STAT_TASTER_LESELICHT_VORNE_RECHTS | int | 0: 	nicht gedrückt 1:	gedrückt |
| STAT_TASTER_LESELICHT_VORNE_LINKS | int | 0: 	nicht gedrückt 1:	gedrückt |
| STAT_TASTER_INNENLICHT_VORNE | int | 0: 	nicht gedrückt 1:	gedrückt |
| STAT_TASTER_LESELICHT_HINTEN_RECHTS | int | 0: 	nicht gedrückt 1:	gedrückt |
| STAT_TASTER_LESELICHT_HINTEN_LINKS | int | 0: 	nicht gedrückt 1:	gedrückt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-innenlicht-leuchten"></a>
### _STEUERN_INNENLICHT_LEUCHTEN

Steuert den Zustand der Innenlicht-Leuchten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERN_INNENLICHT_AKTION | int | Auswahl, welche Aktion bei Innenlicht-Leuchten durchgeführt werden soll 0x00: ReturnControl2ECU 0x01: ShortTermAdjustment |
| STEUERN_LESELICHT_RECHTS_VORNE | int | 0:	Leuchte aus 1:	Leuchte an |
| STEUERN_LESELICHT_LINKS_VORNE | int | 0:	Leuchte aus 1:	Leuchte an |
| STEUERN_INNENLICHT_VORNE | int | 0:	Leuchte aus 1:	Leuchte an |
| STEUERN_LESELICHT_RECHTS_HINTEN | int | 0:	Leuchte aus 1:	Leuchte an |
| STEUERN_LESELICHT_LINKS_HINTEN | int | 0:	Leuchte aus 1:	Leuchte an |
| STEUERN_INNENLICHT_RECHTS_HINTEN | int | 0:	Leuchte aus 1:	Leuchte an |
| STEUERN_INNENLICHT_LINKS_HINTEN | int | 0:	Leuchte aus 1:	Leuchte an |
| STEUERN_MAKEUP_SPIEGELLEUCHTEN_FREIGABE | int | 0:	Leuchte aus 1:	Leuchte an |
| STEUERN_BACKLIGHTING | int | 0:	Leuchte aus 1-199:	Leuchte an, gedimmt 0.5%-Schritten 200:    Leuchte an, voll |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-innenlicht-taster"></a>
### STEUERN_INNENLICHT_TASTER

Steuert den Zustand der Innenlicht-Taster Job stellt Tastimpuls auf der Leitung per CAN nach

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERN_INNENLICHT_TASTER_AKTION | int | Auswahl, welche Aktion bei Innenlicht-Taster durchgeführt werden soll 0x00: ReturnControl2ECU 0x01: ShortTermAdjustment |
| STEUERN_IL_TASTER_LESELICHT_VORNE_RECHTS | int | 0:	Taster nicht betätigt 1:	Taster betätigt |
| STEUERN_IL_TASTER_LESELICHT_VORNE_LINKS | int | 0:	Taster nicht betätigt 1:	Taster betätigt |
| STEUERN_IL_TASTER_INNENLICHT_VORNE | int | 0:	Taster nicht betätigt 1:	Taster betätigt |
| STEUERN_IL_TASTER_LESELICHT_HINTEN_RECHTS | int | 0:	Taster nicht betätigt 1:	Taster betätigt |
| STEUERN_IL_TASTER_LESELICHT_HINTEN_LINKS | int | 0:	Taster nicht betätigt 1:	Taster betätigt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-digital-licht"></a>
### STEUERN_DIGITAL_LICHT

Ansteuerung der Innenlicht-Leuchten Verwendet Tabelle für ELEMENT: STEUERN_DIGITAL_LICHT Verwendete Tabelle für AKTION: DIGITAL_ARGUMENT Folgende Lichter werden gemeinsam geschaltet: Alle Innenlichter Die Makeup-Spiegelleuchten-Freigabe Diese Einschränkung ist Hardware-Abhängig

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ELEMENT | int | aus table STEUERN_DIGITAL_LICHT Verwendete Werte: 0x00: Rückgabe der Kontrolle an das SG(nicht in der Tabelle) 0x70: Alle Leuchten Dachhimmel 0x71: Alle Leuchten Innenlicht 0x74: Alle Leuchten Leselicht 0x75: Alle Leuchten Leselicht vorne 0x76: Leuchte Leselicht vorne links 0x77: Leuchte Leselicht vorne rechts 0x78: Leuchte Leselicht hinten alle 0x79: Leuchte Leselicht hinten links 0x7A: Leuchte Leselicht hinten rechts 0x7E: Leuchte Make-Up Spiegel rechts und links 0x80: Alle Leuchten Suchbeleuchtung, Ambiente Beleuchtung |
| AKTION | string | aus table DIGITAL_ARGUMENT Verwendete Werte: "ein": entsprechende Leuchten anschalten "aus": entsprechende Leuchten abschalten tbd: Rückgeben der Kontrolle an das SG |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen-parametriert"></a>
### _FS_LESEN_PARAMETRIERT

parametrierte Version des FS_LESEN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FaultMode | int | 0: Identified SAJ 1: Supported SAJ 2: Identified HEX 3: Supported HEX |
| STAT_GODTC | int | 0xFFFF: Alle Fehler aus allen Bereichen 0xFFFE: Nur Netzwerkfehler 0xFFFD: Nur Karosseriefehler 0xFFFC: Nur Fahrwerkfehler 0xFFFB: Nur Antriebsfehler |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-loeschen-parametriert"></a>
### _FS_LOESCHEN_PARAMETRIERT

Parametrierte Version des Jobs FS_LOESCHEN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GODTC | int | 0xFFFF: Alle Fehler aus allen Bereichen 0xFFFE: Nur Netzwerkfehler 0xFFFD: Nur Karosseriefehler 0xFFFC: Nur Fahrwerkfehler 0xFFFB: Nur Antriebsfehler oder: Angabe eines Einzelfehlers |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-loeschen-parametriert"></a>
### _IS_LOESCHEN_PARAMETRIERT

Parametrierte Version des Jobs IS_LOESCHEN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DTC_SPEC | int | 0: 		alle loeschen 1-0xFF:		Bestimmte Position loeschen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-mds-test"></a>
### _MDS_TEST

Jobvorlage

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-irs-alarmcounter"></a>
### STATUS_IRS_ALARMCOUNTER

Auslesen der Stati der Innenraum-Sensoren Ausgegeben werden die Anzahl der intern gespeicherten Alarme Das Zurücksetzen der Werte erfolgt über den Job STEUERN_IRS_ALARM_LEVELS_RESET

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ALARMCOUNTER_IRS_REAR | int | Anzahl der Alarme hinterer IRS |
| STAT_ALARMCOUNTER_IRS_FRONT | int | Anzahl der Alarme vorderer IRS |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-irs-alarm-levels"></a>
### STATUS_IRS_ALARM_LEVELS

Auslesen der letzten 10 Alarm-Levels Der ALARM_LEVEL_ARRAY_xxx identifiziert dabei einen Parameter Set Dieser Set wird von der Doppler-Erkennung zur Alarmerkennung genutzt Der Wert '0' bedeutet: Kein Alarm an dieser Stelle gespeichert Das Zurücksetzen der Werte erfolgt über den Job STEUERN_IRS_ALARM_LEVELS_RESET Mögliche Werte des jeweiligen Alarm-Level Eintrags sind: ALARM_LEVEL_ARRAY IRS inaktiv Normal Fenster / Dach offen Klimaanlage an Mögliche Werte des Alarm-Levels sind: Thermal levels VL = 0 -&gt; -40°C .. -15°C L  = 1 -&gt; -15°C .. + 5°C M  = 2 -&gt;  +5°C .. +45°C H  = 3 -&gt; +45°C .. +65°C VH = 4 -&gt; +65°C .. +85°C Hardware gain level _LO_GAIN = 0 -&gt; low _ML_GAIN = 1 -&gt; medium low _MH_GAIN = 2 -&gt; medium high _HI_GAIN = 3 -&gt; high Sensitivity

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ALARM_LEVEL_ARRAY_HINTEN_1 | int | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_ALARM_LEVEL_ARRAY_TEXT_HINTEN_1 | string | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_THERMAL_LEVEL_HINTEN_1 | int | Wertbedeutung siehe Jobinfo |
| STAT_HW_GAIN_LEVEL_HINTEN_1 | int | Wertbedeutung siehe Jobinfo |
| STAT_SENSITIVITY_HINTEN_1 | int | Wertbedeutung siehe Jobinfo |
| STAT_ALARM_LEVEL_ARRAY_HINTEN_2 | int | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_ALARM_LEVEL_ARRAY_TEXT_HINTEN_2 | string | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_THERMAL_LEVEL_HINTEN_2 | int | Wertbedeutung siehe Jobinfo |
| STAT_HW_GAIN_LEVEL_HINTEN_2 | int | Wertbedeutung siehe Jobinfo |
| STAT_SENSITIVITY_HINTEN_2 | int | Wertbedeutung siehe Jobinfo |
| STAT_ALARM_LEVEL_ARRAY_HINTEN_3 | int | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_ALARM_LEVEL_ARRAY_TEXT_HINTEN_3 | string | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_THERMAL_LEVEL_HINTEN_3 | int | Wertbedeutung siehe Jobinfo |
| STAT_HW_GAIN_LEVEL_HINTEN_3 | int | Wertbedeutung siehe Jobinfo |
| STAT_SENSITIVITY_HINTEN_3 | int | Wertbedeutung siehe Jobinfo |
| STAT_ALARM_LEVEL_ARRAY_HINTEN_4 | int | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_ALARM_LEVEL_ARRAY_TEXT_HINTEN_4 | string | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_THERMAL_LEVEL_HINTEN_4 | int | Wertbedeutung siehe Jobinfo |
| STAT_HW_GAIN_LEVEL_HINTEN_4 | int | Wertbedeutung siehe Jobinfo |
| STAT_SENSITIVITY_HINTEN_4 | int | Wertbedeutung siehe Jobinfo |
| STAT_ALARM_LEVEL_ARRAY_HINTEN_5 | int | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_ALARM_LEVEL_ARRAY_TEXT_HINTEN_5 | string | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_THERMAL_LEVEL_HINTEN_5 | int | Wertbedeutung siehe Jobinfo |
| STAT_HW_GAIN_LEVEL_HINTEN_5 | int | Wertbedeutung siehe Jobinfo |
| STAT_SENSITIVITY_HINTEN_5 | int | Wertbedeutung siehe Jobinfo |
| STAT_ALARM_LEVEL_ARRAY_HINTEN_6 | int | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_ALARM_LEVEL_ARRAY_TEXT_HINTEN_6 | string | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_THERMAL_LEVEL_HINTEN_6 | int | Wertbedeutung siehe Jobinfo |
| STAT_HW_GAIN_LEVEL_HINTEN_6 | int | Wertbedeutung siehe Jobinfo |
| STAT_SENSITIVITY_HINTEN_6 | int | Wertbedeutung siehe Jobinfo |
| STAT_ALARM_LEVEL_ARRAY_HINTEN_7 | int | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_ALARM_LEVEL_ARRAY_TEXT_HINTEN_7 | string | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_THERMAL_LEVEL_HINTEN_7 | int | Wertbedeutung siehe Jobinfo |
| STAT_HW_GAIN_LEVEL_HINTEN_7 | int | Wertbedeutung siehe Jobinfo |
| STAT_SENSITIVITY_HINTEN_7 | int | Wertbedeutung siehe Jobinfo |
| STAT_ALARM_LEVEL_ARRAY_HINTEN_8 | int | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_ALARM_LEVEL_ARRAY_TEXT_HINTEN_8 | string | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_THERMAL_LEVEL_HINTEN_8 | int | Wertbedeutung siehe Jobinfo |
| STAT_HW_GAIN_LEVEL_HINTEN_8 | int | Wertbedeutung siehe Jobinfo |
| STAT_SENSITIVITY_HINTEN_8 | int | Wertbedeutung siehe Jobinfo |
| STAT_ALARM_LEVEL_ARRAY_HINTEN_9 | int | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_ALARM_LEVEL_ARRAY_TEXT_HINTEN_9 | string | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_THERMAL_LEVEL_HINTEN_9 | int | Wertbedeutung siehe Jobinfo |
| STAT_HW_GAIN_LEVEL_HINTEN_9 | int | Wertbedeutung siehe Jobinfo |
| STAT_SENSITIVITY_HINTEN_9 | int | Wertbedeutung siehe Jobinfo |
| STAT_ALARM_LEVEL_ARRAY_HINTEN_10 | int | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_ALARM_LEVEL_ARRAY_TEXT_HINTEN_10 | string | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_THERMAL_LEVEL_HINTEN_10 | int | Wertbedeutung siehe Jobinfo |
| STAT_HW_GAIN_LEVEL_HINTEN_10 | int | Wertbedeutung siehe Jobinfo |
| STAT_SENSITIVITY_HINTEN_10 | int | Wertbedeutung siehe Jobinfo |
| STAT_ALARM_LEVEL_ARRAY_VORNE_1 | int | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_ALARM_LEVEL_ARRAY_TEXT_VORNE_1 | string | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_THERMAL_LEVEL_VORNE_1 | int | Wertbedeutung siehe Jobinfo |
| STAT_HW_GAIN_LEVEL_VORNE_1 | int | Wertbedeutung siehe Jobinfo |
| STAT_SENSITIVITY_VORNE_1 | int | Wertbedeutung siehe Jobinfo |
| STAT_ALARM_LEVEL_ARRAY_VORNE_2 | int | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_ALARM_LEVEL_ARRAY_TEXT_VORNE_2 | string | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_THERMAL_LEVEL_VORNE_2 | int | Wertbedeutung siehe Jobinfo |
| STAT_HW_GAIN_LEVEL_VORNE_2 | int | Wertbedeutung siehe Jobinfo |
| STAT_SENSITIVITY_VORNE_2 | int | Wertbedeutung siehe Jobinfo |
| STAT_ALARM_LEVEL_ARRAY_VORNE_3 | int | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_ALARM_LEVEL_ARRAY_TEXT_VORNE_3 | string | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_THERMAL_LEVEL_VORNE_3 | int | Wertbedeutung siehe Jobinfo |
| STAT_HW_GAIN_LEVEL_VORNE_3 | int | Wertbedeutung siehe Jobinfo |
| STAT_SENSITIVITY_VORNE_3 | int | Wertbedeutung siehe Jobinfo |
| STAT_ALARM_LEVEL_ARRAY_VORNE_4 | int | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_ALARM_LEVEL_ARRAY_TEXT_VORNE_4 | string | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_THERMAL_LEVEL_VORNE_4 | int | Wertbedeutung siehe Jobinfo |
| STAT_HW_GAIN_LEVEL_VORNE_4 | int | Wertbedeutung siehe Jobinfo |
| STAT_SENSITIVITY_VORNE_4 | int | Wertbedeutung siehe Jobinfo |
| STAT_ALARM_LEVEL_ARRAY_VORNE_5 | int | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_ALARM_LEVEL_ARRAY_TEXT_VORNE_5 | string | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_THERMAL_LEVEL_VORNE_5 | int | Wertbedeutung siehe Jobinfo |
| STAT_HW_GAIN_LEVEL_VORNE_5 | int | Wertbedeutung siehe Jobinfo |
| STAT_SENSITIVITY_VORNE_5 | int | Wertbedeutung siehe Jobinfo |
| STAT_ALARM_LEVEL_ARRAY_VORNE_6 | int | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_ALARM_LEVEL_ARRAY_TEXT_VORNE_6 | string | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_THERMAL_LEVEL_VORNE_6 | int | Wertbedeutung siehe Jobinfo |
| STAT_HW_GAIN_LEVEL_VORNE_6 | int | Wertbedeutung siehe Jobinfo |
| STAT_SENSITIVITY_VORNE_6 | int | Wertbedeutung siehe Jobinfo |
| STAT_ALARM_LEVEL_ARRAY_VORNE_7 | int | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_ALARM_LEVEL_ARRAY_TEXT_VORNE_7 | string | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_THERMAL_LEVEL_VORNE_7 | int | Wertbedeutung siehe Jobinfo |
| STAT_HW_GAIN_LEVEL_VORNE_7 | int | Wertbedeutung siehe Jobinfo |
| STAT_SENSITIVITY_VORNE_7 | int | Wertbedeutung siehe Jobinfo |
| STAT_ALARM_LEVEL_ARRAY_VORNE_8 | int | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_ALARM_LEVEL_ARRAY_TEXT_VORNE_8 | string | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_THERMAL_LEVEL_VORNE_8 | int | Wertbedeutung siehe Jobinfo |
| STAT_HW_GAIN_LEVEL_VORNE_8 | int | Wertbedeutung siehe Jobinfo |
| STAT_SENSITIVITY_VORNE_8 | int | Wertbedeutung siehe Jobinfo |
| STAT_ALARM_LEVEL_ARRAY_VORNE_9 | int | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_ALARM_LEVEL_ARRAY_TEXT_VORNE_9 | string | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_THERMAL_LEVEL_VORNE_9 | int | Wertbedeutung siehe Jobinfo |
| STAT_HW_GAIN_LEVEL_VORNE_9 | int | Wertbedeutung siehe Jobinfo |
| STAT_SENSITIVITY_VORNE_9 | int | Wertbedeutung siehe Jobinfo |
| STAT_ALARM_LEVEL_ARRAY_VORNE_10 | int | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_ALARM_LEVEL_ARRAY_TEXT_VORNE_10 | string | siehe Tabelle TAB_ALARMLEVELARRAY_IRS |
| STAT_THERMAL_LEVEL_VORNE_10 | int | Wertbedeutung siehe Jobinfo |
| STAT_HW_GAIN_LEVEL_VORNE_10 | int | Wertbedeutung siehe Jobinfo |
| STAT_SENSITIVITY_VORNE_10 | int | Wertbedeutung siehe Jobinfo |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-irs-false-wakeup-levels"></a>
### STATUS_IRS_FALSE_WAKEUP_LEVELS

Auslesen der letzten 10 Wakeup-Levels ohne Alarmauslösung D.h. der Doppler-Mode wurde aktiviviert ohne Alarm auszulösen Der Werte '0' bedeutet: Kein Alarm an dieser Stelle gespeichert Das Zurücksetzen der Werte erfolgt über den Job STEUERN_IRS_FALSE_WAKEUP_LEVELS_RESET

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANZ_FALSE_DOPPLER_HINTEN_1 | int | number of single unsuccessful doppler signal analysis |
| STAT_IDLE_WERT_HINTEN_1 | int | 0: kein Idle erkannt 1: Idle erkannt |
| STAT_ANZ_FALSE_DOPPLER_HINTEN_2 | int | number of single unsuccessful doppler signal analysis |
| STAT_IDLE_WERT_HINTEN_2 | int | 0: kein Idle erkannt 1: Idle erkannt |
| STAT_ANZ_FALSE_DOPPLER_HINTEN_3 | int | number of single unsuccessful doppler signal analysis |
| STAT_IDLE_WERT_HINTEN_3 | int | 0: kein Idle erkannt 1: Idle erkannt |
| STAT_ANZ_FALSE_DOPPLER_HINTEN_4 | int | number of single unsuccessful doppler signal analysis |
| STAT_IDLE_WERT_HINTEN_4 | int | 0: kein Idle erkannt 1: Idle erkannt |
| STAT_ANZ_FALSE_DOPPLER_HINTEN_5 | int | number of single unsuccessful doppler signal analysis |
| STAT_IDLE_WERT_HINTEN_5 | int | 0: kein Idle erkannt 1: Idle erkannt |
| STAT_ANZ_FALSE_DOPPLER_HINTEN_6 | int | number of single unsuccessful doppler signal analysis |
| STAT_IDLE_WERT_HINTEN_6 | int | 0: kein Idle erkannt 1: Idle erkannt |
| STAT_ANZ_FALSE_DOPPLER_HINTEN_7 | int | number of single unsuccessful doppler signal analysis |
| STAT_IDLE_WERT_HINTEN_7 | int | 0: kein Idle erkannt 1: Idle erkannt |
| STAT_ANZ_FALSE_DOPPLER_HINTEN_8 | int | number of single unsuccessful doppler signal analysis |
| STAT_IDLE_WERT_HINTEN_8 | int | 0: kein Idle erkannt 1: Idle erkannt |
| STAT_ANZ_FALSE_DOPPLER_HINTEN_9 | int | number of single unsuccessful doppler signal analysis |
| STAT_IDLE_WERT_HINTEN_9 | int | 0: kein Idle erkannt 1: Idle erkannt |
| STAT_ANZ_FALSE_DOPPLER_HINTEN_10 | int | number of single unsuccessful doppler signal analysis |
| STAT_IDLE_WERT_HINTEN_10 | int | 0: kein Idle erkannt 1: Idle erkannt |
| STAT_ANZ_FALSE_DOPPLER_VORNE_1 | int | number of single unsuccessful doppler signal analysis |
| STAT_IDLE_WERT_VORNE_1 | int | 0: kein Idle erkannt 1: Idle erkannt |
| STAT_ANZ_FALSE_DOPPLER_VORNE_2 | int | number of single unsuccessful doppler signal analysis |
| STAT_IDLE_WERT_VORNE_2 | int | 0: kein Idle erkannt 1: Idle erkannt |
| STAT_ANZ_FALSE_DOPPLER_VORNE_3 | int | number of single unsuccessful doppler signal analysis |
| STAT_IDLE_WERT_VORNE_3 | int | 0: kein Idle erkannt 1: Idle erkannt |
| STAT_ANZ_FALSE_DOPPLER_VORNE_4 | int | number of single unsuccessful doppler signal analysis |
| STAT_IDLE_WERT_VORNE_4 | int | 0: kein Idle erkannt 1: Idle erkannt |
| STAT_ANZ_FALSE_DOPPLER_VORNE_5 | int | number of single unsuccessful doppler signal analysis |
| STAT_IDLE_WERT_VORNE_5 | int | 0: kein Idle erkannt 1: Idle erkannt |
| STAT_ANZ_FALSE_DOPPLER_VORNE_6 | int | number of single unsuccessful doppler signal analysis |
| STAT_IDLE_WERT_VORNE_6 | int | 0: kein Idle erkannt 1: Idle erkannt |
| STAT_ANZ_FALSE_DOPPLER_VORNE_7 | int | number of single unsuccessful doppler signal analysis |
| STAT_IDLE_WERT_VORNE_7 | int | 0: kein Idle erkannt 1: Idle erkannt |
| STAT_ANZ_FALSE_DOPPLER_VORNE_8 | int | number of single unsuccessful doppler signal analysis |
| STAT_IDLE_WERT_VORNE_8 | int | 0: kein Idle erkannt 1: Idle erkannt |
| STAT_ANZ_FALSE_DOPPLER_VORNE_9 | int | number of single unsuccessful doppler signal analysis |
| STAT_IDLE_WERT_VORNE_9 | int | 0: kein Idle erkannt 1: Idle erkannt |
| STAT_ANZ_FALSE_DOPPLER_VORNE_10 | int | number of single unsuccessful doppler signal analysis |
| STAT_IDLE_WERT_VORNE_10 | int | 0: kein Idle erkannt 1: Idle erkannt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-irs-noise"></a>
### STATUS_IRS_NOISE

Gibt Maßzahl für das Störrauschen an Wird erreichnet aus dem Verhältnis Anzahl Echo mode / Anzahl Doppler Mode Berechnet als gleitender Mittelwert in Anzahl/Minute Das Zurücksetzen der Werte erfolgt über den Job STEUERN_IRS_NOISE_RESET

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NOISE_IRS_REAR | int | moving average, ratio of echo mode count / doppler mode count IRS hinten |
| STAT_NOISE_IRS_FRONT | int | moving average, ratio of echo mode count / doppler mode count IRS vorne |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sensor-empfindlichkeit"></a>
### STATUS_SENSOR_EMPFINDLICHKEIT

Liest die Empfindlichkeit der Innenraumsensoren aus 0x00:   Normal mode 0x01:   Window opened 0x02:   Roof opened 0x03:   Air condition/heater on

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_IRS_SENS_EMPFINDLICHKEIT | int | Wertbedeutung siehe Jobinfo |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sensor-empfindlichkeit"></a>
### STEUERN_SENSOR_EMPFINDLICHKEIT

Stellt die Empfindlichkeit der Innenraumsensoren ein Eingestellte Werte werden mit Entschärfen der DWA automatisch zurückgesetzt 0x00:   Normal mode 0x01:   Window opened 0x02:   Roof opened 0x03:   Air condition/heater on

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SENSOR_EMPFINDLICHKEIT | int | Wertbedeutung siehe Jobinfo |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-irs-selftest"></a>
### STEUERN_IRS_SELFTEST

Selbsttest der Innenraumschutz-Sensoren Dieser Job ist nur im ungeschärften Zustand der IRS ausführbar Es wird ein statischer Fehlercode zurückgegeben: 8:  defect detected - both channels 9:  defect detected - Channel Front(A) 10: defect detected - Channel Rear(B) 11: the internal usis selftest has passed, no defect detected

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SELFTEST_WERT | int | Werte von 0 - 255, Wertbedeutung siehe Jobinfo |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-irs-noise-reset"></a>
### STEUERN_IRS_NOISE_RESET

Noise-Level löschen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_IRS | int | waehlt aus, welche IRS-Kanal Werte zurückgesetzt werden sollen 0x01: Hinterer Kanal 0x02: Vorderer Kanal 0x03: beide Kanäle |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-irs-alarm-levels-reset"></a>
### STEUERN_IRS_ALARM_LEVELS_RESET

Löschen der letzten 10 Alarm-Level

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_IRS | int | waehlt aus, welche IRS-Kanal Werte zurückgesetzt werden sollen 0x01: Hinterer Kanal 0x02: Vorderer Kanal 0x03: beide Kanäle |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-irs-false-wakeup-levels-reset"></a>
### STEUERN_IRS_FALSE_WAKEUP_LEVELS_RESET

Löschen der letzen 10 False-Wakeup Level

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL_IRS | int | waehlt aus, welche IRS-Kanal Werte zurückgesetzt werden sollen 0x01: Hinterer Kanal 0x02: Vorderer Kanal 0x03: beide Kanäle |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Auftragstelegramm an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (4 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (77 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [HARTTEXTE](#table-harttexte) (14 × 2)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (2 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (77 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [HORTTEXTE](#table-horttexte) (27 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [HUMWELTMATRIX](#table-humweltmatrix) (1 × 5)
- [HUMWELTTEXTE](#table-humwelttexte) (32 × 9)
- [IORTTEXTE](#table-iorttexte) (54 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [AUTOINIT_MDS_STATUS_TEXT](#table-autoinit-mds-status-text) (4 × 2)
- [STATUS_DWA_TEXT](#table-status-dwa-text) (4 × 2)
- [STATUS_MDS_BK_SCHALTER_TAB](#table-status-mds-bk-schalter-tab) (7 × 3)
- [STATUS_DWA_LED_STATE](#table-status-dwa-led-state) (5 × 2)
- [STEUERN_DIGITAL_SHD_TAB](#table-steuern-digital-shd-tab) (6 × 3)
- [STATUS_FETRAWE_TAB](#table-status-fetrawe-tab) (5 × 2)
- [STAT_RESETGRUND_TAB](#table-stat-resetgrund-tab) (15 × 2)
- [DWA_STATUS_INTERN_TAB](#table-dwa-status-intern-tab) (19 × 2)
- [DWA_SYSTEM_SELFTEST_TAB](#table-dwa-system-selftest-tab) (22 × 2)
- [DWA_SENSOR_EMPFINDLICHKEIT_TAB](#table-dwa-sensor-empfindlichkeit-tab) (9 × 2)
- [DATUM](#table-datum) (1 × 5)
- [HISTORY](#table-history) (1 × 17)
- [POSITIONEN](#table-positionen) (1 × 11)
- [LAENGE_FT](#table-laenge-ft) (14 × 2)
- [LAENGE_BFT](#table-laenge-bft) (14 × 2)
- [LAENGE_FTH](#table-laenge-fth) (14 × 2)
- [LAENGE_BFTH](#table-laenge-bfth) (14 × 2)
- [LAENGE_SHD](#table-laenge-shd) (14 × 2)
- [LAENGE_SHD2](#table-laenge-shd2) (12 × 2)
- [TEMPERATURE](#table-temperature) (33 × 2)
- [TAB_USIS_ERROR](#table-tab-usis-error) (1 × 2)
- [TAB_ALARMLEVELARRAY_IRS](#table-tab-alarmlevelarray-irs) (5 × 2)
- [STAT_BEDIENKONZEPT_TAB](#table-stat-bedienkonzept-tab) (4 × 2)
- [STEUERN_DIGITAL_LICHT_TAB](#table-steuern-digital-licht-tab) (15 × 5)
- [STEUERN_DIGITAL_VERFAHREN](#table-steuern-digital-verfahren) (12 × 3)
- [SHD_EINLERNEN](#table-shd-einlernen) (3 × 2)
- [FZD_SPEICHERSEGMENT](#table-fzd-speichersegment) (12 × 3)

<a id="table-konzept-tabelle"></a>
### KONZEPT_TABELLE

Dimensions: 4 rows × 2 columns

| NR | KONZEPT_TEXT |
| --- | --- |
| 0x0F | BMW-FAST |
| 0x0D | KWP2000* |
| 0x0C | KWP2000 |
| 0x06 | DS2 |

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 95 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x10 | ERROR_ECU_GENERAL_REJECT |
| 0x11 | ERROR_ECU_SERVICE_NOT_SUPPORTED |
| 0x12 | ERROR_ECU_SUBFUNCTION_NOT_SUPPORTED__INVALID_FORMAT |
| 0x21 | ERROR_ECU_BUSY_REPEAT_REQUEST |
| 0x22 | ERROR_ECU_CONDITIONS_NOT_CORRECT_OR_REQUEST_SEQUENCE_ERROR |
| 0x23 | ERROR_ECU_ROUTINE_NOT_COMPLETE |
| 0x31 | ERROR_ECU_REQUEST_OUT_OF_RANGE |
| 0x33 | ERROR_ECU_SECURITY_ACCESS_DENIED__SECURITY_ACCESS_REQUESTED |
| 0x36 | ERROR_ECU_EXCEED_NUMBER_OF_ATTEMPTS |
| 0x37 | ERROR_ECU_REQUIRED_TIME_DELAY_NOT_EXPIRED |
| 0x40 | ERROR_ECU_DOWNLOAD_NOT_ACCEPTED |
| 0x41 | ERROR_ECU_IMPROPER_DOWNLOAD_TYPE |
| 0x42 | ERROR_ECU_CANNOT_DOWNLOAD_TO_SPECIFIED_ADDRESS |
| 0x43 | ERROR_ECU_CANNOT_DOWNLOAD_NUMBER_OF_BYTES_REQUESTED |
| 0x50 | ERROR_ECU_UPLOAD_NOT_ACCEPTED |
| 0x51 | ERROR_ECU_IMPROPER_UPLOAD_TYPE |
| 0x52 | ERROR_ECU_CANNOT_UPLOAD_FROM_SPECIFIED_ADDRESS |
| 0x53 | ERROR_ECU_CANNOT_UPLOAD_NUMBER_OF_BYTES_REQUESTED |
| 0x71 | ERROR_ECU_TRANSFER_SUSPENDED |
| 0x72 | ERROR_ECU_TRANSFER_ABORTED |
| 0x74 | ERROR_ECU_ILLEGAL_ADDRESS_IN_BLOCK_TRANSFER |
| 0x75 | ERROR_ECU_ILLEGAL_BYTE_COUNT_IN_BLOCK_TRANSFER |
| 0x76 | ERROR_ECU_ILLEGAL_BLOCK_TRANSFER_TYPE |
| 0x77 | ERROR_ECU_BLOCKTRANSFER_DATA_CHECKSUM_ERROR |
| 0x78 | ERROR_ECU_REQUEST_CORRECTLY_RECEIVED__RESPONSE_PENDING |
| 0x79 | ERROR_ECU_INCORRECT_BYTE_COUNT_DURING_BLOCK_TRANSFER |
| 0x80 | ERROR_ECU_SERVICE_NOT_SUPPORTED_IN_ACTIVE_DIAGNOSTIC_MODE |
| ?00? | OKAY |
| ?02? | ERROR_ECU_INCORRECT_RESPONSE_ID |
| ?03? | ERROR_ECU_INCORRECT_LEN |
| ?04? | ERROR_ECU_INCORRECT_LIN_RESPONSE_ID |
| ?05? | ERROR_ECU_INCORRECT_LIN_LEN |
| ?10? | ERROR_F_CODE |
| ?11? | ERROR_TABLE |
| ?12? | ERROR_INTERPRETATION |
| ?13? | ERROR_F_POS |
| ?20? | ERROR_SEGMENT |
| ?21? | ERROR_ADDRESS |
| ?22? | ERROR_NUMBER |
| ?30? | ERROR_DATA |
| ?40? | ERROR_MODE |
| ?41? | ERROR_BAUDRATE |
| ?50? | ERROR_BYTE1 |
| ?51? | ERROR_BYTE2 |
| ?52? | ERROR_BYTE3 |
| ?60? | ERROR_DATA_OUT_OF_RANGE |
| ?70? | ERROR_NUMBER_ARGUMENT |
| ?71? | ERROR_RANGE_ARGUMENT |
| ?72? | ERROR_VERIFY |
| ?73? | ERROR_NO_BIN_BUFFER |
| ?74? | ERROR_BIN_BUFFER |
| ?75? | ERROR_DATA_TYPE |
| ?76? | ERROR_CHECKSUM |
| ?80? | ERROR_FLASH_SIGNATURE_CHECK |
| ?81? | ERROR_VIHICLE_IDENTFICATON_NR |
| ?82? | ERROR_PROGRAMMING_DATE |
| ?83? | ERROR_ASSEMBLY_NR |
| ?84? | ERROR_CALIBRATION_DATASET_NR |
| ?85? | ERROR_EXHAUST_REGULATION_OR_TYPE_APPROVAL_NR |
| ?86? | ERROR_REPAIR_SHOP_NR |
| ?87? | ERROR_TESTER_SERIAL_NR |
| ?88? | ERROR_MILAGE |
| ?89? | ERROR_PROGRAMMING_REFERENCE |
| ?8A? | ERROR_NO_FREE_UIF |
| ?8B? | ERROR_MAX_UIF |
| ?8C? | ERROR_SIZE_UIF |
| ?8D? | ERROR_LEVEL |
| ?8E? | ERROR_KEY |
| ?8F? | ERROR_AUTHENTICATION |
| ?90? | ERROR_NO_DREF |
| ?91? | ERROR_CHECK_PECUHN |
| ?92? | ERROR_CHECK_PRGREF |
| ?93? | ERROR_AIF_NR |
| ?94? | ERROR_CHECK_DREF |
| ?95? | ERROR_CHECK_HWREF |
| ?96? | ERROR_CHECK_HWREF |
| ?97? | ERROR_CHECK_PRGREFB |
| ?98? | ERROR_CHECK_VMECUH*NB |
| ?99? | ERROR_CHECK_PRGREFB |
| ?9A? | ERROR_CHECK_VMECUH*N |
| ?9B? | ERROR_MOST_CAN_GATEWAY_DISABLE |
| ?9C? | ERROR_NO_P2MIN |
| ?9D? | ERROR_NO_P2MAX |
| ?9E? | ERROR_NO_P3MIN |
| ?9F? | ERROR_NO_P3MAX |
| ?A0? | ERROR_NO_P4MIN |
| ?B0? | ERROR_DIAG_PROT |
| ?B1? | ERROR_SG_ADRESSE |
| ?B2? | ERROR_SG_MAXANZAHL_AIF |
| ?B3? | ERROR_SG_GROESSE_AIF |
| ?B4? | ERROR_SG_ENDEKENNUNG_AIF |
| ?B5? | ERROR_SG_AUTHENTISIERUNG |
| ?C0? | ERROR_TELEGRAM_LEN_OUT_OFF_RANGE |
| ?F0? | ERROR_ARGUMENT |
| 0xXY | ERROR_ECU_UNKNOWN_NEGATIVE_RESPONSE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 77 rows × 2 columns

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
| 0xFF | unbekannter Hersteller |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 14 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | kein passendes Fehlersymptom |
| 0x01 | Signal oder Wert oberhalb Schwelle |
| 0x02 | Signal oder Wert unterhalb Schwelle |
| 0x04 | kein Signal oder Wert |
| 0x08 | unplausibles Signal oder Wert |
| 0x10 | Testbedingungen erfüllt |
| 0x11 | Testbedingungen noch nicht erfüllt |
| 0x20 | Fehler bisher nicht aufgetreten |
| 0x21 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x22 | Fehler momentan vorhanden, aber noch nicht gespeichert (Entprellphase) |
| 0x23 | Fehler momentan vorhanden und bereits gespeichert |
| 0x30 | Fehler würde kein Aufleuchten einer Warnlampe verursachen |
| 0x31 | Fehler würde das Aufleuchten einer Warnlampe verursachen |
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

<a id="table-authentisierung"></a>
### AUTHENTISIERUNG

Dimensions: 4 rows × 2 columns

| AUTH_NR | AUTH_TEXT |
| --- | --- |
| 0x01 | Simple |
| 0x02 | Symetrisch |
| 0x03 | Asymetrisch |
| 0xFF | Keine |

<a id="table-diagmode"></a>
### DIAGMODE

Dimensions: 14 rows × 3 columns

| NR | MODE | MODE_TEXT |
| --- | --- | --- |
| 0x81 | DEFAULT | DefaultMode |
| 0x82 | PT | PeriodicTransmissions |
| 0x84 | EOLSSM | EndOfLineSystemSupplierMode |
| 0x85 | ECUPM | ECUProgrammingMode |
| 0x86 | ECUDM | ECUDevelopmentMode |
| 0x87 | ECUAM | ECUAdjustmentMode |
| 0x88 | ECUVCM | ECUVariantCodingMode |
| 0x89 | ECUSM | ECUSafetyMode |
| 0xFA | SSS_A | SystemSupplierSpecific (A) |
| 0xFB | SSS_B | SystemSupplierSpecific (B) |
| 0xFC | SSS_C | SystemSupplierSpecific (C) |
| 0xFD | SSS_D | SystemSupplierSpecific (D) |
| 0xFE | SSS_E | SystemSupplierSpecific (E) |
| 0xXY | -- | unbekannter Diagnose-Mode |

<a id="table-baudrate"></a>
### BAUDRATE

Dimensions: 7 rows × 3 columns

| NR | BAUD | BAUD_TEXT |
| --- | --- | --- |
| 0x01 | PC9600 | Baudrate 9.6 kBaud |
| 0x02 | PC19200 | Baudrate 19.2 kBaud |
| 0x03 | PC38400 | Baudrate 38.4 kBaud |
| 0x04 | PC57600 | Baudrate 57.6 kBaud |
| 0x05 | PC115200 | Baudrate 115.2 kBaud |
| 0x06 | SB | Specific Baudrate |
| 0xXY | -- | unbekannte Baudrate |

<a id="table-harttexte"></a>
### HARTTEXTE

Dimensions: 14 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | kein passendes Fehlersymptom |
| 0x01 | Signal oder Wert oberhalb Schwelle |
| 0x02 | Signal oder Wert unterhalb Schwelle |
| 0x04 | kein Signal oder Wert |
| 0x08 | unplausibles Signal oder Wert |
| 0x10 | Testbedingungen erfüllt |
| 0x11 | Testbedingungen noch nicht erfüllt |
| 0x20 | Fehler bisher nicht aufgetreten |
| 0x21 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x22 | Fehler momentan vorhanden, aber noch nicht gespeichert (Entprellphase) |
| 0x23 | Fehler momentan vorhanden und bereits gespeichert |
| 0x30 | Fehler würde kein Aufleuchten einer Warnlampe verursachen |
| 0x31 | Fehler würde das Aufleuchten einer Warnlampe verursachen |
| 0xFF | unbekannte Fehlerart |

<a id="table-iarttexte"></a>
### IARTTEXTE

Dimensions: 14 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | kein passendes Fehlersymptom |
| 0x01 | Signal oder Wert oberhalb Schwelle |
| 0x02 | Signal oder Wert unterhalb Schwelle |
| 0x04 | kein Signal oder Wert |
| 0x08 | unplausibles Signal oder Wert |
| 0x10 | Testbedingungen erfüllt |
| 0x11 | Testbedingungen noch nicht erfüllt |
| 0x20 | Fehler bisher nicht aufgetreten |
| 0x21 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x22 | Fehler momentan vorhanden, aber noch nicht gespeichert (Entprellphase) |
| 0x23 | Fehler momentan vorhanden und bereits gespeichert |
| 0x30 | Fehler würde kein Aufleuchten einer Warnlampe verursachen |
| 0x31 | Fehler würde das Aufleuchten einer Warnlampe verursachen |
| 0xFF | unbekannte Fehlerart |

<a id="table-programmierstatus"></a>
### PROGRAMMIERSTATUS

Dimensions: 19 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | Anlieferzustand |
| 0x01 | Normalbetrieb |
| 0x02 | nicht benutzt |
| 0x03 | Speicher gelöscht |
| 0x04 | nicht benutzt |
| 0x05 | Signaturprüfung PAF nicht durchgeführt |
| 0x06 | Signaturprüfung DAF nicht durchgeführt |
| 0x07 | Programmprogrammiersitzung aktiv |
| 0x08 | Datenprogrammiersitzung aktiv |
| 0x09 | Hardwarereferenzeintrag fehlerhaft |
| 0x0A | Programmreferenzeintrag fehlerhaft |
| 0x0B | Referenzierungsfehler Hardware -&gt; Programm |
| 0x0C | Programm nicht vorhanden oder nicht vollständig |
| 0x0D | Datenreferenzeintrag fehlerhaft |
| 0x0E | Referenzierungsfehler Programm -&gt; Daten |
| 0x0F | Daten nicht vorhanden oder nicht vollständig |
| 0x10 | Reserviert fuer BMW |
| 0x80 | Reserviert fuer Zulieferer |
| 0xXY | unbekannter Programmierstatus |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 2 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| ?F0? | Error_Argument |
| 0xXY | ERROR_UNKNOWN |

<a id="table-sg-diagnosekonzept"></a>
### SG_DIAGNOSEKONZEPT

Dimensions: 4 rows × 2 columns

| RANG | KONZEPT_TEXT |
| --- | --- |
| 1 | BMW-FAST |
| - | KWP2000* |
| - | KWP2000 |
| - | DS2 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 77 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9500 | SHD Hall A Puls fehlt 0x9500 |
| 0x9501 | SHD Hall B Puls fehlt 0x9501 |
| 0x9502 | SHD Hallsensor B unplausibel 0x9502 |
| 0x9503 | SHD Motorbrücke steuert nicht an 0x9503 |
| 0x9504 | SHD Illegale Motoransteuerung 0x9504 |
| 0x9506 | SHD Motorklemmenspannung unplausibel 0x9506 |
| 0x9507 | SHD Ausfall von U_bat während der Bewegung 0x9507 |
| 0x9508 | SHD ungültige Dachposition 0x9508 |
| 0x9509 | SHD Kennlinie Schiebebereich ungültig 0x9509 |
| 0x950A | SHD Kennlinie Hebebereich ungültig 0x950A |
| 0x950B | SHD Checksummenfehler Parametrierung 0x950B |
| 0x950C | SHD Kurzschluss Hall Sensor A 0x950C |
| 0x950D | SHD Kurzschluss Hall Sensor B 0x950D |
| 0x9540 | SHD Manuelle Dachbewegung 0x9540 |
| 0x9541 | SHD Aktivierung der SKB 0x9541 |
| 0x9542 | SHD Temperatur Monitor Startverhinderung 0x9542 |
| 0x9543 | SHD Temperatur Monitor Abbruch 0x9543 |
| 0x9600 | ESH Hall A Puls fehlt 0x9600 |
| 0x9601 | ESH  Hall B Puls fehlt 0x9601 |
| 0x9602 | ESH Hallsensor B unplausibel 0x9602 |
| 0x9603 | ESH  Motorbrücke steuert nicht an 0x9603 |
| 0x9604 | ESH Illegale Motoransteuerung 0x9604 |
| 0x9606 | ESH Motorklemmenspannung unplausibel 0x9606 |
| 0x9607 | ESH Ausfall von U_bat während der Bewegung 0x9607 |
| 0x9608 | ESH ungültige Dachposition 0x9608 |
| 0x9609 | ESH Kennlinie Schiebebereich ungültig 0x9609 |
| 0x960A | ESH Kennlinie Hebebereich ungültig 0x960A |
| 0x960B | ESH Checksummenfehler Parametrierung 0x960B |
| 0x960C | ESH Kurzschluss Hallsensor A 0x960C |
| 0x960D | ESH Kurzschluss Hallsensor B 0x960D |
| 0x9640 | ESH  Manuelle Dachbewegung 0x9640 |
| 0x9641 | ESH  Aktivierung der SKB 0x6941 |
| 0x9642 | ESH Temperatur Monitor Startverhinderung 0x9642 |
| 0x9643 | ESH Temperatur Monitor Abbruch 0x9643 |
| 0x9D0C | DWA BUS DWA-Bus-Leitungsfehler, Kurzschluss gegen KL30 oder gegen GND |
| 0xA088 | Bedienschalter SHD unzulaessige Kombination der 3 Schaltereingaenge |
| 0xA08D | Codierung inkonsistent, d.h. Checksumme falsch 0xA08D |
| 0xA090 | SHD Mechanik schwergängig 0xA090 |
| 0xA091 | SHD Motor, Kabelbaum und Elektronik 0xA091 |
| 0xA092 | SHD Normierung 0xA092 |
| 0xA0A0 | ESH Mechanik schwergängig 0xA0A0 |
| 0xA0A1 | ESH  Motor, Kabelbaum und Elektronik 0xA0A1 |
| 0xA0A2 | ESH  Normierung 0xA0A2 |
| 0xA40D | EEPROM Schreibfehler |
| 0xA668 | Lichtfunktion Fehler Leselicht rechts |
| 0xA669 | Lichtfunktion Fehler Innenlicht |
| 0xA66A | Lichtfunktion Fehler Leselicht links |
| 0xA66B | Lichtfunktion Fehler MakeUp Beleuchtung |
| 0xA66C | Lichtfunktion Fehler Leselicht rechts Fond |
| 0xA66D | Lichtfunktion Fehler Leselicht links Fond |
| 0xA66E | Lichtfunktion Fehler Innenlicht Fond Rechts |
| 0xA66F | BSS Fehler Kurzschluss Sensorversorgung BSS 0xA66F |
| 0xA670 | BSS Fehler Signalleitung BSS 0xA670 |
| 0xA671 | Taster SHD haengt |
| 0xA672 | Taster Innenlicht haengt |
| 0xA673 | Taster Leselicht links haengt |
| 0xA674 | Taster Leselicht rechts haengt |
| 0xA675 | Taster Innenlicht Fond haengt |
| 0xA676 | Taster Leselicht Fond links haengt |
| 0xA677 | Taster Leselicht Fond rechts haengt |
| 0xA678 | Lichtfunktion Fehler Innenlicht Fond Links |
| 0xA679 | EC-Spiegel Analogsignal außerhalb des zulässigen Bereiches 0xA679 |
| 0xA67A | RAM-Fehler entdeckt |
| 0xA67B | ROM-Fehler entdeckt |
| 0xA682 | Fehler Haltegriffbeleuchtung |
| 0xA683 | Versorgungsspannung RLSS |
| 0xA685 | EC-Spiegel, Kurzschluß S_REF |
| 0xA687 | Energiesparmode aktiv |
| 0xDE84 | CAN Leitungsfehler |
| 0xDE87 | CAN Kommunikationsfehler |
| 0xDE88 | Bus LIN Leitungsfehler 0xDE88 |
| 0xDE8B | Bus LIN Kommunikationsfehler zum RLSS 0xDE8B |
| 0xDE8C | Bus LIN Protokollfehler |
| 0x9CEC | DWA defekt: Ultraschall-Sensorik defekt |
| 0x9D00 | Sirene Kommunikationsfehler |
| 0x9CF9 | DWA-LED Fehler |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | nein |
| F_UWB_ERW | nein |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 27 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9315 | Reserve |
| 0x9316 | Reserve |
| 0x9317 | Alarm Klappenkontakt Motorhaube |
| 0x9318 | Alarm Klappenkontakt Kofferraum |
| 0x9319 | Alarm Klappenkontakt Fahrertür vorne |
| 0x931A | Alarm Klappenkontakt Beifahrertür vorne |
| 0x931B | Alarm Klappenkontakt Fahrertür hinten |
| 0x931C | Alarm Klappenkontakt Beifahrertür hinten |
| 0x931D | Alarm Reifenstechen |
| 0x931E | Alarm Leitungsüberwachung DWA-Bus |
| 0x931F | Alarm Manipulation Authentisierung |
| 0x9320 | Alarm Bordcomputer |
| 0x9321 | Alarm Klappenkontakt Heckscheibe |
| 0x9322 | Alarm Manipulation DWa-Bus |
| 0x9323 | Alarm Distribution |
| 0x9324 | Panikalarm |
| 0x9325 | Alarm Ultraschall vorne |
| 0x9326 | Alarm Ultraschall hinten |
| 0x9327 | Alarm Ultraschall vorne und hinten |
| 0x9328 | Alarm Neigungssensor Neigung X-Achse |
| 0x9329 | Alarm Neigungssensor Neigung Y-Achse |
| 0x932A | Alarm Neigungssensor Neigung X/Y-Achse |
| 0x932B | Alarm Sirene, Unterbrechung Spannungsversorgung |
| 0x932C | Alarm DWA-Bus, Kurzschluß nach 12V |
| 0x932D | Alarm DWA-Bus, Kurzschluß nach Masse |
| 0x932E | Alarm DWA-Bus, kein Telegramm absetzbar |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-hdetailstruktur"></a>
### HDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | nein |
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-humweltmatrix"></a>
### HUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | HISTORY | DATUM | POSITIONEN | - |

<a id="table-humwelttexte"></a>
### HUMWELTTEXTE

Dimensions: 32 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Datum | Monat | - | unsigned char | - | 1 | 1 | 0 |
| 0x02 | Datum | Tag | - | unsigned char | - | 1 | 1 | 0 |
| 0x03 | Datum | Stunden | - | unsigned char | - | 1 | 1 | 0 |
| 0x04 | Datum | Minuten | - | unsigned char | - | 1 | 1 | 0 |
| 0x05 | Fensterposition Fahrertuer vorne | 0-n | - | 0xf0000000 | LAENGE_FT | - | 1 | - |
| 0x06 | Fensterposition Beifahrertuer vorne | 0-n | - | 0x0f000000 | LAENGE_BFT | - | 1 | - |
| 0x07 | Fensterposition Fahrertuer hinten | 0-n | - | 0x00f00000 | LAENGE_FTH | - | 1 | - |
| 0x08 | Fensterposition Beifahrertuer hinten | 0-n | - | 0x000f0000 | LAENGE_BFTH | - | 1 | - |
| 0x09 | Schiebedachposition | 0-n | - | 0x00000f00 | LAENGE_SHD | - | 1 | - |
| 0x0a | Schiebedach Neigung | 0-n | - | 0x0000f000 | LAENGE_SHD2 | - | 1 | - |
| 0x0b | Aussentemperatur | 0-n | - | 0x0000001f | TEMPERATURE | - | 1 | - |
| 0x0c | Status Standklima /-heizung | 0/1 | - | 0x00000020 | - | - | 1 | - |
| 0x0d | Status Standlueften | 0/1 | - | 0x00000040 | - | - | 1 | - |
| 0x0e | Status Standgeblaese | 0/1 | - | 0x00000080 | - | - | 1 | - |
| 0x11 | Fahrertuer vorne | 0/1 | high | 0x0001 | - | - | 1 | - |
| 0x12 | Fahrertuer hinten | 0/1 | high | 0x0002 | - | - | 1 | - |
| 0x13 | Beifahrertuer vorne | 0/1 | high | 0x0004 | - | - | 1 | - |
| 0x14 | Beifahrertuer hinten | 0/1 | high | 0x0008 | - | - | 1 | - |
| 0x15 | Motorhaube | 0/1 | high | 0x0010 | - | - | 1 | - |
| 0x16 | Heckklappe | 0/1 | high | 0x0020 | - | - | 1 | - |
| 0x17 | Ultraschall Innenraumschutz | 0/1 | high | 0x0040 | - | - | 1 | - |
| 0x18 | Neigungsgeber | 0/1 | high | 0x0080 | - | - | 1 | - |
| 0x19 | Leitungsueberwachung | 0/1 | high | 0x0100 | - | - | 1 | - |
| 0x1a | Authentisierung | 0/1 | high | 0x0200 | - | - | 1 | - |
| 0x1b | DWA-Bus Manipulation | 0/1 | high | 0x0400 | - | - | 1 | - |
| 0x1c | Reifenstechen | 0/1 | high | 0x0800 | - | - | 1 | - |
| 0x1d | Distributionsmode | 0/1 | high | 0x1000 | - | - | 1 | - |
| 0x1e | Heckscheibenkontakt | 0/1 | high | 0x2000 | - | - | 1 | - |
| 0x1f | Unbekannter Alarmtrigger 2 | 0/1 | high | 0x4000 | - | - | 1 | - |
| 0x20 | Unbekannter Alarmtrigger 3 | 0/1 | high | 0x8000 | - | - | 1 | - |
| 0xFF | ohne Bedeutung | 1 | - | unsigned char | - | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 54 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9401 | Letzter Reset wurde durch Watchdog ausgelöst |
| 0x9402 | System: ungueltiger OP-Code erkannt |
| 0x9405 | System: FZD Temperatur außerhalb des erlaubten Bereiches |
| 0x9440 | Allgemein: Aktivierung des Panik-Modes |
| 0x9441 | Allgemein: Anzahl der manuellen Initialisierungen |
| 0x9442 | Allgemein: Anzahl der Autoinits |
| 0x9443 | Allgemein: Initialisierung nicht vollständig durchgeführt |
| 0x9444 | Allgemein: Unterspannung, Ubatt 500 ms lang kleiner als 9 V |
| 0x9445 | Allgemein: Ueberspannung, UBatt 500 ms lang größer als 16,5 V |
| 0x9447 | System: Anzahl der Codierungen |
| 0x9448 | System: Anzahl der ungueltigen Codierungen |
| 0x9500 | Motor SHD: Hall A Impuls fehlt |
| 0x9501 | Motor SHD: Hall B Impuls fehlt |
| 0x9502 | Motor SHD: Hallsensor B unplausibel |
| 0x9503 | Motor SHD: Motorbruecke steuert nicht an |
| 0x9504 | Motor SHD: illegale Motoransteuerung |
| 0x9505 | Motor SHD: Motor Kurzschluss |
| 0x9506 | Motor SHD: Motorklemmenspannung unplausibel |
| 0x9507 | Motor SHD: Ausfall von UBatt waehrend der Bewegung |
| 0x9508 | Motor SHD: Ungueltige Dachposition |
| 0x9509 | Motor SHD: Kennlinie Schiebebereich ungueltig |
| 0x950A | Motor SHD: Kennlinie Hebebereich ungueltig |
| 0x950B | Motor SHD: Checksummenfehler Parametrierung |
| 0x950C | Motor SHD: Kurzschluss Hall Sensor A |
| 0x950D | Motor SHD: Kurzschluss Hall Sensor B |
| 0x9540 | Motor SHD: Manuelle Dachbewegung |
| 0x9541 | Motor SHD: Aktivierung der SKB |
| 0x9542 | Motor SHD: Temperatur Monitor Startverhinderung |
| 0x9543 | Motor SHD: Temperatur Monitor Abbruch |
| 0x9600 | Motor ESH: Hall A Impuls fehlt |
| 0x9601 | Motor ESH: Hall B Impuls fehlt |
| 0x9602 | Motor ESH: Hallsensor B unplausibel |
| 0x9603 | Motor ESH: Motorbruecke steuert nicht an |
| 0x9604 | Motor ESH: illegale Motoransteuerung |
| 0x9605 | Motor ESH: Motor Kurzschluss |
| 0x9606 | Motor ESH: Motorklemmenspannung unplausibel |
| 0x9607 | Motor ESH: Ausfall von UBatt waehrend der Bewegung |
| 0x9608 | Motor ESH: Ungueltige Dachposition |
| 0x9609 | Motor ESH: Kennlinie Schiebebereich ungueltig |
| 0x960A | Motor ESH: Kennlinie Hebebereich ungueltig |
| 0x960B | Motor ESH: Checksummenfehler Parametrierung |
| 0x960C | Motor ESH: Kurzschluss Hall Sensor A |
| 0x960D | Motor ESH: Kurzschluss Hall Sensor B |
| 0x9640 | Motor ESH: Manuelle Dachbewegung |
| 0x9641 | Motor ESH: Aktivierung der SKB |
| 0x9642 | Motor ESH: Temperatur Monitor Startverhinderung |
| 0x9643 | Motor ESH: Temperatur Monitor Abbruch |
| 0x9308 | Ultraschall-Sensorik vorn, unplausibles Signal |
| 0x9309 | Ultraschall-Sensorik hinten, umplausibles Signal |
| 0x930A | Klappenkontakt fehlerhaft |
| 0x9314 | Innenraumsensor / Neigungssensor deaktiviert durch Funkschluessel |
| 0xC904 | Weckgrund: FZD hat geweckt |
| 0xC905 | Weckgrund: FZD wurde geweckt |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | nein |
| F_UWB_ERW | nein |

<a id="table-autoinit-mds-status-text"></a>
### AUTOINIT_MDS_STATUS_TEXT

Dimensions: 4 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0x01 | AutoInit abgeschlossen |
| 0x02 | AutoInit läuft |
| 0xFF | AutoInit Fehler |
| 0xyz | Fehler in Tabelle |

<a id="table-status-dwa-text"></a>
### STATUS_DWA_TEXT

Dimensions: 4 rows × 2 columns

| CODE | TEXT |
| --- | --- |
| 0x01 | DWA entschärft |
| 0x02 | DWA in Schärfung |
| 0x04 | DWA geschärft |
| 0xFF | Fehler in Tabelle |

<a id="table-status-mds-bk-schalter-tab"></a>
### STATUS_MDS_BK_SCHALTER_TAB

Dimensions: 7 rows × 3 columns

| CODE | OUTPUT | BESCHREIBUNG |
| --- | --- | --- |
| 0x00 | 0x00 | Nichts gedrückt |
| 0x01 | 0x01 | MDS auf |
| 0x02 | 0x02 | MDS zu |
| 0x04 | 0x04 | MDS heben |
| 0x11 | 0x11 | MAUT auf |
| 0x12 | 0x12 | MAUT zu |
| 0xFF |  | Fehler in  Tabelle |

<a id="table-status-dwa-led-state"></a>
### STATUS_DWA_LED_STATE

Dimensions: 5 rows × 2 columns

| CODE | TEXT |
| --- | --- |
| 0x00 | DWA-LED aus |
| 0x01 | DWA-LED ein |
| 0x02 | DWA-LED blinkt |
| 0x03 | DWA-LED blitzt |
| 0xFF | Fehler in Tabelle |

<a id="table-steuern-digital-shd-tab"></a>
### STEUERN_DIGITAL_SHD_TAB

Dimensions: 6 rows × 3 columns

| CODE | ANFORDERUNG | BESCHREIBUNG |
| --- | --- | --- |
| 0x00 | Stopp | Allle Aktionen stoppen |
| 0x8A | SHD verfahren | Schiebedach verfahren |
| 0x8B | SHD heben | Schiebedach heben |
| 0x8C | ESH verfahren | Elektrischen Schiebehimmel verfahren |
| 0x8D | ESH heben | Elektrischen Schiebehimmel heben |
| 0xFF |  | Fehler in Tabelle |

<a id="table-status-fetrawe-tab"></a>
### STATUS_FETRAWE_TAB

Dimensions: 5 rows × 2 columns

| CODE | TEXT |
| --- | --- |
| 0x00 | kein Energiesparmodus aktiv |
| 0x01 | Fertigungsmodus aktiv |
| 0x02 | Transportmodus aktiv |
| 0x04 | Werkstattmodus aktiv |
| 0xFF | Fehler |

<a id="table-stat-resetgrund-tab"></a>
### STAT_RESETGRUND_TAB

Dimensions: 15 rows × 2 columns

| CODE | TEXT |
| --- | --- |
| 0x00 | unbekannt / nicht definiert |
| 0x13 | Hardware Reset |
| 0x21 | Interner µC Watchdog Reset |
| 0x30 | Software Task Watchdog -&gt; Diagnose Task |
| 0x31 | Software Task Watchdog -&gt; Fault Manager Task |
| 0x32 | Software Task Watchdog -&gt; Operating Manager Task |
| 0x33 | Software Task Watchdog -&gt; Non Volatile Manager Task (Eeprom Handling) |
| 0x34 | Software Task Watchdog -&gt; DAS Task (Dach Antriebs Steuerung) |
| 0x35 | Software Task Watchdog -&gt; DWA Task (Diebstahlwarnanlage) |
| 0x40 | Software Reset Request |
| 0x46 | Software Reset Bootloader |
| 0x49 | Software Reset -&gt; Unexpected Fault Bootloader |
| 0x4a | Software Reset -&gt; unexpected Fault Application |
| 0x50 | Stack Watchdog Reset |
| 0xFF | Fehler in Tabelle |

<a id="table-dwa-status-intern-tab"></a>
### DWA_STATUS_INTERN_TAB

Dimensions: 19 rows × 2 columns

| CODE | TEXT |
| --- | --- |
| 0x00 | DWA entschärft |
| 0x01 | DWA in Schärfung |
| 0x02 | DWA geschärft |
| 0x03 | DWA wird entschärft |
| 0x04 | DWA Alarm |
| 0x05 | DWA Pause nach Alarm |
| 0x06 | DWA Transport Mode |
| 0x07 | DWA Werkstattmode |
| 0x09 | DWA geschärft - ohne Sensoren |
| 0x0A | DWA geschärft - Distributionsmodus |
| 0x0B | DWA Energiesparmode wird beendet |
| 0x0C | DWA Powerdown Mode |
| 0x0D | DWA Panik Alarm Mode |
| 0x0E | DWA geschärft - Hotelstellung aktiv |
| 0x0F | DWA geschärft - IRS & Neigungssensor nicht aktiv |
| 0x10 | DWA geschärft - IRS nicht aktiv |
| 0x11 | DWA geschärft - Neigungssensor nicht aktiv |
| 0x12 | DWA Schnelltest aktiv |
| 0xFF | Fehler in Tabelle |

<a id="table-dwa-system-selftest-tab"></a>
### DWA_SYSTEM_SELFTEST_TAB

Dimensions: 22 rows × 2 columns

| CODE | TEXT |
| --- | --- |
| 0x00 | ok |
| 0x01 | DWA nicht in Ordnung |
| 0x06 | DWA ROM Checksumme fehlerhaft |
| 0x07 | DWA RAM Hardware Fehler |
| 0x08 | DWA Sound Short Circuit failure |
| 0x09 | DWA Sound Open Circuit failure |
| 0x0A | DWA Sound Circuit failure |
| 0x0B | DWA Fehler interne Batterie |
| 0x0D | DWA LED fehlerhaft |
| 0x0E | DWA ADXL Neigungsgeber fehlerhaft |
| 0x0F | External Battery voltage &lt; 9V |
| 0x10 | DWA Protection Circuit VS Filter defect |
| 0x11 | DWA Protection Circuit Sense defekt |
| 0x12 | DWA Protection Circuit external battery_switch off defect |
| 0x13 | External Battery Voltage &gt; 16V |
| 0x14 | DWA Wake UP Circuit failure |
| 0x3C | EEPROM addressing failure |
| 0x3D | EEPROM access timeout |
| 0x3E | EEPROM write failure |
| 0x3F | EEPROM test failure |
| 0x40 | EEPROM read failure |
| 0xFF | Fehler in Tabelle |

<a id="table-dwa-sensor-empfindlichkeit-tab"></a>
### DWA_SENSOR_EMPFINDLICHKEIT_TAB

Dimensions: 9 rows × 2 columns

| CODE | TEXT |
| --- | --- |
| 0x00 | Min |
| 0x01 | 1 |
| 0x02 | 2 |
| 0x03 | 3 |
| 0x04 | 4 |
| 0x05 | 5 |
| 0x06 | 6 |
| 0x07 | Max |
| 0xFF | Fehler |

<a id="table-datum"></a>
### DATUM

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x01 | 0x02 | 0x03 | 0x04 |

<a id="table-history"></a>
### HISTORY

Dimensions: 1 rows × 17 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR | UW13_NR | UW14_NR | UW15_NR | UW16_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 16 | 0x11 | 0x12 | 0x13 | 0x14 | 0x15 | 0x16 | 0x17 | 0x18 | 0x19 | 0x1a | 0x1b | 0x1c | 0x1d | 0x1e | 0x1f | 0x20 |

<a id="table-positionen"></a>
### POSITIONEN

Dimensions: 1 rows × 11 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 10 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0a | 0x0b | 0x0c | 0x0d | 0x0e |

<a id="table-laenge-ft"></a>
### LAENGE_FT

Dimensions: 14 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000000 | geschlossen |
| 0x10000000 | 4cm geoeffnet |
| 0x20000000 | 8cm geoeffnet |
| 0x30000000 | 12cm geoeffnet |
| 0x40000000 | 16cm geoeffnet |
| 0x50000000 | 20cm geoeffnet |
| 0x60000000 | 24cm geoeffnet |
| 0x70000000 | 28cm geoeffnet |
| 0x80000000 | 32cm geoeffnet |
| 0x90000000 | 36cm geoeffnet |
| 0xa0000000 | 40cm geoeffnet |
| 0xb0000000 | 44cm geoeffnet |
| 0xc0000000 | 48cm geoeffnet |
| 0xXY | unplausibel |

<a id="table-laenge-bft"></a>
### LAENGE_BFT

Dimensions: 14 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000000 | geschlossen |
| 0x01000000 | 4cm geoeffnet |
| 0x02000000 | 8cm geoeffnet |
| 0x03000000 | 12cm geoeffnet |
| 0x04000000 | 16cm geoeffnet |
| 0x05000000 | 20cm geoeffnet |
| 0x06000000 | 24cm geoeffnet |
| 0x07000000 | 28cm geoeffnet |
| 0x08000000 | 32cm geoeffnet |
| 0x09000000 | 36cm geoeffnet |
| 0x0a000000 | 40cm geoeffnet |
| 0x0b000000 | 44cm geoeffnet |
| 0x0c000000 | 48cm geoeffnet |
| 0xXY | unplausibel |

<a id="table-laenge-fth"></a>
### LAENGE_FTH

Dimensions: 14 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x000000 | geschlossen |
| 0x100000 | 4cm geoeffnet |
| 0x200000 | 8cm geoeffnet |
| 0x300000 | 12cm geoeffnet |
| 0x400000 | 16cm geoeffnet |
| 0x500000 | 20cm geoeffnet |
| 0x600000 | 24cm geoeffnet |
| 0x700000 | 28cm geoeffnet |
| 0x800000 | 32cm geoeffnet |
| 0x900000 | 36cm geoeffnet |
| 0xa00000 | 40cm geoeffnet |
| 0xb00000 | 44cm geoeffnet |
| 0xc00000 | 48cm geoeffnet |
| 0xXY | unplausibel |

<a id="table-laenge-bfth"></a>
### LAENGE_BFTH

Dimensions: 14 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x000000 | geschlossen |
| 0x010000 | 4cm geoeffnet |
| 0x020000 | 8cm geoeffnet |
| 0x030000 | 12cm geoeffnet |
| 0x040000 | 16cm geoeffnet |
| 0x050000 | 20cm geoeffnet |
| 0x060000 | 24cm geoeffnet |
| 0x070000 | 28cm geoeffnet |
| 0x080000 | 32cm geoeffnet |
| 0x090000 | 36cm geoeffnet |
| 0x0a0000 | 40cm geoeffnet |
| 0x0b0000 | 44cm geoeffnet |
| 0x0c0000 | 48cm geoeffnet |
| 0xXY | unplausibel |

<a id="table-laenge-shd"></a>
### LAENGE_SHD

Dimensions: 14 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | geschlossen |
| 0x0100 | 4cm geoeffnet |
| 0x0200 | 8cm geoeffnet |
| 0x0300 | 12cm geoeffnet |
| 0x0400 | 16cm geoeffnet |
| 0x0500 | 20cm geoeffnet |
| 0x0600 | 24cm geoeffnet |
| 0x0700 | 28cm geoeffnet |
| 0x0800 | 32cm geoeffnet |
| 0x0900 | 36cm geoeffnet |
| 0x0a00 | 40cm geoeffnet |
| 0x0b00 | 44cm geoeffnet |
| 0x0c00 | 48cm geoeffnet |
| 0xXY | unplausibel |

<a id="table-laenge-shd2"></a>
### LAENGE_SHD2

Dimensions: 12 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | geschlossen |
| 0x1000 | 2cm geoeffnet |
| 0x2000 | 4cm geoeffnet |
| 0x3000 | 6cm geoeffnet |
| 0x4000 | 8cm geoeffnet |
| 0x5000 | 10cm geoeffnet |
| 0x6000 | 12cm geoeffnet |
| 0x7000 | 14cm geoeffnet |
| 0x8000 | 16cm geoeffnet |
| 0x9000 | 18cm geoeffnet |
| 0xa000 | 20cm geoeffnet |
| 0xXY | unplausibel |

<a id="table-temperature"></a>
### TEMPERATURE

Dimensions: 33 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | -40 Grad Celsius |
| 0x01 | -36 Grad Celsius |
| 0x02 | -32 Grad Celsius |
| 0x03 | -28 Grad Celsius |
| 0x04 | -24 Grad Celsius |
| 0x05 | -20 Grad Celsius |
| 0x06 | -16 Grad Celsius |
| 0x07 | -12 Grad Celsius |
| 0x08 | -8 Grad Celsius |
| 0x09 | -4 Grad Celsius |
| 0x0a | 0 Grad Celsius |
| 0x0b | 4 Grad Celsius |
| 0x0c | 8 Grad Celsius |
| 0x0d | 12 Grad Celsius |
| 0x0e | 16 Grad Celsius |
| 0x0f | 20 Grad Celsius |
| 0x10 | 24 Grad Celsius |
| 0x11 | 28 Grad Celsius |
| 0x12 | 32 Grad Celsius |
| 0x13 | 36 Grad Celsius |
| 0x14 | 40 Grad Celsius |
| 0x15 | 44 Grad Celsius |
| 0x16 | 48 Grad Celsius |
| 0x17 | 52 Grad Celsius |
| 0x18 | 56 Grad Celsius |
| 0x19 | 60 Grad Celsius |
| 0x1a | 64 Grad Celsius |
| 0x1b | 68 Grad Celsius |
| 0x1c | 72 Grad Celsius |
| 0x1d | 76 Grad Celsius |
| 0x1e | 80 Grad Celsius |
| 0x1f | 84 Grad Celsius |
| 0xXY | unplausibel |

<a id="table-tab-usis-error"></a>
### TAB_USIS_ERROR

Dimensions: 1 rows × 2 columns

| CODE | TEXT |
| --- | --- |
| 0xFF | unbekannter Fehler |

<a id="table-tab-alarmlevelarray-irs"></a>
### TAB_ALARMLEVELARRAY_IRS

Dimensions: 5 rows × 2 columns

| CODE | TEXT |
| --- | --- |
| 0x00 | IRS inaktiv |
| 0x01 | normal |
| 0x02 | Fenster / Dach offen |
| 0x03 | Klimaanlage an |
| 0xFF | Fehler |

<a id="table-stat-bedienkonzept-tab"></a>
### STAT_BEDIENKONZEPT_TAB

Dimensions: 4 rows × 2 columns

| CODE | TEXT |
| --- | --- |
| 0x00 | Panoramadach |
| 0x01 | Glashubdach |
| 0x02 | SchiebeHebeDach |
| 0xFF | Fehler in Tabelle |

<a id="table-steuern-digital-licht-tab"></a>
### STEUERN_DIGITAL_LICHT_TAB

Dimensions: 15 rows × 5 columns

| ARGUMENT | NAME | BESCHREIBUNG | BITMASKE LEUCHTEN | BITMASKE AMBIENT |
| --- | --- | --- | --- | --- |
| 0x70 | DACHHIMMEL_ALLE | Alle Leuchten Dachhimmel | 0xFF | 0xC8 |
| 0x71 | INNENLICHT_ALLE | Alle Leuchten Innenlicht | 0x64 | 0x00 |
| 0x74 | LESELICHT_ALLE | Alle Leuchten Leselicht | 0x1B | 0x00 |
| 0x75 | LESELICHT_FRONT_ALLE | Alle Leuchten Leselicht vorne | 0x03 | 0x00 |
| 0x76 | LESELICHT_FRONT_LINKS | Leuchte Leselicht vorne links | 0x02 | 0x00 |
| 0x77 | LESELICHT_FRONT_RECHTS | Leuchte Leselicht vorne rechts | 0x01 | 0x00 |
| 0x78 | LESELICHT_FOND_ALLE | Alle Leuchten Leselicht hinten | 0x18 | 0x00 |
| 0x79 | LESELICHT_FOND_LINKS | Leuchte Leselicht hinten links | 0x10 | 0x00 |
| 0x7A | LESELICHT_FOND_RECHTS | Leuchte Leselicht hinten rechts | 0x08 | 0x00 |
| 0x7B | HECKLEUCHTE | HeckLeuchte | 0x00 | 0x00 |
| 0x7C | GEPAECKRAUMLEUCHTE | Gepaeckraumleuchte | 0x00 | 0x00 |
| 0x7D | HANDSCHUHFACHLEUCHTE | Leuchte Handschuhfach | 0x00 | 0x00 |
| 0x7E | MAKEUP_RECHTS | Leuchte Make-Up Spiegel links und rechts | 0x80 | 0x00 |
| 0x80 | SUCHBEL_AMBIENT | Alle Leuchten Suchbeleuchtung,  Ambiente Beleuchtung | 0x00 | 0xC8 |
| 0xFF | FEHLER | Argument nicht gefunden | 0x00 | 0x00 |

<a id="table-steuern-digital-verfahren"></a>
### STEUERN_DIGITAL_VERFAHREN

Dimensions: 12 rows × 3 columns

| ARGUMENT | NAME | BESCHREIBUNG |
| --- | --- | --- |
| 0x00 | Vorgang Abbrechen | Vorgang Abbrechen |
| 0x80 | SHD_MAUT_AUF | Schiebedach Maut oeffnen |
| 0x81 | SHD_AUF | Schiebedach oeffnen |
| 0x82 | SHD_MAUT_ZU | Schiebedach Maut schliessen |
| 0x83 | SHD_ZU | Schiebedach schliessen |
| 0x84 | SHD_HEBEN | Schiebedach heben |
| 0x85 | ESH_MAUT_AUF | Elektrischer Schiebehimmel Maut oeffnen |
| 0x86 | ESH_AUF | Elektrischer Schiebehimmel oeffnen |
| 0x87 | ESH_MAUT_ZU | Elektrischer Schiebehimmel Maut schliessen |
| 0x88 | ESH_ZU | Elektrischer Schiebehimmel schliessen |
| 0x89 | ESH_HEBEN | Elektrischer Schiebehimmel heben |
| 0xFF | FEHLER | Fehler passiert, nur für Auswertung der Tabelle |

<a id="table-shd-einlernen"></a>
### SHD_EINLERNEN

Dimensions: 3 rows × 2 columns

| CODE | BESCHREIBUNG |
| --- | --- |
| 0x00 | Vorgang abgebrochen |
| 0x01 | Vorgang gestartet |
| 0x02 | Vorgang vollendet |

<a id="table-fzd-speichersegment"></a>
### FZD_SPEICHERSEGMENT

Dimensions: 12 rows × 3 columns

| SEG_BYTE | SEG_NAME | SEG_TEXT |
| --- | --- | --- |
| 0x00 | LAR | linearAdressRange |
| 0x01 | ROMI | ROM / EPROM, internal |
| 0x02 | ROMX | ROM / EPROM, external |
| 0x03 | NVRAM | NV-RAM (characteristic zones, DTC memory |
| 0x04 | RAMIS | RAM, internal (short MOV) |
| 0x05 | RAMXX | RAM, external (x data MOV) |
| 0x06 | FLASH | Flash EPROM, internal |
| 0x07 | UIFM | User Info Field Memory |
| 0x08 | VODM | Vehicle Order Data Memory |
| 0x09 | FLASHX | Flash EPROM, external |
| 0x0B | RAMIL | RAM, internal (long MOV / Register) |
| 0xFF | ??? | unbekanntes Speichersegment |
