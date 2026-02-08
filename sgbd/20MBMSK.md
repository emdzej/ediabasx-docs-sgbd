# 20MBMSK.prg

- Jobs: [120](#jobs)
- Tables: [39](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | mrbmsk |
| ORIGIN | BMW EA-92 Modispacher |
| REVISION | 6.100 |
| AUTHOR | Askon Consulting EE-22 Mougin, BMW EE-22 Britze, S&S GmbH EE-22 Klepp, BMW EE-22 Kirmayer, IST GmbH EA-41 Ulbricht, IST GmbH EA-41 Breuer |
| COMMENT | nur KWP2000 |
| PACKAGE | 1.35 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [DIAGNOSEPROTOKOLL_LESEN](#job-diagnoseprotokoll-lesen) - Gibt die möglichen Diagnoseprotokolle für eine Auswahl an den Aufrufer zurück
- [DIAGNOSEPROTOKOLL_SETZEN](#job-diagnoseprotokoll-setzen) - Wählt ein Diagnoseprotokoll aus
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default
- [FS_LESEN_DETAIL](#job-fs-lesen-detail) - Fehlerspeicher lesen (ein Fehler / alle Details) KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus: Default
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : Default
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels KWP2000: $22 ReadDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [NORMALER_DATENVERKEHR](#job-normaler-datenverkehr) - Sperren bzw. Freigeben des normalen Datenverkehrs KWP2000: $28 DisableNormalMessageTransmission KWP2000: $29 EnableNormalMessageTransmission Modus  : Default
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode des SG aufrecht erhalten KWP2000: $3E TesterPresent Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
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
- [AIF_SCHREIBEN](#job-aif-schreiben) - Schreiben des Anwender Informations Feldes Standard Flashjob KWP 2000: $3D WriteMemoryByAddress Modus   : Default
- [STEUERN_ABS_LOESCHEN](#job-steuern-abs-loeschen) - Auftrag: KWP2000 :   $31 StartRoutineByLocalIdentifier Request Service Id $2F inputOutputLocalIdentifier "B_abs ruecksetzen" Auftrag2: KWP2000 :   $22     ReadDataByCommonIdentifier $40 $00 RecordCommonIdentifier "Meßwerte lesen"  Überprüfung der Motordrehzahl mittels Auftrag2 wenn Drehzahl = 0 , Bedingung ABS-SG ist/war verbaut (B_abs) wird zurückgesetzt Bedingung B_abs wird gesetzt sofern eine entsprechende CAN-Message vom ABS-SG empfangen wurde
- [STATUS_ADAPTIONSWERTE](#job-status-adaptionswerte) - KWP2000 :   $21 ReadDataByLocalIdentifier Request Service Id $0B recordLocalIdentifier "Adaptionswerte_lesen"  Adaptionswerte: ABS     (ABS-SG verbaut(=1)/nicht verbaut(=0)) LOWBAT  (UB liegt zw. 6 und 7 V (=1) und fuehrt zu Einschraenkungen beim Ansteuern des Anlassers) SPERREKP(EKP,Zünd./Einsp. & Anlasser gesperrt(=1) über Tester) DKPA    (Drosselklappe im Nullanschlag) GANGAN  (Getriebepoti in Neutralstellung) GANGA1  (Stellung Getriebepoti 1.Gang) GANGA2  (Stellung Getriebepoti 2.Gang) GANGA3  (Stellung Getriebepoti 3.Gang) GANGA4  (Stellung Getriebepoti 4.Gang) GANGA5  (Stellung Getriebepoti 5.Gang) GANGA6  (Stellung Getriebepoti 6.Gang)
- [STEUERN_ADAPTIONSWERTE_LOESCHEN](#job-steuern-adaptionswerte-loeschen) - KWP2000 :   $31 StartRoutineByLocalIdentifier Request Service Id $E9 inputOutputLocalIdentifier "Adaptionswerte löschen"  sofern die Motordrehzahl = 0 ist, wird nach Abschluß der aktuellen Kommunikation ein Reset ausgelöst, währenddessen die Adaptionswerte gelöscht und beim Hochfahren wieder initialisiert werden
- [STATUS_AUSGAENGE_DIGITAL](#job-status-ausgaenge-digital) - KWP2000:    $22     ReadDataByCommonIdentifier $40 $05 RecordCommonIdentifier "Ausgänge prüfen"  Ausgänge:   UETMC ( Kontrollleuchte Motortemperatur, 1=aktiv 0=inaktiv) ANLASSER ( Ansteuerung Anlasserrelais, 1=aktiv 0=inaktiv) AKL ( Akustikklappe, 1=offen 0=geschlossen=nicht verbaut) SLV1 ( Sekundärluftventil, 1=offen 0=geschlossen) TEV ( Taktventil Tankentlüftung, 1=offen 0=geschlossen) EKPBTS ( Kraftstoffpumpe, 1=läuft 0=läuft nicht) ELUE1 ( E-Lüfter, 1=läuft 0=läuft nicht) MIL ( Motornotlauf, 1=Notlauf 0=kein Notlauf) HSV ( Lambdasondenheizung 1, 1=aktiv 0=inaktiv) HSV2 ( Lambdasondenheizung 2, 1=aktiv 0=inaktiv) B_A_SCHUTZ ( Anlasserschutz, 1=aktiv 0=inaktiv löst Sicherheitsabschaltung aus) B_FRGANL ( Anlasser Freigabe, 1=freigegeben 0=nicht freigegeben) B_MOTORSTP ( Motor Abschalten, 1=aktiv 0=inaktiv)
- [STATUS_FUNKTIONSSTATI](#job-status-funktionsstati) - KWP2000:    $22     ReadDataByCommonIdentifier $40 $07 RecordCommonIdentifier "Funktionsstati lesen"  Funktionsstati: LL (Bedingung Leerlauf, 1=aktiv 0=inaktiv gesetzt wenn sich Motor im Leerlauf befindet) VL (Bedingung Vollast, 1=Vollast 0=keine Vollast gesetzt wenn: - Bedingung Leerlauf inaktiv und - drehzahlabhängiger Drosselklappenwinkel gegeben ist) TEHB (Bedingung Tankentlüftung mit hoher Beladung 1=aktiv 0=inaktiv, Beladung=HC-Konzentration im Regeneriergasstrom(aus Tankentlüftung) SA (Bedingung Schubabschalten, 1=aktiv 0=inaktiv Abschaltung Einspritzung, Zündung, EKP u.a., um vorhandenes positives Drehmoment(Schub) auf Null zu reduzieren wenn keine Drehmomentanforderung mehr besteht SBBVK (Bedingung Sonde betriebsbereit vor Kat 1=betriebsbereit 0=nicht betriebsbereit) BM (Zylinder-1 Erkennung, 1=erkannt 0=nicht erkannt gesetzt wenn TPU und Kurbelwelle synchron, dauerhaft gesetzt) LR (Lambdaregelung, 1=aktiv 0=inaktiv, Wert ist dauerhaft gesetzt wenn alle Bedingungen (z.b. Warm- laufphase beendet, Lambdasondenheizung i.O. ...) erfüllt sind NWSYN (Synchronisierung ueber Nockenwelle 1=synchronisiert 0=NW Notlauf)
- [GET_PARAMETER](#job-get-parameter) - Lesen der Globalen Variablen
- [STEUERN_IO_FREIGEBEN](#job-steuern-io-freigeben) - KWP2000 :   $30 InputOutputControlByLocalIdentifier Request Service Id $xx inputOutputLocalIdentifier $00 inputOutputControlParameter "RCTECU - ReturnControlToECU"  Freigabe der aufgelisteten Bauteile über ihr MNEMO Freigabe bedeutet, daß die zeitweilige Kontrolle des jeweiligen Bauteils durch den Tester (Ansteuerung) wieder an das Steuergerät zurückgegeben wird explizite Freigabe ist notwendig, wenn Ansteuerung noch vor Ablauf der Ansteuerdauer abgebrochen werden soll Benutzung der Freigabe nach Ablauf der Ansteuerdauer ist überflüssig
- [STEUERN_IO_VORGEBEN](#job-steuern-io-vorgeben) - Auftrag : KWP2000 : $30 InputOutputControlByLocalIdentifier Request Service Id $xx inputOutputLocalIdentifier $07 inputOutputControlParameter "STA - ShortTermAdjustment" $xx data Auftrag2: KWP2000 : $22     ReadDataByCommonIdentifier $40 $00 RecordCommonIdentifier "Meßwerte lesen"  1. Prüfung der Drehzahlbedingung entsprechend Tabelle Bauteilansteuerung 2. Nebenbedingung Drehzahl = 0 erforderlich für: EKP, EV1...EV4, STPABGL, MIL Drehzahl &gt; 0 erforderlich für: UETMC 3. Ansteuerung der aufgelisteten Bauteile über ihr MNEMO und ein entsprechenden [PARAMETER] 4. Dauer der Ansteuerung: 20s - gilt für alle aufgeführten Bauteile 5. Nach Ablauf der Ansteuerdauer implizite Rückgabe der Kontrolle über das jeweilige Bauteil an das Steuergerät (Freigabe)
- [STATUS_INNENTEMP](#job-status-innentemp) - Auslesen der Steuergeräte-Innentemperatur KWP2000: $22   ReadDataByCommonIdentifier $40   Fasta-Block 1 1. Byte des Fasta-Block1 verwenden 0.75 °C/Bit, 0 entspricht -48 °C
- [STATUS_MIL_ON](#job-status-mil-on) - KWP2000:    $21     ReadDataByLocalIdentifier $09     RecordLocalIdentifier "Fahrstrecke mit MIL-ON lesen" 
- [SECURITY_ACCESS](#job-security-access) - KWP2000: $27 SecurityAccess Service $01 requestSeed $FB Key
- [SET_BAUDRATE](#job-set-baudrate) - Initialisierung der Kommunikationsparameter mit bestimmter Baudrate
- [START_COMMUNICATION](#job-start-communication) - KWP2000 $81 startCommunication Request Service Id
- [STATUS_ANALOG](#job-status-analog) - KWP2000:    $22 readDataByCommonIdentifier Request Service Id $40 00 recordCommonIdentifier "Meßwerte lesen"  liefert die physikalischen Werte der aufgelisteten Größen TI       (effektive Einspritzzeit) FR       (Lambda-Regler-Ausgang, Bank 1) FR2      (Lambda-Regler-Ausgang, Bank 2) VFZG     (Fahrzeuggeschwindigkeit - ermittelt aus Geschwindigkeitssignal des ABS-SG) NMOT     (Motordrehzahl, hohe Auflösung) NSOL     (Leerlaufsolldrehzahl) WNWI0    (Nockenwellenposition Einlaß -&gt; nicht existent, Dummy-Wert 0) WNWI1    (Nockenwellenposition Auslaß -&gt; nicht existent, Dummy-Wert 0) TANS     (Ansauglufttemperatur) TMOT     (Motortemperatur Öl(K25)bzw. Wasser(K40,K71)) TMOTZYL1 (Motortemperatur Zylinder 1) TMOTZYL2 (Motortemperatur Zylinder 2) ZWOUT    (Zündwinkel-Ausgabe, in Grad KW relativ zu ? ) WDKBA    (relativer Drosselklappenwinkel bezogen auf unteren DK-Anschlag, ermittelt aus Position Drosselklappenpoti) MSHFM    (Luftmassen HFM Mittelwert -&gt; wird nicht ermittelt, Wert fest auf 0) MIIST    (indiziertes Ist-Motormoment) UB       (Spannung Klemme 30) RKRN0    (normierter Referenzspannungspegel des Klopfsensors (zylinderindividuell), muß innerhalb der drehzahlabhängigen oberen und unteren Referenzspannungsschwellen liegen) RKRN1    (siehe RKRN0) RKRN2    (siehe RKRN0) RKRN3    (siehe RKRN0) SZOUT    (Schließzeit der Zündspulen 1 - 4) KMSTAND  (Fahrstrecke des Fahrzeugs als Information über CAN empfangen) TRMIN    (relative Zeit in Minuten über CAN vom Kombi) VVRAD    (Geschwindigkeit Vorderrad über CAN vom ABS-SG) VHRAD    (Geschwindigkeit Hinterrad über CAN vom ABS-SG) STCURPOS1(aktuelle Position des Schrittmotors der Leerlaufregelung links, 0...204) STCURPOS2(aktuelle Position des Schrittmotors der Leerlaufregelung rechts, 0...204) PU       (Umgebungsluftdruck - Druck außerhalb des Saugrohres, ca. 1000 hPa) GANG     (Getriebeschaltwalzenposition) KWIRQ    (Interruptzaehler der Kurbelwelle) NWIRQ    (Interruptzaehler der Nockenwelle)
- [STATUS_DIGITAL](#job-status-digital) - KWP2000:    $22     ReadDataByCommonIdentifier $40 $02 RecordCommonIdentifier "Schalter Stati lesen"  liefert Schalterstati sowie andere digitale Werte S_KUPP    (Schalter Kupplung, 1=betätigt 0=nicht betätigt) ES_SST    (Seitenstützen-Schalter (aus Diagnose), 1=eingeklappt 0=ausgeklappt, ermittelt aus den Zuständen der Seitenstützen 1 und 2 bzw. nur 1) ES_SST1   (Schalter Seitenstütze 1, 1=eingeklappt 0=ausgeklappt) ES_SST2   (Schalter Seitenstütze 2, 1=ausgeklappt 0=eingeklappt) ES_OELNIV (Ölniveau-Schwimmer-Schalter, 1=Ölniveau i.O. 0=nicht i.O.) ES_POEL   (Öldruck-Schalter, 1=vorhanden 0=nicht vorhanden) ES_START  (Startschalter, 1=betätigt 0=nicht betätigt) S_KL15    (Schalter Klemme 15, 1=betätigt 0=nicht betätigt) ES_KILL   (Not-Aus-Schalter, 1=Not-aus aktiv 0=in Betriebsstellung) B_KL15_ZFE(Status Klemme 15 aus ZFE2 über CAN, 1=betätigt 0=nicht betätigt)
- [STOP_COMMUNICATION](#job-stop-communication) - KWP2000 $82 StopCommunication Request Service Id
- [STATUS_UEBERDREHZAHLEREIGNISSE](#job-status-ueberdrehzahlereignisse) - KWP2000:    $21 ReadDataByLocalIdentifier Request Service Id $03 recordLocalIdentifier "Überdrehsicherung lesen"  liefert Informationen bezüglich der Überschreitung der Drehzahlgrenze NUEMAX  (Motorüberdrehzahlgrenzwert, U/min, Festwert) NMAXVK  (vorgekommene Maximaldrehzahl, U/min) KMSTNMAX(Kilometerstand beim Auftreten der letzten Überdrehzahl, km) ANZNMAX (Anzahl der aufgetretenen Überdrehzahlereignisse)
- [STEUERN_UEBERDREHZAHLEREIGNISSE_LOESCHEN](#job-steuern-ueberdrehzahlereignisse-loeschen) - KWP2000:    $30 InputOutputControlByLocalIdentifier Request Service Id $A7 inputOutputLocalIdentifier "Überdrehsicherung löschen" $04 inputOutputControlParameter "RTD - ResetToDefault"  setzt die gespeicherten Einträge bezüglich Überdrehzahlereignissen zurück betrifft folgende Werte: ANZNMAX (Anzahl der aufgetretenen Überdrehzahlereignisse) NMAXVK  (vorgekommene Maximaldrehzahl) KMSTNMAX(Kilometerstand beim Auftreten der letzten Überdrehzahl)
- [STATUS_ZYLINDERANZAHL](#job-status-zylinderanzahl) - Auslesen der Zylinderanzahl KWP2000: $22        ReadDataByCommonIdentifier $40 $0C    "Adaptionswerte 2 Messblock lesen" Entweder 2 oder 4 Zylinder
- [FS_LESEN_SPEZIAL](#job-fs-lesen-spezial) - RDBLI Fehlerspeicher lesen (lang, mit FF und Logistik) KWP2000:        0x21 ReadDataByLocalIdentifier 0x0A routineLocalIdentifier 0xXX 0xXX groupOfDTC
- [FLASH_PARAMETER_LESEN](#job-flash-parameter-lesen) - Gibt die SG-spezifischen Flash-Parameter zurück
- [FLASH_PARAMETER_SETZEN](#job-flash-parameter-setzen) - Setzt die SG-spezifischen Flash-Parameter
- [STATUS_ADC_WERTE](#job-status-adc-werte) - Auslesen der unverarbeiteten Rohwerte der analogen Eingänge KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_L_SONDE](#job-status-l-sonde) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_L_SONDE_2](#job-status-l-sonde-2) - KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default
- [STATUS_L_ADD](#job-status-l-add) - Auslesen der additiven Lambdaregelung
- [STATUS_L_ADD_2](#job-status-l-add-2) - Auslesen der additiven Lambdaregelung Bank2
- [STATUS_L_INT](#job-status-l-int) - Auslesen der Lambdaregelung
- [STATUS_L_INT_2](#job-status-l-int-2) - Auslesen der Lambdaregelung
- [STATUS_L_MUL](#job-status-l-mul) - Auslesen der multiplikativen Lambdaregelung
- [STATUS_L_MUL_2](#job-status-l-mul-2) - Auslesen der multipikativen Lambdaregelung
- [STATUS_MOTORLAUFUNRUHE](#job-status-motorlaufunruhe) - KWP2000:    $22     ReadDataByCommonIdentifier $40 $03 RecordCommonIdentifier "Laufunruhewert lesen"  Auslesen der Laufunruhewerte (Laufqualität) Werte stellen ein Maß für die Verbrennungsqualität der einzelnen Zylinder dar
- [STATUS_SPI_MAX_T_TIME](#job-status-spi-max-t-time) - KWP2000:    $30 InputOutputControlByLocalIdentifier Request Service Id $5C inputOutputLocalIdentifier Raw Data $01 inputOutputControlParameter "RCS - ReportCurrentState"  liefert die maximale Übertragungszeit aller bisherigen SPI Sequenzen Übertragungzeit entspricht der Zeitdauer des folgenden Ablaufs: 1. Eintrag vorbereiteter SPI-Sequenz in die Sequenz-Queue - Zeitmarke speichern 2. Senden der Sequenz an einen peripheren Baustein 3. Empfang der Antwortdaten 4. Auslesen dieser Daten aus dem Hardwarepuffer der SPI-Schittstelle -&gt; Zeitdauer 1 - 4 ermitteln
- [STEUERN_EKP_ENTSPERREN](#job-steuern-ekp-entsperren) - KWP2000 :   $30 InputOutputControlByLocalIdentifier Request Service Id $D4 inputOutputLocalIdentifier "Sperrbedingung EKP" $04 inputOutputControlParameter "RTD - ResetToDefault"  entsperrt die EKP, Anlasserfreigabe, Einspitzung und Zuendung
- [STEUERN_EKP_SPERREN](#job-steuern-ekp-sperren) - KWP2000 :   $30 InputOutputControlByLocalIdentifier Request Service Id $D4 inputOutputLocalIdentifier "Sperrbedingung EKP" $05 inputOutputControlParameter "FCS - FreezeCurrentState" KWP2000 :   $22     ReadDataByCommonIdentifier $40 $00 RecordCommonIdentifier "Meßwerte lesen"  sperrt die EKP, Anlasserfreigabe, Einspritzung und Zuendung Nebenbedingung: Drehzahl muß Null sein.
- [ACCESS_TIMING_PARAMETER](#job-access-timing-parameter) - KWP2000:    $83 AccessTimingParamater Request Service Id $xx timingParameterIdentifier  ermöglicht auslesen und modifizieren der Flash-Zugriffsparameter
- [STEUERN_FAHRGESTELLNUMMER](#job-steuern-fahrgestellnummer) - 17 ASCII "Fahrgestellnummer" schreiben KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $30 Modus  : Default
- [STATUS_FAHRGESTELLNUMMER](#job-status-fahrgestellnummer) - 17 ASCII Byte Fahrgestell-Nummer KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $30 Modus   : Default
- [STEUERN_PROG_LOCATION_DATUM](#job-steuern-prog-location-datum) - Schreibt 3 Byte "Programmier-Ort/Datum"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $29 Modus  : Default
- [STATUS_PROG_LOCATION_DATUM](#job-status-prog-location-datum) - Ort und Datum der ECU-Programmierung KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $29 Modus   : Default
- [STEUERN_TRSP_INIT](#job-steuern-trsp-init) - KWP2000:    $3B WriteDataByLocalIdentifier Request Service Id $2A recordLocalIdentifier "TFA - Transponder Funktion Aktivieren"  dient der Aktivierung/Deaktivierung des Transponders(Ringantenne) Nutzung für den Werksprozess Bedingung: SG nicht verriegelt
- [STATUS_TRSP_INIT](#job-status-trsp-init) - aktueller Status "TRSP, Init-Kennung" KWP2000:    $21 ReadDataByLocalIdentifier Request Service Id $2A recordLocalIdentifier "Funktion Transponder"  ermittelt den Aktivierungsstatus des Transponders(Ringantenne) Nutzung für den Werksprozess - aktiviert:    "0xAA,0xAA,0xAA" - deaktiviert:  "0xFF,0xFF,0xFF"
- [STATUS_MECHANISCHER_SCHLUESSELCODE](#job-status-mechanischer-schluesselcode) - KWP2000:    $21 ReadDataByLocalIdentifier Request Service Id $28 recordLocalIdentifier  mechanischer Schliesscode ist in jedem Schlüssel hinterlegt wird vom SG aus dem ersten angelernten Schlüssel übernommen job liefert Schliesscode aus SG (0000Kxxxxx) Default Schliesscode vor dem ersten angelernten Schlüssel - 0000K00000
- [STATUS_AKTUELLER_SCHLUESSEL](#job-status-aktueller-schluessel) - aktuelle Schluessel KWP2000:    $21 ReadDataByLocalIdentifier $35 recordLocalIdentifier Modus   : Default liest die aktuellen Statusinformationen zum gesteckten Schluessel
- [STATUS_MREWS_DIAGNOSE](#job-status-mrews-diagnose) - aktuelle Schluessel KWP2000:    $21 ReadDataByLocalIdentifier $34 recordLocalIdentifier Modus  : Default liest die Diagnoseinformationen bzgl. EWS-SG, Ringantenne und Transponder
- [STEUERN_MREWS_INIT](#job-steuern-mrews-init) - KWP2000:    $3B WriteDataByLocalIdentifier $2C recordLocalIdentifier "IES - Initialisierungserkennung-status"  ermöglicht Verriegelung des SG keine Entriegelung möglich ! sperrt einige Diagnose-Jobs, z.B.: STATUS_SCHLUESSELDATEN STEUERN_SCHLUESSELDATEN STEUERN_FAHRGESTELLNUMMER STEUERN_TRSP_INIT STEUERN_PROG_LOCATION_DATUM STEUERN_MECHANISCHER_SCHLUESSELCODE
- [STATUS_MREWS_INIT](#job-status-mrews-init) - aktueller Status "MREWS, Init-Kennung" KWP2000:    $21 ReadDataByLocalIdentifier $2C recordLocalIdentifier  Feststellung, ob das SG verriegelt ist
- [STEUERN_SCHLUESSEL_SPERREN](#job-steuern-schluessel-sperren) - Schreibt 1 Byte "Schluessel-Sperre"  KWP2000:    $3B WriteDataByLocalIdentifier $2E recordLocalIdentifier Modus  :    Default sperrt den über die Schluesselnummer eingegebenen Schluessel mit diesem gesperrten Schluessel kein Fahrzeugstart mehr möglich zum Sperren muß Schluessel gesteckt sein -&gt; dieser nicht sperrbar
- [STEUERN_SCHLUESSEL_FREIGEBEN](#job-steuern-schluessel-freigeben) - Schreibt 1 Byte "Schluessel-Nummer"  KWP2000:    $3B WriteDataByLocalIdentifier $2F recordLocalIdentifier Modus  :    Default gibt den über die Schluesselnummer eingegebenen Schlüssel frei
- [STATUS_TRSP_DATEN](#job-status-trsp-daten) - KWP2000:    $21 ReadDataByLocalIdentifier $xx recordLocalIdentifier, $40-$49  auslesen bestimmter Statusdaten aus SG fuer den eingegebenen Schluessel
- [STATUS_SCHLUESSELDATEN](#job-status-schluesseldaten) - Auslesen der SCHLUESSELDATEN KWP2000 :   $21 ReadDataByLocalIdentifier $36...$3F  recordLocalIdentifier Modus   :   Default listet die kompletten Schluesseldaten aus SG-Tabelle zur eingegebenen Schluesselnummer auf Ausführung ist nur vor der Verriegelung möglich
- [STEUERN_SCHLUESSELDATEN](#job-steuern-schluesseldaten) - Schreibt 17 Byte "Schluessel-Daten"  KWP2000:    $3B WriteDataByLocalIdentifier $36...$3F recordLocalIdentifier Modus  :    Default dient dem Befüllen der internen Schluesseltabelle vor dem eigentlichen Schluesselanlernen Ausführung ist nur vor der Verriegelung möglich
- [STEUERN_MECHANISCHER_SCHLUESSELCODE](#job-steuern-mechanischer-schluesselcode) - 5 ASCII "Mechanischer Schliesscode" schreiben KWP2000: $3B WriteDataByLocalIdentifier $28 recordLocalIdentifier "MSC - mechanischer Schlüsselcode"  speichert/schreibt mechanischen Schliesscode des Schluessels ins SG dient der Ersatzteilcodierung und der Nacharbeit nur bei unverriegeltem SG möglich
- [INTERFACETYP](#job-interfacetyp) - Ermitteln des Interface-Typ
- [STEUERN_GRUNDADAPTION_ANFORDERN](#job-steuern-grundadaption-anfordern) - KWP2000 : $31 Start Routine By Local Identifier Request Service Id $32 routineLocalIdentifier legt Grundadaption fuer Tankentlueftungssystem an wird erst bei Klemme 15 AUS/EIN zurueckgesetzt
- [STEUERN_PM_AKTIVIEREN](#job-steuern-pm-aktivieren) - KWP2000 : $31 Start Routine By Local Identifier Request Service Id $83 inputOutputLocalIdentifier "EWS initialisieren"
- [STATUS_TRSP_AUTH](#job-status-trsp-auth) - Transponder Page KWP2000:    $21 ReadDataByLocalIdentifier $4C recordLocalIdentifier  vor Ausführung dieses Jobs muß STEUERN_TRSP_AUTH ausgeführt werden manuelle Authentisierung des TRSP und lesen/plausibilisieren der relevanten Pages
- [STEUERN_TRSP_AUTH](#job-steuern-trsp-auth) - Schreibt 5 Byte "TRSP-Page"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $33 Modus  : Default dieser Job muß vor STATUS_TRSP_AUTH ausgeführt werden
- [STATUS_READ_TRSP_PAGE](#job-status-read-trsp-page) - Transponder Page KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $4A Modus   : Default
- [STEUERN_CMD_READ_PAGE_TRSP](#job-steuern-cmd-read-page-trsp) - Schreibt 1 Byte "Transponder Page"  KWP 2000: $3B WriteDataByLocalIdentifier LocalIdentifier $31 Modus   : Default
- [STATUS_WRITE_PAGE_TRSP](#job-status-write-page-trsp) - Page TRSP KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $4B Modus   : Default
- [STEUERN_CMD_WRITE_PAGE_TRSP](#job-steuern-cmd-write-page-trsp) - Schreibt 5 Byte "TRSP-Page"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $32 Modus  : Default
- [STEUERN_NOCKENWELLENDIAGNOSE_AN](#job-steuern-nockenwellendiagnose-an) - KWP2000 :   $30 InputOutputControlByLocalIdentifier Request Service Id $D6 inputOutputLocalIdentifier "Freigabe Anlasser und Sperren Zuendung und Einsprizung" $08 inputOutputControlParameter "LTA - LongtermAdjustment" KWP2000 :   $22     ReadDataByCommonIdentifier $40 $00 RecordCommonIdentifier "Meßwerte lesen"  sperrt die Einspritzung und Zuendung und gibt gleichzeitig den Anlasser frei Dazu werden die Interruptzaehler der Kurbelwelle und Nockenwelle angzeigt Nebenbedingung: Drehzahl muß kleiner als 500 U/min sein.
- [STEUERN_NOCKENWELLENDIAGNOSE_AUS](#job-steuern-nockenwellendiagnose-aus) - KWP2000 :   $30 InputOutputControlByLocalIdentifier Request Service Id $D6 inputOutputLocalIdentifier "Freigabe Anlasser und Sperren Zuendung und Einsprizung" $04 inputOutputControlParameter "RTD - ResetToDefault"  gibt Kontrolle von Einspitzung, Zuendung und Anlasserfreigabe wieder an SG zurueck
- [STATUS_ADAPTIONSWERTE2](#job-status-adaptionswerte2) - KWP2000:    $22     ReadDataByCommonIdentifier $40 $0C RecordCommonIdentifier "ADAPTIONSWERTE2 lesen"  Adaptionswerte: DMVAD (Delta-Motordrehmom. aus Verlustmom.-Adapt.) UDKP1MX (Drosselklappenadaption max. Anschlag) RKA (Adaptive Korrektur Kraftstoffmasse) RKA2 (Adaptive Korrektur Kraftstoffmasse Bank 2) FRAO (multipl. Gemischadapt.fakt. ob. Lastbereich) FRAO2 (multipl. Gemischadapt.fakt. ob. Lastbereich Bank 2) FRAU (multipl.Gemischadapt.fakt. unt. mult.Bereich) FRAU2 (multipl.Gemischadapt.fakt. unt. mult.Bereich Bank 2) RKAZ (addit.Gemischkorr. (pro Zuend.) der Gemischadapt.) RKAZ2 (addit.Gemischkorr. (pro Zuend.) der Gemischadapt. Bank 2) FMSLA (Korrekturfak. SLmasse adaptiv) FMSLA2 (Korrekturfak. SLmasse adaptiv Bank 2) FMSLVA (Sekundaerluft Adaptionswert) FMSLVA2 (Sekundaerluft Adaptionswert Bank 2) NWFEHLER (Anzahl Nockenwellenfehler)
- [STATUS_ANALOG2](#job-status-analog2) - KWP2000:    $22     ReadDataByCommonIdentifier $40 $11 RecordCommonIdentifier "Analogwerte 2 lesen"  STP1 (Stepperposition 1 in Prozent) STP2 (Stepperposition 2 in Prozent) VSIKM (Restkilometerstand fuer Ventilspielserviceintervall) VSIDEL (Anzahl von Loeschungen der VSI-km) FRPS (gefilterter Wert des Kraftstoffdrucksensors) TOEL (Motoroeltemperatur)
- [STATUS_MREWS_RETRY](#job-status-mrews-retry) - aktueller Status "MREWS, Init-Kennung" KWP2000:    $21 ReadDataByLocalIdentifier $4D recordLocalIdentifier  Zum Auslesen der Retry Counter
- [STATUS_NCOLL](#job-status-ncoll) - KWP2000:    $22     ReadDataByCommonIdentifier $40 $0F RecordCommonIdentifier "NCOLL WERTE lesen"  Adaptionswerte: NCOLL1 (Motorlaufzeit von 9000 - 9249 U/min in Sekunden) NCOLL2 (Motorlaufzeit von 9250 - 9499 U/min in Sekunden) NCOLL3 (Motorlaufzeit von 9500 - 9749 U/min in Sekunden) NCOLL4 (Motorlaufzeit von 9750 - 9999 U/min in Sekunden) NCOLL5 (Motorlaufzeit von 10000 - 10249 U/min in Sekunden) NCOLL6 (Motorlaufzeit von 10250 - 10499 U/min in Sekunden) NCOLL7 (Motorlaufzeit von 10500 - 10749 U/min in Sekunden) NCOLL8 (Motorlaufzeit von 10750 - 10999 U/min in Sekunden) NCOLL9 (Motorlaufzeit von 11000 - 11250 U/min in Sekunden)
- [STATUS_ASC_WERTE](#job-status-asc-werte) - KWP2000:    $22     ReadDataByCommonIdentifier $40 $10 RecordCommonIdentifier "ASC Status-/Messwerteblock lesen"  Messwerte:      ACTCTR    (Dauer der ASC-Regelungen in Sekunden) INTCTR    (mittlere Intensität/Momentrücknahme der ASC-Regelungen in Prozent) ASCSTATUS (aktueller Status der ASC-Funktion: 0 = RESERVIERT 1 = KOMFORT_STANDBY 2 = GS_STANDBY 3 = KEINE_FREIGABE 4 = KEINE_FREIGABE_GS 5 = KOMFORT_AKTIV 6 = GS_AKTIV 7 = AUS 8 = FEHLER ) ASCMODUS  (gewählter Modus der ASC-Funktion: 7 = AUS 1 = KOMFORT 2 = GS ) ES_ASC    (ASC-Taster, 0=nicht betätigt 1=betätigt 2=NOT-AUS aktiv ) RADCOR    (gesamte Radiuskorrektur der Reifenradiusadaption in mm, rücksetzen über den Job STEUERN_ADAPTIONSWERTE_LÖSCHEN möglich)
- [STEUERN_SEKUNDAERLUFTVENTILDIAGNOSE_AN](#job-steuern-sekundaerluftventildiagnose-an) - KWP2000 :   $30 InputOutputControlByLocalIdentifier Request Service Id $D8 inputOutputLocalIdentifier "Sekundärluftventildiagnose über Tester" $08 inputOutputControlParameter "LTA - LongtermAdjustment"  gibt die Sekundaerluftventildiagnose frei
- [STEUERN_SEKUNDAERLUFTVENTILDIAGNOSE_AUS](#job-steuern-sekundaerluftventildiagnose-aus) - KWP2000 :   $30 InputOutputControlByLocalIdentifier Request Service Id $D8 inputOutputLocalIdentifier "Sekundärluftventildiagnose über Tester" $04 inputOutputControlParameter "RTD - ResetToDefault"  nimmt die Freigabe der Sekundaerluftventildiagnose wieder zurueck
- [STATUS_SEKUNDAERLUFTVENTILDIAGNOSE](#job-status-sekundaerluftventildiagnose) - KWP2000:    $22     ReadDataByCommonIdentifier $40 $0E RecordCommonIdentifier "SLV-Diagnose-Stati lesen"  Stati:      B_ANFSLV (Bedingung Anforderung SLV-Diagnose) B_DSLVE  (Bedingung Durchführung SLV-Diagnose) B_DSLVA  (Bedingung Abbruch SLV-Diagnose) B_ADSLV  (Bedingung SLV-Diagnose abgeschlossen)
- [STEUERN_NMOTMAXWERK_EIN](#job-steuern-nmotmaxwerk-ein) - KWP2000 :   $30 InputOutputControlByLocalIdentifier Request Service Id $D9 inputOutputLocalIdentifier "Drehzahlbegrenzung über Tester" $08 inputOutputControlParameter "LTA - LongtermAdjustment"  aktiviert die Drehzahlbegrenzung Werk
- [STEUERN_NMOTMAXWERK_AUS](#job-steuern-nmotmaxwerk-aus) - KWP2000 :   $30 InputOutputControlByLocalIdentifier Request Service Id $D9 inputOutputLocalIdentifier "Drehzahlbegrenzung über Tester" $04 inputOutputControlParameter "RTD - ResetToDefault"  nimmt die Drehzahlbegrenzung Werk wieder zurueck
- [STEUERN_NVRAM_LOESCHEN](#job-steuern-nvram-loeschen) - KWP2000 :   $31 StartRoutineByLocalIdentifier Request Service Id $EA inputOutputLocalIdentifier "NVRAM löschen"  sofern die Motordrehzahl = 0 ist, wird nach Abschluß der aktuellen Kommunikation ein Reset ausgelöst, währenddessen das NVRAM gelöscht wird
- [STEUERN_VENTILSPIELSERVICE_SETZEN](#job-steuern-ventilspielservice-setzen) - KWP2000 : $2E     WriteDataByCommonIdentifier Request Service Id $40 $13 recordCommonIdentifier "VSI Restwegstrecke und Löschzähler setzen" $xx $xx $xx data  1. SG-interne Prüfung auf Drehzahl = 0 2. Setzen der Restwegstrecke (in km) und des Löschzählers
- [IDENT](#job-ident) - Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default
- [ZIF_LESEN](#job-zif-lesen) - Auslesen des Zulieferinfofeldes KWP2000: $22   ReadDataByCommonIdentifier $2503 ProgrammReferenz und KWP2000: $1A   ReadECUIdentification $91   VehicleManufacturerECUHardware*Number oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [ZIF_BACKUP_LESEN](#job-zif-backup-lesen) - Auslesen des Backups des Zulieferinfofeldes ProgrammReferenzBackup         PRGREFB vehicleManufECUHW*NumberBackup VMECUH*NB KWP2000: $22   ReadDataByCommonIdentifier $2500 PRBHW*B oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender Informations Feldes Standard Flashjob KWP 2000: $23 ReadMemoryByAddress Modus   : Default

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

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

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

<a id="job-steuern-abs-loeschen"></a>
### STEUERN_ABS_LOESCHEN

Auftrag: KWP2000 :   $31 StartRoutineByLocalIdentifier Request Service Id $2F inputOutputLocalIdentifier "B_abs ruecksetzen" Auftrag2: KWP2000 :   $22     ReadDataByCommonIdentifier $40 $00 RecordCommonIdentifier "Meßwerte lesen"  Überprüfung der Motordrehzahl mittels Auftrag2 wenn Drehzahl = 0 , Bedingung ABS-SG ist/war verbaut (B_abs) wird zurückgesetzt Bedingung B_abs wird gesetzt sofern eine entsprechende CAN-Message vom ABS-SG empfangen wurde

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-adaptionswerte"></a>
### STATUS_ADAPTIONSWERTE

KWP2000 :   $21 ReadDataByLocalIdentifier Request Service Id $0B recordLocalIdentifier "Adaptionswerte_lesen"  Adaptionswerte: ABS     (ABS-SG verbaut(=1)/nicht verbaut(=0)) LOWBAT  (UB liegt zw. 6 und 7 V (=1) und fuehrt zu Einschraenkungen beim Ansteuern des Anlassers) SPERREKP(EKP,Zünd./Einsp. & Anlasser gesperrt(=1) über Tester) DKPA    (Drosselklappe im Nullanschlag) GANGAN  (Getriebepoti in Neutralstellung) GANGA1  (Stellung Getriebepoti 1.Gang) GANGA2  (Stellung Getriebepoti 2.Gang) GANGA3  (Stellung Getriebepoti 3.Gang) GANGA4  (Stellung Getriebepoti 4.Gang) GANGA5  (Stellung Getriebepoti 5.Gang) GANGA6  (Stellung Getriebepoti 6.Gang)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ABS_TEXT | string | ABS Steuergerät |
| STAT_ABS_ZUST | string | ABS Steuergerät |
| STAT_ABS_WERT | long | ABS Steuergerät |
| STAT_LOWBAT_TEXT | string | U-Bat zwischen 6 und 7 Volt |
| STAT_LOWBAT_ZUST | string | U-Bat zwischen 6 und 7 Volt |
| STAT_LOWBAT_WERT | long | U-Bat zwischen 6 und 7 Volt |
| STAT_SPERREKP_TEXT | string | EKP gesperrt über Tester |
| STAT_SPERREKP_ZUST | string | EKP gesperrt über Tester |
| STAT_SPERREKP_WERT | long | EKP gesperrt über Tester |
| STAT_DKPA_TEXT | string | Adaptionswert Drosselklappenpoti |
| STAT_DKPA_EINH | string | Adaptionswert Drosselklappenpoti |
| STAT_DKPA_WERT | real | Adaptionswert Drosselklappenpoti |
| STAT_GANGAN_TEXT | string | Adaptionswert Getriebeschaltwalzenpoti Neutralstellung |
| STAT_GANGAN_EINH | string | Adaptionswert Getriebeschaltwalzenpoti Neutralstellung |
| STAT_GANGAN_WERT | real | Adaptionswert Getriebeschaltwalzenpoti Neutralstellung |
| STAT_GANGA1_TEXT | string | Adaptionswert Getriebeschaltwalzenpoti 1.Gang |
| STAT_GANGA1_EINH | string | Adaptionswert Getriebeschaltwalzenpoti 1.Gang |
| STAT_GANGA1_WERT | real | Adaptionswert Getriebeschaltwalzenpoti 1.Gang |
| STAT_GANGA2_TEXT | string | Adaptionswert Getriebeschaltwalzenpoti 2.Gang |
| STAT_GANGA2_EINH | string | Adaptionswert Getriebeschaltwalzenpoti 2.Gang |
| STAT_GANGA2_WERT | real | Adaptionswert Getriebeschaltwalzenpoti 2.Gang |
| STAT_GANGA3_TEXT | string | Adaptionswert Getriebeschaltwalzenpoti 3.Gang |
| STAT_GANGA3_EINH | string | Adaptionswert Getriebeschaltwalzenpoti 3.Gang |
| STAT_GANGA3_WERT | real | Adaptionswert Getriebeschaltwalzenpoti 3.Gang |
| STAT_GANGA4_TEXT | string | Adaptionswert Getriebeschaltwalzenpoti 4.Gang |
| STAT_GANGA4_EINH | string | Adaptionswert Getriebeschaltwalzenpoti 4.Gang |
| STAT_GANGA4_WERT | real | Adaptionswert Getriebeschaltwalzenpoti 4.Gang |
| STAT_GANGA5_TEXT | string | Adaptionswert Getriebeschaltwalzenpoti 5.Gang |
| STAT_GANGA5_EINH | string | Adaptionswert Getriebeschaltwalzenpoti 5.Gang |
| STAT_GANGA5_WERT | real | Adaptionswert Getriebeschaltwalzenpoti 5.Gang |
| STAT_GANGA6_TEXT | string | Adaptionswert Getriebeschaltwalzenpoti 6.Gang |
| STAT_GANGA6_EINH | string | Adaptionswert Getriebeschaltwalzenpoti 6.Gang |
| STAT_GANGA6_WERT | real | Adaptionswert Getriebeschaltwalzenpoti 6.Gang |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-adaptionswerte-loeschen"></a>
### STEUERN_ADAPTIONSWERTE_LOESCHEN

KWP2000 :   $31 StartRoutineByLocalIdentifier Request Service Id $E9 inputOutputLocalIdentifier "Adaptionswerte löschen"  sofern die Motordrehzahl = 0 ist, wird nach Abschluß der aktuellen Kommunikation ein Reset ausgelöst, währenddessen die Adaptionswerte gelöscht und beim Hochfahren wieder initialisiert werden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-ausgaenge-digital"></a>
### STATUS_AUSGAENGE_DIGITAL

KWP2000:    $22     ReadDataByCommonIdentifier $40 $05 RecordCommonIdentifier "Ausgänge prüfen"  Ausgänge:   UETMC ( Kontrollleuchte Motortemperatur, 1=aktiv 0=inaktiv) ANLASSER ( Ansteuerung Anlasserrelais, 1=aktiv 0=inaktiv) AKL ( Akustikklappe, 1=offen 0=geschlossen=nicht verbaut) SLV1 ( Sekundärluftventil, 1=offen 0=geschlossen) TEV ( Taktventil Tankentlüftung, 1=offen 0=geschlossen) EKPBTS ( Kraftstoffpumpe, 1=läuft 0=läuft nicht) ELUE1 ( E-Lüfter, 1=läuft 0=läuft nicht) MIL ( Motornotlauf, 1=Notlauf 0=kein Notlauf) HSV ( Lambdasondenheizung 1, 1=aktiv 0=inaktiv) HSV2 ( Lambdasondenheizung 2, 1=aktiv 0=inaktiv) B_A_SCHUTZ ( Anlasserschutz, 1=aktiv 0=inaktiv löst Sicherheitsabschaltung aus) B_FRGANL ( Anlasser Freigabe, 1=freigegeben 0=nicht freigegeben) B_MOTORSTP ( Motor Abschalten, 1=aktiv 0=inaktiv)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_UETMC_AKTIV | int | Kontrollleuchte Motortemperatur |
| STAT_UETMC_TEXT | string | Kontrollleuchte Motortemperatur |
| STAT_UETMC_ZUSTAND | string | Kontrollleuchte Motortemperatur |
| STAT_ANLASSER_AKTIV | int | Anlasser |
| STAT_ANLASSER_TEXT | string | Anlasser |
| STAT_ANLASSER_ZUSTAND | string | Anlasser |
| STAT_AKL_AKTIV | int | Akkustik Klappe |
| STAT_AKL_TEXT | string | Akkustik Klappe |
| STAT_AKL_ZUSTAND | string | Akkustik Klappe |
| STAT_SLV1_AKTIV | int | Sekundaerluftventil 1 |
| STAT_SLV1_TEXT | string | Sekundaerluftventil 1 |
| STAT_SLV1_ZUSTAND | string | Sekundaerluftventil 1 |
| STAT_TEV_AKTIV | int | Tankentlüftung |
| STAT_TEV_TEXT | string | Tankentlüftung |
| STAT_TEV_ZUSTAND | string | Tankentlüftung |
| STAT_EKPBTS_AKTIV | int | Kraftstoffpumpe |
| STAT_EKPBTS_TEXT | string | Kraftstoffpumpe |
| STAT_EKPBTS_ZUSTAND | string | Kraftstoffpumpe |
| STAT_ELUE1_AKTIV | int | Lüfter |
| STAT_ELUE1_TEXT | string | Lüfter |
| STAT_ELUE1_ZUSTAND | string | Lüfter |
| STAT_MIL_AKTIV | int | Motornotlauf |
| STAT_MIL_TEXT | string | Motornotlauf |
| STAT_MIL_ZUSTAND | string | Motornotlauf |
| STAT_HSV_AKTIV | int | Lambdasondenheizung 1 |
| STAT_HSV_TEXT | string | Lambdasondenheizung 1 |
| STAT_HSV_ZUSTAND | string | Lambdasondenheizung 1 |
| STAT_HSV2_AKTIV | int | Lambdasondenheizung 2 |
| STAT_HSV2_TEXT | string | Lambdasondenheizung 2 |
| STAT_HSV2_ZUSTAND | string | Lambdasondenheizung 2 |
| STAT_B_A_SCHUTZ_AKTIV | int | Anlasser Schutz |
| STAT_B_A_SCHUTZ_TEXT | string | Anlasser Schutz |
| STAT_B_A_SCHUTZ_ZUSTAND | string | Anlasser Schutz |
| STAT_B_FRGANL_AKTIV | int | Anlasser Freigabe |
| STAT_B_FRGANL_TEXT | string | Anlasser Freigabe |
| STAT_B_FRGANL_ZUSTAND | string | Anlasser Freigabe |
| STAT_B_MOTORSTP_AKTIV | int | Motor Abschalten |
| STAT_B_MOTORSTP_TEXT | string | Motor Abschalten |
| STAT_B_MOTORSTP_ZUSTAND | string | Motor Abschalten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-status-funktionsstati"></a>
### STATUS_FUNKTIONSSTATI

KWP2000:    $22     ReadDataByCommonIdentifier $40 $07 RecordCommonIdentifier "Funktionsstati lesen"  Funktionsstati: LL (Bedingung Leerlauf, 1=aktiv 0=inaktiv gesetzt wenn sich Motor im Leerlauf befindet) VL (Bedingung Vollast, 1=Vollast 0=keine Vollast gesetzt wenn: - Bedingung Leerlauf inaktiv und - drehzahlabhängiger Drosselklappenwinkel gegeben ist) TEHB (Bedingung Tankentlüftung mit hoher Beladung 1=aktiv 0=inaktiv, Beladung=HC-Konzentration im Regeneriergasstrom(aus Tankentlüftung) SA (Bedingung Schubabschalten, 1=aktiv 0=inaktiv Abschaltung Einspritzung, Zündung, EKP u.a., um vorhandenes positives Drehmoment(Schub) auf Null zu reduzieren wenn keine Drehmomentanforderung mehr besteht SBBVK (Bedingung Sonde betriebsbereit vor Kat 1=betriebsbereit 0=nicht betriebsbereit) BM (Zylinder-1 Erkennung, 1=erkannt 0=nicht erkannt gesetzt wenn TPU und Kurbelwelle synchron, dauerhaft gesetzt) LR (Lambdaregelung, 1=aktiv 0=inaktiv, Wert ist dauerhaft gesetzt wenn alle Bedingungen (z.b. Warm- laufphase beendet, Lambdasondenheizung i.O. ...) erfüllt sind NWSYN (Synchronisierung ueber Nockenwelle 1=synchronisiert 0=NW Notlauf)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LL_TEXT | string | Leerlaufregelung |
| STAT_LL_ZUST | string | Leerlaufregelung |
| STAT_LL_WERT | long | Leerlaufregelung |
| STAT_VL_TEXT | string | Bedingung Vollast |
| STAT_VL_ZUST | string | Bedingung Vollast |
| STAT_VL_WERT | long | Bedingung Vollast |
| STAT_TEHB_TEXT | string | Bedingung Tankentlüftung mit hoher Beladung |
| STAT_TEHB_ZUST | string | Bedingung Tankentlüftung mit hoher Beladung |
| STAT_TEHB_WERT | long | Bedingung Tankentlüftung mit hoher Beladung |
| STAT_SA_TEXT | string | Bedingung Schubabschalten |
| STAT_SA_ZUST | string | Bedingung Schubabschalten |
| STAT_SA_WERT | long | Bedingung Schubabschalten |
| STAT_SBBVK_TEXT | string | Bedingung Sonde betriebsbereit vor Kat |
| STAT_SBBVK_ZUST | string | Bedingung Sonde betriebsbereit vor Kat |
| STAT_SBBVK_WERT | long | Bedingung Sonde betriebsbereit vor Kat |
| STAT_SBBVK2_TEXT | string | Bedingung Sonde betriebsbereit vor Kat, Bank 2 |
| STAT_SBBVK2_ZUST | string | Bedingung Sonde betriebsbereit vor Kat, Bank 2 |
| STAT_SBBVK2_WERT | long | Bedingung Sonde betriebsbereit vor Kat, Bank 2 |
| STAT_BM_TEXT | string | Zylinder-1 Erkennung |
| STAT_BM_ZUST | string | Zylinder-1 Erkennung |
| STAT_BM_WERT | long | Zylinder-1 Erkennung |
| STAT_LR_TEXT | string | Lambdaregelung |
| STAT_LR_ZUST | string | Lambdaregelung |
| STAT_LR_WERT | long | Lambdaregelung |
| STAT_NWSYN_TEXT | string | Synchronisierung ueber Nockenwelle |
| STAT_NWSYN_ZUST | string | Synchronisierung ueber Nockenwelle |
| STAT_NWSYN_WERT | long | Synchronisierung ueber Nockenwelle |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-get-parameter"></a>
### GET_PARAMETER

Lesen der Globalen Variablen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ECU | string | ECU als text |
| ABGASVARIANTE | string | Abgas-Variante als text |
| LAENDERVARIANTE | string | Länder-Variante als text |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-io-freigeben"></a>
### STEUERN_IO_FREIGEBEN

KWP2000 :   $30 InputOutputControlByLocalIdentifier Request Service Id $xx inputOutputLocalIdentifier $00 inputOutputControlParameter "RCTECU - ReturnControlToECU"  Freigabe der aufgelisteten Bauteile über ihr MNEMO Freigabe bedeutet, daß die zeitweilige Kontrolle des jeweiligen Bauteils durch den Tester (Ansteuerung) wieder an das Steuergerät zurückgegeben wird explizite Freigabe ist notwendig, wenn Ansteuerung noch vor Ablauf der Ansteuerdauer abgebrochen werden soll Benutzung der Freigabe nach Ablauf der Ansteuerdauer ist überflüssig

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MNEMO | string | MNEMO   TEXT (PARAMETER) Elu             E-Lüfter SLV             Sekundärluftventil AKL             Akustik Klappe TEV             Taktventil Tankentlüftung EKP             Kraftstoffpumpe HSV             Lambdasondenheizung vor Kat 1 HSV2            Lambdasondenheizung vor Kat 2 EV1 .. EV4      Einspritzventil 1..4 STPLL1          Stepper 1: LL-Regelung rechts STPLL2          Stepper 2: K25 LL-Regelung links oder K40 Vmax-Begrenzung Gangadp         Gangadaption ueber Tester UETMC           Kontrolleuchte Übertemperatur MIL             Check-Engine-Lampe VSIDEL          Ventilspielserviceintervall |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-steuern-io-vorgeben"></a>
### STEUERN_IO_VORGEBEN

Auftrag : KWP2000 : $30 InputOutputControlByLocalIdentifier Request Service Id $xx inputOutputLocalIdentifier $07 inputOutputControlParameter "STA - ShortTermAdjustment" $xx data Auftrag2: KWP2000 : $22     ReadDataByCommonIdentifier $40 $00 RecordCommonIdentifier "Meßwerte lesen"  1. Prüfung der Drehzahlbedingung entsprechend Tabelle Bauteilansteuerung 2. Nebenbedingung Drehzahl = 0 erforderlich für: EKP, EV1...EV4, STPABGL, MIL Drehzahl &gt; 0 erforderlich für: UETMC 3. Ansteuerung der aufgelisteten Bauteile über ihr MNEMO und ein entsprechenden [PARAMETER] 4. Dauer der Ansteuerung: 20s - gilt für alle aufgeführten Bauteile 5. Nach Ablauf der Ansteuerdauer implizite Rückgabe der Kontrolle über das jeweilige Bauteil an das Steuergerät (Freigabe)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MNEMO | string | MNEMO           TEXT [PARAMETER] Elu             E-Lüfter [ein / aus] SLV             Sekundärluftventil [ein] AKL             Akustik Klappe [ein] TEV             Taktventil Tankentlüftung (Tastverhaeltnis [0 ... 100]% bei 15Hz) EKP             Kraftstoffpumpe (Tastverhaeltnis [0 ... 100]% bei 1kHz) HSV             Lambdasondenheizung vor Kat 1 (im 100 ms Raster: 100 ms Puls - [n]ms Pause - 100 ms Puls - ...) HSV2            Lambdasondenheizung vor Kat 2 (im 100 ms Raster: 100 ms Puls - [n]ms Pause - 100 ms Puls - ...) (bei der Wahl der Pulspause Ansteuerungsdauer beachten -&gt; 0 &lt; n &lt; 20000, n&lt;100 bedeutet Dauerpuls) EV1 .. EV4      Einspritzventil 1..4 [ein / aus] STPLL1          Stepper 1: LL-Regelung rechts [0 ... 100%] STPLL2          Stepper 2: K25 LL-Regelung links oder K40 Vmax-Begrenzung [0 ... 100%] STPABGL         Stepper-Abgleich [ein] Gangadp         Freischalten der Gangadaption ueber Tester [ein] UETMC           Kontrolleuchte Übertemperatur [ein / aus] MIL             Check-Engine-Lampe [ein / aus] VSIDEL          Ventilspielserviceintervall Kilometerstand zuruecksetzen [ein] |
| PARAMETER | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |

<a id="job-status-innentemp"></a>
### STATUS_INNENTEMP

Auslesen der Steuergeräte-Innentemperatur KWP2000: $22   ReadDataByCommonIdentifier $40   Fasta-Block 1 1. Byte des Fasta-Block1 verwenden 0.75 °C/Bit, 0 entspricht -48 °C

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SG_INNENTEMP_WERT | string | SG-Innentemperatur |
| STAT_SG_INNENTEMP_EINH | string | Grad C |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mil-on"></a>
### STATUS_MIL_ON

KWP2000:    $21     ReadDataByLocalIdentifier $09     RecordLocalIdentifier "Fahrstrecke mit MIL-ON lesen" 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_F_KM_WERT | int | gefahrene Kilometer bei MIL aktiv |
| STAT_F_KM_EINH | string | Kilometerstand |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-security-access"></a>
### SECURITY_ACCESS

KWP2000: $27 SecurityAccess Service $01 requestSeed $FB Key

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ACCESS_MODE | int | 1: Request Seed with the level of security defined in the ECU´s project specification 2: Send Key with the level of security defined in the ECU´s project specification 3, 5 - 7F: Request Seed with different levels of security defined in the ECU´s project specification 4, 6 - 80: Send Key with different levels of security defined in the ECU´s project specification |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-set-baudrate"></a>
### SET_BAUDRATE

Initialisierung der Kommunikationsparameter mit bestimmter Baudrate

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BAUDRATE | string | die gewuenschte Baudrate |
| KONZEPT | string | Konzept |
| TIMEOUT | string | Timeout in ms |
| REGENERATIONSZEIT | string | Regenerationszeit in ms |
| TELEGRAMMENDEZEIT | string | Telegrammendezeit in ms |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-start-communication"></a>
### START_COMMUNICATION

KWP2000 $81 startCommunication Request Service Id

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| KB_NR | string | Key Byte |
| FORMAT | string | FORMAT |
| HEADER | string | HEADER |
| TIMING | string | TIMING |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-status-analog"></a>
### STATUS_ANALOG

KWP2000:    $22 readDataByCommonIdentifier Request Service Id $40 00 recordCommonIdentifier "Meßwerte lesen"  liefert die physikalischen Werte der aufgelisteten Größen TI       (effektive Einspritzzeit) FR       (Lambda-Regler-Ausgang, Bank 1) FR2      (Lambda-Regler-Ausgang, Bank 2) VFZG     (Fahrzeuggeschwindigkeit - ermittelt aus Geschwindigkeitssignal des ABS-SG) NMOT     (Motordrehzahl, hohe Auflösung) NSOL     (Leerlaufsolldrehzahl) WNWI0    (Nockenwellenposition Einlaß -&gt; nicht existent, Dummy-Wert 0) WNWI1    (Nockenwellenposition Auslaß -&gt; nicht existent, Dummy-Wert 0) TANS     (Ansauglufttemperatur) TMOT     (Motortemperatur Öl(K25)bzw. Wasser(K40,K71)) TMOTZYL1 (Motortemperatur Zylinder 1) TMOTZYL2 (Motortemperatur Zylinder 2) ZWOUT    (Zündwinkel-Ausgabe, in Grad KW relativ zu ? ) WDKBA    (relativer Drosselklappenwinkel bezogen auf unteren DK-Anschlag, ermittelt aus Position Drosselklappenpoti) MSHFM    (Luftmassen HFM Mittelwert -&gt; wird nicht ermittelt, Wert fest auf 0) MIIST    (indiziertes Ist-Motormoment) UB       (Spannung Klemme 30) RKRN0    (normierter Referenzspannungspegel des Klopfsensors (zylinderindividuell), muß innerhalb der drehzahlabhängigen oberen und unteren Referenzspannungsschwellen liegen) RKRN1    (siehe RKRN0) RKRN2    (siehe RKRN0) RKRN3    (siehe RKRN0) SZOUT    (Schließzeit der Zündspulen 1 - 4) KMSTAND  (Fahrstrecke des Fahrzeugs als Information über CAN empfangen) TRMIN    (relative Zeit in Minuten über CAN vom Kombi) VVRAD    (Geschwindigkeit Vorderrad über CAN vom ABS-SG) VHRAD    (Geschwindigkeit Hinterrad über CAN vom ABS-SG) STCURPOS1(aktuelle Position des Schrittmotors der Leerlaufregelung links, 0...204) STCURPOS2(aktuelle Position des Schrittmotors der Leerlaufregelung rechts, 0...204) PU       (Umgebungsluftdruck - Druck außerhalb des Saugrohres, ca. 1000 hPa) GANG     (Getriebeschaltwalzenposition) KWIRQ    (Interruptzaehler der Kurbelwelle) NWIRQ    (Interruptzaehler der Nockenwelle)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TI_WERT | real | Einspritzzeit EV |
| STAT_TI_EINH | string | Einspritzzeit EV |
| STAT_TI_TEXT | string | Einspritzzeit EV |
| STAT_FR_WERT | real | Lambdaregler 1 |
| STAT_FR_EINH | string | Lambdaregler 1 |
| STAT_FR_TEXT | string | Lambdaregler 1 |
| STAT_FR2_WERT | real | Lambdaregler 2 |
| STAT_FR2_EINH | string | Lambdaregler 2 |
| STAT_FR2_TEXT | string | Lambdaregler 2 |
| STAT_VFZG_WERT | real | Fahrzeuggeschwindigkeit |
| STAT_VFZG_EINH | string | Fahrzeuggeschwindigkeit |
| STAT_VFZG_TEXT | string | Fahrzeuggeschwindigkeit |
| STAT_NMOT_WERT | real | Motordrehzahl hoch aufgelöst |
| STAT_NMOT_EINH | string | Motordrehzahl hoch aufgelöst |
| STAT_NMOT_TEXT | string | Motordrehzahl hoch aufgelöst |
| STAT_NSOL_WERT | real | Leerlauf-Solldrehzahl |
| STAT_NSOL_EINH | string | Leerlauf-Solldrehzahl |
| STAT_NSOL_TEXT | string | Leerlauf-Solldrehzahl |
| STAT_WNWI0_WERT | real | Nockenwellenposition Einlaß |
| STAT_WNWI0_EINH | string | Nockenwellenposition Einlaß |
| STAT_WNWI0_TEXT | string | Nockenwellenposition Einlaß |
| STAT_WNWI1_WERT | real | Nockenwellenposition Auslaß |
| STAT_WNWI1_EINH | string | Nockenwellenposition Auslaß |
| STAT_WNWI1_TEXT | string | Nockenwellenposition Auslaß |
| STAT_TANS_WERT | real | Ansauglufttemperatur |
| STAT_TANS_EINH | string | Ansauglufttemperatur |
| STAT_TANS_TEXT | string | Ansauglufttemperatur |
| STAT_TMOT_WERT | real | Motortemperatur |
| STAT_TMOT_EINH | string | Motortemperatur |
| STAT_TMOT_TEXT | string | Motortemperatur |
| STAT_TMOTZYL1_WERT | real | Motortemperatur Zylinder 1 |
| STAT_TMOTZYL1_EINH | string | Motortemperatur Zylinder 1 |
| STAT_TMOTZYL1_TEXT | string | Motortemperatur Zylinder 1 |
| STAT_TMOTZYL2_WERT | real | Motortemperatur Zylinder 2 |
| STAT_TMOTZYL2_EINH | string | Motortemperatur Zylinder 2 |
| STAT_TMOTZYL2_TEXT | string | Motortemperatur Zylinder 2 |
| STAT_ZWOUT_WERT | real | Zündwinkel |
| STAT_ZWOUT_EINH | string | Zündwinkel |
| STAT_ZWOUT_TEXT | string | Zündwinkel |
| STAT_WDKBA_WERT | real | DK Winkel rel. DK-Anschlag |
| STAT_WDKBA_EINH | string | DK Winkel rel. DK-Anschlag |
| STAT_WDKBA_TEXT | string | DK Winkel rel. DK-Anschlag |
| STAT_MSHFM_WERT | real | Luftmasse |
| STAT_MSHFM_EINH | string | Luftmasse |
| STAT_MSHFM_TEXT | string | Luftmasse |
| STAT_MIIST_WERT | real | indiziertes Motormoment nach Eingriffe |
| STAT_MIIST_EINH | string | indiziertes Motormoment nach Eingriffe |
| STAT_MIIST_TEXT | string | indiziertes Motormoment nach Eingriffe |
| STAT_UB_WERT | real | Spannung Kl. 30 |
| STAT_UB_EINH | string | Spannung Kl. 30 |
| STAT_UB_TEXT | string | Spannung Kl. 30 |
| STAT_RKRN0_WERT | real | Klopfsensor Ref. Pegel |
| STAT_RKRN0_EINH | string | Klopfsensor Ref. Pegel |
| STAT_RKRN0_TEXT | string | Klopfsensor Ref. Pegel |
| STAT_RKRN1_WERT | real | Klopfsensor Ref. Pegel |
| STAT_RKRN1_EINH | string | Klopfsensor Ref. Pegel |
| STAT_RKRN1_TEXT | string | Klopfsensor Ref. Pegel |
| STAT_RKRN2_WERT | real | Klopfsensor Ref. Pegel |
| STAT_RKRN2_EINH | string | Klopfsensor Ref. Pegel |
| STAT_RKRN2_TEXT | string | Klopfsensor Ref. Pegel |
| STAT_RKRN3_WERT | real | Klopfsensor Ref. Pegel |
| STAT_RKRN3_EINH | string | Klopfsensor Ref. Pegel |
| STAT_RKRN3_TEXT | string | Klopfsensor Ref. Pegel |
| STAT_SZOUT_WERT | real | Zündspule 1 bis 4 Schließzeit |
| STAT_SZOUT_EINH | string | Zündspule 1 bis 4 Schließzeit |
| STAT_SZOUT_TEXT | string | Zündspule 1 bis 4 Schließzeit |
| STAT_KMSTAND_WERT | real | Fahrstrecke des Fahrzeugs als Information über CAN |
| STAT_KMSTAND_EINH | string | Fahrstrecke des Fahrzeugs als Information über CAN |
| STAT_KMSTAND_TEXT | string | Fahrstrecke des Fahrzeugs als Information über CAN |
| STAT_TRMIN_WERT | real | Relative time |
| STAT_TRMIN_EINH | string | Relative time |
| STAT_TRMIN_TEXT | string | Relative time |
| STAT_VVRAD_WERT | real | front wheel speed |
| STAT_VVRAD_EINH | string | front wheel speed |
| STAT_VVRAD_TEXT | string | front wheel speed |
| STAT_VHRAD_WERT | real | back wheel speed |
| STAT_VHRAD_EINH | string | back wheel speed |
| STAT_VHRAD_TEXT | string | back wheel speed |
| STAT_STCURPOS1_WERT | real | Leerlaufregler links |
| STAT_STCURPOS1_EINH | string | Leerlaufregler links |
| STAT_STCURPOS1_TEXT | string | Leerlaufregler links |
| STAT_STCURPOS2_WERT | real | Leerlaufregler rechts |
| STAT_STCURPOS2_EINH | string | Leerlaufregler rechts |
| STAT_STCURPOS2_TEXT | string | Leerlaufregler rechts |
| STAT_PU_WERT | real | Umgebungsdruck |
| STAT_PU_EINH | string | Umgebungsdruck |
| STAT_PU_TEXT | string | Umgebungsdruck |
| STAT_GANG_WERT | real | Getriebeschaltwalzenposition |
| STAT_GANG_EINH | string | Getriebeschaltwalzenposition |
| STAT_GANG_TEXT | string | Getriebeschaltwalzenposition |
| STAT_KW_ZAEHLER_WERT | real | Wert des Interruptzaehler der Kurbelwelle |
| STAT_KW_ZAEHLER_EINH | string | Interruptzaehler der Kurbelwelle |
| STAT_KW_ZAEHLER_TEXT | string | Interruptzaehler der Kurbelwelle |
| STAT_NW_ZAEHLER_WERT | real | Wert des Interruptzaehler der Nockenwelle |
| STAT_NW_ZAEHLER_EINH | string | Interruptzaehler der Nockenwelle |
| STAT_NW_ZAEHLER_TEXT | string | Interruptzaehler der Nockenwelle |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

KWP2000:    $22     ReadDataByCommonIdentifier $40 $02 RecordCommonIdentifier "Schalter Stati lesen"  liefert Schalterstati sowie andere digitale Werte S_KUPP    (Schalter Kupplung, 1=betätigt 0=nicht betätigt) ES_SST    (Seitenstützen-Schalter (aus Diagnose), 1=eingeklappt 0=ausgeklappt, ermittelt aus den Zuständen der Seitenstützen 1 und 2 bzw. nur 1) ES_SST1   (Schalter Seitenstütze 1, 1=eingeklappt 0=ausgeklappt) ES_SST2   (Schalter Seitenstütze 2, 1=ausgeklappt 0=eingeklappt) ES_OELNIV (Ölniveau-Schwimmer-Schalter, 1=Ölniveau i.O. 0=nicht i.O.) ES_POEL   (Öldruck-Schalter, 1=vorhanden 0=nicht vorhanden) ES_START  (Startschalter, 1=betätigt 0=nicht betätigt) S_KL15    (Schalter Klemme 15, 1=betätigt 0=nicht betätigt) ES_KILL   (Not-Aus-Schalter, 1=Not-aus aktiv 0=in Betriebsstellung) B_KL15_ZFE(Status Klemme 15 aus ZFE2 über CAN, 1=betätigt 0=nicht betätigt)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_S_KUPP_AKTIV | int | Schalter Kupplung |
| STAT_S_KUPP_TEXT | string | Kupplungs-Schalter |
| STAT_S_KUPP_ZUSTAND | string | Kupplungs-Schalter |
| STAT_ES_SST_AKTIV | int | Seitenstützen-Schalter (nach Diagnose) |
| STAT_ES_SST_TEXT | string | Seitenstützen-Schalter (nach Diagnose) |
| STAT_ES_SST_ZUSTAND | string | Seitenstützen-Schalter (nach Diagnose) |
| STAT_ES_SST1_AKTIV | int | Seitenstützen-Schalter 1 |
| STAT_ES_SST1_TEXT | string | Seitenstützen-Schalter 1 |
| STAT_ES_SST1_ZUSTAND | string | Seitenstützen-Schalter 1 |
| STAT_ES_SST2_AKTIV | int | Seitenstützen-Schalter 2 |
| STAT_ES_SST2_TEXT | string | Seitenstützen-Schalter 2 |
| STAT_ES_SST2_ZUSTAND | string | Seitenstützen-Schalter 2 |
| STAT_ES_OELNIV_AKTIV | int | Ölniveau-Schwimmer-Schalter |
| STAT_ES_OELNIV_TEXT | string | Ölniveau-Schwimmer-Schalter |
| STAT_ES_OELNIV_ZUSTAND | string | Ölniveau-Schwimmer-Schalter |
| STAT_ES_POEL_AKTIV | int | Öldruckschalter |
| STAT_ES_POEL_TEXT | string | Öldruck-Schalter |
| STAT_ES_POEL_ZUSTAND | string | Öldruck-Schalter |
| STAT_ES_START_AKTIV | int | Startschalter |
| STAT_ES_START_TEXT | string | Startschalter |
| STAT_ES_START_ZUSTAND | string | Startschalter |
| STAT_S_KL15_AKTIV | int | Schalter Kl 15 |
| STAT_S_KL15_TEXT | string | Schalter Kl 15 |
| STAT_S_KL15_ZUSTAND | string | Schalter Kl 15 |
| STAT_ES_KILL_AKTIV | int | Not-Aus-Schalter |
| STAT_ES_KILL_TEXT | string | Not-Aus-Schalter |
| STAT_ES_KILL_ZUSTAND | string | Not-Aus-Schalter |
| STAT_B_KL15_ZFE_AKTIV | int | KL 15 aus ZFE |
| STAT_B_KL15_ZFE_TEXT | string | KL 15 aus ZFE |
| STAT_B_KL15_ZFE_ZUSTAND | string | KL 15 aus ZFE |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-stop-communication"></a>
### STOP_COMMUNICATION

KWP2000 $82 StopCommunication Request Service Id

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-status-ueberdrehzahlereignisse"></a>
### STATUS_UEBERDREHZAHLEREIGNISSE

KWP2000:    $21 ReadDataByLocalIdentifier Request Service Id $03 recordLocalIdentifier "Überdrehsicherung lesen"  liefert Informationen bezüglich der Überschreitung der Drehzahlgrenze NUEMAX  (Motorüberdrehzahlgrenzwert, U/min, Festwert) NMAXVK  (vorgekommene Maximaldrehzahl, U/min) KMSTNMAX(Kilometerstand beim Auftreten der letzten Überdrehzahl, km) ANZNMAX (Anzahl der aufgetretenen Überdrehzahlereignisse)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NUEMAX | string | Motorüberdrehzahlgrenzwert |
| STAT_NMAXVK | string | vorgekommene Maximaldrehzahl |
| STAT_KMSTNMAX | string | Kilometerstand beim Auftreten der letzten Überdrehzahl |
| STAT_ANZNMAX | string | Anzahl der Überdrehzahlereignisse |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-steuern-ueberdrehzahlereignisse-loeschen"></a>
### STEUERN_UEBERDREHZAHLEREIGNISSE_LOESCHEN

KWP2000:    $30 InputOutputControlByLocalIdentifier Request Service Id $A7 inputOutputLocalIdentifier "Überdrehsicherung löschen" $04 inputOutputControlParameter "RTD - ResetToDefault"  setzt die gespeicherten Einträge bezüglich Überdrehzahlereignissen zurück betrifft folgende Werte: ANZNMAX (Anzahl der aufgetretenen Überdrehzahlereignisse) NMAXVK  (vorgekommene Maximaldrehzahl) KMSTNMAX(Kilometerstand beim Auftreten der letzten Überdrehzahl)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-status-zylinderanzahl"></a>
### STATUS_ZYLINDERANZAHL

Auslesen der Zylinderanzahl KWP2000: $22        ReadDataByCommonIdentifier $40 $0C    "Adaptionswerte 2 Messblock lesen" Entweder 2 oder 4 Zylinder

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZYLINDERANZAHL | int | Zylinderanzahl |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-fs-lesen-spezial"></a>
### FS_LESEN_SPEZIAL

RDBLI Fehlerspeicher lesen (lang, mit FF und Logistik) KWP2000:        0x21 ReadDataByLocalIdentifier 0x0A routineLocalIdentifier 0xXX 0xXX groupOfDTC

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | string | gewaehlter Fehlercode (CDK Nr) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort (CDK high und low Byte) |
| F_ORT_TEXT | string | Fehlerort als Text (CDK-Text) table FOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standart-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standart-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standart-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standart-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standart-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standart-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standart-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standart-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_P_CODE_TEXT | string | table FOrtTexte2 MAX/MIN/SIG/PLAUS-TEXT |
| F_AKTIV_FLAG | string |  |
| F_STOP_FLAG | string |  |
| F_ZYKLUS_FLAG | string |  |
| F_ERROR_FLAG | string |  |
| F_MIL_FLAG | string |  |
| F_ENTPRELL_FLAG | string |  |
| F_HFK | int | immer 1 Haufigkeitszaehler als Zahl Wertebereich 0 - 255 -1: ohne Haufigkeitszaehler |
| F_HLC | int | immer 255 Logistikzaehler als Zahl Wertebereich 0 - 255 -1: ohne Logistikzaehler |
| F_LZ | int | immer 255 Logistikzaehler als Zahl Wertebereich 0 - 255 -1: ohne Logistikzaehler |
| F_CLA | int | Fehlerklasse tabelle FOrtTexte oder lesen in dem Antwortedaten |
| F_FLC | int | Entprellzähler |
| F_DLC | int | Löschzähler |
| F_TSF | int | Schwerezähler |
| F_ART_ANZ | int | Anzahl der Fehlerarten Je nach dieser Anzahl a (a = 0, 1, 2, ...) existieren a mal folgende Results: (long) F_ARTa_NR Index der a. Fehlerart (string) F_ARTa_TEXT Text zur a. Fehlerart |
| F_UW_KM | string | Umweltbedingung Kilometerstand Wertebereich Auftreten Erste-, Zweite- und Letztemal |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen des einzelnen Fehlers |
| F_UW1_NR | long | Index der 1. Umweltbedingung |
| F_UW1_TEXT | string | Text zur 1. Umweltbedingung |
| F_UW1_WERT | real | Wert der 1. Umweltbedingung |
| F_UW1_EINH | string | Einheit der 1. Umweltbedingung |
| F_UW2_NR | long | Index der 2. Umweltbedingung |
| F_UW2_TEXT | string | Text zur 2. Umweltbedingung |
| F_UW2_WERT | real | Wert der 2. Umweltbedingung |
| F_UW2_EINH | string | Einheit der 2. Umweltbedingung |
| F_UW3_NR | long | Index der 3. Umweltbedingung |
| F_UW3_TEXT | string | Text zur 3. Umweltbedingung |
| F_UW3_WERT | real | Wert der 3. Umweltbedingung |
| F_UW3_EINH | string | Einheit der 3. Umweltbedingung |
| F_UW4_NR | long | Index der 4. Umweltbedingung |
| F_UW4_TEXT | string | Text zur 4. Umweltbedingung |
| F_UW4_WERT | real | Wert der 4. Umweltbedingung |
| F_UW4_EINH | string | Einheit der 4. Umweltbedingung |
| F_ZUSAETLICH_PARAM | int | table FUmweltTexte UWNR [0x01 .. 0x0B] Motordrehzahl, Fahrzeuggeschwindigkeit, Motortemperatur ... |
| F_FF1_TEXT | string | Ansauglufttemperatur (tans) |
| F_FF1_WERT | real | Ansauglufttemperatur (tans) |
| F_FF1_EINH | string | Ansauglufttemperatur (tans) |
| F_FF2_TEXT | string | Batteriespannung (ub) |
| F_FF2_WERT | real | Batteriespannung (ub) |
| F_FF2_EINH | string | Batteriespannung (ub) |
| F_FF3_TEXT | string | Drosselklappenwinkel (wdkba) |
| F_FF3_WERT | real | Drosselklappenwinkel (wdkba) |
| F_FF3_EINH | string | Drosselklappenwinkel (wdkba) |
| F_FF4_TEXT | string | Text zur Motortemperatur SAE J1979 |
| F_FF4_WERT | real | Wert der Motortemperatur SAE J1979 |
| F_FF4_EINH | string | Einheit der Motortemperatur SAE J1979 |
| F_FF5_TEXT | string | Text zur Lambda Regelfaktor Bank 1 SAE J1979 |
| F_FF5_WERT | real | Wert der Lambda Regelfaktor Bank 1 SAE J1979 |
| F_FF5_EINH | string | Einheit der Lambda Regelfaktor Bank 1 SAE J1979 |
| F_FF6_TEXT | string | Text zur Lambda Adaptionsfaktor Bank 1 SAE J1979 |
| F_FF6_WERT | real | Wert der Lambda Adaptionsfaktor Bank 1 SAE J1979 |
| F_FF6_EINH | string | Einheit der Lambda Adaptionsfaktor Bank 1 SAE J1979 |
| F_FF7_TEXT | string | Text zur Lambda Regelfaktor Bank 2 SAE J1979 |
| F_FF7_WERT | real | Wert der Lambda Regelfaktor Bank 2 SAE J1979 |
| F_FF7_EINH | string | Einheit der Lambda Regelfaktor Bank 2 SAE J1979 |
| F_FF8_TEXT | string | Text zur Lambda Adaptionsfaktor Bank 2 SAE J1979 |
| F_FF8_WERT | real | Wert der Lambda Adaptionsfaktor Bank 2 SAE J1979 |
| F_FF8_EINH | string | Einheit der Lambda Adaptionsfaktor Bank 2 SAE J1979 |
| F_FF9_TEXT | string | relative Luftmasse (rl) |
| F_FF9_WERT | real | relative Luftmasse (rl) |
| F_FF9_EINH | string | relative Luftmasse (rl) |
| F_FF10_TEXT | string | Text zur Motordrehzahl SAE J1979 (nmot) |
| F_FF10_WERT | real | Wert der Motordrehzahl SAE J1979 (nmot) |
| F_FF10_EINH | string | Einheit der Motordrehzahl SAE J1979 (nmot) |
| F_FF11_TEXT | string | Text zur Fahrzeuggeschwindigkeit entspr. SAE J1979 (vfzg_u) |
| F_FF11_WERT | real | Wert der Fahrzeuggeschwindigkeit entspr. SAE J1979 (vfzg_u) |
| F_FF11_EINH | string | Einheit der Fahrzeuggeschwindigkeit entspr. SAE J1979 (vfzg_u) |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-flash-parameter-lesen"></a>
### FLASH_PARAMETER_LESEN

Gibt die SG-spezifischen Flash-Parameter zurück

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY oder ERROR_DIAG_PROT oder ERROR_SG_AUTHENTISIERUNG |
| SG_ADRESSE | int | Steuergeräteadresse |
| SG_MAXANZAHL_AIF | int | Anzahl der Anwender-Infofelder |
| SG_GROESSE_AIF | int | Grösse des Anwender-Infofeldes |
| SG_ENDEKENNUNG_AIF | int | Offset für letztes Anwender-Infofeld |
| SG_AUTHENTISIERUNG | string | Authentisierungsart table Authentisierung AUTH_TEXT |
| DIAG_PROT_IST | string | Gibt das aktuelle gewählte Protokoll aus table KONZEPT_TABELLE KONZEPT_TEXT |

<a id="job-flash-parameter-setzen"></a>
### FLASH_PARAMETER_SETZEN

Setzt die SG-spezifischen Flash-Parameter

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SG_ADRESSE | int | Steuergeräteadresse |
| SG_MAXANZAHL_AIF | int | Anzahl der Anwender-Infofelder 0x00  Nicht zulässig sonst Anzahl der AIF |
| SG_GROESSE_AIF | int | Grösse des Anwender-Infofeldes 0x12  18 dez kleines AIF 0x33  51 dez grosses AIF 0x40  64 dez grosses AIF ( gilt nur für Power-Pc ) sonst Nicht zulässig |
| SG_ENDEKENNUNG_AIF | int | Offset für letztes Anwender-Infofeld 0xFE  Letztes AIF nicht überschreibbar 0x01  Letztes AIF ist überschreibbar sonst Nicht zulässig |
| SG_AUTHENTISIERUNG | string | Authentisierungsart table Authentisierung AUTH_TEXT |
| DIAG_PROT | string | optionaler Parameter Diagnoseprotokoll table KONZEPT_TABELLE KONZEPT_TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |

<a id="job-status-adc-werte"></a>
### STATUS_ADC_WERTE

Auslesen der unverarbeiteten Rohwerte der analogen Eingänge KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_UB_TEXT | string | Batteriespannung |
| STAT_UB_EINH | string | Batteriespannung |
| STAT_UB_WERT | real | Batteriespannung |
| STAT_DKP_TEXT | string | DK-Poti |
| STAT_DKP_EINH | string | DK-Poti |
| STAT_DKP_WERT | real | DK-Poti |
| STAT_TMOT_TEXT | string | Motortemperatur |
| STAT_TMOT_EINH | string | Motortemperatur |
| STAT_TMOT_WERT | real | Motortemperatur |
| STAT_TANS_TEXT | string | Ansauglufttemperatur |
| STAT_TANS_EINH | string | Ansauglufttemperatur |
| STAT_TANS_WERT | real | Ansauglufttemperatur |
| STAT_TZYL1_TEXT | string | Temperatur Zylinderkopf links |
| STAT_TZYL1_EINH | string | Temperatur Zylinderkopf links |
| STAT_TZYL1_WERT | real | Temperatur Zylinderkopf links |
| STAT_TZYL2_TEXT | string | Temperatur Zylinderkopf links |
| STAT_TZYL2_EINH | string | Temperatur Zylinderkopf links |
| STAT_TZYL2_WERT | real | Temperatur Zylinderkopf links |
| STAT_KS1_TEXT | string | Integrator Wert Klopfsensor 1 |
| STAT_KS1_EINH | string | Integrator Wert Klopfsensor 1 |
| STAT_KS1_WERT | real | Integrator Wert Klopfsensor 1 |
| STAT_KS2_TEXT | string | Integrator Wert Klopfsensor 2 |
| STAT_KS2_EINH | string | Integrator Wert Klopfsensor 2 |
| STAT_KS2_WERT | real | Integrator Wert Klopfsensor 2 |
| STAT_GETRG_TEXT | string | Getriebe Schaltwalze |
| STAT_GETRG_EINH | string | Getriebe Schaltwalze |
| STAT_GETRG_WERT | real | Getriebe Schaltwalze |
| STAT_DSK_TEXT | string | Kraftstoffdruck |
| STAT_DSK_EINH | string | Kraftstoffdruck |
| STAT_DSK_WERT | real | Kraftstoffdruck |
| STAT_LSVK1_TEXT | string | Lambdasonde1 |
| STAT_LSVK1_EINH | string | Lambdasonde1 |
| STAT_LSVK1_WERT | real | Lambdasonde1 |
| STAT_LSVK2_TEXT | string | Lambdasonde2 |
| STAT_LSVK2_EINH | string | Lambdasonde2 |
| STAT_LSVK2_WERT | real | Lambdasonde2 |
| STAT_SYS_TEXT | string | Betriebspannung System |
| STAT_SYS_EINH | string | Betriebspannung System |
| STAT_SYS_WERT | real | Betriebspannung System |
| STAT_ISYS_TEXT | string | Betriebstrom System |
| STAT_ISYS_EINH | string | Betriebstrom System |
| STAT_ISYS_WERT | real | Betriebstrom System |
| STAT_ZDG_TEXT | string | Betriebspannung Zündung |
| STAT_ZDG_EINH | string | Betriebspannung Zündung |
| STAT_ZDG_WERT | real | Betriebspannung Zündung |
| STAT_IZDG_TEXT | string | Betriebstrom Zündung |
| STAT_IZDG_EINH | string | Betriebstrom Zündung |
| STAT_IZDG_WERT | real | Betriebstrom Zündung |
| STAT_EKP_TEXT | string | Betriebspannung EKP |
| STAT_EKP_EINH | string | Betriebspannung EKP |
| STAT_EKP_WERT | real | Betriebspannung EKP |
| STAT_IEKP_TEXT | string | Betriebstrom EKP |
| STAT_IEKP_EINH | string | Betriebstrom EKP |
| STAT_IEKP_WERT | real | Betriebstrom EKP |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-l-sonde"></a>
### STATUS_L_SONDE

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LSVK1_TEXT | string | Lambdasonde1 |
| STAT_LSVK1_WERT | real | Lambdasonde1 |
| STAT_LSVK1_EINH | string | Lambdasonde1 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-l-sonde-2"></a>
### STATUS_L_SONDE_2

KWP2000: $30 InputOutputControlByLocalIdentifier $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LSVK2_TEXT | string | Lambdasonde2 |
| STAT_LSVK2_WERT | real | Lambdasonde2 |
| STAT_LSVK2_EINH | string | Lambdasonde2 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-l-add"></a>
### STATUS_L_ADD

Auslesen der additiven Lambdaregelung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_L_ADD_WERT | real | Wert des additiven Lambdaregelung |
| STAT_L_ADD_EINH | string | Einheit des additiven Lambdaregelung |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-status-l-add-2"></a>
### STATUS_L_ADD_2

Auslesen der additiven Lambdaregelung Bank2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_L_ADD_2_WERT | real | Wert des additiven Lambdaregelung Bank2 |
| STAT_L_ADD_2_EINH | string | Einheit des additiven Lambdaregelung Bank2 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-status-l-int"></a>
### STATUS_L_INT

Auslesen der Lambdaregelung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_L_INT_WERT | real | Wert der Lambdasondenregelung |
| STAT_L_INT_EINH | string | Einheit der Lambdasondenregelung |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-status-l-int-2"></a>
### STATUS_L_INT_2

Auslesen der Lambdaregelung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_L_INT_2_WERT | real | Wert der Lambdasondenregelung |
| STAT_L_INT_2_EINH | string | Einheit der Lambdasondenregelung |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-status-l-mul"></a>
### STATUS_L_MUL

Auslesen der multiplikativen Lambdaregelung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_L_MUL_WERT | real | Wert der multiplikativen Lambdaregelung |
| STAT_L_MUL_EINH | string | Einheit der multiplikativen Lambdaregelung |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-status-l-mul-2"></a>
### STATUS_L_MUL_2

Auslesen der multipikativen Lambdaregelung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_L_MUL_2_WERT | real | Wert der multiplikativen Lambdaregelung |
| STAT_L_MUL_2_EINH | string | Einheit der multiplikativen Lambdaregelung |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-status-motorlaufunruhe"></a>
### STATUS_MOTORLAUFUNRUHE

KWP2000:    $22     ReadDataByCommonIdentifier $40 $03 RecordCommonIdentifier "Laufunruhewert lesen"  Auslesen der Laufunruhewerte (Laufqualität) Werte stellen ein Maß für die Verbrennungsqualität der einzelnen Zylinder dar

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZYL1_WERT | real | Wert von LUTSFI1 |
| STAT_ZYL2_WERT | real | Wert von LUTSFI2 |
| STAT_ZYL3_WERT | real | Wert von LUTSFI3 |
| STAT_ZYL4_WERT | real | Wert von LUTSFI4 |
| STAT_LAUFUNRUHE_EINH | string | Einheit in sec^-2 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-status-spi-max-t-time"></a>
### STATUS_SPI_MAX_T_TIME

KWP2000:    $30 InputOutputControlByLocalIdentifier Request Service Id $5C inputOutputLocalIdentifier Raw Data $01 inputOutputControlParameter "RCS - ReportCurrentState"  liefert die maximale Übertragungszeit aller bisherigen SPI Sequenzen Übertragungzeit entspricht der Zeitdauer des folgenden Ablaufs: 1. Eintrag vorbereiteter SPI-Sequenz in die Sequenz-Queue - Zeitmarke speichern 2. Senden der Sequenz an einen peripheren Baustein 3. Empfang der Antwortdaten 4. Auslesen dieser Daten aus dem Hardwarepuffer der SPI-Schittstelle -&gt; Zeitdauer 1 - 4 ermitteln

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MAX_TIME_EINH | string | max SPI Übertragungszeit |
| STAT_MAX_TIME_WERT | real | max SPI Übertragungszeit |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-ekp-entsperren"></a>
### STEUERN_EKP_ENTSPERREN

KWP2000 :   $30 InputOutputControlByLocalIdentifier Request Service Id $D4 inputOutputLocalIdentifier "Sperrbedingung EKP" $04 inputOutputControlParameter "RTD - ResetToDefault"  entsperrt die EKP, Anlasserfreigabe, Einspitzung und Zuendung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-ekp-sperren"></a>
### STEUERN_EKP_SPERREN

KWP2000 :   $30 InputOutputControlByLocalIdentifier Request Service Id $D4 inputOutputLocalIdentifier "Sperrbedingung EKP" $05 inputOutputControlParameter "FCS - FreezeCurrentState" KWP2000 :   $22     ReadDataByCommonIdentifier $40 $00 RecordCommonIdentifier "Meßwerte lesen"  sperrt die EKP, Anlasserfreigabe, Einspritzung und Zuendung Nebenbedingung: Drehzahl muß Null sein.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-access-timing-parameter"></a>
### ACCESS_TIMING_PARAMETER

KWP2000:    $83 AccessTimingParamater Request Service Id $xx timingParameterIdentifier  ermöglicht auslesen und modifizieren der Flash-Zugriffsparameter

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | int | 0 = readLimitsOfPossibleTimingParameter 1 = setTimingParamatersToDefaultValue 2 = readCurrentlyActivetimingParamaters 3 = setTimingParametersToGivenValues .       default .       $32 P2min = 25 ms (0,5 ms Res.) .       $02 P2max = 50 ms (25 ms Res.) .       $6E P3min = 55 ms ( 0.5 ms Res.) .       $14 P3max = 5000 ms ( 250 ms Res.) .       $0A P4min = 5 ms (0,5 ms Res.) |
| P2_MIN | int | Time between tester request and ECU response or two ECU responses (0,5 ms Res.) |
| P2_MAX | int | Time between tester request and ECU response or two ECU responses (25 ms Res.) |
| P3_MIN | int | Time between end of ECU responses and start of new tester request ( 0.5 ms Res.) |
| P3_MAX | int | Time between end of ECU responses and start of new tester request ( 250 ms Res.) |
| P4_MIN | int | Inter byte time for tester request (0,5 ms Res.) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| P2_MIN_WERT | int | Time between tester request and ECU response or two ECU responses (ms) |
| P2_MAX_WERT | int | Time between tester request and ECU response or two ECU responses (ms) |
| P3_MIN_WERT | int | Time between end of ECU responses and start of new tester request (ms) |
| P3_MAX_WERT | int | Time between end of ECU responses and start of new tester request (ms) |
| P4_MIN_WERT | int | Inter byte time for tester request (ms) |
| MODE_TEXT | string | Mode) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-steuern-fahrgestellnummer"></a>
### STEUERN_FAHRGESTELLNUMMER

17 ASCII "Fahrgestellnummer" schreiben KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $30 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NUMMER | string | "Fahrgestellnummer" 17 x {1...0A...Z} ======&gt; Byte0-16 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fahrgestellnummer"></a>
### STATUS_FAHRGESTELLNUMMER

17 ASCII Byte Fahrgestell-Nummer KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $30 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FGNUMMER | string | ausgelesene Fahrgestellnummer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-prog-location-datum"></a>
### STEUERN_PROG_LOCATION_DATUM

Schreibt 3 Byte "Programmier-Ort/Datum"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $29 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PROG_LOCATION | unsigned char | "Ort":   0-15 ======&gt; Byte0, Bit4-7 |
| PROG_TIME_DAY | unsigned char | "Tag":   1-31 ======&gt; Byte1 |
| PROG_TIME_MONTH | unsigned char | "Monat": 1-12 ======&gt; Byte0, Bit0-3 |
| PROG_TIME_YEAR_2_DIGITS | unsigned int | "Jahr":  0-99 ======&gt; Byte2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-prog-location-datum"></a>
### STATUS_PROG_LOCATION_DATUM

Ort und Datum der ECU-Programmierung KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $29 Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PROG_LOCATION | unsigned char | "Ort":   0-15 Byte0 |
| STAT_PROG_TIME_MONTH | unsigned char | "Monat": 1-12 Byte1 |
| STAT_PROG_TIME_DAY | unsigned int | "Tag":   1-31 Byte2 |
| STAT_PROG_TIME_YEAR_2_DIGITS | unsigned char | "Jahr":  0-99 Byte3 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-trsp-init"></a>
### STEUERN_TRSP_INIT

KWP2000:    $3B WriteDataByLocalIdentifier Request Service Id $2A recordLocalIdentifier "TFA - Transponder Funktion Aktivieren"  dient der Aktivierung/Deaktivierung des Transponders(Ringantenne) Nutzung für den Werksprozess Bedingung: SG nicht verriegelt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | "Daten": z.B. "0xAA,0xAA,0xAA" =&gt; aktivieren o."0xFF,0xFF,0xFF" =&gt; deaktivieren ======&gt; Byte 0 - 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-trsp-init"></a>
### STATUS_TRSP_INIT

aktueller Status "TRSP, Init-Kennung" KWP2000:    $21 ReadDataByLocalIdentifier Request Service Id $2A recordLocalIdentifier "Funktion Transponder"  ermittelt den Aktivierungsstatus des Transponders(Ringantenne) Nutzung für den Werksprozess - aktiviert:    "0xAA,0xAA,0xAA" - deaktiviert:  "0xFF,0xFF,0xFF"

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TRSP_INIT | binary | 3 Byte |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-status-mechanischer-schluesselcode"></a>
### STATUS_MECHANISCHER_SCHLUESSELCODE

KWP2000:    $21 ReadDataByLocalIdentifier Request Service Id $28 recordLocalIdentifier  mechanischer Schliesscode ist in jedem Schlüssel hinterlegt wird vom SG aus dem ersten angelernten Schlüssel übernommen job liefert Schliesscode aus SG (0000Kxxxxx) Default Schliesscode vor dem ersten angelernten Schlüssel - 0000K00000

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SCHLUESSELCODE | string | ausgelesener Mechanischer Schluesselcode |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-aktueller-schluessel"></a>
### STATUS_AKTUELLER_SCHLUESSEL

aktuelle Schluessel KWP2000:    $21 ReadDataByLocalIdentifier $35 recordLocalIdentifier Modus   : Default liest die aktuellen Statusinformationen zum gesteckten Schluessel

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KEY_IS_VALID | unsigned char | Bereich 0/1, Byte0, Bit0 Authentisierung erfolgt |
| STAT_KEY_IS_LOCKED | unsigned char | Bereich 0/1, Byte0, Bit1 Authentisierung erfolgt, Schluessel aber per Daten gesperrt |
| STAT_KEY_ERR | unsigned char | Bereich 0/1, Byte0, Bit2 Authentisierung fehlgeschlagen |
| STAT_ID_FOUND | unsigned char | Bereich 0/1, Byte0, Bit3 TRSP-ID in ECU bekannt |
| STAT_DEFAULT_AUTH | unsigned char | Bereich 0/1, Byte0, Bit4 Authentisierung mit Defaultwerten durchgeführt |
| STAT_NS_AUTH | unsigned char | Bereich 0/1, Byte0, Bit5 Authentisierung als Nachschlüssel |
| STAT_EE_MREWS_INIT | unsigned char | Bereich 0/1, Byte0, Bit6 ECU verriegelt |
| STAT_EE_TRSP_INIT | unsigned char | Bereich 0/1, Byte0, Bit7 TRSP-SW aktiviert Byte 1, Diagnoseinfo TRSP-SW, TRSP-Kommunikation |
| STAT_COM_NO_ERR | unsigned char | kein Fehler |
| STAT_COM_NO_ID | unsigned char | Authentisierung konnte mit keinem Schluesseldatensatz durchgeführt werden |
| STAT_COM_WRONG_P3 | unsigned char | Authentisierung scheitert da Page3 nicht korrekt |
| STAT_COM_TIME_OUT | unsigned char | Schnittstelle hat keine Daten mehr empfangen |
| STAT_COM_ANTENNA_FAIL | unsigned char | ABIC meldet Fehler im Antennenkreis |
| STAT_COM_IRQ_ERROR | unsigned char | Schnittstellen-SW meldet IRQ-Fehler |
| STAT_COM_WRONG_WRITE_CMD | unsigned char | Falsche Bestätigung für den Schreibbefehl empfangen |
| STAT_COM_DREAD_ERROR | unsigned char | 2fach Lesen liefert ungleiches Ergebnis |
| STAT_COM_RAW_ERROR | unsigned char | Lesen nach Schreiben liefert ungleiches Ergebnis Byte 2, Statusbyte aktueller Schlüssel (laut LH) wird zu null gesetzt falls kein gültiger Schluessel gefunden ist |
| STAT_KEY_USED | unsigned char | Bereich 0/1, Byte2, Bit0 Schluessel benutzt |
| STAT_MEC_CODE_OK | unsigned char | Bereich 0/1, Byte2, Bit1 mechanischer Schluesselcode gültig |
| STAT_MEC_CODE_NOT_TESTED | unsigned char | Bereich 0/1, Byte2, Bit2 mechanischer Schluesselcode nicht getestet |
| STAT_KEY_AUTOINIT | unsigned char | Bereich 0/1, Byte2, Bit3 Auto-Init im Werk |
| STAT_KEY_TYPE | unsigned char | Bereich 0/1, Byte2, Bit4/5/6 Schluesseltyp (010=GB-Key,011=Standard-Key,111=Nach-Key) |
| STAT_ERC | unsigned char | Bereich 0/1, Byte2, Bit7 CRC Checksummenfehler Byte 3, Initialisierungs-Status aktueller Schluessel (laut LH) wird zu null gesetzt,  falls kein gueltiger Schluessel gefunden ist |
| STAT_INIT_COMPLETED | unsigned char | Initialisierung komplett (EEProm des Transponders gesperrt) |
| STAT_PAGE_4_7_OK | unsigned char | Page 4-7 geschrieben |
| STAT_PAGE_1_3_OK | unsigned char | Page 1,2,3 geschrieben und verifiziert |
| STAT_PAGE_1_2_OK | unsigned char | Page 1,2 (Secret-Key komplett) geschrieben und verifiziert |
| STAT_PAGE_2_OK | unsigned char | Page 2 (Secret-High) geschrieben und verifiziert |
| STAT_ID_MECHSC_SAVED | unsigned char | Identifier und mechanischer Code in BMS-K Flashspeicher geschrieben |
| STAT_INIT_START | unsigned char | Initialisierungszustand nach Codierung (CAS-Init durch Diagnose) |
| STAT_INIT_DEFAULT | unsigned char | Anlieferungszustand Byte 4, Schluesselnummer des aktuellen Schluessels (0-10,0=ungueltiger Key) |
| STAT_KEY_NUMBER | unsigned char | Bereich: 0-10 Schluessel (0=ungueltiger Schluessel) Byte4 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-status-mrews-diagnose"></a>
### STATUS_MREWS_DIAGNOSE

aktuelle Schluessel KWP2000:    $21 ReadDataByLocalIdentifier $34 recordLocalIdentifier Modus  : Default liest die Diagnoseinformationen bzgl. EWS-SG, Ringantenne und Transponder

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BTS_ACTIV | unsigned char | Bereich 0/1, Byte0, Bit0 Status Spannungsversorgung für Ringantenne |
| STAT_KILL_ACTIV | unsigned char | Bereich 0/1, Byte0, Bit1 Status Kill-Schalter(unterbricht Spannungversorgung zur Ringantenne) |
| STAT_CRC_ERROR | unsigned char | Bereich 0/1, Byte0, Bit2 Status CRC-Fehler für alle MREWS-Daten |
| STAT_EWS_AUTHENT | unsigned char | Bereich 0/1, Byte0, Bit3 Authentisierung mit aktuellem Schluessel erfolgt |
| STAT_ID_FOUND | unsigned char | Bereich 0/1, Byte0, Bit4 TRSP sendet bekannte ID |
| STAT_INIT_STATUS_KEY | unsigned char | Bereich 0/1, Byte0, Bit5 Status Init-Byte==0 aktueller Schlüssel |
| STAT_WIR_ACTIV | unsigned char | Bereich 0/1, Byte0, Bit6 Diagnoseinfo aus Werksinitalisierung Status Werks-Init aktiv -&gt; Kriterium für Bewertung Status Byte2 |
| STAT_NSR_ACTIV | unsigned char | Bereich 0/1, Byte0, Bit7 Diagnoseinfo aus NAchschlüsselinitalisierung Byte0, Bit7 |
| STAT_MREWS_INIT_DONE | unsigned char | Bereich 0/1, Byte1, Bit0 ECU verriegelt |
| STAT_TRSP_INIT_DONE | unsigned char | Bereich 0/1, Byte1, Bit1 TRSP-SW aktiviert |
| STAT_LOW_VOLTAGE | unsigned char | Bereich 0/1, Byte1, Bit2 Unterspannung detektiert |
| STAT_SW_EXTENSION | unsigned char | Bereich 0/1, Byte1, Bit7 Unterspannung detektiert Byte 2, Fehlermeldungen im Ablauf WIR oder NSR |
| STAT_NO_ERR | unsigned char | kein Fehler |
| STAT_COMM_ABORTED | unsigned char | TRSP-Kommando abgebrochen  -&gt; weitere Bewertung siehe Status Byte3 |
| STAT_KEY_WRONG_MECH_KEY | unsigned char | gesetzt wenn ein STAT_MECHSC_xxx_xxx gesetzt |
| STAT_MECHSC_ASCII_BCD | unsigned char | Fehler bei Umcodierung Daten für mechanischen Schliesscode ASCII zu BCD |
| STAT_MECHSC_BCD_ASCII | unsigned char | Fehler bei Umcodierung Daten für mechanischen Schliesscode BCD zu ASCII |
| STAT_MECHSC_IN_TRSP | unsigned char | mechanischer Schliesscode im TRSP nicht plausibel (laut LH) |
| STAT_MECHSC_NOT_EQUAL | unsigned char | mechanischer Schliesscode im TRSP und in ECU stimmt nicht überein |
| STAT_KEY_TYP_NOT_EQUAL | unsigned char | Schluesseltyp in TRSP und ECU stimmen nicht überein |
| STAT_KEY_TYPE_IN_TRSP | unsigned char | Schluesseltyp in TRSP nicht plausibel |
| STAT_KEY_NO_NORMAL_KEY | unsigned char | kein normaler Schluessel gesteckt |
| STAT_KEY_NO_POCKET_KEY | unsigned char | kein Geldboersenschluessel gesteckt |
| STAT_FGNR_ASCII_BCD | unsigned char | Fehler bei Umcodierung Daten für Fahrgestellnummer ASCII zu BCD |
| STAT_FGNR_BCD_ASCII | unsigned char | Fehler bei Umcodierung Daten für Fahrgestellnummer BCD zu ASCII |
| STAT_FGNR_NOT_EQUAL | unsigned char | Fahrgestellnummer im TRSP und in ECU stimmt nicht ueberein |
| STAT_CRYPTO_DATA | unsigned char | Fehler TRSP-Daten für Nachschluessel in ECU |
| STAT_ID_UNKNOWN | unsigned char | TRSP-ID unbekannt Byte 3, Diagnoseinfo TRSP-SW, TRSP-Kommunikation |
| STAT_COM_NO_ERR | unsigned char | kein Fehler |
| STAT_COM_NO_ID | unsigned char | Authentisierung konnte mit keinem Schluesseldatensatz durchgefuehrt werden |
| STAT_COM_WRONG_P3 | unsigned char | Authentisierung scheitert da Page3 nicht korrekt |
| STAT_COM_TIME_OUT | unsigned char | Schnittstelle hat keine Daten mehr empfangen |
| STAT_COM_ANTENNA_FAIL | unsigned char | ABIC meldet Fehler im Antennenkreis |
| STAT_COM_IRQ_ERROR | unsigned char | Schnittstellen-SW meldet IRQ-Fehler |
| STAT_COM_WRONG_WRITE_CMD | unsigned char | Falsche Bestaetigung für den Schreibbefehl empfangen |
| STAT_COM_DREAD_ERROR | unsigned char | 2fach Lesen liefert ungleiches Ergebnis |
| STAT_COM_RAW_ERROR | unsigned char | Lesen nach Schreiben liefert unerwartetes Ergebnis |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mrews-init"></a>
### STEUERN_MREWS_INIT

KWP2000:    $3B WriteDataByLocalIdentifier $2C recordLocalIdentifier "IES - Initialisierungserkennung-status"  ermöglicht Verriegelung des SG keine Entriegelung möglich ! sperrt einige Diagnose-Jobs, z.B.: STATUS_SCHLUESSELDATEN STEUERN_SCHLUESSELDATEN STEUERN_FAHRGESTELLNUMMER STEUERN_TRSP_INIT STEUERN_PROG_LOCATION_DATUM STEUERN_MECHANISCHER_SCHLUESSELCODE

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | "Daten": z.B. "0xAA,0xAA,0xAA" =&gt; verriegelt o."0xFF,0xFF,0xFF" =&gt; nicht verriegelt ======&gt; Byte 0 - 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mrews-init"></a>
### STATUS_MREWS_INIT

aktueller Status "MREWS, Init-Kennung" KWP2000:    $21 ReadDataByLocalIdentifier $2C recordLocalIdentifier  Feststellung, ob das SG verriegelt ist

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MREWS_INIT | binary | 3 Byte =&gt; "0xAA,0xAA,0xAA" =&gt; SG verriegelt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-schluessel-sperren"></a>
### STEUERN_SCHLUESSEL_SPERREN

Schreibt 1 Byte "Schluessel-Sperre"  KWP2000:    $3B WriteDataByLocalIdentifier $2E recordLocalIdentifier Modus  :    Default sperrt den über die Schluesselnummer eingegebenen Schluessel mit diesem gesperrten Schluessel kein Fahrzeugstart mehr möglich zum Sperren muß Schluessel gesteckt sein -&gt; dieser nicht sperrbar

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KEY_NUMBER | unsigned int | Schluesselnummer: 1...10 ======&gt; Byte0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-schluessel-freigeben"></a>
### STEUERN_SCHLUESSEL_FREIGEBEN

Schreibt 1 Byte "Schluessel-Nummer"  KWP2000:    $3B WriteDataByLocalIdentifier $2F recordLocalIdentifier Modus  :    Default gibt den über die Schluesselnummer eingegebenen Schlüssel frei

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KEY_NUMBER | unsigned int | "Nr.":   1-10 ======&gt; Byte0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-trsp-daten"></a>
### STATUS_TRSP_DATEN

KWP2000:    $21 ReadDataByLocalIdentifier $xx recordLocalIdentifier, $40-$49  auslesen bestimmter Statusdaten aus SG fuer den eingegebenen Schluessel

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SCHLUESSEL_NUMMER | int | Werte: 1...10 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATE1 | unsigned char | Bereich Byte 0, Bit 0 - 7 1. Schlüssel-Status-Byte(NOT_VALID_KEY): gesperrt=TRUE/frei=FALSE |
| STAT_STATE2 | unsigned char | Bereich Byte 1, Bit 0 - 7 2. Schlüssel-Status-Byte: x x x x x x x x \| \| \| \| \| \| \| \|-&gt; Bit 0:  ERC-Checksummenfehler \| \| \| \| \| \| \|---&gt; Bit 1:  Bit 1 - 3 -&gt; Typ: 010 GB_KEY \| \| \| \| \| \|-----&gt; Bit 2:                    011 FB_KEY \| \| \| \| \|-------&gt; Bit 3:                    111 NS_KEY \| \| \| \|---------&gt; Bit 4:  1=automatisch zu initialisieren \| \| \|                     0=bereits initialisiert \| \| \|-----------&gt; Bit 5:  1=mech. Schlüsselcode noch nicht getestet \| \|                       0=mech. Schlüsselcode getestet \| \|-------------&gt; Bit 6:  1=mech. Schlüsselcode gültig \|                         0=mech. Schlüsselcode nicht gültig \|---------------&gt; Bit 7:  1=Schlüssel benutzt 0=Schlüssel unbenutzt |
| STAT_INITIALISIERUNG | unsigned char | Bereich Byte 2, Bit 0 - 7 Initialisierungs-Status-Byte: 0x0   ISTATE_OK 0x1   ISTATE_P_4to7_OK 0x2   ISTATE_P_1to3_OK 0x3   ISTATE_P_1and2_OK 0x4   ISTATE_P_2_OK 0x5   ISTATE_ID_MECHSC_SAVED 0x6   ISTATE_MECHSC_OK 0x7   ISTATE_DEFAULT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-schluesseldaten"></a>
### STATUS_SCHLUESSELDATEN

Auslesen der SCHLUESSELDATEN KWP2000 :   $21 ReadDataByLocalIdentifier $36...$3F  recordLocalIdentifier Modus   :   Default listet die kompletten Schluesseldaten aus SG-Tabelle zur eingegebenen Schluesselnummer auf Ausführung ist nur vor der Verriegelung möglich

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SCHLUESSEL_NUMMER | int | Werte: 1...10 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_BYTE1 | unsigned char | Schluessel-Status-Byte1 |
| STAT_STATUS_BYTE2 | unsigned char | Schluessel-Status-Byte2 |
| STAT_INITIALISIERUNGSSTATUS | unsigned char | Initialisierungsstatus |
| STAT_IDENTIFIER | binary | Schluessel-Identifier, 4 Byte |
| STAT_SECRET_KEY | binary | Secret Key, 6 Byte |
| STAT_CONFIG_BYTE | unsigned char | Config-Byte |
| STAT_PASSWORD_TRANSPONDER | binary | Password Transponder, 3 Byte |
| STAT_CRC_BYTE | unsigned char | CyclicRedundancyCheck-Byte |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-schluesseldaten"></a>
### STEUERN_SCHLUESSELDATEN

Schreibt 17 Byte "Schluessel-Daten"  KWP2000:    $3B WriteDataByLocalIdentifier $36...$3F recordLocalIdentifier Modus  :    Default dient dem Befüllen der internen Schluesseltabelle vor dem eigentlichen Schluesselanlernen Ausführung ist nur vor der Verriegelung möglich

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KEY_NUMBER | int | "Schl-Nr": 1-10 ======&gt; Array-Index |
| STATUS_BYTE1 | unsigned char | "Status1": 0-255 ======&gt; Byte 0 |
| STATUS_BYTE2 | unsigned char | "Status1": 0-255 ======&gt; Byte 1 |
| INITIALISIERUNGSSTATUS | unsigned char | "Init-Status": 0-255 ======&gt; Byte 2 |
| IDENTIFIER | string | "Identifier": (z.B. 0x01,0x02,0x03,0x04) ======&gt; Byte 3-6 |
| SECRET_KEY | string | "Secret Key": (z.B. 0x01,0x02,0x03,0x04,0x05,0x06) ======&gt; Byte 7-12 |
| CONFIG_BYTE | unsigned char | Config-Byte ======&gt; Byte 13 |
| PASSWORD_TRANSPONDER | string | "Password-Transponder": (z.B. 0x01,0x02,0x03) ======&gt; Byte 14-16 |
| CRC_BYTE | unsigned char | "CyclicRedundancyCheck": 0-255 ======&gt; Byte 17 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-steuern-mechanischer-schluesselcode"></a>
### STEUERN_MECHANISCHER_SCHLUESSELCODE

5 ASCII "Mechanischer Schliesscode" schreiben KWP2000: $3B WriteDataByLocalIdentifier $28 recordLocalIdentifier "MSC - mechanischer Schlüsselcode"  speichert/schreibt mechanischen Schliesscode des Schluessels ins SG dient der Ersatzteilcodierung und der Nacharbeit nur bei unverriegeltem SG möglich

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SCHLUESSELCODE | string | siehe STATUS_MECHANISCHER_SCHLUESSELCODE |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-interfacetyp"></a>
### INTERFACETYP

Ermitteln des Interface-Typ

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| INTERFACE_TYP | string | Interface-Typ |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-steuern-grundadaption-anfordern"></a>
### STEUERN_GRUNDADAPTION_ANFORDERN

KWP2000 : $31 Start Routine By Local Identifier Request Service Id $32 routineLocalIdentifier legt Grundadaption fuer Tankentlueftungssystem an wird erst bei Klemme 15 AUS/EIN zurueckgesetzt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-pm-aktivieren"></a>
### STEUERN_PM_AKTIVIEREN

KWP2000 : $31 Start Routine By Local Identifier Request Service Id $83 inputOutputLocalIdentifier "EWS initialisieren"

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-trsp-auth"></a>
### STATUS_TRSP_AUTH

Transponder Page KWP2000:    $21 ReadDataByLocalIdentifier $4C recordLocalIdentifier  vor Ausführung dieses Jobs muß STEUERN_TRSP_AUTH ausgeführt werden manuelle Authentisierung des TRSP und lesen/plausibilisieren der relevanten Pages

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KEY_AUTHENT | unsigned char | Byte0, Bit0, Bereich 0/1 1=Authentisierung Schluessel erfolgt |
| STAT_MECH_SC_EQUAL | unsigned char | Byte0, Bit1, Bereich 0/1 1=mechanischer Schliesscode im Schluessel und in der BMSK identisch |
| STAT_NO_MECH_SC_ECU | unsigned char | Byte0, Bit2, Bereich 0/1 1=kein mechanischer Schliesscode in der BMSK gespeichert |
| STAT_FGNR_EQUAL | unsigned char | Byte0, Bit3, Bereich 0/1 1=Fahrgestellnummer im Schluessel und in der BMSK identisch |
| STAT_NO_FGNR_ECU | unsigned char | Byte0, Bit4, Bereich 0/1 1=keine Fahrgestellnummer in BMSK gespeichert Byte 1, Diagnoseinfo TRSP-SW, TRSP-Kommunikation |
| STAT_NO_ERR | unsigned char | kein Fehler |
| STAT_NO_ID | unsigned char | Authentisierung konnte mit keinem Schluesseldatensatz durchgeführt werden |
| STAT_WRONG_P3 | unsigned char | Authentisierung scheitert da Page3 nicht korrekt |
| STAT_TIME_OUT | unsigned char | Schnittstelle hat keine Daten mehr empfangen |
| STAT_ANTENNA_FAIL | unsigned char | ABIC meldet Fehler im Antennenkreis |
| STAT_IRQ_ERROR | unsigned char | Schnittstellen-SW meldet IRQ-Fehler |
| STAT_WRONG_WRITE_CMD | unsigned char | Falsche Bestätigung für den Schreibbefehl empfangen |
| STAT_DREAD_ERROR | unsigned char | 2fach Lesen liefert ungleiches Ergebnis |
| STAT_RAW_ERROR | unsigned char | Lesen nach Schreiben liefert ungleiches Ergebnis |
| STAT_PAGE4 | binary | Inhalt Page 4 der TRSP OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PAGE5 | binary | Inhalt Page 5 der TRSP OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PAGE6 | binary | Inhalt Page 6 der TRSP OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-trsp-auth"></a>
### STEUERN_TRSP_AUTH

Schreibt 5 Byte "TRSP-Page"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $33 Modus  : Default dieser Job muß vor STATUS_TRSP_AUTH ausgeführt werden

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUTHENTISIERUNGSSTATE | unsigned char | "Art der Authentisierung" ======&gt; Byte0 0 = Standardauthenisierung 1 = Authentisierung mit default Schluesseln 2 = Authenisierung mit übergebenen Schluesseln |
| SECRET_KEY | string | "Secret Key": (z.B. 0x01,0x02,0x03,0x04,0x05,0x06) ======&gt; Byte 1-6 Wird nur im Modus 2 benoetigt |
| PASSWORD_TRANSPONDER | string | "Password-Transponder": (z.B. 0x01,0x02,0x03) ======&gt; Byte 7-10 Wird nur im Modus 2 benoetigt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-read-trsp-page"></a>
### STATUS_READ_TRSP_PAGE

Transponder Page KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $4A Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TRANSPONDER_PAGE | binary | Transponder Page |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-cmd-read-page-trsp"></a>
### STEUERN_CMD_READ_PAGE_TRSP

Schreibt 1 Byte "Transponder Page"  KWP 2000: $3B WriteDataByLocalIdentifier LocalIdentifier $31 Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PAGE_NUMMER | unsigned char | "Page": 0-7,0xFF, "WUP": 0xFE ======&gt; Byte0 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-write-page-trsp"></a>
### STATUS_WRITE_PAGE_TRSP

Page TRSP KWP 2000: $21 ReadDataByLocalIdentifier LocalIdentifier $4B Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANSWER | unsigned char | Test Data |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-cmd-write-page-trsp"></a>
### STEUERN_CMD_WRITE_PAGE_TRSP

Schreibt 5 Byte "TRSP-Page"  KWP2000: $3B WriteDataByLocalIdentifier LocalIdentifier $32 Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PAGE | unsigned char | "Page": 0-7, 0xFF, "WUP": 0xFE ======&gt; Byte0 |
| DATA_HIGH | string | "High": 0x0000 bis 0xFFFF ======&gt; Byte1-2 =========================================== ALTERNATIV 4 Bytes "High und Low": 0x00000000 bis 0xFFFFFFFF |
| DATA_LOW | string | "Low":  0x0000 bis 0xFFFF ======&gt; Byte3-4 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-nockenwellendiagnose-an"></a>
### STEUERN_NOCKENWELLENDIAGNOSE_AN

KWP2000 :   $30 InputOutputControlByLocalIdentifier Request Service Id $D6 inputOutputLocalIdentifier "Freigabe Anlasser und Sperren Zuendung und Einsprizung" $08 inputOutputControlParameter "LTA - LongtermAdjustment" KWP2000 :   $22     ReadDataByCommonIdentifier $40 $00 RecordCommonIdentifier "Meßwerte lesen"  sperrt die Einspritzung und Zuendung und gibt gleichzeitig den Anlasser frei Dazu werden die Interruptzaehler der Kurbelwelle und Nockenwelle angzeigt Nebenbedingung: Drehzahl muß kleiner als 500 U/min sein.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KW_ZAEHLER_WERT | real | Wert des Interruptzaehler der Kurbelwelle |
| STAT_NW_ZAEHLER_WERT | real | Wert des Interruptzaehler der Nockenwelle |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-nockenwellendiagnose-aus"></a>
### STEUERN_NOCKENWELLENDIAGNOSE_AUS

KWP2000 :   $30 InputOutputControlByLocalIdentifier Request Service Id $D6 inputOutputLocalIdentifier "Freigabe Anlasser und Sperren Zuendung und Einsprizung" $04 inputOutputControlParameter "RTD - ResetToDefault"  gibt Kontrolle von Einspitzung, Zuendung und Anlasserfreigabe wieder an SG zurueck

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-adaptionswerte2"></a>
### STATUS_ADAPTIONSWERTE2

KWP2000:    $22     ReadDataByCommonIdentifier $40 $0C RecordCommonIdentifier "ADAPTIONSWERTE2 lesen"  Adaptionswerte: DMVAD (Delta-Motordrehmom. aus Verlustmom.-Adapt.) UDKP1MX (Drosselklappenadaption max. Anschlag) RKA (Adaptive Korrektur Kraftstoffmasse) RKA2 (Adaptive Korrektur Kraftstoffmasse Bank 2) FRAO (multipl. Gemischadapt.fakt. ob. Lastbereich) FRAO2 (multipl. Gemischadapt.fakt. ob. Lastbereich Bank 2) FRAU (multipl.Gemischadapt.fakt. unt. mult.Bereich) FRAU2 (multipl.Gemischadapt.fakt. unt. mult.Bereich Bank 2) RKAZ (addit.Gemischkorr. (pro Zuend.) der Gemischadapt.) RKAZ2 (addit.Gemischkorr. (pro Zuend.) der Gemischadapt. Bank 2) FMSLA (Korrekturfak. SLmasse adaptiv) FMSLA2 (Korrekturfak. SLmasse adaptiv Bank 2) FMSLVA (Sekundaerluft Adaptionswert) FMSLVA2 (Sekundaerluft Adaptionswert Bank 2) NWFEHLER (Anzahl Nockenwellenfehler)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DMVAD_WERT | real | Wert von DMVAD_W |
| STAT_DMVAD_TEXT | string | Delta-Motordrehmom. aus Verlustmom.-Adapt. |
| STAT_DMVAD_EINH | string | Einheit von DMVAD_W |
| STAT_UDKP1MX_WERT | real | Wert von Drosselklappenadaption max. Anschlag |
| STAT_UDKP1MX_TEXT | string | Drosselklappenadaption max. Anschlag |
| STAT_UDKP1MX_EINH | string | Einheit von UDKP1MX |
| STAT_RKA_WERT | real | Wert von Adaptive Korrektur Kraftstoffmasse |
| STAT_RKA_TEXT | string | Adaptive Korrektur Kraftstoffmasse |
| STAT_RKA_EINH | string | Einheit von RKA |
| STAT_RKA2_WERT | real | Wert von Adaptive Korrektur Kraftstoffmasse Bank 2 |
| STAT_RKA2_TEXT | string | Adaptive Korrektur Kraftstoffmasse Bank 2 |
| STAT_RKA2_EINH | string | Einheit von RKA2 |
| STAT_FRAO_WERT | real | Wert von multipl. Gemischadapt.fakt. ob. Lastbereich |
| STAT_FRAO_TEXT | string | multipl. Gemischadapt.fakt. ob. Lastbereich |
| STAT_FRAO_EINH | string | Einheit von FRAO |
| STAT_FRAO2_WERT | real | Wert von multipl. Gemischadapt.fakt. ob. Lastbereich Bank 2 |
| STAT_FRAO2_TEXT | string | multipl. Gemischadapt.fakt. ob. Lastbereich Bank 2 |
| STAT_FRAO2_EINH | string | Einheit von FRAO2 |
| STAT_FRAU_WERT | real | Wert von multipl.Gemischadapt.fakt. unt. mult.Bereich |
| STAT_FRAU_TEXT | string | multipl.Gemischadapt.fakt. unt. mult.Bereich |
| STAT_FRAU_EINH | string | Einheit von FRAU |
| STAT_FRAU2_WERT | real | Wert von multipl.Gemischadapt.fakt. unt. mult.Bereich Bank 2 |
| STAT_FRAU2_TEXT | string | multipl.Gemischadapt.fakt. unt. mult.Bereich Bank 2 |
| STAT_FRAU2_EINH | string | Einheit von FRAU2 |
| STAT_RKAZ_WERT | real | Wert von addit.Gemischkorr. (pro Zuend.) der Gemischadapt. |
| STAT_RKAZ_TEXT | string | addit.Gemischkorr. (pro Zuend.) der Gemischadapt. |
| STAT_RKAZ_EINH | string | Einheit von RKAZ |
| STAT_RKAZ2_WERT | real | Wert von addit.Gemischkorr. (pro Zuend.) der Gemischadapt. Bank 2 |
| STAT_RKAZ2_TEXT | string | addit.Gemischkorr. (pro Zuend.) der Gemischadapt. Bank 2 |
| STAT_RKAZ2_EINH | string | Einheit von RKAZ2 |
| STAT_FMSLA_WERT | real | Wert von Korrekturfak. SLmasse adaptiv |
| STAT_FMSLA_TEXT | string | Korrekturfak. SLmasse adaptiv |
| STAT_FMSLA_EINH | string | Einheit von FMSLA |
| STAT_FMSLA2_WERT | real | Wert von Korrekturfak. SLmasse adaptiv Bank 2 |
| STAT_FMSLA2_TEXT | string | Korrekturfak. SLmasse adaptiv Bank 2 |
| STAT_FMSLA2_EINH | string | Einheit von FMSLA2 |
| STAT_FMSLVA_WERT | real | Wert von Sekundaerluft Adaptionswert |
| STAT_FMSLVA_TEXT | string | Sekundaerluft Adaptionswert |
| STAT_FMSLVA_EINH | string | Einheit von FMSLVA |
| STAT_FMSLVA2_WERT | real | Wert von Sekundaerluft Adaptionswert Bank 2 |
| STAT_FMSLVA2_TEXT | string | Sekundaerluft Adaptionswert Bank 2 |
| STAT_FMSLVA2_EINH | string | Einheit von FMSLVA2 |
| STAT_NWFEHLER_WERT | real | Anzahl Nockenwellenfehler |
| STAT_NWFEHLER_TEXT | string | Anzahl Nockenwellenfehler |
| STAT_NWFEHLER_EINH | string | Anzahl Nockenwellenfehler |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-status-analog2"></a>
### STATUS_ANALOG2

KWP2000:    $22     ReadDataByCommonIdentifier $40 $11 RecordCommonIdentifier "Analogwerte 2 lesen"  STP1 (Stepperposition 1 in Prozent) STP2 (Stepperposition 2 in Prozent) VSIKM (Restkilometerstand fuer Ventilspielserviceintervall) VSIDEL (Anzahl von Loeschungen der VSI-km) FRPS (gefilterter Wert des Kraftstoffdrucksensors) TOEL (Motoroeltemperatur)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STP1_WERT | real | Wert von Stepperposition 1 |
| STAT_STP1_TEXT | string | Stepperposition 1 |
| STAT_STP1_EINH | string | Einheit von Stepperposition 1 |
| STAT_STP2_WERT | real | Wert von Stepperposition 2 |
| STAT_STP2_TEXT | string | Stepperposition 2 |
| STAT_STP2_EINH | string | Einheit von Stepperposition 2 |
| STAT_VSIKM_WERT | real | Restkilometerstand fuer Ventilspielserviceintervall |
| STAT_VSIKM_TEXT | string | Restkilometerstand fuer Ventilspielserviceintervall |
| STAT_VSIKM_EINH | string | Einheit |
| STAT_VSIDEL_WERT | real | Anzahl von Loeschungen der VSI-km |
| STAT_VSIDEL_TEXT | string | Anzahl von Loeschungen der VSI-km |
| STAT_VSIDEL_EINH | string | Einheit |
| STAT_FRPS_WERT | real | gefilterter Wert des Kraftstoffdrucksensors |
| STAT_FRPS_TEXT | string | gefilterter Wert des Kraftstoffdrucksensors |
| STAT_FRPS_EINH | string | Einheit |
| STAT_TOEL_WERT | real | Wert von Motoroeltemperatur |
| STAT_TOEL_TEXT | string | Text von Motoroeltemperatur |
| STAT_TOEL_EINH | string | Einheit von Motoroeltemperatur |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-status-mrews-retry"></a>
### STATUS_MREWS_RETRY

aktueller Status "MREWS, Init-Kennung" KWP2000:    $21 ReadDataByLocalIdentifier $4D recordLocalIdentifier  Zum Auslesen der Retry Counter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RETRY_COUNTER_TOTAL | unsigned char | Retry_Counter total |
| STAT_RETRY_COUNTER_KL15 | unsigned char | Retry_Counter für einen Kl15 Zyklus |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ncoll"></a>
### STATUS_NCOLL

KWP2000:    $22     ReadDataByCommonIdentifier $40 $0F RecordCommonIdentifier "NCOLL WERTE lesen"  Adaptionswerte: NCOLL1 (Motorlaufzeit von 9000 - 9249 U/min in Sekunden) NCOLL2 (Motorlaufzeit von 9250 - 9499 U/min in Sekunden) NCOLL3 (Motorlaufzeit von 9500 - 9749 U/min in Sekunden) NCOLL4 (Motorlaufzeit von 9750 - 9999 U/min in Sekunden) NCOLL5 (Motorlaufzeit von 10000 - 10249 U/min in Sekunden) NCOLL6 (Motorlaufzeit von 10250 - 10499 U/min in Sekunden) NCOLL7 (Motorlaufzeit von 10500 - 10749 U/min in Sekunden) NCOLL8 (Motorlaufzeit von 10750 - 10999 U/min in Sekunden) NCOLL9 (Motorlaufzeit von 11000 - 11250 U/min in Sekunden)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NCOLL1_WERT | real | Wert von NCOLL1 |
| STAT_NCOLL1_TEXT | string | Motorlaufzeit von 9000 - 9249 U/min in Sekunden |
| STAT_NCOLL1_EINH | string | Einheit von NCOLL1 |
| STAT_NCOLL2_WERT | real | Wert von NCOLL2 |
| STAT_NCOLL2_TEXT | string | Motorlaufzeit von 9250 - 9499 U/min in Sekunden |
| STAT_NCOLL2_EINH | string | Einheit von NCOLL2 |
| STAT_NCOLL3_WERT | real | Wert von NCOLL3 |
| STAT_NCOLL3_TEXT | string | Motorlaufzeit von 9500 - 9749 U/min in Sekunden |
| STAT_NCOLL3_EINH | string | Einheit von NCOLL3 |
| STAT_NCOLL4_WERT | real | Wert von NCOLL4 |
| STAT_NCOLL4_TEXT | string | Motorlaufzeit von 9750 - 9999 U/min in Sekunden |
| STAT_NCOLL4_EINH | string | Einheit von NCOLL4 |
| STAT_NCOLL5_WERT | real | Wert von NCOLL5 |
| STAT_NCOLL5_TEXT | string | Motorlaufzeit von 10000 - 10249 U/min in Sekunden |
| STAT_NCOLL5_EINH | string | Einheit von NCOLL5 |
| STAT_NCOLL6_WERT | real | Wert von NCOLL6 |
| STAT_NCOLL6_TEXT | string | Motorlaufzeit von 10250 - 10499 U/min in Sekunden |
| STAT_NCOLL6_EINH | string | Einheit von NCOLL6 |
| STAT_NCOLL7_WERT | real | Wert von NCOLL7 |
| STAT_NCOLL7_TEXT | string | Motorlaufzeit von 10500 - 10749 U/min in Sekunden |
| STAT_NCOLL7_EINH | string | Einheit von NCOLL7 |
| STAT_NCOLL8_WERT | real | Wert von NCOLL8 |
| STAT_NCOLL8_TEXT | string | Motorlaufzeit von 10750 - 10999 U/min in Sekunden |
| STAT_NCOLL8_EINH | string | Einheit von NCOLL8 |
| STAT_NCOLL9_WERT | real | Wert von NCOLL9 |
| STAT_NCOLL9_TEXT | string | Motorlaufzeit von 11000 - 11250 U/min in Sekunden |
| STAT_NCOLL9_EINH | string | Einheit von NCOLL9 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-status-asc-werte"></a>
### STATUS_ASC_WERTE

KWP2000:    $22     ReadDataByCommonIdentifier $40 $10 RecordCommonIdentifier "ASC Status-/Messwerteblock lesen"  Messwerte:      ACTCTR    (Dauer der ASC-Regelungen in Sekunden) INTCTR    (mittlere Intensität/Momentrücknahme der ASC-Regelungen in Prozent) ASCSTATUS (aktueller Status der ASC-Funktion: 0 = RESERVIERT 1 = KOMFORT_STANDBY 2 = GS_STANDBY 3 = KEINE_FREIGABE 4 = KEINE_FREIGABE_GS 5 = KOMFORT_AKTIV 6 = GS_AKTIV 7 = AUS 8 = FEHLER ) ASCMODUS  (gewählter Modus der ASC-Funktion: 7 = AUS 1 = KOMFORT 2 = GS ) ES_ASC    (ASC-Taster, 0=nicht betätigt 1=betätigt 2=NOT-AUS aktiv ) RADCOR    (gesamte Radiuskorrektur der Reifenradiusadaption in mm, rücksetzen über den Job STEUERN_ADAPTIONSWERTE_LÖSCHEN möglich)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ACTCTR_WERT | real | Wert von ACTCTR |
| STAT_ACTCTR_TEXT | string | Dauer der ASC-Regelungen in Sekunden |
| STAT_ACTCTR_EINH | string | Einheit von ACTCTR |
| STAT_INTCTR_WERT | real | Wert von INTCTR |
| STAT_INTCTR_TEXT | string | mittlere Intensität/Momentrücknahme der ASC-Regelungen in Prozent |
| STAT_INTCTR_EINH | string | Einheit von INTCTR |
| STAT_ASCSTATUS_WERT | int | Wert von ASCSTATUS |
| STAT_ASCSTATUS_TEXT | string | aktueller Status der ASC-Funktion |
| STAT_ASCSTATUS_EINH | string | Einheit von ASCSTATUS |
| STAT_ASCMODUS_WERT | int | Wert von ASCMODUS |
| STAT_ASCMODUS_TEXT | string | gewählter Modus der ASC-Funktion |
| STAT_ASCMODUS_EINH | string | Einheit von ASCMODUS |
| STAT_ES_ASC_WERT | int | ASC-Taster |
| STAT_ES_ASC_TEXT | string | ASC-Taster |
| STAT_ES_ASC_EINH | string | ASC-Taster |
| STAT_RADCOR_WERT | real | Wert von RADCOR |
| STAT_RADCOR_TEXT | string | gesamte Radiuskorrektur der Reifenradiusadaption in mm |
| STAT_RADCOR_EINH | string | Einheit von RADCOR |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-steuern-sekundaerluftventildiagnose-an"></a>
### STEUERN_SEKUNDAERLUFTVENTILDIAGNOSE_AN

KWP2000 :   $30 InputOutputControlByLocalIdentifier Request Service Id $D8 inputOutputLocalIdentifier "Sekundärluftventildiagnose über Tester" $08 inputOutputControlParameter "LTA - LongtermAdjustment"  gibt die Sekundaerluftventildiagnose frei

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-sekundaerluftventildiagnose-aus"></a>
### STEUERN_SEKUNDAERLUFTVENTILDIAGNOSE_AUS

KWP2000 :   $30 InputOutputControlByLocalIdentifier Request Service Id $D8 inputOutputLocalIdentifier "Sekundärluftventildiagnose über Tester" $04 inputOutputControlParameter "RTD - ResetToDefault"  nimmt die Freigabe der Sekundaerluftventildiagnose wieder zurueck

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-sekundaerluftventildiagnose"></a>
### STATUS_SEKUNDAERLUFTVENTILDIAGNOSE

KWP2000:    $22     ReadDataByCommonIdentifier $40 $0E RecordCommonIdentifier "SLV-Diagnose-Stati lesen"  Stati:      B_ANFSLV (Bedingung Anforderung SLV-Diagnose) B_DSLVE  (Bedingung Durchführung SLV-Diagnose) B_DSLVA  (Bedingung Abbruch SLV-Diagnose) B_ADSLV  (Bedingung SLV-Diagnose abgeschlossen)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_B_ANFSLV_AKTIV | int | Bedingung Anforderung SLV-Diagnose |
| STAT_B_ANFSLV_TEXT | string | Bedingung Anforderung SLV-Diagnose |
| STAT_B_ANFSLV_ZUSTAND | string | Bedingung Anforderung SLV-Diagnose |
| STAT_B_DSLVE_AKTIV | int | Bedingung Durchführung SLV-Diagnose |
| STAT_B_DSLVE_TEXT | string | Bedingung Durchführung SLV-Diagnose |
| STAT_B_DSLVE_ZUSTAND | string | Bedingung Durchführung SLV-Diagnose |
| STAT_B_DSLVA_AKTIV | int | Bedingung Abbruch SLV-Diagnose |
| STAT_B_DSLVA_TEXT | string | Bedingung Abbruch SLV-Diagnose |
| STAT_B_DSLVA_ZUSTAND | string | Bedingung Abbruch SLV-Diagnose |
| STAT_B_ADSLV_AKTIV | int | Bedingung SLV-Diagnose abgeschlossen |
| STAT_B_ADSLV_TEXT | string | Bedingung SLV-Diagnose abgeschlossen |
| STAT_B_ADSLV_ZUSTAND | string | Bedingung SLV-Diagnose abgeschlossen |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-steuern-nmotmaxwerk-ein"></a>
### STEUERN_NMOTMAXWERK_EIN

KWP2000 :   $30 InputOutputControlByLocalIdentifier Request Service Id $D9 inputOutputLocalIdentifier "Drehzahlbegrenzung über Tester" $08 inputOutputControlParameter "LTA - LongtermAdjustment"  aktiviert die Drehzahlbegrenzung Werk

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-nmotmaxwerk-aus"></a>
### STEUERN_NMOTMAXWERK_AUS

KWP2000 :   $30 InputOutputControlByLocalIdentifier Request Service Id $D9 inputOutputLocalIdentifier "Drehzahlbegrenzung über Tester" $04 inputOutputControlParameter "RTD - ResetToDefault"  nimmt die Drehzahlbegrenzung Werk wieder zurueck

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-nvram-loeschen"></a>
### STEUERN_NVRAM_LOESCHEN

KWP2000 :   $31 StartRoutineByLocalIdentifier Request Service Id $EA inputOutputLocalIdentifier "NVRAM löschen"  sofern die Motordrehzahl = 0 ist, wird nach Abschluß der aktuellen Kommunikation ein Reset ausgelöst, währenddessen das NVRAM gelöscht wird

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-steuern-ventilspielservice-setzen"></a>
### STEUERN_VENTILSPIELSERVICE_SETZEN

KWP2000 : $2E     WriteDataByCommonIdentifier Request Service Id $40 $13 recordCommonIdentifier "VSI Restwegstrecke und Löschzähler setzen" $xx $xx $xx data  1. SG-interne Prüfung auf Drehzahl = 0 2. Setzen der Restwegstrecke (in km) und des Löschzählers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VSIDEL_WERT | real | Löschzähler Ventilspielserviceintervall |
| STAT_VSIKM_WERT | real | Restwegstrecke Ventilspielserviceintervall (in km) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

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

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (85 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (3 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (75 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FARTTEXTEERWEITERT](#table-farttexteerweitert) (7 × 3)
- [FUMWELTMATRIX](#table-fumweltmatrix) (75 × 5)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (101 × 9)
- [TAB_ADAPTIONSWERTE](#table-tab-adaptionswerte) (35 × 8)
- [KEYBYTES](#table-keybytes) (18 × 4)
- [LSUNPSTAT](#table-lsunpstat) (6 × 2)
- [BAUTEILANSTEUERUNG](#table-bauteilansteuerung) (18 × 7)
- [NOBDKLASSE](#table-nobdklasse) (10 × 15)
- [TAB_FUNKTIONSSTATI](#table-tab-funktionsstati) (9 × 4)
- [DIGITALWERTE](#table-digitalwerte) (23 × 6)
- [ADCLESENTABELLE](#table-adclesentabelle) (21 × 6)
- [MESSWERTE](#table-messwerte) (32 × 7)
- [FORTTEXTE2](#table-forttexte2) (75 × 5)
- [BETRIEBSWTAB](#table-betriebswtab) (39 × 13)
- [TAB_VERBAUT](#table-tab-verbaut) (2 × 2)
- [TAB_AKTIV](#table-tab-aktiv) (2 × 2)
- [TAB_ERKANNT](#table-tab-erkannt) (2 × 2)
- [TAB_SYNCHRO](#table-tab-synchro) (2 × 2)
- [MESSWERTE2](#table-messwerte2) (7 × 7)
- [TAB_ASCWERTE](#table-tab-ascwerte) (6 × 16)
- [TAB_DSLV_STATI](#table-tab-dslv-stati) (4 × 7)

<a id="table-konzept-tabelle"></a>
### KONZEPT_TABELLE

Dimensions: 5 rows × 2 columns

| NR | KONZEPT_TEXT |
| --- | --- |
| 0x10 | D-CAN |
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
| ?81? | ERROR_VEHICLE_IDENTIFICATION_NR |
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

Dimensions: 85 rows × 2 columns

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
| 0x81 | Tyco Electronics |
| 0x82 | Paragon AG |
| 0x83 | IEE S.A |
| 0x84 | TEMIC AUTOMOTIVE of NA |
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

<a id="table-speichersegment"></a>
### SPEICHERSEGMENT

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

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 3 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| ?F5? | ERROR_CONDITIONS_RPM |
| ?F6? | INCORRECT_NUMBER_OF_DATA_IN_RESPONSE-TELEGRAM |
| 0xXY | ERROR_UNKNOWN |

<a id="table-sg-diagnosekonzept"></a>
### SG_DIAGNOSEKONZEPT

Dimensions: 4 rows × 2 columns

| RANG | KONZEPT_TEXT |
| --- | --- |
| - | BMW-FAST |
| - | KWP2000* |
| 1 | KWP2000 |
| - | DS2 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 75 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x2718 | Drehzahlgeber Zahnfehler |
| 0x271A | Lambda-Sonde vor Kat |
| 0x271B | Endstufe Lamddasonden-Heizung 1 |
| 0x2722 | Lambda-Sonde2 vor Kat |
| 0x2723 | Endstufe Lamddasonden-Heizung 2 |
| 0x2736 | Kraftstoffdrucksensor |
| 0x2740 | Ölstandgeber |
| 0x2751 | Zylinderkopftemperatur 1 |
| 0x2752 | Zylinderkopftemperatur 2 |
| 0x2760 | Sekundärluftdiagnose |
| 0x2765 | Endstufe Sekundärluft-Ventil 1 |
| 0x276B | Endstufe Sekundärluft-Ventil 2 |
| 0x276C | Tankentlueftungssystem |
| 0x276D | Tankentlueftung Kleinstleck |
| 0x2772 | Tank-Entlüftungs-Ventil 1 |
| 0x2774 | SG-Defekt |
| 0x2778 | Schalter Kupplung |
| 0x2779 | SG Selbsttest RAM |
| 0x277B | SG Selbsttest ROM |
| 0x277C | SG Selbsttest RESET |
| 0x277D | Batteriespannung |
| 0x277F | Seitenstuetzenschalter |
| 0x2783 | Getriebeschaltwalzenpoti |
| 0x2786 | Vorderradgeschwindigkeit ASC |
| 0x2787 | Hinterradgeschwindigkeit ASC |
| 0x2788 | Fahrzeuggeschwindigkeit |
| 0x278A | Killschalter |
| 0x278B | Motortemperatur |
| 0x278C | Ansauglufttemperatur |
| 0x278D | Motoroeltemperatur |
| 0x279D | Elektrischer Motor-Lüfter |
| 0x27A6 | Einspritzventil Zylinder 1 |
| 0x27A7 | Einspritzventil Zylinder 2 |
| 0x27A8 | Einspritzventil Zylinder 3 |
| 0x27A9 | Einspritzventil Zylinder 4 |
| 0x27B4 | Drucksensor Umgebung |
| 0x27B7 | Endstufe Elektrische Kraftstoff Pumpe |
| 0x27B8 | Elektrisches Kraftstoff System |
| 0x27D9 | Fehler 5V-Versorgung Kraftstoffdrucksensor |
| 0x27DA | Fehler 5V-Versorgung Getriebeschaltwalzenpoti |
| 0x27DB | Fehler 5V-Versorgung Drosselklappengeber |
| 0x27E0 | alle Klopfsensoren defekt |
| 0x27E1 | Klopfsensor 1 |
| 0x27E2 | Klopfsensor 2 |
| 0x27E3 | Uebertemperatur Spannungsversorgung |
| 0x27E4 | Uebertemperatur Treiberbaustein CJ945 |
| 0x27E6 | Klopfregelung Nulltest |
| 0x27E7 | Klopfregelung Offset |
| 0x27E8 | Klopfregelung Testimpuls |
| 0x27EA | CAN-Timeout KOMBI |
| 0x27EB | CAN-Timeout ZFE |
| 0x27EC | CAN-Timeout ABS |
| 0x27F9 | Endstufe Starter-Relais |
| 0x283D | CAN Bus Off |
| 0x2847 | Fehler Drosselklappenpoti |
| 0x2848 | Drosselklappenadaption Grenze überschritten |
| 0x28A6 | Seitenstuetzenschalter Endstufe |
| 0x28A8 | Endstufe Drehzahlausgang |
| 0x28AA | Akustik Klappe Endstufe |
| 0x28AC | Schalter Klemme 15 |
| 0x28C8 | LR-Abweichung |
| 0x28C9 | LR-Abweichung (Bank 2) |
| 0x28CA | Sicherung aktiv System-Versorgung |
| 0x28CB | Sicherung aktiv EKP |
| 0x28CC | Sicherung aktiv Zuendung |
| 0x28CD | Bezugsmarkengeber Kurbelwelle |
| 0x28CE | Phasengeber |
| 0x28FA | Endstufe Elektronische Wegfahrsperre |
| 0x28FB | Fehler Elektronische Wegfahrsperre |
| 0x2904 | Schrittmotor 1 |
| 0x2905 | Schrittmotor 2 |
| 0x2934 | LR-Adaption |
| 0x2935 | LR-Adaption (Bank 2) |
| 0x2972 | Leerlaufregler |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | 00654321 |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-farttexteerweitert"></a>
### FARTTEXTEERWEITERT

Dimensions: 7 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| xxxxxxx1 | 1 | Aktiv-Status der Diagnosefunktion |
| xxxxxx1x | 2 | Diagnose gestoppt oder beendet |
| xxxxx1xx | 3 | Zyklus-flag gesetzt |
| xxxx1xxx | 4 | Fehlerflag E_xyz = TRUE |
| xxx1xxxx | 5 | MIL ein |
| xx1xxxxx | 6 | Fehler in Entprellphase |
| xxxxxxxx | 0 | -- |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 75 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x2718 | 0x0B | 0x41 | 0x04 | 0x1A |
| 0x271A | 0x16 | 0x0A | 0x1A | 0x0F |
| 0x271B | 0x16 | 0x0A | 0x1A | 0x0F |
| 0x2722 | 0x18 | 0x0A | 0x1A | 0x10 |
| 0x2723 | 0x18 | 0x0A | 0x1A | 0x10 |
| 0x2736 | 0x3C | 0x1B | 0x0A | 0x03 |
| 0x2740 | 0x04 | 0x01 | 0x0A | 0x09 |
| 0x2751 | 0x21 | 0x04 | 0x0B | 0x1A |
| 0x2752 | 0x45 | 0x04 | 0x0B | 0x1A |
| 0x2760 | 0x0A | 0x05 | 0x09 | 0x04 |
| 0x2765 | 0x0A | 0x0B | 0x02 | 0x0C |
| 0x276B | 0x01 | 0x01 | 0x01 | 0x01 |
| 0x276C | 0x1A | 0x03 | 0x0A | 0x85 |
| 0x276D | 0x1A | 0x03 | 0x0A | 0x85 |
| 0x2772 | 0x0A | 0x0B | 0x02 | 0x0C |
| 0x2774 | 0x0A | 0x01 | 0x02 | 0x1A |
| 0x2778 | 0x0A | 0x41 | 0x0B | 0x23 |
| 0x2779 | 0x0A | 0x01 | 0x02 | 0x1A |
| 0x277B | 0x0A | 0x01 | 0x02 | 0x1A |
| 0x277C | 0x0A | 0x01 | 0x02 | 0x1A |
| 0x277D | 0x40 | 0x0B | 0x0A | 0x1A |
| 0x277F | 0x0A | 0x0B | 0x03 | 0x1A |
| 0x2783 | 0x19 | 0x0A | 0x0B | 0x03 |
| 0x2786 | 0x0B | 0x0A | 0x02 | 0x03 |
| 0x2787 | 0x0B | 0x0A | 0x02 | 0x03 |
| 0x2788 | 0x0A | 0x41 | 0x03 | 0x8C |
| 0x278A | 0x0A | 0x0B | 0x02 | 0x1A |
| 0x278B | 0x3E | 0x1D | 0x0B | 0x1A |
| 0x278C | 0x24 | 0x04 | 0x1A | 0x0B |
| 0x278D | 0x3E | 0x1D | 0x0B | 0x1A |
| 0x279D | 0x12 | 0x0C | 0x0A | 0x0F |
| 0x27A6 | 0x0A | 0x0B | 0x02 | 0x0D |
| 0x27A7 | 0x0A | 0x0B | 0x02 | 0x0D |
| 0x27A8 | 0x0A | 0x0B | 0x02 | 0x0D |
| 0x27A9 | 0x0A | 0x0B | 0x02 | 0x0D |
| 0x27B4 | 0x0A | 0x03 | 0x04 | 0x1A |
| 0x27B7 | 0x0A | 0x0B | 0x02 | 0x0E |
| 0x27B8 | 0x0E | 0x3C | 0x0A | 0x03 |
| 0x27D9 | 0x02 | 0x0A | 0x09 | 0x1A |
| 0x27DA | 0x02 | 0x0A | 0x09 | 0x1A |
| 0x27DB | 0x02 | 0x0A | 0x09 | 0x1A |
| 0x27E0 | 0x8D | 0x8E | 0x8F | 0x0A |
| 0x27E1 | 0x8D | 0x8E | 0x8F | 0x0A |
| 0x27E2 | 0x8E | 0x8D | 0x0A | 0x90 |
| 0x27E3 | 0x0A | 0x01 | 0x02 | 0x1A |
| 0x27E4 | 0x0A | 0x01 | 0x02 | 0x1A |
| 0x27E6 | 0x80 | 0x04 | 0x0A | 0x09 |
| 0x27E7 | 0x81 | 0x04 | 0x0A | 0x09 |
| 0x27E8 | 0x81 | 0x77 | 0x0A | 0x09 |
| 0x27EA | 0x0A | 0x01 | 0x02 | 0x1A |
| 0x27EB | 0x0A | 0x01 | 0x02 | 0x1A |
| 0x27EC | 0x0A | 0x01 | 0x02 | 0x1A |
| 0x27F9 | 0x0A | 0x0B | 0x02 | 0x0D |
| 0x283D | 0x0A | 0x01 | 0x02 | 0x1A |
| 0x2847 | 0x26 | 0x0A | 0x0B | 0x17 |
| 0x2848 | 0x26 | 0x0A | 0x0B | 0x17 |
| 0x28A6 | 0x14 | 0x02 | 0x0A | 0x01 |
| 0x28A8 | 0x01 | 0x01 | 0x01 | 0x01 |
| 0x28AA | 0x0A | 0x0B | 0x02 | 0x0C |
| 0x28AC | 0x02 | 0x0C | 0x0A | 0x1A |
| 0x28C8 | 0x03 | 0x05 | 0x0A | 0x1D |
| 0x28C9 | 0x03 | 0x07 | 0x0A | 0x1D |
| 0x28CA | 0x0C | 0x0A | 0x02 | 0x1A |
| 0x28CB | 0x0E | 0x0A | 0x02 | 0x1A |
| 0x28CC | 0x0D | 0x0A | 0x02 | 0x1A |
| 0x28CD | 0x0A | 0x04 | 0x0B | 0x1A |
| 0x28CE | 0x0A | 0x04 | 0x1A | 0x0B |
| 0x28FA | 0x0D | 0x02 | 0x0A | 0x0B |
| 0x28FB | 0x0D | 0x02 | 0x0A | 0x0B |
| 0x2904 | 0x0A | 0x03 | 0x1A | 0x0C |
| 0x2905 | 0x0A | 0x03 | 0x1A | 0x0C |
| 0x2934 | 0x03 | 0x85 | 0x0A | 0x1D |
| 0x2935 | 0x03 | 0x86 | 0x0A | 0x1D |
| 0x2972 | 0x05 | 0x07 | 0x0A | 0x1D |
| 0xFFFF | 0xFF | 0xFF | 0xFF | 0xFF |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
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
| F_UWB_ERW | nein |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
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
| F_HFK | nein |
| F_LZ | nein |
| F_UWB_ERW | nein |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 101 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Ansauglufttemperatur (tans) | Grad C | - | unsigned char | - | 0.75 | 1 | -48 |
| 0x02 | Batteriespannung (ub) | V | - | unsigned char | - | 0.0942 | 1 | 0 |
| 0x03 | Drosselklappenwinkel bezogen auf DK- Anschlag (wdkba) | %DK | - | unsigned char | - | 100 | 256 | 0 |
| 0x04 | Motortemperatur SAE J1979 (tmot_u) | Grad C | - | unsigned char | - | 1 | 1 | -40 |
| 0x05 | Lambda Regelfaktor Bank 1 SAE J1979 (fr_u) | - | - | unsigned char | - | 2 | 256 | 0 |
| 0x06 | Lambda Adaptionsfaktor Bank 1 SAE J1979 (fra_u) | - | - | unsigned char | - | 2 | 256 | 0 |
| 0x07 | Lambda Regelfaktor Bank 2 SAE J1979 (fr2_u) | - | - | unsigned char | - | 2 | 256 | 0 |
| 0x08 | Lambda Adaptionsfaktor Bank 2 SAE J1979 (fra2_u) | - | - | unsigned char | - | 2 | 256 | 0 |
| 0x09 | relative Luftfüllung (rl) | % | - | unsigned char | - | 0.75 | 1 | 0 |
| 0x0A | Motordrehzahl SAE J1979 (nmot) | U/min | - | unsigned char | - | 40 | 1 | 0 |
| 0x0B | Fahrzeuggeschwindigkeit entspr. SAE J1979 (vfzg_u) | km/h | - | unsigned char | - | 1 | 1 | 0 |
| 0x0C | Spannung System BTS (uusys) | V | - | unsigned char | - | 0.0942 | 1 | 0 |
| 0x0D | Spannung Zündung BTS (uuzdg) | V | - | unsigned char | - | 0.0942 | 1 | 0 |
| 0x0E | Spannung EKP BTS (uuekp) | V | - | unsigned char | - | 0.0942 | 1 | 0 |
| 0x0F | Abgastemperatur vor Kat aus Modell (für LSH bei Boxer-Motoren); (tabgmls) | Grad C | - | unsigned char | - | 5 | 1 | -50 |
| 0x10 | Abgastemperatur vor Kat aus Modell (für LSH bei Boxer-Motoren) Bank2; (tabgmls2) | Grad C | - | unsigned char | - | 5 | 1 | -50 |
| 0x11 | Luftmassenfluß (ml) | kg/h | - | unsigned char | - | 4 | 1 | 0 |
| 0x12 | Motortemperatur in Systemquantisierung (tmot) | Grad C | - | unsigned char | - | 0.75 | 1 | -48 |
| 0x13 | Lambda Regelstatus Bank 1 SAE J1979 (flglrs) | 0-n | - | 0xFF | Lambdaregelstatus | 1 | 1 | 0 |
| 0x14 | Lambda Regelstatus Bank 2 SAE J1979 (flglrs2) | 0-n | - | 0xFF | Lambdaregelstatus | 1 | 1 | 0 |
| 0x15 | Relative Luftmasse SAE J1979 (rml) | % | - | unsigned char | - | 100 | 256 | 0 |
| 0x16 | Lambdasondenspannung Bank 1 (usvk) | V | - | unsigned char | - | 0.0052 | 1 | -0.2 |
| 0x17 | adaptierter Spannungswert bei geschlossener Drosselklappe (udkpa_u) | V | - | unsigned char | - | 5 | 256 | 0 |
| 0x18 | Lambdasondenspannung Bank 2 (usvk2) | V | - | unsigned char | - | 0.0052 | 1 | -0.2 |
| 0x19 | Spannungswert von Getriebeschaltwalze (ugetrg) | V | - | unsigned char | - | 5 | 256 | 0 |
| 0x1A | Zeit nach Motorstart(tnst_u) | s | - | unsigned char | - | 64 | 100 | 0 |
| 0x1B | Einspritzzeit(te_u) | ms | - | unsigned char | - | 64 | 1000 | 0 |
| 0x1C | Kraftstoffdruck gefiltert(frps_fu) | hPa | - | unsigned char | - | 5 | 256 | 0 |
| 0x1D | Zylinderkopftemperatur(tmotzyl_u) | Grad C | - | unsigned char | - | 75 | 100 | -48 |
| 0x1E | Zuendwinkel(zwout_u) | Grad KW | - | unsigned char | - | 191.25 | 255 | -96 |
| 0x1F | aktuelle Position Stepper 1 (st_curp1_u) | steps | - | unsigned char | - | 1 | 1 | 0 |
| 0x20 | aktuelle Position Stepper 2 (st_curp2_u) | steps | - | unsigned char | - | 1 | 1 | 0 |
| 0x21 | Spannungswert Temperatursensor Zylinder 1 (utzyl1) | V | - | unsigned char | - | 5 | 256 | 0 |
| 0x22 | Pfadidentifier aus Reset (rstpfad) | 0-n | - | 0xFF | - | 1 | 1 | 0 |
| 0x23 | Normierter Fahrpedalwinkel (wped) | %PED | - | unsigned char | - | 100 | 255 | 0 |
| 0x24 | ADC-Spannung Ansauglufttemperatur (wtans) | V | - | unsigned char | - | 5 | 256 | 0 |
| 0x25 | Motortemperatur- Ersatzwert aus Modell (tmew) | Grad C | - | unsigned char | - | 0.75 | 1 | -48 |
| 0x26 | Spannung DK- Poti 1 (udkp1_u) | V | - | unsigned char | - | 5 | 256 | 0 |
| 0x27 | Fahrzeuggeschwindigkeit aus Übersetzungsverhältnis und nmot (vfzggang_u) | V | - | unsigned char | - | 1 | 1 | 0 |
| 0x28 | Sollwert DK, bezogen auf unteren Anschlag (wdks) | - | - | unsigned char | - | 100 | 256 | 0 |
| 0x29 | Abgastemperatur vor Katalysator aus Modell (tabgm) | Grad C | - | unsigned char | - | 5 | 1 | -50 |
| 0x2A | Abgastemperatur vor Katalysator aus Modell; Bank 2 (tabgm2) | Grad C | - | unsigned char | - | 5 | 1 | -50 |
| 0x2B | Katalysatortemperatur aus Modell (tkatm) | Grad C | - | unsigned char | - | 5 | 1 | -50 |
| 0x2C | Katalysatortemperatur Bank 2 aus Modell (tkatm2) | Grad C | - | unsigned char | - | 5 | 1 | -50 |
| 0x2D | Spannung an der Heizerendstufe vor Kat (uhsv) | V | - | unsigned char | - | 5 | 256 | 0 |
| 0x2E | Spannung an der Heizerendstufe 2 vor Kat (uhsv2) | V | - | unsigned char | - | 5 | 256 | 0 |
| 0x2F | aktuelle Geschw. Stepper 1 (st_curs1_u) | - | - | unsigned char | - | 4 | 1 | 0 |
| 0x30 | aktuelle Geschw. Stepper 2 (st_curs2_u) | - | - | unsigned char | - | 4 | 1 | 0 |
| 0x31 | Innenwiderstand Lambdasonde vor Kat. (rinv_u) | Ohm | - | unsigned char | - | 64 | 1 | 0 |
| 0x32 | Innenwiderstand Lambdasonde vor Kat. Bank 2 (rinv2_u) | Ohm | - | unsigned char | - | 64 | 1 | 0 |
| 0x33 | Referenzierung Stepper 1 (st_ref_a[0]) | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x34 | Referenzierung Stepper 2 (st_ref_a[1]) | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x35 | Umgebungsdruck (pu) | hPa | - | unsigned char | - | 5 | 1 | 0 |
| 0x36 | Gefilterte Periodendauer Lambdasonde vor Kat. (tpsvkmf_u) | s | - | unsigned char | - | 0.04 | 1 | 0 |
| 0x37 | Gefilterte Periodendauer Lambdasonde vor Kat Bank 2 (tpsvkmf2_u) | s | - | unsigned char | - | 0.04 | 1 | 0 |
| 0x38 | ersetzt durch Nr. 5 (fr_u) | - | - | unsigned char | - | 2 | 256 | 0 |
| 0x39 | ersetzt durch Nr. 6 (fra_u) | - | - | unsigned char | - | 2 | 256 | 0 |
| 0x3A | ersetzt durch Nr. 7 (fr2_u) | - | - | unsigned char | - | 2 | 256 | 0 |
| 0x3B | ersetzt durch Nr. 8 (fra2_u) | - | - | unsigned char | - | 2 | 256 | 0 |
| 0x3C | gemessener Kraftstoffdruck (frps_measu) | hPa | - | unsigned char | - | 5 | 256 | 0 |
| 0x3D | ersetzt durch Nr. 26 (rl) | % | - | unsigned char | - | 0.75 | 1 | 0 |
| 0x3E | Motortemperatur, linearisiert und umgerechnet (tmotlin) | Grad C | - | unsigned char | - | 0.75 | 1 | -48 |
| 0x3F | Motortemperatur-Referenzwert aus Modell (tmrw) | Grad C | - | unsigned char | - | 0.75 | 1 | -48 |
| 0x40 | ADC-Wert Batteriespannung (wub) | V | - | unsigned char | - | 0.0942 | 1 | 0 |
| 0x41 | Ist-Gang (gangi) | Gang | - | unsigned char | - | 1 | 1 | 0 |
| 0x42 | Zulässiges indiziertes Moment vor Filter (mizuvfil) | % | - | unsigned char | - | 100 | 256 | 0 |
| 0x43 | prellen Stepper 1 (B_prell_a[0]) | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x44 | prellen Stepper 2 (B_prell_a[1]) | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x45 | Spannungswert Temperatursensor Zylinder 2 (utzyl2) | V | - | unsigned char | - | 5 | 256 | 0 |
| 0x66 | Integratorgradient für Offsetkorrektur Klopfregelung (igokr_u) | V/s | - | unsigned char | - | 23.84375 | 1 | 0 |
| 0x67 | ADC- Spannung Lambdasonde vor Katalysator (uusvk)  | V | - | unsigned char | - | 5 | 256 | 0 |
| 0x68 | ADC- Spannung Lambdasonde vor Katalysator 2 (uusvk2) | V | - | unsigned char | - | 5 | 256 | 0 |
| 0x6B | Tastverhältnis E- Lüfter (taml) | % | - | unsigned char | - | 100 | 1 | 256 |
| 0x72 | ADC- Spannung Motortemperatur (adtm_u) | V | - | unsigned char | - | 5 | 256 | 0 |
| 0x73 | ADC- Spannung Ansauglufttemperatur (adta_u) | V | - | unsigned char | - | 5 | 256 | 0 |
| 0x75 | ADC- Spannung Saugrohrabsolutdruck (addsu_u) | V | - | unsigned char | - | 5 | 256 | 0 |
| 0x77 | Integratorwert Klopfregelung Meßfensterende Testimpuls (ikrmet) | V | - | unsigned char | - | 5 | 256 | 0 |
| 0x80 | Integratorgradient für Nulltest-Diagnose Klopfregelung (igod_u) | V/s | - | unsigned char | - | 23.84375 | 1 | 0 |
| 0x81 | Integratorwert Klopfregelung Meßfensteranfang (ikrma) | V | - | unsigned char | - | 5 | 256 | 0 |
| 0x82 | Lambda-Sollwert bezogen auf Einbauort Lambda-Sensor (lamsons_u) | - | - | unsigned char | - | 16 | 256 | 0 |
| 0x83 | Lambda-Sollwert bezogen auf Einbauort Lambda-Sensor bank 2 r (lamsons2_u) | - | - | unsigned char | - | 16 | 256 | 0 |
| 0x84 | Motorstarttemperatur (tmst) | Grad C | - | unsigned char | - | 0.75 | 1 | -25 |
| 0x85 | Filtered feedback (frm_u) | - | - | unsigned char | - | 2 | 256 | 0 |
| 0x86 | Filtered feedback Bank2 (frm2_u) | - | - | unsigned char | - | 2 | 256 | 0 |
| 0x87 | Festwert (dummy) | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x88 | Festwert (dummy) | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x8B | Faktor Luftdichte f(Ansauglufttemp., Höhe) (frhol_u) | - | - | unsigned char | - | 2 | 256 | 0 |
| 0x8C | Zeitzähler ab Startende (tnse_u) | s | - | unsigned char | - | 25.6 | 1 | 0 |
| 0x8D | normierter Referenzpegel KR SW- Zylinder 0 (rkrn_u_0) | V | - | unsigned char | - | 5 | 8 | 0 |
| 0x8E | normierter Referenzpegel KR SW- Zylinder 1 (rkrn_u_1) | V | - | unsigned char | - | 5 | 8 | 0 |
| 0x8F | normierter Referenzpegel KR SW- Zylinder 2 (rkrn_u_2) | V | - | unsigned char | - | 5 | 8 | 0 |
| 0x90 | normierter Referenzpegel KR SW- Zylinder 3 (rkrn_u_3) | V | - | unsigned char | - | 5 | 8 | 0 |
| 0xA3 | Abgasmassenfluß gefiltert, Bank 1 (msabg) | kg/h | - | unsigned char | - | 4 | 1 | 0 |
| 0xA4 | Abgasmassenfluß gefiltert, Bank 2 (msabg2) | kg/h | - | unsigned char | - | 4 | 1 | 0 |
| 0xA5 | Abstellzeit (tabst_u) | s | - | unsigned char | - | 256 | 1 | 0 |
| 0xA8 | Sondenspannung vor Kat einer Breitbandlambdasonde (uulsuv_u) | V | - | unsigned char | - | 5 | 256 | 0 |
| 0xA9 | Sondenspannung vor Kat einer Breitbandlambdasonde Bank2 (uulsuv2_u) | V | - | unsigned char | - | 5 | 256 | 0 |
| 0xAC | multiplikativer Gemischadaptionsfaktor unterer mult. Bereich (frau_u) | - | - | unsigned char | - | 2 | 256 | 0 |
| 0xAD | multipl. Gemischadaptionsfaktor unterer mult. Bereich der Bank 2 (frau2_u) | - | - | unsigned char | - | 2 | 256 | 0 |
| 0xFF | ohne Bedeutung | - | - | unsigned char | - | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | - | - | unsigned char | - | - | - | - |

<a id="table-tab-adaptionswerte"></a>
### TAB_ADAPTIONSWERTE

Dimensions: 35 rows × 8 columns

| MNEMO | TEXT | INDEX | NAME | EINHEIT | ADD | FAKTOR | TYP |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ABS | ABS Steuergerät verbaut/nicht verbaut | 88 | tab_Verbaut | - | - | - | - |
| LOWBAT | U-Bat war zwischen 6 Volt und 7 Volt | 89 | tab_Aktiv | - | - | - | - |
| SPERREKP | EKP, Zünd./Einsp. & Anlasser gesperrt | 90 | tab_Aktiv | - | - | - | - |
| DKPA | Adaptionswert Drosselklappenpoti | 24 | - | Volt | 0 | 0,001222 | word |
| GANGAN | Adaptionswert Neutral Gang | 32 | - | Volt | 0 | 0,019531 | byte |
| GANGA1 | Adaptionswert 1. Gang | 40 | - | Volt | 0 | 0,019531 | byte |
| GANGA2 | Adaptionswert 2. Gang | 48 | - | Volt | 0 | 0,019531 | byte |
| GANGA3 | Adaptionswert 3. Gang | 56 | - | Volt | 0 | 0,019531 | byte |
| GANGA4 | Adaptionswert 4. Gang | 64 | - | Volt | 0 | 0,019531 | byte |
| GANGA5 | Adaptionswert 5. Gang | 72 | - | Volt | 0 | 0,019531 | byte |
| GANGA6 | Adaptionswert 6. Gang | 80 | - | Volt | 0 | 0,019531 | byte |
| DMVAD | Delta-Motordrehmom. aus Verlustmom.-Adapt. | - | - | % | 0 | 0,0030517578125 | word |
| UDKP1MX | Drosselklappenadaption max. Anschlag | - | - | Volt | 0 | 0.00122200 | word |
| RKA | Adaptive Korrektur Kraftstoffmasse | - | - | % | 0 | 0,046875 | word |
| RKA2 | Adaptive Korrektur Kraftstoffmasse Bank 2 | - | - | % | 0 | 0,046875 | word |
| FRAO | multipl. Gemischadapt.fakt. ob. Lastbereich | - | - | - | 0 | 0,000030517578125 | word |
| FRAO2 | multipl. Gemischadapt.fakt. ob. Lastbereich Bank 2 | - | - | - | 0 | 0,000030517578125 | word |
| FRAU | multipl.Gemischadapt.fakt. unt. mult.Bereich | - | - | - | 0 | 0,000030517578125 | word |
| FRAU2 | multipl.Gemischadapt.fakt. unt. mult.Bereich Bank 2 | - | - | - | 0 | 0,000030517578125 | word |
| RKAZ | addit.Gemischkorr. (pro Zuend.) der Gemischadapt. | - | - | % | 0 | 0,046875 | word |
| RKAZ2 | addit.Gemischkorr. (pro Zuend.) der Gemischadapt. Bank 2 | - | - | % | 0 | 0,046875 | word |
| FMSLA | Korrekturfak. SLmasse adaptiv | - | - | - | 0 | 0,0078125 | byte |
| FMSLA2 | Korrekturfak. SLmasse adaptiv Bank 2 | - | - | - | 0 | 0,0078125 | byte |
| FMSLVA | Sekundaerluft Adaptionswert | - | - | - | 0 | 0,0078125 | byte |
| FMSLVA2 | Sekundaerluft Adaptionswert Bank 2 | - | - | - | 0 | 0,0078125 | byte |
| NWFEHLER | Anzahl Nockenwellenfehler | - | - | - | 0 | 1 | byte |
| NCOLL1 | Motorlaufzeit von 9000 - 9249 U/min in Sekunden | - | - | sec | 0 | 1 | long |
| NCOLL2 | Motorlaufzeit von 9250 - 9499 U/min in Sekunden | - | - | sec | 0 | 1 | long |
| NCOLL3 | Motorlaufzeit von 9500 - 9749 U/min in Sekunden | - | - | sec | 0 | 1 | long |
| NCOLL4 | Motorlaufzeit von 9750 - 9999 U/min in Sekunden | - | - | sec | 0 | 1 | long |
| NCOLL5 | Motorlaufzeit von 10000 - 10249 U/min in Sekunden | - | - | sec | 0 | 1 | long |
| NCOLL6 | Motorlaufzeit von 10250 - 10499 U/min in Sekunden | - | - | sec | 0 | 1 | long |
| NCOLL7 | Motorlaufzeit von 10500 - 10749 U/min in Sekunden | - | - | sec | 0 | 1 | long |
| NCOLL8 | Motorlaufzeit von 10750 - 10999 U/min in Sekunden | - | - | sec | 0 | 1 | long |
| NCOLL9 | Motorlaufzeit von 11000 - 11250 U/min in Sekunden | - | - | sec | 0 | 1 | long |

<a id="table-keybytes"></a>
### KEYBYTES

Dimensions: 18 rows × 4 columns

| KB | FMT | HEADER | TIMING |
| --- | --- | --- | --- |
| 0x8FD5 | Format byte | 1 byte header | Extended timing |
| 0x8FD6 | Additional length byte | 1 byte header | Extended timing |
| 0x8F57 | Both modes possible | 1 byte header | Extended timing |
| 0x8FD9 | Format byte | Header with target and source information | Extended timing |
| 0x8FDA | Additional length byte | Header with target and source information | Extended timing |
| 0x8F5B | Both modes possible | Header with target and source information | Extended timing |
| 0x8F5D | Format byte | Both types of header supported | Extended timing |
| 0x8F5E | Additional length byte | Both types of header supported | Extended timing |
| 0x8FDF | Both modes possible | Both types of header supported | Extended timing |
| 0x8FE5 | Format byte | 1 byte header | Normal timing |
| 0x8FE6 | Additional length byte | 1 byte header | Normal timing |
| 0x8F67 | Both modes possible | 1 byte header | Normal timing |
| 0x8FE9 | Format byte | Header with target and source information | Normal timing |
| 0x8FEA | Additional length byte | Header with target and source information | Normal timing |
| 0x8F6B | Both modes possible | Header with target and source information | Normal timing |
| 0x8F6D | Format byte | Both types of header supported | Normal timing |
| 0x8F6E | Additional length byte | Both types of header supported | Normal timing |
| 0x8FEF | Both modes possible | Both types of header supported | Normal timing |

<a id="table-lsunpstat"></a>
### LSUNPSTAT

Dimensions: 6 rows × 2 columns

| TEXT | NR |
| --- | --- |
| Abgleichltg.unterbrochen | 1 |
| Sonde nicht eingebaut aber angeschlossen | 2 |
| HW-Fehler | 4 |
| mager-Fehler | 8 |
| fett-Fehler | 16 |
| Unterbrechung | 32 |

<a id="table-bauteilansteuerung"></a>
### BAUTEILANSTEUERUNG

Dimensions: 18 rows × 7 columns

| MNEMO | TEXT | IOLI | TYP | FAKTOR | DREHZAHL | EINH |
| --- | --- | --- | --- | --- | --- | --- |
| Elu | E-Lüfter | 0xC1 | 3 | - | 3 | - |
| SLV | Sekundärluftventil | 0xC3 | 3 | - | 3 | - |
| AKL | Akustik Klappe | 0xC4 | 3 | - | 3 | - |
| TEV | Taktventil Tankentlüftung | 0xC5 | 0 | - | 3 | % |
| EKP | Kraftstoffpumpe | 0xC6 | 0 | 1 | 1 | % |
| HSV | Lambdasondenheizung vor Kat 1 | 0xC7 | 0 | 0,01 | 3 | ms |
| HSV2 | Lambdasondenheizung vor Kat 2 | 0xC9 | 0 | 0,01 | 3 | ms |
| EV1 | Einspritzventil 1 | 0xCB | 3 | - | 1 | - |
| EV2 | Einspritzventil 2 | 0xCC | 3 | - | 1 | - |
| EV3 | Einspritzventil 3 | 0xCD | 3 | - | 1 | - |
| EV4 | Einspritzventil 4 | 0xCE | 3 | - | 1 | - |
| STPLL2 | Stepper LL-Regelung 2 | 0xCF | 0 | 2,56 | 3 | % |
| STPLL1 | Stepper LL-Regelung 1 | 0xD1 | 0 | 2,56 | 3 | % |
| STPABGL | Stepper-Abgleich | 0xD2 | 3 | - | 1 | - |
| UETMC | Kontrollleuchte Übertemperatur | 0xD3 | 3 | - | 3 | - |
| MIL | Check-Engine-Lampe | 0xF1 | 3 | - | 1 | - |
| Gangadp | Gangadaption | 0xD5 | 3 | - | 3 | - |
| VSIDEL | VSI Kilometerstand zuruecksetzen | 0xD7 | 3 | - | 3 | - |

<a id="table-nobdklasse"></a>
### NOBDKLASSE

Dimensions: 10 rows × 15 columns

| CLA | MIL | FLC_TRIGGER | FLC_WERT | HLC_TRIGGER | HLC_WERT | SCAN_TOOL_AUSGABE | DLC_TRIGGER_CARB | DLC_WERT_PENDING | DLC_TRIGGER_BMW | DLC_WERT_CARB | DLC_WERT_BMW | FREEZE_FRAME_PRIORITAET | EPCL | TEXT |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CL30LINE | 0 | 0 | 0 | 1 | 5 | 0 | 2 | 2 | 2 | 2 | 2 | 255 | 0 | nicht verwendet |
| CL31LINE | 0 | 4 | 2 | 5 | 4 | 1 | 2 | 80 | 3 | 40 | 40 | 20 | 0 | verwendet für Aussetztererkennung; FLC Trigger über Funktionsroutine; hohe FF Priorität |
| CL32LINE | 0 | 2 | 2 | 2 | 4 | 1 | 3 | 40 | 3 | 40 | 40 | 30 | 0 | identisch mit Klasse 33; früher verwendet für Fehler, die die Lambdaregelung sperren, da bei diesen Fehlern die MIL sofort anging |
| CL33LINE | 0 | 2 | 2 | 2 | 4 | 1 | 3 | 40 | 3 | 40 | 40 | 30 | 0 | Standard OBDII Klasse; MIL on nach 2 driving cycles; MIL off nach 3 fehlerfreien driving cycles (wegen Funktionsfehler DFPM auf 4 driving cycles appliziert); DTC löschen nach 40 warm up cycles |
| CL34LINE | 0 | 2 | 2 | 2 | 4 | 1 | 3 | 40 | 3 | 40 | 40 | 30 | 1 | OBDII Steuerung wie Standard Klasse 33; zusätzlich EPCL (EML lampe bzw. Motornotprogramm) ein; verwendet für DK und SG interne Fehler |
| CL35LINE | 0 | 0 | 0 | 0 | 0 | 0 | 3 | 40 | 3 | 40 | 40 | 30 | 1 | Standard BMW Fehler; keine MIL, keine scan tool Ausgabe;EPCL ein; verwendet für PWG Fehler |
| CL36LINE | 0 | 0 | 0 | 0 | 0 | 0 | 3 | 40 | 3 | 40 | 40 | 50 | 0 | Standard BMW Fehler; keine MIL, keine scan tool Ausgabe; keine EPCL |
| CL37LINE | 0 | 2 | 2 | 2 | 4 | 1 | 3 | 40 | 3 | 40 | 40 | 30 | 0 | Standard EOBD Fehler; keine MIL, jedoch Ausgabe an scan tool; keine EPCL; Fehler löschen nach 40 warm up cycles |
| CL38LINE | 0 | 0 | 255 | 1 | 5 | 0 | 3 | 20 | 3 | 2 | 15 | 50 | 0 | nicht verwendet |
| CL39LINE | 0 | 1 | 0 | 1 | 0 | 1 | 2 | 0 | 2 | 0 | 0 | 50 | 0 | nicht verwendet |

<a id="table-tab-funktionsstati"></a>
### TAB_FUNKTIONSSTATI

Dimensions: 9 rows × 4 columns

| MNEMO | TEXT | INDEX | NAME |
| --- | --- | --- | --- |
| LL | Leerlaufregelung  | 24 | tab_Aktiv |
| VL | Bedingung Vollast | 25 | tab_Aktiv |
| TEHB | Bedingung Tankentlüftung mit hoher Beladung | 26 | tab_Aktiv |
| SA | Bedingung Schubabschalten | 27 | tab_Aktiv |
| SBBVK | Bedingung Sonde betriebsbereit vor Kat  | 29 | tab_Aktiv |
| SBBVK2 | Bedingung Sonde betriebsbereit vor Kat, Bank 2  | 28 | tab_Aktiv |
| BM | Zylinder-1 Erkennung | 30 | tab_Erkannt |
| LR | Lambdaregelung | 31 | tab_Aktiv |
| NWSYN | Bedingung Synchronisierung erfolgreich | 32 | tab_synchro |

<a id="table-digitalwerte"></a>
### DIGITALWERTE

Dimensions: 23 rows × 6 columns

| MNEMONIC | TEXT | INDEX | NAME | 0 | 1 |
| --- | --- | --- | --- | --- | --- |
| B_KL15_ZFE | Status KL 15 aus ZFE ueber CAN | 29 | - | nicht betätigt | betätigt |
| S_KUPP | Kupplungs-Schalter | 32 | - | nicht betätigt | betätigt |
| ES_SST1 | Seitenstützen-Schalter 1 | 33 | - | ausgeklappt | eingeklappt |
| ES_OELNIV | Ölniveau-Schwimmer-Schalter | 34 | - | nicht i.O. | Ölniveau i.O. |
| ES_POEL | Öldruck-Schalter | 35 | - | nicht vorhanden | vorhanden |
| ES_START | Startschalter | 36 | - | nicht betätigt | betätigt |
| S_KL15 | Schalter Kl 15 | 37 | - | nicht betätigt | betätigt |
| ES_KILL | Not-Aus-Schalter | 38 | - | in Betriebsstellung | Not-Aus aktiv |
| B_AKL | Akkustik Klappe | 0 | - | nicht aktiv | aktiv |
| B_SLV1 | Sekundrluft-Ventil | 33 | - | nicht aktiv | aktiv |
| B_TEV | Taktventil Tankentlüftung | 34 | - | nicht aktiv | aktiv |
| B_HSV2 | Lambdasondenheizung vor Kat 2 | 51 | - | nicht aktiv | aktiv |
| B_HSV | Lambdasondenheizung vor Kat 1 | 48 | - | nicht aktiv | aktiv |
| B_ELUE1 | Motorlüfter  | 49 | - | nicht aktiv | aktiv |
| B_EKPBTS | Kraftstoffpumpe | 50 | - | nicht aktiv | aktiv |
| A_ANLASSER | Anlasser-Relais | 54 | - | nicht aktiv | aktiv |
| B_UETMC | Kontrollleuchte Motortemperatur | 55 | - | nicht aktiv | aktiv |
| B_MOTORSTP | Motorstopp | 59 | - | nicht aktiv | aktiv |
| B_FRGANL |  Freigabe Anlasser | 60 | - | nicht aktiv | aktiv |
| A_SCHUTZ | Anlasser Stopp | 62 | - | nicht aktiv | aktiv |
| B_MIL | Motornotlauf  | 63 | - | nicht aktiv | aktiv |
| ES_SST2 | Seitenstützen-Schalter 2 | 39 | - | eingeklappt | ausgeklappt |
| ES_SST | Seitenständer (nach Diagnose) | 25 | - | ausgeklappt | eingeklappt |

<a id="table-adclesentabelle"></a>
### ADCLESENTABELLE

Dimensions: 21 rows × 6 columns

| HEX | IOLI | MNEMONIC | U_FAKTOR | EINH | TYP |
| --- | --- | --- | --- | --- | --- |
| 0x4A | Batteriespannung | UB | 0,0942 | V | byte |
| 0x4E | DK-Poti | DKP | 0,001222 | V | word |
| 0x4F | Heißluftmassenmesser | HFM | 0,00977 | V | word |
| 0x50 | Motortemperatur | TMOT | 0,019531 | V | byte |
| 0x51 | Ansauglufttemperatur | TANS | 0,019531 | V | byte |
| 0x53 | Spannungsversorgung E-Lüfter  | ELUE | 0,0942 | V | byte |
| 0x54 | Integrator Wert Klopfsensor 1 | KS1 | 0,019531 | V | byte |
| 0x55 | Integrator Wert Klopfsensor 2 | KS2 | 0,019531 | V | byte |
| 0x56 | Getriebe Schaltwalze | GETRG | 0,019531 | V | byte |
| 0x57 | Kraftstoffdruck | DSK | 0,019531 | V | byte |
| 0x58 | Betriebstrom E-Lüfter | IELUE | 0,0488 | A | word |
| 0x59 | Spannungsversorgung | SYS | 0,0942 | V | byte |
| 0x5A | Betriebstrom 1 | ISYS | 0,0488 | A | word |
| 0x60 | Lambdasonde 1 | LSVK1 | 0,019531 | V | byte |
| 0x61 | Lambdasonde 2 | LSVK2 | 0,019531 | V | byte |
| 0x63 | Temperatur Zylinderkopf links | TZYL1 | 0,019531 | V | byte |
| 0x64 | Temperatur Zylinderkopf rechts | TZYL2 | 0,019531 | V | byte |
| 0x67 | Spannungsversorgung 2 | ZDG | 0,0942 | V | byte |
| 0x68 | Betriebstrom 2 | IZDG | 0,0488 | A | word |
| 0x71 | Spannungsversorgung 3 | EKP | 0,0942 | V | byte |
| 0x72 | Betriebstrom 3 | IEKP | 0,0488 | A | word |

<a id="table-messwerte"></a>
### MESSWERTE

Dimensions: 32 rows × 7 columns

| NR | TEXT | TYP | EINH | NAME | ADD | FAKTOR |
| --- | --- | --- | --- | --- | --- | --- |
| 0 | Einspritzzeit EV | word | msec | te_w | 0 | 0,008 |
| 1 | Lambdaregler 1 | word | - | fr_w | 0 | 3,05176E-05 |
| 2 | Lambdaregler 2 | word | - | fr2_w | 0 | 3,05176E-05 |
| 3 | Fahrzeuggeschwindigkeit  | byte | km/h | vfzg | 0 | 1,25 |
| 4 | Motordrehzahl | word | U/min | nmot_w | 0 | 0,25 |
| 5 | Leerlauf-Solldrehzahl  | byte | U/min | nsol | 0 | 10 |
| 6 | Nockenwellenposition Einlaß | word | - | wnwkwe_w | 0 | 0,1 |
| 7 | Nockenwellenposition Auslaß | word | - | wnwkwa_w | 0 | 0,1 |
| 8 | Ansauglufttemperatur | byte | Grad C | tans | -48 | 0,75 |
| 9 | Motortemperatur | byte | Grad C | tmot | -48 | 0,75 |
| 10 | Temperatur Zylinder 1 | word | Grad C | tmotzyl1_w | -48 | 0,75 |
| 11 | Temperatur Zylinder 2 | word | Grad C | tmotzyl2_w | -48 | 0,75 |
| 12 | Zündwinkel | byte | Grad KW | zwout | -96 | 0,75 |
| 13 | Drosselklappen-Potentiometer | byte | % | wdkba | 0 | 0,39216 |
| 14 | Luftmasse | word | kg/h | mshfm_w | 0 | 0,1 |
| 15 | indiziertes Motormoment nach Eingriffe | word | % | miist_w | 0 | 0,0015259 |
| 16 | Spannung Kl. 30 | byte | V | ub | 0 | 0,0942 |
| 17 | Klopfsensor 1 Ref. Pegel | word | V | rkrn_w | 0 | 0,019531 |
| 18 | Klopfsensor 2 Ref. Pegel | word | V | rkrn_w | 0 | 0,019531 |
| 19 | Klopfsensor 3 Ref. Pegel | word | V | - | 0 | 0,019531 |
| 20 | Klopfsensor 4 Ref. Pegel | word | V | - | 0 | 0,019531 |
| 21 | Zündspule 1 bis 4 Schließzeit | word | msec | szout_w | 0 | 0,001 |
| 22 | Fahrstrecke des Fahrzeugs | long | km | kmstand | 0 | 1 |
| 23 | Zeitzähler | long | sec | trmin_w | 0 | 1 |
| 24 | Vorderradgeschwindigkeit | word | km/h | v_vrad | 0 | 0,0625 |
| 25 | Hinterradgeschwindigkeit | word | km/h | v_hrad | 0 | 0,0625 |
| 26 | Leerlaufregler 1 | word | ySteps | st_cur_pos | 0 | 0,1 |
| 27 | Leerlaufregler 2  | word | ySteps | st_cur_pos | 0 | 0,1 |
| 28 | Umgebungsdruck | word | hPa | pu_w | 0 | 0,0390625 |
| 29 | Getriebe-Schaltwalzen-Position | byte | Gang | gangi | 0 | 1 |
| 30 | Kurbelwelleninterrupt Zaehler | word | - | Kwirq | 0 | 1 |
| 31 | Nockenwelleninterrupt Zaehler | word | - | Nwe1_irq | 0 | 1 |

<a id="table-forttexte2"></a>
### FORTTEXTE2

Dimensions: 75 rows × 5 columns

| ORT | MAXTEXT | MINTEXT | SIGTEXT | PLAUSTEXT |
| --- | --- | --- | --- | --- |
| 0x2718 | - | - | kein Signal | - |
| 0x271A | Offset über Grenzwert Sonde 1 Bank 1 | Langsame Sonde Sonde 1 Bank 1 | Nebenschluß Sonde mit Heizer Sonde 1 Bank 1 | Signal unplausibel Sonde 1 Bank 1 (siehe Umweltbedingung LSUNPSTAT) |
| 0x271B | Kurzschluss zur Batterie | Kurzschluss zur Masse | Kabelbruch | - |
| 0x2722 | Offset über Grenzwert Sonde 1 Bank 2 | Langsame Sonde Sonde 1 Bank 2 | Nebenschluß Sonde mit Heizer Sonde 1 Bank 2 | Signal unplausibel Sonde 1 Bank 2 (siehe Umweltbedingung LSUNPSTAT2) |
| 0x2723 | Kurzschluss zur Batterie | Kurzschluss zur Masse | Kabelbruch | - |
| 0x2736 | Kurzschluss zur Batterie | Kurzschluss zur Masse | - | Kraftstoffdruck unplausibel |
| 0x2740 | Ölstand zu niedrig | - | - | - |
| 0x2751 | Kurzschluss Masse | Leitungsunterbrechung oder Kurzschluss UB | - | - |
| 0x2752 | Kurzschluss Masse | Leitungsunterbrechung oder Kurzschluss UB | - | - |
| 0x2760 | - | Sekundärluftmasse zu gering | - | - |
| 0x2765 | Kurzschluss zur Batterie | Kurzschluss zur Masse | Kabelbruch | - |
| 0x276B | Kurzschluss zur Batterie | Kurzschluss zur Masse | Kabelbruch | - |
| 0x276C | - | Tankentlüftungssystem | - | - |
| 0x276D | - | Tankentlüftungssystem | - | - |
| 0x2772 | Kurzschluss zur Batterie | Kurzschluss zur Masse | Kabelbruch | - |
| 0x2774 | - | - | Eintrag fehlt | - |
| 0x2778 | - | Kurzschluss zur Masse | - | - |
| 0x2779 | - | - | - | Rechnerüberwachung: RAM |
| 0x277B | - | - | - | Rechnerüberwachung: ROM |
| 0x277C | - | - | - | Rechnerüberwachung: RESET |
| 0x277D | Spannungsschwellwert überschritten | Spannungsschwellwert unterschritten | - | ADC-Fehler, HW-Fehler |
| 0x277F | - | - | Seitenstützenschalter defekt | - |
| 0x2783 | Leitungsunterbrechung oder Kurzschluss UB | Kurzschluss zur Masse | - | Gang unplausibel |
| 0x2786 | - | - | - | Signal Vorderradgeschwindigkeit unplausibel |
| 0x2787 | - | - | - | Signal Hinterradgeschwindigkeit unplausibel |
| 0x2788 | - | - | fehlendes Signal Fahrzeuggeschwindigkeit | - |
| 0x278A | - | - | Defekt Killschalter | - |
| 0x278B | Kurzschluss nach Minus | Kurzschluss nach Plus oder Leitungsunterbrechung | Motortemperaturschwelle für Lambdaregelungsfreigabe nicht erreicht | Motortemperatursignal unplausibel ggü. Modell |
| 0x278C | Kurzschluss nach Minus | Kurzschluss nach Plus | - | - |
| 0x278D | Kurzschluss nach Minus | Kurzschluss nach Plus oder Leitungsunterbrechung | - | - |
| 0x279D | Kurzschluss zur Batterie | Kurzschluss zur Masse | Kabelbruch | - |
| 0x27A6 | Kurzschluss zur Batterie | Kurzschluss zur Masse | Kabelbruch | - |
| 0x27A7 | Kurzschluss zur Batterie | Kurzschluss zur Masse | Kabelbruch | - |
| 0x27A8 | Kurzschluss zur Batterie | Kurzschluss zur Masse | Kabelbruch | - |
| 0x27A9 | Kurzschluss zur Batterie | Kurzschluss zur Masse | Kabelbruch | - |
| 0x27B4 | Max-Fehler Umgebungsdrucksensor | Min-Fehler Umgebungsdrucksensor | - | Umgebungsdrucksensor unplausibel |
| 0x27B7 | Kurzschluss zur Batterie | Kurzschluss zur Masse | Kabelbruch | - |
| 0x27B8 | Kurzschluss zur Batterie | Kurzschluss zur Masse | Kabelbruch | - |
| 0x27D9 | Spannung zu hoch | Spannung zu niedrig | - | - |
| 0x27DA | Spannung zu hoch | Spannung zu niedrig | - | - |
| 0x27DB | Spannung zu hoch | Spannung zu niedrig | - | - |
| 0x27E0 | - | - | beide Klopfsensoren defekt | - |
| 0x27E1 | Motor mechanisch zu laut oder KS 1 außerhalb Toleranz (Empfindlichkeit) | elektrischer Fehler KS1 (Wackelkontakt) oder KS locker | - | - |
| 0x27E2 | Motor mechanisch zu laut oder KS 2 außerhalb Toleranz (Empfindlichkeit) | elektrischer Fehler KS2 (Wackelkontakt) oder KS locker | - | - |
| 0x27E3 | Übertemperatur bei CY315 | - | - | - |
| 0x27E4 | Übertemperatur bei CJ945 | - | - | - |
| 0x27E6 | - | - | - | Klopfbaustein defekt |
| 0x27E7 | - | - | - | Klopfbaustein defekt |
| 0x27E8 | - | - | - | Klopfbaustein defekt |
| 0x27EA | - | CAN-Schnittstelle, Timeout KOMBI | kein Signal | Plausibilitätsfehler |
| 0x27EB | - | CAN-Schnittstelle, Timeout ZFE | kein Signal | Plausibilitätsfehler |
| 0x27EC | - | CAN-Schnittstelle, Timeout ABS | kein Signal | Plausibilitätsfehler |
| 0x27F9 | Kurzschluss zur Batterie | Kurzschluss zur Masse | Kabelbruch | - |
| 0x283D | CAN Baustein im Zustand Passiv | DPRAM CAN- Baustein defekt | - | CAN-Baustein Bus Off oder CAN-Bus defekt |
| 0x2847 | Kurzschluss zur Batterie | Kurzschluss zur Masse | - | Versorgung Drosselklappengeber defekt |
| 0x2848 | oberer Adaptionsgrenzwert überschritten | unterer Adaptionsgrenzwert unterschritten | - | - |
| 0x28A6 | Kurzschluss zur Batterie | Kurzschluss zur Masse | open load | - |
| 0x28A8 | Kurzschluss zur Batterie | Kurzschluss zur Masse | open load | - |
| 0x28AA | Kurzschluss zur Batterie | Kurzschluss zur Masse | open load | - |
| 0x28AC | - | - | - | Schalter Klemme 15 defekt |
| 0x28C8 | obere Plausibilitätsschwelle unterschritten(short test) | untere Plausibilitätsschwelle unterschritten(short test) | - |  unplausibles Prüfresultat  erkannt (DKVS Kurztest) |
| 0x28C9 | obere Plausibilitätsschwelle unterschritten(short test) | untere Plausibilitätsschwelle unterschritten(short test) | - |  unplausibles Prüfresultat  erkannt (DKVS Kurztest) |
| 0x28CA | Sicherung System Supply | - | - | - |
| 0x28CB | Sicherung EKP | - | - | - |
| 0x28CC | Sicherung Zuendung | - | - | - |
| 0x28CD | - | - | - | Kurbelwellen-Zahnfehler / Lueckenverlust |
| 0x28CE | - | - | keine /abweichende Nockenwellenflanke | Phasenflanke / Einbaulage auserhalb zulaessiger Toleranz |
| 0x28FA | Kurzschluss zur Batterie | Kurzschluss zur Masse | Kabelbruch | - |
| 0x28FB | Fehler Ringantenne | Fehler CRC in BMSK | Schnittstelle EWS - BMSK gestoert | EWS-Daten unplausibel |
| 0x2904 | Kurzschluss UB  | Kurzschluss Masse | Kabelbruch | - |
| 0x2905 | Kurzschluss UB  | Kurzschluss Masse | Kabelbruch | - |
| 0x2934 | Eintrag fehlt | Eintrag fehlt | - | - |
| 0x2935 | Eintrag fehlt | Eintrag fehlt | - | - |
| 0x2972 | Leerlaufregler Anschlag oben | Leerlaufregler Anschlag unten | - | - |
| 0xFFFF | - | - | - | - |

<a id="table-betriebswtab"></a>
### BETRIEBSWTAB

Dimensions: 39 rows × 13 columns

| NAME | TELEGRAM | POS_ADR | LEN_ADR | ADR | BYTE | DATA_TYPE | COMPU_TYPE | FACT_A | FACT_B | MASK | VALUE | MEAS |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| UB | 8312F1304A01 | 0 | 0 | 0x00 | 4 | 2 | -- | 0.0942 | 0 | 0 | 0 | V |
| DKP | 8312F1304E01 | 0 | 0 | 0x00 | 4 | 5 | -- | 0.001222 | 0 | 0 | 0 | V |
| HFM | 8312F1304F01 | 0 | 0 | 0x00 | 4 | 5 | -- | 0.00977 | 0 | 0 | 0 | V |
| TMOT | 8312F1305001 | 0 | 0 | 0x00 | 4 | 2 | -- | 0.019531 | 0 | 0 | 0 | V |
| TANS | 8312F1305101 | 0 | 0 | 0x00 | 4 | 2 | -- | 0.019531 | 0 | 0 | 0 | V |
| TZYL1 | 8312F1306301 | 0 | 0 | 0x00 | 4 | 2 | -- | 0.019531 | 0 | 0 | 0 | V |
| TZYL2 | 8312F1306401 | 0 | 0 | 0x00 | 4 | 2 | -- | 0.019531 | 0 | 0 | 0 | V |
| KS1 | 8312F1305401 | 0 | 0 | 0x00 | 4 | 2 | -- | 0.019531 | 0 | 0 | 0 | V |
| KS2 | 8312F1305501 | 0 | 0 | 0x00 | 4 | 2 | -- | 0.019531 | 0 | 0 | 0 | V |
| GETRG | 8312F1305601 | 0 | 0 | 0x00 | 4 | 2 | -- | 0.019531 | 0 | 0 | 0 | V |
| DSK | 8312F1305701 | 0 | 0 | 0x00 | 4 | 2 | -- | 0.019531 | 0 | 0 | 0 | V |
| LSVK1 | 8312F1306001 | 0 | 0 | 0x00 | 4 | 2 | -- | 0.019531 | 0 | 0 | 0 | V |
| LSVK2 | 8312F1306101 | 0 | 0 | 0x00 | 4 | 2 | -- | 0.019531 | 0 | 0 | 0 | V |
| SYS | 8312F1305901 | 0 | 0 | 0x00 | 4 | 2 | -- | 0.0942 | 0 | 0 | 0 | V |
| ISYS | 8312F1305A01 | 0 | 0 | 0x00 | 4 | 5 | -- | 0.00488 | 0 | 0 | 0 | V |
| ZDG | 8312F1306701 | 0 | 0 | 0x00 | 4 | 2 | -- | 0.0942 | 0 | 0 | 0 | V |
| IZDG | 8312F1306801 | 0 | 0 | 0x00 | 4 | 5 | -- | 0.00488 | 0 | 0 | 0 | V |
| EKP | 8312F1307101 | 0 | 0 | 0x00 | 4 | 2 | -- | 0.0942 | 0 | 0 | 0 | V |
| IEKP | 8312F1307201 | 0 | 0 | 0x00 | 4 | 5 | -- | 0.00488 | 0 | 0 | 0 | V |
| FR_W | 8312F1224000 | 0 | 0 | 0x00 | 8 | 5 | -- | 0.0030517578125 | -100 | 0 | 0 | % |
| FR2_W | 8312F1224000 | 0 | 0 | 0x00 | 10 | 5 | -- | 0.0030517578125 | -100 | 0 | 0 | % |
| RKAT | 8312F1224004 | 0 | 0 | 0x00 | 6 | 7 | -- | 0.046875 | 0 | 0 | 0 | % |
| RKAT2 | 8312F1224004 | 0 | 0 | 0x00 | 8 | 7 | -- | 0.046875 | 0 | 0 | 0 | % |
| FRA | 8312F1224004 | 0 | 0 | 0x00 | 10 | 5 | -- | 0.000030517578125 | 0 | 0 | 0 | - |
| FRA2 | 8312F1224004 | 0 | 0 | 0x00 | 12 | 5 | -- | 0.000030517578125 | 0 | 0 | 0 | - |
| LUTSFI1 | 8312F1224003 | 0 | 0 | 0x00 | 4 | 7 | -- | 0.00390625 | 0 | 0 | 0 | 1/sec^2 |
| LUTSFI2 | 8312F1224003 | 0 | 0 | 0x00 | 4 | 7 | -- | 0.00390625 | 0 | 0 | 0 | 1/sec^2 |
| LUTSFI3 | 8312F1224003 | 0 | 0 | 0x00 | 4 | 7 | -- | 0.00390625 | 0 | 0 | 0 | 1/sec^2 |
| LUTSFI4 | 8312F1224003 | 0 | 0 | 0x00 | 4 | 7 | -- | 0.00390625 | 0 | 0 | 0 | 1/sec^2 |
| SPI | 8312F1305C01 | 0 | 0 | 0x00 | 4 | 5 | -- | 1 | 0 | 0 | 0 | usec |
| EKPS | 8312F130D405 | 0 | 0 | 0x00 | 4 | 1 | -- | 1 | 0 | 0 | 0 | - |
| EKPE | 8312F130D404 | 0 | 0 | 0x00 | 4 | 1 | -- | 1 | 0 | 0 | 0 | - |
| NWTESTON | 8312F130D608 | 0 | 0 | 0x00 | 4 | 1 | -- | 1 | 0 | 0 | 0 | - |
| NWTESTOFF | 8312F130D604 | 0 | 0 | 0x00 | 4 | 1 | -- | 1 | 0 | 0 | 0 | - |
| NWTESTDATA | 8312F1224000 | 0 | 0 | 0x00 | 4 | 5 | -- | 1 | 0 | 0 | 0 | - |
| SLVTESTON | 8312F130D808 | 0 | 0 | 0x00 | 4 | 1 | -- | 1 | 0 | 0 | 0 | - |
| SLVTESTOFF | 8312F130D804 | 0 | 0 | 0x00 | 4 | 1 | -- | 1 | 0 | 0 | 0 | - |
| NMAXLIMON | 8312F130D908 | 0 | 0 | 0x00 | 4 | 1 | -- | 1 | 0 | 0 | 0 | - |
| NMAXLIMOFF | 8312F130D904 | 0 | 0 | 0x00 | 4 | 1 | -- | 1 | 0 | 0 | 0 | - |

<a id="table-tab-verbaut"></a>
### TAB_VERBAUT

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Nicht verbaut |
| 1 | verbaut |

<a id="table-tab-aktiv"></a>
### TAB_AKTIV

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Nicht aktiv |
| 1 | aktiv |

<a id="table-tab-erkannt"></a>
### TAB_ERKANNT

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Nicht erkannt |
| 1 | erkannt |

<a id="table-tab-synchro"></a>
### TAB_SYNCHRO

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | NW Notlauf |
| 1 | synchronisiert |

<a id="table-messwerte2"></a>
### MESSWERTE2

Dimensions: 7 rows × 7 columns

| MNEMO | TEXT | TYP | EINH | NAME | ADD | FAKTOR |
| --- | --- | --- | --- | --- | --- | --- |
| STP1 | Position Steppermotor 1 | word | % | - | 0 | 0,1 |
| STP2 | Position Steppermotor 2 | word | % | - | 0 | 0,1 |
| VSIKM | Restkilometerstand fuer Ventilspielserviceintervall | word | km | - | 0 | 10 |
| VSIDEL | Anzahl von Loeschungen der VSI-km | byte | - | - | 0 | 1 |
| KMBMSK | interner Kilometerstand der BMSK | word | km | - | 0 | 6 |
| FRPS | gefilterter Wert des Kraftstoffdrucksensors | word | hPa | - | 0 | 0,2 |
| TOEL | Motoroeltemperatur | word | °C | - | -48 | 0,75 |

<a id="table-tab-ascwerte"></a>
### TAB_ASCWERTE

Dimensions: 6 rows × 16 columns

| MNEMO | TEXT | TYP | EINHEIT | NAME | ADD | FAKTOR | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ASCACTCTR | Dauer der ASC-Regelungen | long | s | ascActCtr | 0 | 0,01 |  |  |  |  |  |  |  |  |  |
| ASCINTCTR | mittlere Intensität/Momentrücknahme der ASC-Regelungen | long | % | - | 0 | 1 |  |  |  |  |  |  |  |  |  |
| ASCSTATUS | aktueller Status der ASC-Funktion | byte | - | ascStatus | 0 | 1 | RESERVIERT | KOMFORT_STANDBY | GS_STANDBY | KEINE_FREIGABE | KEINE_FREIGABE_GS | KOMFORT_AKTIV | GS_AKTIV | AUS | FEHLER |
| ASCMODUS | gewählter Modus der ASC-Funktion | byte | - | ascModus | 0 | 1 |  | KOMFORT | GS |  |  |  |  | AUS |  |
| ES_ASC | ASC-Taster | byte | - | ES_asc_tst | 0 | 1 | ASC-Taster nicht betätigt | ASC-Taster betätigt | NOT-AUS aktiv |  |  |  |  |  |  |
| RADCOR | gesamte Radiuskorrektur der Reifenradiusadaption | word | mm | radcor | 0 | 0,061035 |  |  |  |  |  |  |  |  |  |

<a id="table-tab-dslv-stati"></a>
### TAB_DSLV_STATI

Dimensions: 4 rows × 7 columns

| MNEMO | TEXT | TYP | EINHEIT | NAME | 0 | 1 |
| --- | --- | --- | --- | --- | --- | --- |
| B_ANFSLV | Bedingung Anforderung SLV-Diagnose | bool | - | B_anfslv | nicht erfüllt | erfüllt |
| B_DSLVE | Bedingung Durchführung SLV-Diagnose | bool | - | B_dslve | nicht erfüllt | erfüllt |
| B_DSLVA | Bedingung Abbruch SLV-Diagnose | bool | - | B_dslva | nicht erfüllt | erfüllt |
| B_ADSLV | Bedingung SLV-Diagnose abgeschlossen | bool | - | B_adslv | nicht erfüllt | erfüllt |
