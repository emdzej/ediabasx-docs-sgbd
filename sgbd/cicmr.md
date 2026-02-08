# cicmr.prg

- Jobs: [330](#jobs)
- Tables: [148](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | CIC Mid Rüko |
| ORIGIN | BMW EI-44 Hr.Mallinson |
| REVISION | 3.005 |
| AUTHOR | HaysAG EI-44 Hr.Bubb, TelemotiveAG EI-42 Hr.Schmidt |
| COMMENT | N/A |
| PACKAGE | 1.52 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [DIAGNOSEPROTOKOLL_LESEN](#job-diagnoseprotokoll-lesen) - Gibt die möglichen Diagnoseprotokolle für eine Auswahl an den Aufrufer zurück
- [DIAGNOSEPROTOKOLL_SETZEN](#job-diagnoseprotokoll-setzen) - Wählt ein Diagnoseprotokoll aus
- [IDENT](#job-ident) - Identdaten KWP2000: $1A ReadECUIdentification Modus  : Default
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus  : Default
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : Default
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels KWP2000: $22 ReadDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [NORMALER_DATENVERKEHR](#job-normaler-datenverkehr) - Sperren bzw. Freigeben des normalen Datenverkehrs KWP2000: $28 DisableNormalMessageTransmission KWP2000: $29 EnableNormalMessageTransmission Modus  : Default
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode des SG aufrecht erhalten KWP2000: $3E TesterPresent Modus  : Default
- [FS_SPERREN](#job-fs-sperren) - Sperren bzw. Freigeben des Fehlerspeichers KWP2000: $85 ControlDTCSetting Modus  : Default
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default
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
- [FS_LESEN_DETAIL](#job-fs-lesen-detail) - Fehlerspeicher lesen (ein Fehler / alle Details) KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus: Default
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry Modus: Default
- [STATUS_SOFTWARENAME](#job-status-softwarename) - Reads out the flashed Buildname
- [STATUS_VERSION_GATEWAYTABELLE](#job-status-version-gatewaytabelle) - Lesen der Versionsnummer der Gateway-Tabelle KWP2000: $21 ReadDataByLocalIdentifier $4D gatewayTableVersionNumber Modus  : Default
- [STATUS_GATEWAY_WAKEUP_SOURCE](#job-status-gateway-wakeup-source) - Liefert die Quelle/Ursache zurück, die zum Wecken des Gateway-Steuergerätes geführt hat. Dieser Job wird von SG ab E60 unterstützt! KWP2000: $21 ReadDataByLocalIdentifier $BB recordLocalIdentifier Modus  : Default
- [STATUS_GATEWAY_MOST_DEVICE_COUNT](#job-status-gateway-most-device-count) - Information über den Gateway-Dispatcher Anzahl der vom Dispatcher erkannten MOST-Teilnehmer im Ring KWP2000: $21 ReadDataByLocalIdentifier $50 recordLocalIdentifier Modus  : Default
- [STATUS_GATEWAY_MOST_DEVICES](#job-status-gateway-most-devices) - Ausgabe der erkannten MOST-Devices. Die Erkennung erfolgt ueber die InstID der Diagnose-Funktionsbloecke Komplex, da auf Grund der Größe mitlerweile Read_Devids_Current_Registry und Read_FBlockIDs_Current_Registry ausgewertet werden muss. Modus  : Default
- [STATUS_GATEWAY_LOCAL_REGISTRY_ELEMENTS](#job-status-gateway-local-registry-elements) - Information über den Gateway-Dispatcher Liste aller lokal (im Gateway-Adreßraum) registrierten FBlocks KWP2000: $21 ReadDataByLocalIdentifier $51 recordLocalIdentifier Modus  : Default
- [STATUS_PRAEPROZESSOR_SWITCH](#job-status-praeprozessor-switch) - Read out status of pre-processor switch KWP2000: $21 ReadDataByLocalIdentifier $55 recordLocalIdentifier - pre-processor switch state Modus  : Default
- [STATUS_INCLUDED_GW_TAB](#job-status-included-gw-tab) - Read out status of included GW table KWP2000: $21 ReadDataByLocalIdentifier $56 recordLocalIdentifier - included GW table state Modus  : Default
- [READ_DEVIDS_CURRENT_REGISTRY](#job-read-devids-current-registry) - Auslesen der DEVIDS der Current Registry KWP2000: $21 ReadDataByLocalIdentifier $49 recordLocalIdentifier Modus   : Default
- [READ_DEVIDS_DEFAULT_REGISTRY](#job-read-devids-default-registry) - Auslesen der DEVIDS der Default Registry KWP2000: $21 ReadDataByLocalIdentifier $4A recordLocalIdentifier Modus   : Default
- [READ_FBLOCKS_CURRENT_REGISTRY](#job-read-fblocks-current-registry) - Auslesen der FBlockIDs einer DEVID der Current Registry KWP2000: $21 ReadDataByLocalIdentifier $4B recordLocalIdentifier Modus   : Default
- [READ_FBLOCKS_DEFAULT_REGISTRY](#job-read-fblocks-default-registry) - Auslesen der FBlockIDs einer DEVID der Default Registry KWP2000: $21 ReadDataByLocalIdentifier $4C recordLocalIdentifier Modus   : Default
- [DIAGTUNNELLING_KWP](#job-diagtunnelling-kwp) - complete tunneling of KWP telegrams
- [LESEN_CONFIGURATION_TABLE](#job-lesen-configuration-table) - Reads out the currently active configuration table.
- [LESEN_DAR](#job-lesen-dar) - Lesen eines DAR Datensatzes
- [LESEN_NAVDVDPIN](#job-lesen-navdvdpin) - Reads the four digits PIN codes to unlock the NAVI DVD.
- [LESEN_TELEFONNUMMERN](#job-lesen-telefonnummern) - Auslesen der in HeadUnit gespeicherten Telefonnummern für - Bereitschaftsdienst - Heimathändler - Passo - Hotline
- [LESEN_TELEFONNUMMER_SDARS](#job-lesen-telefonnummer-sdars)
- [READ_CURRENT_REGISTRY](#job-read-current-registry) - Liefert den Inhalt der Current Registry
- [READ_DEFAULT_REGISTRY](#job-read-default-registry) - Liefert den Inhalt der default Registry
- [READ_06_DEFAULT_REGISTRY](#job-read-06-default-registry) - Liefert den Inhalt der default Registry
- [READ_DIFF_REGISTRY](#job-read-diff-registry) - Liefert den Unterschied zwischen Current und default Registry
- [SCHREIBEN_CONFIGURATION_TABLE](#job-schreiben-configuration-table) - Writes a configuration table selected by a special index n from (0...n) onto the currently active configuration table in the head-unit.
- [SCHREIBEN_DAR](#job-schreiben-dar) - Schreiben eines DAR Datensatzes
- [SCHREIBEN_BMW_ZERTIFIKAT](#job-schreiben-bmw-zertifikat) - Schreiben eines BMW Zertifikates
- [SCHREIBEN_BROWSER_ZERTIFIKAT](#job-schreiben-browser-zertifikat) - Schreiben eines BROWSER Zertifikates
- [SCHREIBEN_NAVDVDPIN](#job-schreiben-navdvdpin) - Writes the four digits PIN code to unlock the NAVI DVD.
- [SCHREIBEN_TELEFONNUMMER_SDARS](#job-schreiben-telefonnummer-sdars) - Nummer des Bereitschaftsdienstes
- [SCHREIBEN_TELEFONNUMMERN](#job-schreiben-telefonnummern) - Schreiben der Telefonnummern für - Bereitschaftsdienst - Heimathändler - Passo - Hotline
- [SER_NR_DOM_LESEN](#job-ser-nr-dom-lesen) - Reads the serial number with 14 digits (DIN ISO 10486)
- [STATUS_ABILITY_TO_WAKE](#job-status-ability-to-wake) - Gibt an ob SG Most Ring wecken darf
- [STATUS_ADAS](#job-status-adas) - Reads out from the navigation system how many Resyncs from which client the navigation system has received and how many messages the navigation system has sent since the beginning of the current lifecycle.
- [STATUS_AKTIVE_GAL_KURVE](#job-status-aktive-gal-kurve) - Reads the number of the active speed dependent volume control curve.
- [STATUS_ANALOG_TEMPERATUR](#job-status-analog-temperatur) - The temperature values on the FOT, in the module and at the amplifier and all other reasonable locations (e.g. drive) in degrees Celsius.
- [STATUS_ANT_DC](#job-status-ant-dc) - Checks the connection between head unit and diversity by performing an impedance measurement
- [STATUS_ANT_EIGEN_DIAG](#job-status-ant-eigen-diag) - Result of the antenna diversity self-diagnosis.
- [STATUS_ANT_QFS](#job-status-ant-qfs) - Reads the current quality and the field strength of the actual radio signal of the actual frequency.
- [STATUS_APPLICATION](#job-status-application) - Reads out applications stati if they are coded and their availability
- [STATUS_AUDIOKANAELE](#job-status-audiokanaele) - Returns the status of the Audiokanaele
- [STATUS_AVERAGE_MESSAGE_RECEPTION_RATE](#job-status-average-message-reception-rate) - Liest die mittlere Nachrichtenabnahmerate des SGs während dieses Gerät geflasht wird, also in der ProgramminSession Auslesbar muss der Status jederzeit sein
- [STATUS_BIT_ERROR_RATE_IBOC](#job-status-bit-error-rate-iboc) - Measures the quality of the reception of the current IBOC station.
- [STATUS_BROWSER_APPLIKATION](#job-status-browser-applikation) - Tests with a simple request onto the browser application (task) if it is coded, if it is active and responds. Test if a user input is actually necessary because of an Online-PopUp.
- [STATUS_CD_MD_CDC](#job-status-cd-md-cdc) - Reads out the disc identifier and the quality level of the digital playback
- [STATUS_DAR_INDEX](#job-status-dar-index) - Indicates the DAR which is selected.
- [STATUS_DEMUTE](#job-status-demute) - Returns the mute status of the current entertainment source.
- [STATUS_DIRECTION](#job-status-direction) - Reads out which direction/type of gear (forwards, backwards, idle) is currently active and where the signal is coming from (source of the signal)
- [STATUS_DREHKNOPF](#job-status-drehknopf) - gibt die Position des Drehknopfes bezüglich des letzen Aufstartens wieder
- [STATUS_DRIVE_CD](#job-status-drive-cd) - Status of DVD Drive
- [STATUS_DRIVE_DVD](#job-status-drive-dvd) - Status of DVD Drive
- [STATUS_EXT_GYROSIGNAL](#job-status-ext-gyrosignal) - Checks if the signal(s) coming from the external gyro is available on the bus.
- [STATUS_FAULT_TRACKING](#job-status-fault-tracking) - Reads out one or all datasets stored by the extended fault tracking mechanism.
- [STATUS_FB_TASTE](#job-status-fb-taste) - Test der Functional Bookmarks
- [STATUS_FBAND_SCAN](#job-status-fband-scan) - Start FBand scan
- [STATUS_FIND_BEST_STATION](#job-status-find-best-station) - Returns the status of the searching process and the information data of the best station if the searching process has been ended successfully.
- [STATUS_FIND_BEST_STATION_DAB](#job-status-find-best-station-dab) - Returns the status of the searching process and the information data about the best DAB ensemble if the searching process has been ended successfully.
- [STATUS_FIND_BEST_TMC_STATION](#job-status-find-best-tmc-station) - Returns the status of the searching process and the information data of the best TMC station if the searching process has been ended successfully.
- [STATUS_FIND_BEST_TMC_STATION_DAB](#job-status-find-best-tmc-station-dab) - Returns the status of the searching process and the information data of the best DAB TMC station if the searching process has been ended successfully.
- [STATUS_FLOTTENMODUS](#job-status-flottenmodus) - Reads out the Flottenmodus (mode of the NAVI DVD locking) that is currently active.
- [STATUS_FOT_TEMPERATUR](#job-status-fot-temperatur) - Gibt an ob SG Most Ring wecken darf
- [STATUS_FREQUENZ](#job-status-frequenz) - Get back the currently active tuner frequency
- [STATUS_GPS](#job-status-gps) - Returns the status of the GPS reception.
- [STATUS_GPS_DILUTION_OF_POSITION](#job-status-gps-dilution-of-position) - Reads out the GPS dilution of position.
- [STATUS_GPS_POSITION](#job-status-gps-position) - Returns the current GPS position.
- [STATUS_GPS_RECEIVER_SW_VERSION](#job-status-gps-receiver-sw-version) - Reads out the software version of the GPS receiver.
- [STATUS_GPS_SATINFO](#job-status-gps-satinfo) - Reads out the number of visible and the number of tracked satellites and returns information about each visible satellite.
- [STATUS_GPS_TIME](#job-status-gps-time) - Reads out the GPS date and time.
- [STATUS_HIGHSYNCCONNECTION_DETAIL](#job-status-highsyncconnection-detail) - Genaue Information zur abgefragten Connection ausgeben
- [STATUS_HIGHSYNCCONNECTION_TABLE](#job-status-highsyncconnection-table) - HighSyncConnectionTable
- [STATUS_HORIZONTAL_HEADING](#job-status-horizontal-heading) - Reads out all data related to the horizontal heading of the car (gyro type, horizontal delta heading and drift) and performs a comparison with the GPS horizontal heading changes.
- [STATUS_HW_VARIANTE](#job-status-hw-variante) - Liefert die HW-Variante der Headunit
- [STATUS_INTERNAL_ACCELERATION_SENSOR](#job-status-internal-acceleration-sensor) - Returns if the internal acceleration sensor is working on the basis of the voltage value.
- [STATUS_INTERNAL_GYRO](#job-status-internal-gyro) - Returns if the internal gyro is working on the basis of the voltage value.
- [STATUS_LAST_CONNECTION](#job-status-last-connection) - Returns various statuses of the currently active session or if no session is active, of the last session.
- [STATUS_LAUTSPRECHER_IMPEDANZMESSUNG](#job-status-lautsprecher-impedanzmessung) - Returns the result of the test performed with steuern_lautsprecher_impedanzmessung.
- [STATUS_LESEN_LAUFWERK](#job-status-lesen-laufwerk) - Reads out which drives the Head-Unit contains and the type and firmware of each drive.
- [STATUS_LESEN_SYSTEMAUDIO](#job-status-lesen-systemaudio) - This job reads which audio system is currently coded
- [STATUS_LESESTATISTIK_DVD](#job-status-lesestatistik-dvd) - Reads out some statistical data concerning the DVD drive and derived from the HDD SMART system
- [STATUS_LOGISTIC_NR](#job-status-logistic-nr) - Reads out the logistic number Lieferumfangsnummer = number that characterizes the Anliefervariante
- [STATUS_MAP_UPDATE](#job-status-map-update) - Returns the status of the map update.
- [STATUS_MAPMATERIAL_VERSION](#job-status-mapmaterial-version) - Reads out the version of the map material.
- [STATUS_MEMORY_USAGE](#job-status-memory-usage) - Returns the usage of the flash and of the RAM memories.
- [STATUS_MOST_3DB](#job-status-most-3db) - xx Status der 3dB Leistungsabsenkung der MOST FOTs.
- [STATUS_MOSTDIAG_DELAY](#job-status-mostdiag-delay) - Verzögerungszeit, bis der Job steuern_zentrale_registry_sollkonfiguration wieder gestartet werden kann
- [STATUS_NAVI_CALIBRATION](#job-status-navi-calibration) - Returns if the Positioning Process is calibrated.
- [STATUS_NAVI_MAP](#job-status-navi-map) - Returns the status of the customer navigation map.
- [STATUS_NAVICHECK](#job-status-navicheck) - Returns the actual results of the NAVICHECK subsystem.
- [STATUS_NEXT_ENTSOURCE](#job-status-next-entsource) - Gives back the status of actual entertainmentsource.
- [STATUS_POI_DOWNLOAD](#job-status-poi-download) - Returns the status of the POI download.
- [STATUS_PROVISIONING](#job-status-provisioning) - Returns the status of the provisioning request.
- [STATUS_RADON](#job-status-radon) - Reads out the status of the RADON control lead.
- [STATUS_RDS](#job-status-rds) - Reads out the activation state of the TP, RDS and AF functionalities.
- [STATUS_ROUTE_DOWNLOAD](#job-status-route-download) - Returns the status of the route download.
- [STATUS_ROUTING_ENGINE](#job-status-routing-engine) - Inhalt der Routing Engine
- [STATUS_SDARS_BER](#job-status-sdars-ber) - Returns the BER of the SDARS signal.
- [STATUS_SDARS_BER_MODE](#job-status-sdars-ber-mode) - Returns the SDARS BER mode that is currently active
- [STATUS_SDARS_CHANNEL](#job-status-sdars-channel) - Sets a definite SDARS channel.
- [STATUS_SDARS_ESN](#job-status-sdars-esn) - Returns the 12 digits ESN of the SDARS tuner.
- [STATUS_SDARS_FACTORY_DEFAULTS](#job-status-sdars-factory-defaults) - Restores the factory defaults of the SDARS tuner.
- [STATUS_SDARS_FIRMWARE_VERSIONS](#job-status-sdars-firmware-versions) - Returns the various firmware versions of the SDARS module
- [STATUS_SDARS_GENERATOR_FREQUENCY](#job-status-sdars-generator-frequency) - Sets the sine generator frequency respectively for the left and right channels.
- [STATUS_SDARS_SIGNAL_QUALITY](#job-status-sdars-signal-quality) - Returns the quality of the SDARS signal.
- [STATUS_SDARS_TUNER_MODE](#job-status-sdars-tuner-mode) - Sets the SDARS tuner in the selected mode.
- [STATUS_SEARCH_FBLOCK](#job-status-search-fblock) - FBlockID.InstID searched in Current Registry
- [STATUS_SENSOR_TEMP](#job-status-sensor-temp) - Returns the temperature of the desired sensor (no matter if the temperature is currently being simulated or not).
- [STATUS_SGBMID_NAVIMAP](#job-status-sgbmid-navimap) - Returns the SGBM ID of the customer navigation map that is currently active.
- [STATUS_SPEED](#job-status-speed) - Reads out all speed data of the car (sensor speed of each wheel, combined sensor speed and GPS speed) and performs a comparison of the combined sensor speed and of the GPS speed.
- [STATUS_TASTE](#job-status-taste) - Auslesen, ob gerade eine Taste gedrueckt ist
- [STATUS_TDA_ATM](#job-status-tda-atm) - Reads out the automatic trigger of a TDA call.
- [STATUS_TEL_MUTE](#job-status-tel-mute) - Outputs whether the phone mute lead is active or inactive.
- [STATUS_TEMP_VERTEILUNG_DVD_DRIVE](#job-status-temp-verteilung-dvd-drive) - Reads out the temperature histogram of the DVD drive.
- [STATUS_TEMP_VERTEILUNG_FOT](#job-status-temp-verteilung-fot) - Reads out the temperature histogram of the FOT unit.
- [STATUS_TEMP_VERTEILUNG_POWER_AMPLIFIER](#job-status-temp-verteilung-power-amplifier) - Reads out the temperature histogram of the power amplifier.
- [STATUS_TEMP_VERTEILUNG_SH4A](#job-status-temp-verteilung-sh4a) - Reads out the temperature histogram of the SH4A.
- [STATUS_TEST_ANTENNE](#job-status-test-antenne) - Returns the results of the impedance measurements performed with steuern_test_antenne
- [STATUS_TMC](#job-status-tmc) - Returns the activation state of the TMC functionality
- [STATUS_TMC_DAB](#job-status-tmc-dab) - Returns the activation state of the DAB TMC functionality.
- [STATUS_TUNER_CODIERUNG](#job-status-tuner-codierung) - Reads all the coding data / flags which are correlated to the tuner.
- [STATUS_TUNER_CODIERUNG_DAB](#job-status-tuner-codierung-dab) - Reads all the coding data / flags which are correlated to the tuner.
- [STATUS_VERSION_MOST_CONTROLLER](#job-status-version-most-controller) - Return Version of MOST Controller
- [STATUS_VERSORGUNGSSPANNUNG](#job-status-versorgungsspannung) - Betriebsspannung am SG. Darstellung mit Millivolt-Auflösung.
- [STATUS_VERTICAL_HEADING](#job-status-vertical-heading) - Reads out all data related to the vertical heading of the car (acceleration sensor type, vertical delta heading and drift) and performs a comparison with the GPS vertical heading changes.
- [STATUS_VOLUMEAUDIO](#job-status-volumeaudio) - Abfragen der Audio-Lautstaerke
- [STATUS_WAKEUP_STATUS](#job-status-wakeup-status) - Gibt an, ob das SG den MOST-Ring geweckt hat oder geweckt wurde.
- [STATUS_WAKEUP_ABSTIME](#job-status-wakeup-abstime) - 7 bytes Zeitpunkt, zu dem das SG den Weckbefehl gegeben hat Bytes werden als Datum interpretiert Beispiel: '20060508131210' in der Reihenfolge YYYYMMDDHHMMSS. Falls das SG nie geweckt hat wird '00000000000000' zurückgegeben
- [STATUS_WAVEBAND](#job-status-waveband) - Returns the waveband that is currently active.
- [STEUERN_ABILITY_TO_WAKE](#job-steuern-ability-to-wake) - Gibt an, ob das SG den MOST-Ring wecken darf.
- [STEUERN_ANT_EIGEN_DIAG](#job-steuern-ant-eigen-diag) - Starts antenna diagnostics cycle for the respective antenna specification
- [STEUERN_ANT_SCAN](#job-steuern-ant-scan) - Creates an 8 Volt peek (if diversity diagnosis modus is active done by steuern_ant_eigen_diagnose) to switch through the FM antennas of the diversity or to switch back to normal operation mode into the AM band with the AM amplifier being active
- [STEUERN_AUDIOKANAELE](#job-steuern-audiokanaele) - Ansteuern eines AudioKanals
- [STEUERN_CLEAR_CKMDATA](#job-steuern-clear-ckmdata) - Restores the delivery state (resets the PIA settings to their default settings) for the desired key/car.
- [STATUS_CLEAR_CKMDATA](#job-status-clear-ckmdata) - Status des Löschens der Car-Key-PIA Daten eines oder aller Schlüssel.
- [STEUERN_CLEAR_TEMP_VERTEILUNG](#job-steuern-clear-temp-verteilung) - Deletes the desired temperature histogram.
- [STEUERN_CODIERUNG_MASTER_BEREICH](#job-steuern-codierung-master-bereich) - Copy the content of the coding working domain into the very secured coding master domain.
- [STEUERN_CODIERUNG_REFERENZ_CRC](#job-steuern-codierung-referenz-crc) - Calculates the CRC of the coding data that are stored into the coding master domain and stores it into a very secured memory domain.
- [STEUERN_COPY_CKMDATA](#job-steuern-copy-ckmdata) - Copies the PIA data from key X to key Y.
- [STEUERN_DELETE_COOKIES](#job-steuern-delete-cookies) - Deletes all cookies inside all http stacks.
- [STEUERN_DEMUTE](#job-steuern-demute) - Controls the mute status of the current entertainment source.
- [STEUERN_EJECT](#job-steuern-eject) - Ejects the media of the selected drives.
- [STEUERN_EMERGENCY_EJECT](#job-steuern-emergency-eject) - Ejects the media of the selected drives.
- [STEUERN_FB_RESET](#job-steuern-fb-reset) - This job resets/restarts the bezel.
- [STEUERN_FBAND_SCAN](#job-steuern-fband-scan) - Start FBand scan
- [STEUERN_FBAND_SCAN_STOP](#job-steuern-fband-scan-stop) - Stoped FBand scan
- [STEUERN_FIND_BEST_STATION](#job-steuern-find-best-station) - Triggers the search in the current waveband of the best station (station with the best reception). When the best station has been detected, the head-unit switches to this best station.
- [STEUERN_FIND_BEST_STATION_DAB](#job-steuern-find-best-station-dab) - Triggers the search of the best DAB ensemble (ensemble with the lowest bit error rate). When the best DAB ensemble has been detected, the head-unit switches to this best ensemble (to the 1st service of the ensemble).
- [STEUERN_FIND_BEST_TMC_STATION](#job-steuern-find-best-tmc-station) - Triggers the search in the current waveband of the best TMC station (station with the best reception). When the best TMC station has been detected, the head-unit switches to this best station.
- [STEUERN_FIND_BEST_TMC_STATION_DAB](#job-steuern-find-best-tmc-station-dab) - Triggers the search of the best DAB TMC station (station with the best reception). When the best DAB TMC station has been detected, the head-unit switches to this best station.
- [STEUERN_FLOTTENMODUS](#job-steuern-flottenmodus) - Set the desired Flottenmodus (mode of the NAVI DVD lock).
- [STEUERN_FREQUENZ](#job-steuern-frequenz) - Set the tuner frequency.
- [STEUERN_KLANGZEICHEN](#job-steuern-klangzeichen) - Ausloesen eines Klangzeichens
- [STEUERN_LINEAR](#job-steuern-linear) - This job resets the tone controls such as bass treble, fader, balance, surround to the default values
- [STEUERN_LOGISTIC_NR](#job-steuern-logistic-nr) - Stores the logistic number Lieferumfangsnummer = number that characterizes the Anliefervariante
- [STEUERN_MOST_3DB](#job-steuern-most-3db) - 3dB Leistungsabsenkung der MOST FOTs
- [STEUERN_NAVI_MAP](#job-steuern-navi-map) - Enables to deactivate or to erase the customer navigation map.
- [STEUERN_NAVI_SIMULATION](#job-steuern-navi-simulation) - Activates or deactivates the navi simulation mode
- [STATUS_NAVI_SIMULATION](#job-status-navi-simulation) - Activation state of the navi simulation mode
- [STEUERN_NAVI_SPEECH](#job-steuern-navi-speech) - Enables to test the navi speech output in the language that is currently set.
- [STEUERN_NEXT_ENTSOURCE](#job-steuern-next-entsource) - Enables to switch to the next or to a specified entertainment source.
- [STEUERN_PDC](#job-steuern-pdc) - Simulates the tone that is hearable at a definite distance to an obstacle
- [STEUERN_PROVISIONING](#job-steuern-provisioning) - Initiates provisioning request.
- [STEUERN_RADON](#job-steuern-radon) - Sets the RADON control lead to logical High or Low.
- [STEUERN_RDS](#job-steuern-rds) - Enables to control the activation state of the RDS and of the TP functionalities.
- [STEUERN_RINGBRUCH_DIAGNOSE](#job-steuern-ringbruch-diagnose) - Ringbruchdiagnose soll gestartet werden
- [STEUERN_SDARS_BER_MODE](#job-steuern-sdars-ber-mode) - Sets the selected SDARS BER mode.
- [STEUERN_SDARS_CHANNEL](#job-steuern-sdars-channel) - Sets a definite SDARS channel.
- [STEUERN_SDARS_FACTORY_DEFAULTS](#job-steuern-sdars-factory-defaults) - Restores the factory defaults of the SDARS tuner.
- [STEUERN_SDARS_GENERATOR_FREQUENCY](#job-steuern-sdars-generator-frequency) - Sets the sine generator frequency respectively for the left and right channels.
- [STEUERN_SDARS_TUNER_MODE](#job-steuern-sdars-tuner-mode) - Sets the SDARS tuner in the selected mode.
- [STEUERN_SENSOR_TEMP](#job-steuern-sensor-temp) - Simulates the temperature of a definite sensor.
- [STEUERN_SINUSGENERATOR_AUS](#job-steuern-sinusgenerator-aus) - Ausschalten des Sinusgenerators
- [STEUERN_SINUSGENERATOR_EIN](#job-steuern-sinusgenerator-ein) - Aktivieren des Sinusgenerators und Ausgabe auf allen ausgewählten Lautsprechern
- [STEUERN_START_NAVICHECK](#job-steuern-start-navicheck) - Initiates the special modus to check the plausibility of the navigation subsystem.
- [STEUERN_STOP_NAVICHECK](#job-steuern-stop-navicheck) - This job stops the NAVICHECK subsystem.
- [STEUERN_TDA_ATM](#job-steuern-tda-atm) - Configures the automatic trigger of a TDA call.
- [STEUERN_TEST_ANTENNE](#job-steuern-test-antenne) - Performs an impedance measurement of one, some or all antennas
- [STEUERN_TMC](#job-steuern-tmc) - Controls the activation state (on/off) of the TMC functionality.
- [STEUERN_TMC_DAB](#job-steuern-tmc-dab) - Controls the activation state (on/off) of the DAB TMC functionality.
- [STEUERN_TRACK_NUMBER](#job-steuern-track-number) - Sets the track number
- [STEUERN_TUNER_SUCHLAUF](#job-steuern-tuner-suchlauf) - Starts station search of tuner in the actual selected waveband.
- [STEUERN_USB_TEST](#job-steuern-usb-test) - Stores VendorID and ProductID for diagnosis of USB mass storage recognition. Internal preparation of control unit for USB recognition (optional).
- [STATUS_USB_TEST](#job-status-usb-test) - Returns status of USB mass storage recognition
- [STATUS_USB_HUB_TEST](#job-status-usb-hub-test) - Returns if a USB HUB is built in
- [STATUS_TEST_USB_TEL](#job-status-test-usb-tel) - Returns status of USB mass storage recognition for USB Interface (KDZ) OR Tele-phone Snap In Adapter (SIA)
- [STEUERN_TEST_USB_TEL](#job-steuern-test-usb-tel) - Stores VendorID and ProductID for diagnosis of USB mass storage recognition for USB Interface (KDZ = Kundenzugang in der Mittelkonsole) or and Telephone Snap In Adapter (SIA)
- [STATUS_USB_STACK_INFO_FOR_DEVICE](#job-status-usb-stack-info-for-device) - Reads out logistical information about the four last connected USB devices four last connected IPOD Players, four last connected MTP Players and four last unrecognized USB devices
- [STEUERN_VOLUMEAUDIO](#job-steuern-volumeaudio) - Adjusts the volume of a definite audio signal
- [STEUERN_VOLUMEAUDIO_DEFAULT](#job-steuern-volumeaudio-default) - Set Volumeaudio default
- [STEUERN_WATCHDOG_TRIGGER_STOP](#job-steuern-watchdog-trigger-stop) - Unterbindet das regelmäßige Rücksetzen des Applikations-Watchdogs nach ARG_TIME_WATCHDOG Sekunden. Wenn ARG_TIME_WATCHDOG nicht angegeben wird, wird der Wert 0 benutzt.
- [STEUERN_WAVEBAND](#job-steuern-waveband) - Activates the desired waveband.
- [STEUERN_ZENTRALE_REGISTRY_SOLLKONFIGURATION](#job-steuern-zentrale-registry-sollkonfiguration) - Die aktuelle Registry wird als Default Registry gespeichert
- [STATUS_TEST_MICROPHONE](#job-status-test-microphone) - Returns the result of the microphone test performed with steuern_test_microphone.
- [STATUS_TEST_VIDEOEINGANG](#job-status-test-videoeingang) - Returns the results of the signal tests performed with steuern_test_videoeingang.
- [STATUS_VIDEOVERBINDUNG](#job-status-videoverbindung) - Returns if a video connection is active and if yes which
- [STATUS_AKTIVES_SPRACHPAKET](#job-status-aktives-sprachpaket) - Reads out which language for speech recognition system is currently stored into the flash memory
- [STATUS_CPU_AUSLASTUNG](#job-status-cpu-auslastung) - Reads out the current system load of the CPU(s) in per cent.
- [STATUS_ETHERNET_CONNECTION_STATE](#job-status-ethernet-connection-state) - Returns the activation state of all Ethernet connections
- [STATUS_GET_IPCONFIG](#job-status-get-ipconfig) - Reads out the actual ipconfig of the Ethernet interface of the HeadUnit.
- [STATUS_LADE_SPRACHPAKET](#job-status-lade-sprachpaket) - Returns the status of the loading process started with the job steuern_lade_sprachpaket.
- [STATUS_LANGUAGE](#job-status-language) - Reads out the languag that is currently active.
- [STATUS_MENU](#job-status-menu) - Reads out the menu that is currently active
- [STATUS_SELBSTTEST](#job-status-selbsttest) - Returns the mute status of the current entertainment source.
- [STATUS_TEST_AUXVERBINDUNG](#job-status-test-auxverbindung) - Returns the results of the impedance measurement performed with steuern_test_aux_verbindung
- [STATUS_TEST_VERBAU](#job-status-test-verbau) - Returns the result of the test of external interfaces performed with steuern_test_verbau
- [STEUERN_CLEAR_FAULT_TRACKING](#job-steuern-clear-fault-tracking) - Clears down to zero the whole area where the extended fault tracking datasets are stored. It also removes the DTC Error_Software from the secondary error memory.
- [STEUERN_ETHERNET_CONNECTION_STATE](#job-steuern-ethernet-connection-state) - Enables to control the activation state of the selected Ethernet connection.
- [STEUERN_INTERNAL_RESET](#job-steuern-internal-reset) - Resets the head-unit with following properties The applications are stored properly before performing the reset The MOST light remains on
- [STEUERN_LADE_SPRACHPAKET](#job-steuern-lade-sprachpaket) - Enables to load the language for speech recognition system and perhaps the speech for the Navi out from the HDD into the Flash memory.
- [STEUERN_LANGUAGE](#job-steuern-language) - Activates the desired languag.
- [STEUERN_LAUTSPRECHER_IMPEDANZMESSUNG](#job-steuern-lautsprecher-impedanzmessung) - Enables to test a loudspeaker connection by performing an impedance measurement.
- [STEUERN_MENU](#job-steuern-menu) - Activates the desired menu.
- [STEUERN_SELBSTTEST](#job-steuern-selbsttest) - Performs a test of internal functions and components.
- [STEUERN_SIGNALAUSGABE](#job-steuern-signalausgabe) - Modifies the video output signal
- [STEUERN_SIGNALAUSGABE_AUS](#job-steuern-signalausgabe-aus) - Ends the output of the signal that was generated with steuern_signalausgabe
- [STEUERN_TEST_AUXVERBINDUNG](#job-steuern-test-auxverbindung) - Performs an impedance measurement of one or all auxiliary connections
- [STEUERN_TEST_MICROPHONE](#job-steuern-test-microphone) - Enables to test a definite microphone by generating a sine tone and starting in parallel the recording mode of the microphone
- [STEUERN_TEST_VERBAU](#job-steuern-test-verbau) - Performs a test of one, some or all external interfaces
- [STEUERN_TEST_VIDEOEINGANG](#job-steuern-test-videoeingang) - Tests the signal(s) from one (some) definite video source(s).
- [STEUERN_VERY_HARD_RESET](#job-steuern-very-hard-reset) - Resets the head-unit analogue to a battery reset.
- [STEUERN_VIDEOVERBINDUNG](#job-steuern-videoverbindung) - Establishes a video connection between a video source and some video sinks
- [STEUERN_VIDEOVERBINDUNG_AUS](#job-steuern-videoverbindung-aus) - Ends the connection that has been established with the job steuern_videoverbindung and restores the normal operation mode
- [STATUS_FAN_HISTORY](#job-status-fan-history) - Reads out the fan histogram.
- [STATUS_LUEFTER](#job-status-luefter) - Returns if and at which speed the fan is running.
- [STATUS_LUEFTER_CONTROL_DATA](#job-status-luefter-control-data) - Reads out the current control parameters of the fan
- [STEUERN_CLEAR_FAN_HISTORY](#job-steuern-clear-fan-history) - Clears the fan histogram
- [STEUERN_LUEFTER](#job-steuern-luefter) - Triggers the fan rotation at its maximal rotation speed
- [STEUERN_LUEFTER_CONTROL_DATA](#job-steuern-luefter-control-data) - Enables to modify one or some control parameters of the fan
- [STATUS_AF_TP_DAB](#job-status-af-tp-dab) - Reads out the activation state of the TP, RDS and AF functionalities.
- [STATUS_AKTIVE_ANTENNE_DAB](#job-status-aktive-antenne-dab) - Reads out which DAB antenna is currently active.
- [STATUS_BIT_ERROR_RATE_DAB](#job-status-bit-error-rate-dab) - Measures the quality of the reception of the current DAB ensemble.
- [STATUS_FREQUENZ_DAB](#job-status-frequenz-dab) - Get back the currently active DAB frequency
- [STATUS_SIGNAL_DAB](#job-status-signal-dab) - Reads out if a valid DAB signal is available.
- [STEUERN_AF_TP_DAB](#job-steuern-af-tp-dab) - Enables to control the activation state of the RDS and of the TP functionalities.
- [STEUERN_AKTIVE_ANTENNE_DAB](#job-steuern-aktive-antenne-dab) - Enables to control the activation state of both DAB antennae
- [STEUERN_FREQUENZ_DAB](#job-steuern-frequenz-dab) - Set the DAB frequency.
- [STATUS_INITIALISIERUNG](#job-status-initialisierung) - Gibt wieder, ob das komplette Steuergerät initialisiert wurde
- [STEUERN_RESCUE_MODE](#job-steuern-rescue-mode) - Resets the HeadUnit in a stable bootloadermode
- [LESEN_INDIVIDUALDATA_LISTE](#job-lesen-individualdata-liste) - Lesen eines Listeneintrags der Individualisierungsdaten KWP2000: $31 ReadDataByLocalIdentifier $80 recordLocalIdentifier
- [LESE_INDIVIDUALDATA](#job-lese-individualdata) - Lesen von Individualisierungsdaten Modus   : Default
- [SCHREIBEN_INDIVIDUALDATA](#job-schreiben-individualdata) - Schreiben von Individualisierungsdaten Modus   : Default
- [STEUERN_BAUREIHE](#job-steuern-baureihe) - Sets the HeadUnit to a desired Baureihe of the Gateway table
- [STATUS_BAUREIHE](#job-status-baureihe) - Reads out the actual Baureihe of the Gateway table
- [STEUERN_NWM_CONFIG_NOTOK](#job-steuern-nwm-config-notok) - Sends a Config.NotOk on the MOST Bus
- [STATUS_HMI_VERSION](#job-status-hmi-version) - Reads out the flashed Buildname
- [STATUS_KOMP_ID](#job-status-komp-id) - Liefert die HDD Download Kompatibilitätskennung gemäß der HW-Variante
- [START_HDDOWNLOAD_MODE](#job-start-hddownload-mode) - Start des HDDownload KWP2000: $108A StartHDDownloadMode Modus  : Default
- [WRITE_DATA_SERVER_ADDRESS](#job-write-data-server-address) - Adresse (URL) des Download-Servers KWP2000: $2E $2507 WriteDataserverAddress Modus  : Default
- [READ_HDDOWNLOAD_KENNUNG](#job-read-hddownload-kennung) - Auslesen der kompletten HDDownload-Kennung KWP2000: $22 $2501 ReadHDDownloadkennung Modus  : Default
- [READ_HDDOWNLOAD_TIMING_PARAMETER](#job-read-hddownload-timing-parameter) - Auslesen aller HDDownload-Timing-Parameter KWP2000: $22 $250A ReadHDDownloadTimingParameter Modus  : Default
- [READ_HDDOWNLOAD_STATUS](#job-read-hddownload-status) - Auslesen des aktuellen HDDownload-Status KWP2000: $22 $250B ReadHDDownloadObjectStatus Modus  : Default
- [READ_HDDOWNLOAD_TIME_TO_COMPLETION](#job-read-hddownload-time-to-completion) - Verbleibende HDDownload-Zeit KWP2000: $22 $250C ReadHDDownloadTimeToCompletion Modus  : Default
- [START_HDDOWNLOAD_ROUTINE](#job-start-hddownload-routine) - Starte Download einer SWE KWP2000: $3110 StartHDDownloadRoutine Modus  : Default
- [START_HDDOWNLOAD_ROUTINE_A](#job-start-hddownload-routine-a) - Starte Download einer SWE KWP2000: $3110 StartHDDownloadRoutine Modus  : Default
- [STOP_HDDOWNLOAD_ROUTINE](#job-stop-hddownload-routine) - Starte Download einer SWE KWP2000: $3210 StopHDDownloadRoutine KWP2000: $3E TesterPresent Modus  : Default
- [TEST_DATA_ARGUMENT](#job-test-data-argument)
- [TEST_XDUMP_ARGUMENT](#job-test-xdump-argument)
- [NG_AUTHENTISIERUNG_START](#job-ng-authentisierung-start) - Authentisierung pruefen KWP2000: $31 StartRoutineByLocalIdentifier $08 ReleaseAuthentication Modus  : Default
- [FLASH_PARAMETER_LESEN](#job-flash-parameter-lesen) - Gibt die SG-spezifischen Flash-Parameter zurück
- [FLASH_PARAMETER_SETZEN](#job-flash-parameter-setzen) - Setzt die SG-spezifischen Flash-Parameter
- [INTERFACETYPE](#job-interfacetype) - Interface-Typ bestimmen und ausgeben Es wird der Name des Interfaces übergeben Wichtig für Baudratenumschaltung weil bei ADS, EADS und OBD sind nur 115200 Baud möglich, bei EDIC nur 125000 Baud möglich
- [NG_FLASH_LOESCHEN](#job-ng-flash-loeschen) - Flash loeschen Standard Flashjob KWP2000: $31 StartRoutineByLocalIdentifier $02 ClearMemory Modus  : Default
- [NG_SIGNATUR_PRUEFEN](#job-ng-signatur-pruefen) - Flash Signatur pruefen KWP2000: $31 StartRoutineByLocalIdentifier $09 CheckSignature Modus  : Default
- [GETTICKCOUNT](#job-gettickcount) - systeminterner Zählerwert in Milli-Sekunden zurückgeben
- [STEUERN_KARTENUPDATE_USB](#job-steuern-kartenupdate-usb) - Update der Kartendaten für die Navigation über USB
- [STATUS_KARTENUPDATE_USB](#job-status-kartenupdate-usb) - Update der Kartendaten für die Navigation über USB
- [STEUERN_MNAND_REPAIR](#job-steuern-mnand-repair) - Formatsequenz für korruptes MNAND
- [STEUERN_NAVIMETADB_PATCH](#job-steuern-navimetadb-patch) - Repairs the navigation metadata database
- [STATUS_ATC_VERSION](#job-status-atc-version) - Reads out the capability of the ATC diagnosis
- [STEUERN_TUNER_FIX](#job-steuern-tuner-fix) - Repairs the tuner coding problem ECE Target-&gt;SouthAmerica
- [STEUERN_MMEDB_ERASE](#job-steuern-mmedb-erase) - Repairs the navigation metadata database
- [STATUS_HMI_LICENSE_FILE](#job-status-hmi-license-file) - Repairs the navigation metadata database
- [STEUERN_HMI_LICENSE_FILE](#job-steuern-hmi-license-file) - Repairs the gpl license file
- [STATUS_TDA_AKTIVIERUNG](#job-status-tda-aktivierung) - Reads out the actual Baureihe of the Gateway table
- [STEUERN_FORMAT_HDD](#job-steuern-format-hdd) - Formats one or all partition(s) of the Hard Disk Drive.
- [STEUERN_ARD_FIX](#job-steuern-ard-fix) - Switch off ARD in dependence of software (only H,I) and modell (only Basis)
- [STEUERN_IPSAFE_FORHDDUPDATE](#job-steuern-ipsafe-forhddupdate) - Saves IP for HDD update against Onlineactivation of MULF TCU
- [STEUERN_IPSAFE_FORHDDUPDATE_CBX1](#job-steuern-ipsafe-forhddupdate-cbx1) - Some special stuff number 1
- [STEUERN_IPSAFE_FORHDDUPDATE_CBX2](#job-steuern-ipsafe-forhddupdate-cbx2) - Some special stuff number 2
- [STEUERN_NO_HMI_WATCHDOG](#job-steuern-no-hmi-watchdog) - Prevents HMI Hang
- [STEUERN_GPS_REPAIR](#job-steuern-gps-repair) - Repariert: 'Keine Provisionierung möglich, wegen falschem GPS Datum'
- [STEUERN_DEL_CERT](#job-steuern-del-cert) - removes cert to trigger download of new one
- [STEUERN_SDARS_ACTIVATION](#job-steuern-sdars-activation) - Schaltet das SDARS Modul ein und aus
- [STATUS_SDARS_ACTIVATION](#job-status-sdars-activation) - Reads out the actual status of sdars modul

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

<a id="job-pruefcode-lesen"></a>
### PRUEFCODE_LESEN

Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PRUEFCODE | binary | Pruefcode Daten |

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

<a id="job-status-softwarename"></a>
### STATUS_SOFTWARENAME

Reads out the flashed Buildname

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NAME | string | The actual flashed Build on the HeadUnit |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-version-gatewaytabelle"></a>
### STATUS_VERSION_GATEWAYTABELLE

Lesen der Versionsnummer der Gateway-Tabelle KWP2000: $21 ReadDataByLocalIdentifier $4D gatewayTableVersionNumber Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VERSION_GATEWAYTABELLE | string | Versionsnummer der Gateway-Tabelle |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-gateway-wakeup-source"></a>
### STATUS_GATEWAY_WAKEUP_SOURCE

Liefert die Quelle/Ursache zurück, die zum Wecken des Gateway-Steuergerätes geführt hat. Dieser Job wird von SG ab E60 unterstützt! KWP2000: $21 ReadDataByLocalIdentifier $BB recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WAKEUP_SOURCE | string | Weckursache table TWakeupSource TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |

<a id="job-status-gateway-most-device-count"></a>
### STATUS_GATEWAY_MOST_DEVICE_COUNT

Information über den Gateway-Dispatcher Anzahl der vom Dispatcher erkannten MOST-Teilnehmer im Ring KWP2000: $21 ReadDataByLocalIdentifier $50 recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOST_DEVICE_COUNT | unsigned char | Anzahl der vom Dispatcher erkannten MOST-Teilnehmer im Ring |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |

<a id="job-status-gateway-most-devices"></a>
### STATUS_GATEWAY_MOST_DEVICES

Ausgabe der erkannten MOST-Devices. Die Erkennung erfolgt ueber die InstID der Diagnose-Funktionsbloecke Komplex, da auf Grund der Größe mitlerweile Read_Devids_Current_Registry und Read_FBlockIDs_Current_Registry ausgewertet werden muss. Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOST_DEVICE | string | Bezeichnung des MOST-Devices table TFBlockIDTexte TEXT |
| STAT_DEVICEID | string | Deviceadresse |
| STAT_FBLOCKID | string | FunktionsblockID |
| STAT_INSTID | string | InstID |
| STAT_FBLOCK_NAME | string | Name des FBlocks |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |

<a id="job-status-gateway-local-registry-elements"></a>
### STATUS_GATEWAY_LOCAL_REGISTRY_ELEMENTS

Information über den Gateway-Dispatcher Liste aller lokal (im Gateway-Adreßraum) registrierten FBlocks KWP2000: $21 ReadDataByLocalIdentifier $51 recordLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ELEMENT_COUNT | unsigned char | Anzahl der registrierten FBlocks bzw. FBlock-Modells (lokale Gateway-Dispatcher-Registry) |
| STAT_NODE_TYPE | string | Typ des registrierten Funktionsblocks bzw. -Modells table TNodeType TEXT |
| STAT_FBLOCK_ID | string | Funktions-Block-ID des registrierten Funktionsblocks bzw. -Modells |
| STAT_INST_ID | string | Instanz-ID des registrierten Funktionsblocks bzw. -Modells |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort vom SG |

<a id="job-status-praeprozessor-switch"></a>
### STATUS_PRAEPROZESSOR_SWITCH

Read out status of pre-processor switch KWP2000: $21 ReadDataByLocalIdentifier $55 recordLocalIdentifier - pre-processor switch state Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PRE_PROS_SWI | string | pre-processor switch state |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-included-gw-tab"></a>
### STATUS_INCLUDED_GW_TAB

Read out status of included GW table KWP2000: $21 ReadDataByLocalIdentifier $56 recordLocalIdentifier - included GW table state Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_INC_GW_TAB | string | status of included GW table |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-devids-current-registry"></a>
### READ_DEVIDS_CURRENT_REGISTRY

Auslesen der DEVIDS der Current Registry KWP2000: $21 ReadDataByLocalIdentifier $49 recordLocalIdentifier Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DEVICEID_CURRENT | string | Deviceadresse |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-devids-default-registry"></a>
### READ_DEVIDS_DEFAULT_REGISTRY

Auslesen der DEVIDS der Default Registry KWP2000: $21 ReadDataByLocalIdentifier $4A recordLocalIdentifier Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DEVICEID_DEFAULT | string | Deviceadresse |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-fblocks-current-registry"></a>
### READ_FBLOCKS_CURRENT_REGISTRY

Auslesen der FBlockIDs einer DEVID der Current Registry KWP2000: $21 ReadDataByLocalIdentifier $4B recordLocalIdentifier Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_DEVNODE | string | Logische MOST-Deviceadresse 4-stellig Beispiel: 0101 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FBLOCKID_CURRENT | string | FBlockID |
| INSTID_CURRENT | string | InstID |
| FBLOCK_NAME_CURRENT | string | Name des FBlocks |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-fblocks-default-registry"></a>
### READ_FBLOCKS_DEFAULT_REGISTRY

Auslesen der FBlockIDs einer DEVID der Default Registry KWP2000: $21 ReadDataByLocalIdentifier $4C recordLocalIdentifier Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_DEVNODE | string | Logische MOST-Deviceadresse 4-stellig Beispiel: 0101 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FBLOCKID_DEFAULT | string | FBlockID |
| INSTID_DEFAULT | string | InstID |
| FBLOCK_NAME_DEFAULT | string | Name des FBlocks |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-diagtunnelling-kwp"></a>
### DIAGTUNNELLING_KWP

complete tunneling of KWP telegrams

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_KWP | string | Haupt KWP stream ab Anfang bsp.:8263F11A80 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-configuration-table"></a>
### LESEN_CONFIGURATION_TABLE

Reads out the currently active configuration table.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_DESIRED_CONFIGTABLE_INDEX | unsigned char | desired configtable 0x00 currently active table, 0x01 first config table, ... |
| ARG_DESIRED_PARAMETER | string | name of desired parameter. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CONFIG_TABLE | string | Returned value. |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-dar"></a>
### LESEN_DAR

Lesen eines DAR Datensatzes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_DAR | unsigned char | Requested DAR Index from 0-9 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RET_STATUS | unsigned char | Status 0x00 OK, &gt;0 Error |
| RET_DAR | string | DAR Datensatz |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-navdvdpin"></a>
### LESEN_NAVDVDPIN

Reads the four digits PIN codes to unlock the NAVI DVD.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NAVDVDPIN | string | 4 digits PIN code to unlock NAVI DVD |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-telefonnummern"></a>
### LESEN_TELEFONNUMMERN

Auslesen der in HeadUnit gespeicherten Telefonnummern für - Bereitschaftsdienst - Heimathändler - Passo - Hotline

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| NR_BEREITSCHAFTSDIENST | string | Nummer des Bereitschaftsdienstes |
| NR_HEIMATHAENDLER | string | Nummer des Heimathändlers |
| NR_PASSO | string | Nummer Passo |
| NR_HOTLINE | string | Nummer der Hotline |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-telefonnummer-sdars"></a>
### LESEN_TELEFONNUMMER_SDARS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NR_SDARS | string | Nummer des Bereitschaftsdienstes |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-current-registry"></a>
### READ_CURRENT_REGISTRY

Liefert den Inhalt der Current Registry

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_DEVICEID | string | Deviceadresse |
| STAT_FBLOCKID | string | FunktionsblockID |
| STAT_INSTID | string | InstID |
| STAT_FBLOCK_NAME | string | Name des FBlocks |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-default-registry"></a>
### READ_DEFAULT_REGISTRY

Liefert den Inhalt der default Registry

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_DEVICEID | string | Deviceadresse |
| STAT_FBLOCKID | string | FunktionsblockID |
| STAT_INSTID | string | InstID |
| STAT_FBLOCK_NAME | string | Name des FBlocks |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-06-default-registry"></a>
### READ_06_DEFAULT_REGISTRY

Liefert den Inhalt der default Registry

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_DEVICEID | string | Deviceadresse |
| STAT_FBLOCKID | string | FunktionsblockID |
| STAT_INSTID | string | InstID |
| STAT_FBLOCK_NAME | string | Name des FBlocks |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-diff-registry"></a>
### READ_DIFF_REGISTRY

Liefert den Unterschied zwischen Current und default Registry

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_DIFF_TYPE | string | Current oder Default-FBloecke |
| STAT_DIFF_NUM | int | Number of differences (0:no diff, -X: x Fblocks too less, Y: y Fblocks to much) |
| STAT_FBLOCKID_DIFF | string | FunktionsblockID |
| STAT_INSTID_DIFF | string | InstID |
| STAT_FBLOCK_NAME_DIFF | string | name des FBlocks |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-schreiben-configuration-table"></a>
### SCHREIBEN_CONFIGURATION_TABLE

Writes a configuration table selected by a special index n from (0...n) onto the currently active configuration table in the head-unit.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_DESIRED_CONFIGTABLE_INDEX | unsigned char | desired configtable 0x00 currently active table, 0x01 first config table, ... |
| ARG_DESIRED_PARAMETER | string | name of desired parameter. |
| ARG_DESIRED_VALUE | string | name of desired value. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-schreiben-dar"></a>
### SCHREIBEN_DAR

Schreiben eines DAR Datensatzes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_DAR | unsigned char | Requested DAR Index from 0-9 |
| ARG_FILE | string | DAR read from file to be written complete path is necessary |
| ARG_STREAM | string | DAR read from STREAM to be written file content as a string |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RET_STATUS | unsigned char | Status 0x00 OK, &gt;0 Error |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-schreiben-bmw-zertifikat"></a>
### SCHREIBEN_BMW_ZERTIFIKAT

Schreiben eines BMW Zertifikates

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_FILE | string | BMW Zertifikat read from file to be written complete path is necessary |
| ARG_STREAM | string | BMW Zertifikat from STREAM to be written file content as a string |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RET_STATUS | unsigned char | Status 0x00 OK, &gt;0 Error |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-schreiben-browser-zertifikat"></a>
### SCHREIBEN_BROWSER_ZERTIFIKAT

Schreiben eines BROWSER Zertifikates

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_FILE | string | BROWSER Zertifikat read from file to be written complete path is necessary |
| ARG_STREAM | string | BROWSER Zertifikat from STREAM to be written file content as a string |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RET_STATUS | unsigned char | Status 0x00 OK, &gt;0 Error |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-schreiben-navdvdpin"></a>
### SCHREIBEN_NAVDVDPIN

Writes the four digits PIN code to unlock the NAVI DVD.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_NAVDVDPIN | string | 4 digits PIN code to unlock the NAVI DVD |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-schreiben-telefonnummer-sdars"></a>
### SCHREIBEN_TELEFONNUMMER_SDARS

Nummer des Bereitschaftsdienstes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_NR_SDARS | string | Nummer des Bereitschaftsdienstes Stringlänge max. 35 Zeichen (ohne Endezeichen \0) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-schreiben-telefonnummern"></a>
### SCHREIBEN_TELEFONNUMMERN

Schreiben der Telefonnummern für - Bereitschaftsdienst - Heimathändler - Passo - Hotline

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_NR_BEREITSCHAFTSDIENST | string | Nummer des Bereitschaftsdienstes |
| ARG_NR_HEIMATHAENDLER | string | Nummer des Heimathändlers |
| ARG_NR_PASSO | string | Nummer Passo |
| ARG_NR_HOTLINE | string | Nummer der Hotline |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ser-nr-dom-lesen"></a>
### SER_NR_DOM_LESEN

Reads the serial number with 14 digits (DIN ISO 10486)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SER_NR_DOM | string | On assembly line for entering into the BMW-DOM database. |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ability-to-wake"></a>
### STATUS_ABILITY_TO_WAKE

Gibt an ob SG Most Ring wecken darf

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ABILITY_TO_WAKE | int | 0 = off, 1 = on,  2= critical ("critical" ist in Most Specs definiert wird aber praktisch nicht benutzt) |
| STAT_ABILITY_TO_WAKE_TEXT | string | 0 = off, 1 = on,  2= critical ("critical" ist in Most Specs definiert wird aber praktisch nicht benutzt) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-adas"></a>
### STATUS_ADAS

Reads out from the navigation system how many Resyncs from which client the navigation system has received and how many messages the navigation system has sent since the beginning of the current lifecycle.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LIFECYCLE_DURATION_WERT | unsigned int | Duration of the current lifecycle in minutes |
| STAT_RECEIVED_RESYNCS_ACC_WERT | unsigned char | Number of resyncs that have been received from the ACC ECU |
| STAT_RECEIVED_RESYNCS_NIVI_WERT | unsigned char | Number of resyncs that have been received from the Night Vision ECU |
| STAT_RECEIVED_RESYNCS_SLI_WERT | unsigned char | Number of resyncs that have been received from the SLI ECU |
| STAT_RECEIVED_RESYNCS_XAGS_WERT | unsigned char | Number of resyncs that have been received from the X-AGS ECU |
| STAT_SENT_NAVGRAPH_WERT | unsigned char | Number of NavGraph messages that have been sent |
| STAT_SENT_NAVGRAPHSYNC_WERT | unsigned char | Number of NavGraphSync messages that have been sent |
| STAT_SENT_NAVGPS1_WERT | unsigned char | Number of NavGPS1 messages that have been sent |
| STAT_SENT_NAVGPS2_WERT | unsigned char | Number of NavGPS2 messages that have been sent |
| STAT_SENT_NAVSYSINFO_WERT | unsigned char | Number of NavSysInfo messages that have been sent |
| STAT_SENT_NAVGRAPHMATCH_WERT | unsigned char | Number of NavGraphMatch messages that have been sent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-aktive-gal-kurve"></a>
### STATUS_AKTIVE_GAL_KURVE

Reads the number of the active speed dependent volume control curve.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GAL_KURVE | unsigned char | Active SDVC curve as integer |
| STAT_GAL_KURVE_TEXT | string | Active SDVC curve table TGalKurve |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog-temperatur"></a>
### STATUS_ANALOG_TEMPERATUR

The temperature values on the FOT, in the module and at the amplifier and all other reasonable locations (e.g. drive) in degrees Celsius.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEMP_FOT_WERT | char | Numerical value of the FOT temperature |
| STAT_TEMP_FOT_EINH | string | Unit of the FOT temperature (degree Celsius) |
| STAT_TEMP_ENDSTU_WERT | int | Numerical value of the power amplifier temperature |
| STAT_TEMP_ENDSTU_EINH | string | Unit of the power amplifier temperature (degree Celsius) |
| STAT_TEMP_GYRO_WERT | char | Numerical value of the gyro temperature |
| STAT_TEMP_GYRO_EINH | string | Unit of the gyro temperature (degree Celsius) |
| STAT_TEMP_MOD_WERT | char | Numerical value of the module (processor) temperature |
| STAT_TEMP_MOD_EINH | string | Unit of the module temperature (degree Celsius) |
| STAT_TEMP_HDD_WERT | char | Numerical value of the HDD temperature |
| STAT_TEMP_HDD_EINH | string | Unit of the HDD temperature (degree Celsius) |
| STAT_TEMP_DVD_WERT | char | Numerical value of the DVD temperature |
| STAT_TEMP_DVD_EINH | string | Unit of the DVD temperature (degree Celsius) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ant-dc"></a>
### STATUS_ANT_DC

Checks the connection between head unit and diversity by performing an impedance measurement

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANT_DC | unsigned char | Result of measurement values from table TTunerRi |
| STAT_ANT_DC_TEXT | string | Result of measurement as text values from table TTunerRi |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ant-eigen-diag"></a>
### STATUS_ANT_EIGEN_DIAG

Result of the antenna diversity self-diagnosis.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANT_EIGEN_DIAG | unsigned char | Result of the antenna diversity self-diagnosis value from Table TAntennaDiag |
| STAT_ANT_EIGEN_DIAG_TEXT | string | Result of the antenna diversity self-diagnosis value from Table TAntennaDiag |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ant-qfs"></a>
### STATUS_ANT_QFS

Reads the current quality and the field strength of the actual radio signal of the actual frequency.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_QUALITY_WERT | unsigned char | Range: 0..15 (the defining value for AF tracking, corresponding to the sum of the weighted individual factors, 15 = best quality) 2-Tuner |
| STAT_FIELDSTRENGTH_WERT | unsigned char | Range: 0…15 (4dB steps from 0 - 60 dBµV) |
| STAT_ANT_PW | unsigned char | Status of the Rad On lead as integer |
| STAT_FIELDSTRENGTH_EXACT_WERT | unsigned char | Range: 0 - 250 (1dB steps from 0 - 250 dB müV) Return value 255 if no reasonable measurement possible. |
| STAT_FREQUENZ_WERT | unsigned long | Current frequency in kHz |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-application"></a>
### STATUS_APPLICATION

Reads out applications stati if they are coded and their availability

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_APPL_1 | unsigned char | ID of application |
| STAT_APPL_1_TEXT | string | Name of application from table TApplication |
| STAT_APPL_ENABLED_1 | unsigned char | Status if application x is running or not values from table TApplicationRunningStatus |
| STAT_APPL_ENABLED_1_TEXT | string | Status if application x is running or not text values from table TApplicationRunningStatus |
| STAT_APPL_CODED_1 | unsigned char | Status if application x is activated via coding or SWT or not values from table TApplicationActivationStatus |
| STAT_APPL_CODED_1_TEXT | string | Status if application x is activated via coding or SWT or not text values from table TApplicationActivationStatus |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-audiokanaele"></a>
### STATUS_AUDIOKANAELE

Returns the status of the Audiokanaele

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KANAL | string | Returned Audiokanaele, bitcombination of following values from table TAudioKanal WERT |
| STAT_KANAL_TEXT | string | Returned Audiokanaele, bitcombination of following values from table TAudioKanal WERT only well known bitcombinations shown |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-average-message-reception-rate"></a>
### STATUS_AVERAGE_MESSAGE_RECEPTION_RATE

Liest die mittlere Nachrichtenabnahmerate des SGs während dieses Gerät geflasht wird, also in der ProgramminSession Auslesbar muss der Status jederzeit sein

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MSG_CMS_SYNC_WERT | unsigned int | Mittl. Nachrichtenabnahmerate des Kontrollkanals [0-1000] |
| STAT_MSG_CMS_ASYNC_WERT | unsigned int | Mittl. Nachrichtenabnahmerate des async. Kanals. Sollte dieses Gerät nicht Async geflasht werden muss dieser Parameter auf 0 gesetzt sein [0-10000] |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bit-error-rate-iboc"></a>
### STATUS_BIT_ERROR_RATE_IBOC

Measures the quality of the reception of the current IBOC station.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BIT_ERROR_RATE_IBOC_WERT | real | Reception quality of the current IBOC station expressed in bit error rate |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-browser-applikation"></a>
### STATUS_BROWSER_APPLIKATION

Tests with a simple request onto the browser application (task) if it is coded, if it is active and responds. Test if a user input is actually necessary because of an Online-PopUp.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BROWSER_ACTIVE | unsigned char | Activation state of the browser application as integer |
| STAT_BROWSER_ACTIVE_TEXT | string | Activation state of the browser application as table TBrowserActivationState |
| STAT_USER_INPUT_NECESSARY | unsigned char | Status if user input is currently necessary as integer |
| STAT_USER_INPUT_NECESSARY_TEXT | string | Status if user input is currently necessary as table TInputNecessary |
| STAT_ONLINE_CODED | unsigned char | Coding status of the online functionality as integer |
| STAT_ONLINE_CODED_TEXT | string | Coding status of the online functionality as table TOnlineCoded |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-cd-md-cdc"></a>
### STATUS_CD_MD_CDC

Reads out the disc identifier and the quality level of the digital playback

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIGITAL_PLAYBACK_QUALITY_WERT | unsigned char | Quality level of the digital playback Range: 0-15 0-1: Media not readable (drive not ok) 2-8: Mutes or distortion which is customer related (drive not ok) 9-14: Media readable, no customer related distortion (drive ok) 15: Media quality 100%, e.g. BLER 0 (drive ok) |
| STAT_DISC_IDENT | string | Disc Identifier of the inserted medium |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dar-index"></a>
### STATUS_DAR_INDEX

Indicates the DAR which is selected.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODED_DAR | unsigned char | Coded DAR Index from 0-9 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-demute"></a>
### STATUS_DEMUTE

Returns the mute status of the current entertainment source.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DEMUTE_SOURCE1 | unsigned char | Mute status of the head-unit or of the left RSE headphones |
| STAT_DEMUTE_SOURCE1_TEXT | string | Mute status of the head-unit or of the left RSE headphones as text from table TSourceDemuteStatus |
| STAT_DEMUTE_SOURCE2 | unsigned char | Mute status of the right RSE headphones |
| STAT_DEMUTE_SOURCE2_TEXT | string | Mute status of the right RSE headphones as text from table TSourceDemuteStatus |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-direction"></a>
### STATUS_DIRECTION

Reads out which direction/type of gear (forwards, backwards, idle) is currently active and where the signal is coming from (source of the signal)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIRECTION | unsigned char | Direction that is currently active as integer |
| STAT_DIRECTION_TEXT | string | Direction that is currently active value from table TGearType |
| STAT_DIRECTION_SOURCE | unsigned char | Source of the direction signal as integer |
| STAT_DIRECTION_SOURCE_TEXT | string | Source of the direction signal value from TDirectionSource |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-drehknopf"></a>
### STATUS_DREHKNOPF

gibt die Position des Drehknopfes bezüglich des letzen Aufstartens wieder

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DREHPOSITION_WERT | unsigned char | Aktuelle relative Position des Drehknopfes |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-drive-cd"></a>
### STATUS_DRIVE_CD

Status of DVD Drive

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MEDIUM_INSERTED | unsigned char | Information, if a medium is inserted in the drive, and which medium type is recognized 0x00 No medium inserted 0x01 Medium recognition in progress 0x02 CD medium inserted 0x03 DVD medium inserted 0x04 Flashspeicher Medium ist eingelegt (n/a for dvd) |
| STAT_MEDIUM_INSERTED_TEXT | string | Information, if a medium is inserted in the drive, and which medium type is recognized |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-drive-dvd"></a>
### STATUS_DRIVE_DVD

Status of DVD Drive

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MEDIUM_INSERTED | unsigned char | Information, if a medium is inserted in the drive, and which medium type is recognized 0x00 No medium inserted 0x01 Medium recognition in progress 0x02 CD medium inserted 0x03 DVD medium inserted 0x04 Flashspeicher Medium ist eingelegt (n/a for dvd) |
| STAT_MEDIUM_INSERTED_TEXT | string | Information, if a medium is inserted in the drive, and which medium type is recognized |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ext-gyrosignal"></a>
### STATUS_EXT_GYROSIGNAL

Checks if the signal(s) coming from the external gyro is available on the bus.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EXT_GYRO_SIGNAL | unsigned char | Availability of the external gyro signal as integer |
| STAT_EXT_GYRO_SIGNAL_TEXT | string | Availability of the external gyro signal as table TExtGyroSignal |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fault-tracking"></a>
### STATUS_FAULT_TRACKING

Reads out one or all datasets stored by the extended fault tracking mechanism.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_COREFILE_NUMBER | unsigned char | Number of Corefile to be read from 0 to 10 if not exists then neg. response out of range is returned |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SIGNAL | unsigned int | 0x0000 : Kein Fehler (dann alles nachfolgende 0) 0x0001 : SIGABRT 0x0002 : SIGBUS 0x0004 : SIGEMT 0x0008 : SIGFPE 0x0010 : SIGILL 0x0020 : SIGQUIT 0x0040 : SIGSEGV 0x0080 : SIGSYS 0x0100 : SIGTRAP 0x0200 : SIGXCPU 0x0400 : SIGXFSZ |
| STAT_THREADNUMBER | unsigned int | Threadnummer |
| STAT_CODE | unsigned int | Code |
| STAT_INSTRUCTIONPOINTER | string | InstructionPointer |
| STAT_STACKPOINTER | string | StackPointer |
| STAT_STACKBASE | string | StackBase |
| STAT_STACKSIZE | string | StackSize |
| STAT_COREFILE | string | name of CoreFile |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fb-taste"></a>
### STATUS_FB_TASTE

Test der Functional Bookmarks

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FB_TASTE_NO | unsigned char | gibt die Nummer der ersten berührten oder gedrückten Taste wieder |
| STAT_FB_TASTE | unsigned char | gibt den Status der zurückgelieferten Taste wieder |
| STAT_FB_TASTE_TEXT | string | gibt den Status der zurückgelieferten Taste wieder as text from table TFbTasteStatus |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fband-scan"></a>
### STATUS_FBAND_SCAN

Start FBand scan

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS | unsigned char | Aktueller Jobstatus values from table TFbandScanStatus |
| STAT_STATUS_TEXT | string | Aktueller Jobstatus values from table TFbandScanStatus |
| STAT_BAND | string | Waveband from table TWaveband (only if STAT_STATUS == 0) |
| STAT_WAIT | unsigned char | Startverzögerung in sekunden (only if STAT_STATUS == 0) |
| STAT_FREQ_START | unsigned long | Startfrequenz (kHz) (only if STAT_STATUS == 0) |
| STAT_FREQ_STOP | unsigned long | letzte zu prüfende Frequenz (kHz) (only if STAT_STATUS == 0) |
| STAT_FREQ_STEP | unsigned long | Frequenzschrittweite (kHz) (only if STAT_STATUS == 0) |
| STAT_BANDWIDTH | unsigned long | Bandbreite (only if STAT_STATUS == 0) |
| STAT_ANZ_MESSUNGEN | unsigned int | Anzahl der Messungen insgesamt. (nur bei Status 0x00) |
| STAT_ANZ_MESSUNGEN_AKTUELL | unsigned int | Anzahl der bereits durchgeführten Messungen. (nur bei Status 0x00,0x01,0x02) |
| STAT_MESSWERTE | string | Messwerte in Form: "wert1 wert2 wert3". (nur bei Status 0x01,0x02) |
| STAT_FEHLER | string | Fehlerursachen (nur bei Status 0xFF) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-find-best-station"></a>
### STATUS_FIND_BEST_STATION

Returns the status of the searching process and the information data of the best station if the searching process has been ended successfully.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SEARCHING_PROCESS_STATUS | unsigned long | Searching process also see table TSearchingProcess WERT |
| STAT_SEARCHING_PROCESS_STATUS_TEXT | string | Searching process also see table TSearchingProcess TEXT |
| STAT_NAME | string | PS name of the best station |
| STAT_PI | string | Programm Identification of the best station |
| STAT_FIELDSTRENGTH | unsigned char | Fieldstrength of the best station Range 0..60 |
| STAT_QUALITY | unsigned char | Quality of the best station Range 0...255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-find-best-station-dab"></a>
### STATUS_FIND_BEST_STATION_DAB

Returns the status of the searching process and the information data about the best DAB ensemble if the searching process has been ended successfully.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SEARCHING_PROCESS_STATUS_DAB | unsigned char | Status of the searching process values from table TSearchingProcess |
| STAT_SEARCHING_PROCESS_STATUS_DAB_TEXT | string | Status of the searching process values from table TSearchingProcess |
| STAT_ENSEMBLE_NAME | string | Label of active ensemble |
| STAT_ENSEMBLE_ID | string | Ensemble Identification |
| STAT_ENSEMBLE_BER_WERT | real | Bit Error Rate of active ensemble |
| STAT_SERVICE_NAME | string | Name of active service (first service of ensemble) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-find-best-tmc-station"></a>
### STATUS_FIND_BEST_TMC_STATION

Returns the status of the searching process and the information data of the best TMC station if the searching process has been ended successfully.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SEARCHING_PROCESS_STATUS | unsigned char | Status of the searching process values from table TSearchingProcess |
| STAT_SEARCHING_PROCESS_STATUS_TEXT | string | Status of the searching process values from table TSearchingProcess |
| STAT_NAME | string | PS name of the best station |
| STAT_PI_WERT | unsigned int | Program Identification of the best station |
| STAT_FIELDSTRENGTH_WERT | unsigned char | Fieldstrength of the best station Range: 0…255 |
| STAT_QUALITY_WERT | unsigned char | Quality of the best station Range: 0…255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-find-best-tmc-station-dab"></a>
### STATUS_FIND_BEST_TMC_STATION_DAB

Returns the status of the searching process and the information data of the best DAB TMC station if the searching process has been ended successfully.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SEARCHING_PROCESS_STATUS_DAB | unsigned char | Status of the searching process values from table TSearchingProcess |
| STAT_SEARCHING_PROCESS_STATUS_DAB_TEXT | string | Status of the searching process values from table TSearchingProcess |
| STAT_ENSEMBLE_NAME | string | Label of active ensemble |
| STAT_ENSEMBLE_ID | string | Ensemble Identification |
| STAT_ENSEMBLE_BER_WERT | unsigned long | Bit Error Rate of active ensemble |
| STAT_SERVICE_NAME | string | Name of active service (first service of ensemble) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-flottenmodus"></a>
### STATUS_FLOTTENMODUS

Reads out the Flottenmodus (mode of the NAVI DVD locking) that is currently active.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MODUS | unsigned char | Flottenmodus that is currently active as integer |
| STAT_MODUS_TEXT | string | Flottenmodus that is currently active as table TFlottenmodus |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fot-temperatur"></a>
### STATUS_FOT_TEMPERATUR

Gibt an ob SG Most Ring wecken darf

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FOT_TEMP_CELSIUS | char | Temperatur am FOT des SG in Celsius -128 C bis +127 C hierbei -128 C bedeutet ungültig (0xFF) |
| STAT_FOT_TEMP_FAHRENHEIT | real | Temperatur am FOT des SG in Fahrenheit -196.6 F bis +260.6 F hierbei bedeutet -198.4 F ungültig ( -128 C) This result is calculated inside the SGBD-Job Fahrenheit = (( Celsius × 9 ) / 5 ) + 32 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-frequenz"></a>
### STATUS_FREQUENZ

Get back the currently active tuner frequency

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FREQUENZ_WERT | unsigned long | Current tuner frequency in kHz |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-gps"></a>
### STATUS_GPS

Returns the status of the GPS reception.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GPS | unsigned char | GPS status as integer |
| STAT_GPS_TEXT | string | GPS status as table TGpsStatus |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-gps-dilution-of-position"></a>
### STATUS_GPS_DILUTION_OF_POSITION

Reads out the GPS dilution of position.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GPS_PDOP_WERT | unsigned char | GPS (Position) Dilution Of Position |
| STAT_GPS_HDOP_WERT | unsigned char | GPS Horizontal Dilution Of Position |
| STAT_GPS_VDOP_WERT | unsigned char | GPS Vertical Dilution Of Position |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-gps-position"></a>
### STATUS_GPS_POSITION

Returns the current GPS position.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GPS_POSITION_VALIDITY | unsigned char | Validity of the GPS position as integer |
| STAT_GPS_POSITION_VALIDITY_TEXT | string | Validity of the GPS position as table TGpsPositionValidity |
| STAT_GPS_POSITION_LATITUDE | string | Latitude |
| STAT_GPS_POSITION_LONGITUDE | string | Longitude |
| STAT_GPS_POSITION_HEIGHT | int | Height |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-gps-receiver-sw-version"></a>
### STATUS_GPS_RECEIVER_SW_VERSION

Reads out the software version of the GPS receiver.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GPS_RECEIVER_SW_VERSION | string | Software version of the GPS receiver |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-gps-satinfo"></a>
### STATUS_GPS_SATINFO

Reads out the number of visible and the number of tracked satellites and returns information about each visible satellite.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NUMBER_VISIBLE_SATS_WERT | unsigned char | Number of satellites that are theoretical visible |
| STAT_NUMBER_TRACKED_SATS_WERT | unsigned char | Number of tracked satellites |
| STAT_SAT_ID_WERT | unsigned char | ID of the satellite |
| STAT_SAT_STATUS | unsigned char | Status of the satellite as integer |
| STAT_SAT_STATUS_TEXT | string | Status of the satellite value from table TSatelliteStatus |
| STAT_SAT_SIGNAL_TO_NOISE | int | Quality of the satellite reception expressed in signal to noise ratio |
| STAT_SAT_AZIMUTH | string | Azimuth of the satellite |
| STAT_SAT_ELEVATION | string | Elevation of the satellite |
| STAT_SAT_EPHEMERIS | string | Ephemeris of the satellite |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-gps-time"></a>
### STATUS_GPS_TIME

Reads out the GPS date and time.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GPS_TIME_VALIDITY | unsigned char | Validity of the GPS time as integer |
| STAT_GPS_TIME_VALIDITY_TEXT | string | Validity of the GPS time as table TGpsTimeValidity |
| STAT_GPS_TIME_DATE | string | GPS date and time |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-highsyncconnection-detail"></a>
### STATUS_HIGHSYNCCONNECTION_DETAIL

Genaue Information zur abgefragten Connection ausgeben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_CONNECTION | int | 2 Byte HILO Hex Value of the desired connection |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CONNTABLE_DETAIL | string | Format: status, FBlock source.Inst source, source number --&gt;FBlock sink.Inst sink, sink number |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-highsyncconnection-table"></a>
### STATUS_HIGHSYNCCONNECTION_TABLE

HighSyncConnectionTable

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HIGHSYNC_CONNECTION_IDS | string | ConnectionIDs aktiver Audioverbindungen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-horizontal-heading"></a>
### STATUS_HORIZONTAL_HEADING

Reads out all data related to the horizontal heading of the car (gyro type, horizontal delta heading and drift) and performs a comparison with the GPS horizontal heading changes.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HORIZONTAL_DELTA_HEADING_WERT | unsigned int | Horizontal heading changes measured by the gyro |
| STAT_GYRO_TYPE | unsigned char | Type of gyro that is present in the car as integer |
| STAT_GYRO_TYPE_TEXT | string | Type of gyro that is present in the car value from table TGyroType |
| STAT_GYRO_DRIFT_WERT | unsigned int | Drift of the gyro in mV |
| STAT_GPS_CORRELATION | unsigned char | Correlation of the horizontal heading changes measured by the gyro with the horizontal heading changes measured via GPS as integer |
| STAT_GPS_CORRELATION_TEXT | string | Correlation of the horizontal heading changes measured by the gyro with the hotizontal heading changes measured via GPS as table TGpsCorrelationHeading |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hw-variante"></a>
### STATUS_HW_VARIANTE

Liefert die HW-Variante der Headunit

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HW_VARIANTE | unsigned long | Hardwarevariante values from table THwVar_Device and table THwVar_Function |
| STAT_HW_VARIANTE_HEX | string | Bitcombination representing the Hardwarevariante |
| STAT_HW_VARIANTE_TEXT | string | Hardwarevariante values from table THwVar_Device and table THwVar_Function |
| STAT_HW_VARIANTE_LIEFERANT | unsigned int | Lieferant as number values from table THwLieferant |
| STAT_HW_VARIANTE_LIEFERANT_TEXT | string | Lieferant as text values from table THwLieferant |
| STAT_HW_EINHEIT | unsigned long | liefert eine eindeutige ID der Hardwarevariante |
| STAT_HW_EINHEIT_TEXT | string | liefert eine eindeutige ID der Hardwarevariante als Text aus table THwEinheit |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-internal-acceleration-sensor"></a>
### STATUS_INTERNAL_ACCELERATION_SENSOR

Returns if the internal acceleration sensor is working on the basis of the voltage value.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_INTERNAL_ACCELERATION_SENSOR_STATUS | unsigned char | Status of the internal acceleration sensor as integer |
| STAT_INTERNAL_ACCELERATION_SENSOR_STATUS_TEXT | string | Status of the internal acceleration sensor as table TInternalAccelerationSensorStatus |
| STAT_ACCELERATION_SENSOR_VOLTAGE_WERT | unsigned int | Acceleration sensor voltage expressed in mV |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-internal-gyro"></a>
### STATUS_INTERNAL_GYRO

Returns if the internal gyro is working on the basis of the voltage value.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_INTERNAL_GYRO_STATUS | unsigned char | Status of the internal gyro as integer |
| STAT_INTERNAL_GYRO_STATUS_TEXT | string | Status of the internal gyro as table TInternalGyroStatus |
| STAT_GYRO_VOLTAGE_WERT | unsigned int | Gyro voltage expressed in mV |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-last-connection"></a>
### STATUS_LAST_CONNECTION

Returns various statuses of the currently active session or if no session is active, of the last session.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ONLINE | int | Online / Offline Status |
| STAT_ONLINE_TEXT | string | Online / Offline Status as text with values from table TOnlineStateTable |
| STAT_CONNECTION_ATTEMPS | int | Number of connection retries of current (if active) or last session |
| STAT_START_TIME_DATE | string | Start of current (if active) or last session |
| STAT_END_TIME_DATE | string | End of current (if active) or last session |
| STAT_BYTES_RECEIVED | long | Bytes received within last or current session (download) |
| STAT_BYTES_SENT | long | Bytes sent within last or current session (upload) |
| STAT_PHONE_NO | string | Telephone number of the RAS server or AP number if GPRS |
| STAT_MODE | int | Digital, analogues or other dial-in |
| STAT_SIM_MNC | string | MNC (mobile network code) of SIM |
| STAT_SIM_MCC | string | MCC (mobile country code) of SIM |
| STAT_NET_MNC | string | MNC of net |
| STAT_NET_MCC | string | MCC of net |
| STAT_IP_NO | string | IP-number of the last or current connection |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lautsprecher-impedanzmessung"></a>
### STATUS_LAUTSPRECHER_IMPEDANZMESSUNG

Returns the result of the test performed with steuern_lautsprecher_impedanzmessung.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FREQUENZ_WERT | unsigned int | Frequency at which the impedance measurement has been performed |
| STAT_LEVEL_WERT | unsigned char | Level of the signal used for the impedance measurement |
| STAT_KANAL | long | Channel(s) on which the impedance measurement has been performed |
| STAT_MESSDAUER_WERT | unsigned int | Duration of the impedance measurement that has been performed |
| STAT_LAUTSPRECHER_IMPEDANZMESSUNG | unsigned char | Status of the test as integer |
| STAT_LAUTSPRECHER_IMPEDANZMESSUNG_TEXT | string | Status of the test as table TTestStatus |
| STAT_ANZAHL_FEHLERHAFTE_KANAELE_WERT | unsigned char | Number of the faulty channels (or loudspeakers if the frequency parameter is used) |
| STAT_FEHLER_1_KANAL | long | Xth faulty channel as table TAudioKanal WERT |
| STAT_FEHLER_1_KANAL_TEXT | string | Xth faulty channel as table TAudioKanal TEXT |
| STAT_FEHLER_1_FEHLERART_KANAL | unsigned char | Type of error of the Xth faulty channel as integer |
| STAT_FEHLER_1_FEHLERART_KANAL_TEXT | string | Type of error of the Xth faulty channel as table TKanalFehlerArt |
| STAT_FEHLER_1_MESSWERT_SPANNUNG_WERT | unsigned int | Voltage measured on the faulty channel in mV |
| STAT_FEHLER_1_MESSWERT_STROMSTAERKE_WERT | unsigned int | Electricity measured on the faulty channel in mA |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lesen-laufwerk"></a>
### STATUS_LESEN_LAUFWERK

Reads out which drives the Head-Unit contains and the type and firmware of each drive.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VERBAUTE_LAUFWERKE | int | Drives that the Head-Unit contains as integer values from table TLaufwerk |
| STAT_VERBAUTE_LAUFWERKE_TEXT | string | List of drives the Head-Unit contains. Format lw1,lw2,... |
| STAT_VENDORID_TAPE | string | Vendor ID of the tape drive |
| STAT_PRODUCTID_TAPE | string | Product ID of the tape drive |
| STAT_FIRMWARE_TAPE | string | Firmware version of the tape drive |
| STAT_VENDORID_CD | string | Vendor ID of the cd drive |
| STAT_PRODUCTID_CD | string | Product ID of the cd drive |
| STAT_FIRMWARE_CD | string | Firmware version of the cd drive |
| STAT_VENDORID_DVD | string | Vendor ID of the dvd drive |
| STAT_PRODUCTID_DVD | string | Product ID of the dvd drive |
| STAT_FIRMWARE_DVD | string | Firmware version of the dvd drive |
| STAT_VENDORID_MD | string | Vendor ID of the md drive |
| STAT_PRODUCTID_MD | string | Product ID of the md drive |
| STAT_FIRMWARE_MD | string | Firmware version of the md drive |
| STAT_VENDORID_HDD | string | Vendor ID of the hdd drive |
| STAT_PRODUCTID_HDD | string | Product ID of the hdd drive |
| STAT_FIRMWARE_HDD | string | Firmware version of the hdd drive |
| STAT_VENDORID_USB | string | Vendor ID of the usb drive |
| STAT_PRODUCTID_USB | string | Product ID of the usb drive |
| STAT_FIRMWARE_USB | string | Firmware version of the usb drive |
| STAT_VENDORID_FLASHSPEICHER | string | Vendor ID of the flash drive |
| STAT_PRODUCTID_FLASHSPEICHER | string | Product ID of the flash drive |
| STAT_FIRMWARE_FLASHSPEICHER | string | Firmware version of the flash drive |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lesen-systemaudio"></a>
### STATUS_LESEN_SYSTEMAUDIO

This job reads which audio system is currently coded

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AUDIO_SYSTEM | unsigned char | Currently coded Audio System, 0	STEREO, 1	HIFI, 2	TOP-HIFI |
| STAT_AUDIO_SYSTEM_TEXT | string | Currently coded Audio System from table TAudioSystem TEXT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lesestatistik-dvd"></a>
### STATUS_LESESTATISTIK_DVD

Reads out some statistical data concerning the DVD drive and derived from the HDD SMART system

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ATA_ID | unsigned int | SmartValue ATA ID |
| STAT_ATA_ID_TEXT | string | SmartValue ATA ID Texte from table THDDSmartValues |
| STAT_NORMALIZED_VALUE | unsigned char | Current normalized SmartValue from 0x01 up to 0xFD |
| STAT_TRESHOLD_VALUE | unsigned char | Treshold for SmartValue |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-logistic-nr"></a>
### STATUS_LOGISTIC_NR

Reads out the logistic number Lieferumfangsnummer = number that characterizes the Anliefervariante

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LOGISTIC_NR | string | Logistic number |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-map-update"></a>
### STATUS_MAP_UPDATE

Returns the status of the map update.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MAP_UPDATE | unsigned char | Status of the map update as integer |
| STAT_MAP_UPDATE_TEXT | string | Status of the map update as table TMapUpdate |
| STAT_PERCENT_COMPLETE_WERT | unsigned char | Completion percentage of the map update |
| STAT_AVAILABLE_DATASETS_WERT | unsigned int | Number of available datasets |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mapmaterial-version"></a>
### STATUS_MAPMATERIAL_VERSION

Reads out the version of the map material.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MAPMATERIAL_VERSION | string | Map material version |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-memory-usage"></a>
### STATUS_MEMORY_USAGE

Returns the usage of the flash and of the RAM memories.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MEMORYSPACE_FLASH_KBYTE_WERT | unsigned long | Total memory space of flash in kbytes |
| STAT_FREE_MEMORYSPACE_FLASH_KBYTE_WERT | unsigned long | Free memory space of flash in kbytes |
| STAT_FREE_MEMORYSPACE_FLASH_PERCENT_WERT | unsigned char | Free memory space of flash in PERCENT |
| STAT_MEMORYSPACE_RAM_KBYTE_WERT | unsigned long | Total memory space of RAM in kbytes |
| STAT_FREE_MEMORYSPACE_RAM_KBYTE_WERT | unsigned long | Free memory space of RAM in kbytes |
| STAT_FREE_MEMORYSPACE_RAM_PERCENT_WERT | unsigned char | Free memory space of RAM in PERCENT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-most-3db"></a>
### STATUS_MOST_3DB

xx Status der 3dB Leistungsabsenkung der MOST FOTs.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOST_3DB | unsigned char | 0 = Lichtleistung abgesenkt, 1 = Volle Lichtleistung Werte aus table TMostLight WERT |
| STAT_MOST_3DB_TEXT | string | 0 = Lichtleistung abgesenkt, 1 = Volle Lichtleistung Werte aus table TMostLight TEXT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mostdiag-delay"></a>
### STATUS_MOSTDIAG_DELAY

Verzögerungszeit, bis der Job steuern_zentrale_registry_sollkonfiguration wieder gestartet werden kann

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DELAY | unsigned char | Verzögerungszeit in Sekunden, bis der Job wieder gestartet werden kann |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-navi-calibration"></a>
### STATUS_NAVI_CALIBRATION

Returns if the Positioning Process is calibrated.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NAVI_CALIBRATION | unsigned char | Calibration status of the Positioning Process as integer |
| STAT_NAVI_CALIBRATION_TEXT | string | Calibration status of the Positioning Process as table TNaviCalibration |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-navi-map"></a>
### STATUS_NAVI_MAP

Returns the status of the customer navigation map.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NAVI_MAP | unsigned char | Status of the customer navigation map as integer |
| STAT_NAVI_MAP_TEXT | string | Status of the customer navigation map as table TNaviMapStatus |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-navicheck"></a>
### STATUS_NAVICHECK

Returns the actual results of the NAVICHECK subsystem.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-next-entsource"></a>
### STATUS_NEXT_ENTSOURCE

Gives back the status of actual entertainmentsource.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ENTSOURCE | unsigned char | Entertainment source that is currently active |
| STAT_ENTSOURCE_TEXT | string | Entertainment source that is currently active as text String values from table TEntSource |
| STAT_DESIRED_ENTSOURCE | unsigned char | Last desired entertainmentsource (from steuern_next_entsource) was available? 0x00 'Entertainmentsource not available', --&gt; NOTOK 0x01 'Entertainmentsource was available', --&gt; OK 0xFF default if job steuern_next_entsource was not executed |
| STAT_DESIRED_ENTSOURCE_TEXT | string | Last desired entertainmentsource (from steuern_next_entsource) was available? 0x00 'Entertainmentsource not available', --&gt; NOTOK 0x01 'Entertainmentsource was available', --&gt; OK 0xFF default if job steuern_next_entsource was not executed values from table TEntSourceStatus |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-poi-download"></a>
### STATUS_POI_DOWNLOAD

Returns the status of the POI download.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_POI_DOWNLOAD | unsigned char | Status of the POI download as integer |
| STAT_POI_DOWNLOAD_TEXT | string | Status of the POI download as table TPoiDownload |
| STAT_PERCENT_COMPLETE_WERT | unsigned char | Completion percentage of the POI download |
| STAT_AVAILABLE_DATASETS_WERT | unsigned int | Number of available datasets (My POI) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-provisioning"></a>
### STATUS_PROVISIONING

Returns the status of the provisioning request.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PROVISIONING | unsigned char | Provisioning status as integer |
| STAT_PROVISIONING_TEXT | string | Provisioning status as table TProvisioningStatus |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-radon"></a>
### STATUS_RADON

Reads out the status of the RADON control lead.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RADON | unsigned char | Value of the RADON control lead as integer |
| STAT_RADON_TEXT | string | Value of the RADON control lead as text |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rds"></a>
### STATUS_RDS

Reads out the activation state of the TP, RDS and AF functionalities.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TP | unsigned char | Activation state of TP |
| STAT_TP_TEXT | string | Activation state of TP as text table TTp |
| STAT_AF | unsigned char | Activation state of AF |
| STAT_AF_TEXT | string | Activation state of AF as text table TAf |
| STAT_RDS | unsigned char | Activation state of RDS |
| STAT_RDS_TEXT | string | Activation state of RDS as text table TRds |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-route-download"></a>
### STATUS_ROUTE_DOWNLOAD

Returns the status of the route download.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ROUTE_DOWNLOAD | unsigned char | Status of the route download as integer |
| STAT_ROUTE_DOWNLOAD_TEXT | string | Status of the route download as table TRouteDownload |
| STAT_PERCENT_COMPLETE_WERT | unsigned char | Completion percentage of the route download |
| STAT_AVAILABLE_DATASETS_WERT | unsigned int | Number of available datasets |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-routing-engine"></a>
### STATUS_ROUTING_ENGINE

Inhalt der Routing Engine

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MTR_0X00 | string | MTR Registerinhalt 0x00 |
| STAT_MTR_0X10 | string | MTR Registerinhalt 0x10 |
| STAT_MTR_0X20 | string | MTR Registerinhalt 0x20 |
| STAT_MTR_0X30 | string | MTR Registerinhalt 0x30 |
| STAT_MTR_0X40 | string | MTR Registerinhalt 0x40 |
| STAT_MTR_0X50 | string | MTR Registerinhalt 0x50 |
| STAT_MTR_0X60 | string | MTR Registerinhalt 0x60 |
| STAT_MTR_0X70 | string | MTR Registerinhalt 0x70 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sdars-ber"></a>
### STATUS_SDARS_BER

Returns the BER of the SDARS signal.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SDARS_BER_WERT | real | BER of the SDARS signal |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sdars-ber-mode"></a>
### STATUS_SDARS_BER_MODE

Returns the SDARS BER mode that is currently active

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SDARS_BER_MODE | unsigned char | BER mode that is currently active values from table TSdarsBerMode |
| STAT_SDARS_BER_MODE_TEXT | string | BER mode that is currently active values from table TSdarsBerMode |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sdars-channel"></a>
### STATUS_SDARS_CHANNEL

Sets a definite SDARS channel.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SDARS_CHANNEL_WERT | unsigned char | Channel number of the current SDARS channel |
| STAT_SDARS_CHANNEL_TUNE_SUCCESS | unsigned char | Status of the current SDARS channel values from table TSdarsChannelTuneSuccess |
| STAT_SDARS_CHANNEL_TUNE_SUCCESS_TEXT | string | Status of the current SDARS channel values from table TSdarsChannelTuneSuccess |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sdars-esn"></a>
### STATUS_SDARS_ESN

Returns the 12 digits ESN of the SDARS tuner.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SDARS_ESN | string | 12 digits ESN of the SDARS tuner |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sdars-factory-defaults"></a>
### STATUS_SDARS_FACTORY_DEFAULTS

Restores the factory defaults of the SDARS tuner.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SDARS_FACTORY_DEFAULTS | unsigned char | Status of the restoring process of the factory defaults of the SDARS tuner values from table TSdarsFactorySuccessful |
| STAT_SDARS_FACTORY_DEFAULTS_TEXT | string | Status of the restoring process of the factory defaults of the SDARS tuner values from table TSdarsFactorySuccessful |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sdars-firmware-versions"></a>
### STATUS_SDARS_FIRMWARE_VERSIONS

Returns the various firmware versions of the SDARS module

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FIRMWARE_SECURITY_PROCESSOR | string | Firmware version of the security processor |
| STAT_FIRMWARE_AUDIO_PROCESSOR | string | Firmware version of the audio processor |
| STAT_BASEBAND_IC_VERSION | string | Baseband IC version |
| STAT_MODULE_UC_SOFTWARE_VERSION | string | Module uC software version |
| STAT_FIRMWARE_PRODUCT_ID | string | Firmware version of the product_id |
| STAT_FIRMWARE_DATE_CODE_VERSION | string | Firmware version of the date code |
| STAT_FIRMWARE_TIME_CODE_VERSION | string | Firmware version of the time code |
| STAT_GCI_VERSION | string | GCI version |
| STAT_DATA_SERVICES_PROGRAM_GUIDE_VERSION | string | Data services program guide version |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sdars-generator-frequency"></a>
### STATUS_SDARS_GENERATOR_FREQUENCY

Sets the sine generator frequency respectively for the left and right channels.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SDARS_GENERATOR_FREQUENCY_LEFT_WERT | unsigned int | Frequency that is currently active on the left channel |
| STAT_SDARS_GENERATOR_FREQUENCY_RIGHT_WERT | unsigned int | Frequency that is currently active on the right channel |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sdars-signal-quality"></a>
### STATUS_SDARS_SIGNAL_QUALITY

Returns the quality of the SDARS signal.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SDARS_COMP_RECEPTION | unsigned char | Composite reception quality values from table TSdarsSignalQuality |
| STAT_SDARS_COMP_RECEPTION_TEXT | string | Composite reception quality values from table TSdarsSignalQuality |
| STAT_SDARS_SAT_RECEPTION | unsigned char | Satellite reception quality values from table TSdarsSignalQuality |
| STAT_SDARS_SAT_RECEPTION_TEXT | string | Satellite reception quality values from table TSdarsSignalQuality |
| STAT_SDARS_TER_RECEPTION | unsigned char | Terrestrial reception quality values from table TSdarsSignalQuality |
| STAT_SDARS_TER_RECEPTION_TEXT | string | Terrestrial reception quality values from table TSdarsSignalQuality |
| STAT_SDARS_GLOBAL_STATUS | unsigned char | Global status values from table TSdarsSignalQualityGlobalStatus |
| STAT_SDARS_GLOBAL_STATUS_TEXT | string | Global status values from table TSdarsSignalQualityGlobalStatus |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sdars-tuner-mode"></a>
### STATUS_SDARS_TUNER_MODE

Sets the SDARS tuner in the selected mode.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SDARS_TUNER_MODE | unsigned char | Mode of the SDARS tuner values from table TSdarsTunerMode |
| STAT_SDARS_TUNER_MODE_TEXT | string | Mode of the SDARS tuner values from table TSdarsTunerMode |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-search-fblock"></a>
### STATUS_SEARCH_FBLOCK

FBlockID.InstID searched in Current Registry

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_FBLOCKID | unsigned char | FBlockID.InstID searched in Registry |
| ARG_INSTID | unsigned char | FBlockID.InstID searched in Registry |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS | unsigned char | 0x00 Fblock/InstID is not in current registry 0x01 Fblock/InstID is in current registry 0x02 Registry Invalid (LightOff oder MPR Change Event, ...) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sensor-temp"></a>
### STATUS_SENSOR_TEMP

Returns the temperature of the desired sensor (no matter if the temperature is currently being simulated or not).

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_SENSOR | unsigned char | Sensor for which the temperature must be returned |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEMPERATURE_WERT | char | Temperature of the selected sensor |
| STAT_DURATION_WERT | unsigned char | Remaining duration for the simulated temperature |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sgbmid-navimap"></a>
### STATUS_SGBMID_NAVIMAP

Returns the SGBM ID of the customer navigation map that is currently active.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SGBMID | string | SGBM ID of the navigation map that is currently active format pk.idididid.hv.uv.pv |
| STAT_SGBMID_DATA | binary | SGBM ID of the navigation map that is currently active format 8 Bytes HexData |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-speed"></a>
### STATUS_SPEED

Reads out all speed data of the car (sensor speed of each wheel, combined sensor speed and GPS speed) and performs a comparison of the combined sensor speed and of the GPS speed.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WHEEL1_SENSOR_SPEED_WERT | int | Speed measured by the sensor of the wheel 1 and transmitted on the bus |
| STAT_WHEEL2_SENSOR_SPEED_WERT | int | Speed measured by the sensor of the wheel 2 and transmitted on the bus |
| STAT_WHEEL3_SENSOR_SPEED_WERT | int | Speed measured by the sensor of the wheel 3 and transmitted on the bus |
| STAT_WHEEL4_SENSOR_SPEED_WERT | int | Speed measured by the sensor of the wheel 4 and transmitted on the bus |
| STAT_COMBINED_SENSOR_SPEED_WERT | int | Combined speed measured by the sensors of the car and transmitted on the bus |
| STAT_GPS_SPEED_WERT | int | Speed calculated on the basis of the GPS signals |
| STAT_SPEED_DIFFERENCE_PERCENT_WERT | unsigned int | Speed difference in percent between the combined sensor speed and the GPS speed |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-taste"></a>
### STATUS_TASTE

Auslesen, ob gerade eine Taste gedrueckt ist

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TASTE | unsigned char | Button that is pressed. Values from table TTaste |
| STAT_TASTE_TEXT | string | Button that is pressed as text |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tda-atm"></a>
### STATUS_TDA_ATM

Reads out the automatic trigger of a TDA call.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TDA_ATM | unsigned char | 0x01 enabled, 0x00 disabled |
| STAT_STARTTIME | unsigned char | Hour when mechanism should start (0-24) |
| STAT_INTERVALL | unsigned char | Minutes between the test calls |
| STAT_CALLID | unsigned char | 0x01, 0x02, 0x04 … |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tel-mute"></a>
### STATUS_TEL_MUTE

Outputs whether the phone mute lead is active or inactive.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEL_MUTE | unsigned char | Tel-Mute lead active or inactive as integer |
| STAT_TEL_MUTE_TEXT | string | Tel-Mute lead active or inactive as table TTelMute |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-temp-verteilung-dvd-drive"></a>
### STATUS_TEMP_VERTEILUNG_DVD_DRIVE

Reads out the temperature histogram of the DVD drive.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MAX_TEMP | char | Maximum temperature that was measured up to 128 degrees |
| STAT_TEMP_RANGE_01 | unsigned long | Increment value for the temperature range -40 C &lt; t &lt;= -35 C |
| STAT_TEMP_RANGE_02 | unsigned long | Increment value for the temperature range -35 C &lt; t &lt;= -30 C |
| STAT_TEMP_RANGE_03 | unsigned long | Increment value for the temperature range -30 C &lt; t &lt;= -25 C |
| STAT_TEMP_RANGE_04 | unsigned long | Increment value for the temperature range -25 C &lt; t &lt;= -20 C |
| STAT_TEMP_RANGE_05 | unsigned long | Increment value for the temperature range -20 C &lt; t &lt;= -15 C |
| STAT_TEMP_RANGE_06 | unsigned long | Increment value for the temperature range -15 C &lt; t &lt;= -10 C |
| STAT_TEMP_RANGE_07 | unsigned long | Increment value for the temperature range -10 C &lt; t &lt;= -5 C |
| STAT_TEMP_RANGE_08 | unsigned long | Increment value for the temperature range -5 C &lt; t &lt;= 0 C |
| STAT_TEMP_RANGE_09 | unsigned long | Increment value for the temperature range 0 C &lt; t &lt;= 5 C |
| STAT_TEMP_RANGE_10 | unsigned long | Increment value for the temperature range 5 C &lt; t &lt;= 10 C |
| STAT_TEMP_RANGE_11 | unsigned long | Increment value for the temperature range 10 C &lt; t &lt;= 15 C |
| STAT_TEMP_RANGE_12 | unsigned long | Increment value for the temperature range 15 C &lt; t &lt;= 20 C |
| STAT_TEMP_RANGE_13 | unsigned long | Increment value for the temperature range 20 C &lt; t &lt;= 25 C |
| STAT_TEMP_RANGE_14 | unsigned long | Increment value for the temperature range 25 C &lt; t &lt;= 30 C |
| STAT_TEMP_RANGE_15 | unsigned long | Increment value for the temperature range 30 C &lt; t &lt;= 35 C |
| STAT_TEMP_RANGE_16 | unsigned long | Increment value for the temperature range 35 C &lt; t &lt;= 40 C |
| STAT_TEMP_RANGE_17 | unsigned long | Increment value for the temperature range 40 C &lt; t &lt;= 45 C |
| STAT_TEMP_RANGE_18 | unsigned long | Increment value for the temperature range 45 C &lt; t &lt;= 50 C |
| STAT_TEMP_RANGE_19 | unsigned long | Increment value for the temperature range 50 C &lt; t &lt;= 55 C |
| STAT_TEMP_RANGE_20 | unsigned long | Increment value for the temperature range 55 C &lt; t &lt;= 60 C |
| STAT_TEMP_RANGE_21 | unsigned long | Increment value for the temperature range 60 C &lt; t &lt;= 65 C |
| STAT_TEMP_RANGE_22 | unsigned long | Increment value for the temperature range 65 C &lt; t &lt;= 70 C |
| STAT_TEMP_RANGE_23 | unsigned long | Increment value for the temperature range 70 C &lt; t &lt;= 75 C |
| STAT_TEMP_RANGE_24 | unsigned long | Increment value for the temperature range 75 C &lt; t &lt;= 80 C |
| STAT_TEMP_RANGE_25 | unsigned long | Increment value for the temperature range 80 C &lt; t &lt;= 85 C |
| STAT_TEMP_RANGE_26 | unsigned long | Increment value for the temperature range 85 C &lt; t &lt;= 90 C |
| STAT_TEMP_RANGE_27 | unsigned long | Increment value for the temperature range 90 C &lt; t &lt;= 95 C |
| STAT_TEMP_RANGE_28 | unsigned long | Increment value for the temperature range 95 C &lt; t &lt;= 100 C |
| STAT_TEMP_RANGE_29 | unsigned long | Increment value for the temperature range 100 C &lt; t &lt;= 105 C |
| STAT_TEMP_RANGE_30 | unsigned long | Increment value for the temperature range 105 C &lt; t &lt;= 110 C |
| STAT_TEMP_RANGE_31 | unsigned long | Increment value for the temperature range 110 C &lt; t &lt;= 115 C |
| STAT_TEMP_RANGE_32 | unsigned long | Increment value for the temperature range 115 C &lt; t &lt;= 120 C |
| STAT_TEMP_RANGE_33 | unsigned long | Increment value for the temperature range 120 C &lt; t &lt;= 125 C |
| STAT_TEMP_RANGE_34 | unsigned long | Increment value for the temperature range 125 C &lt; t &lt;= 130 C |
| STAT_TEMP_RANGE_35 | unsigned long | Increment value for the temperature range 130 C &lt; t &lt;= 135 C |
| STAT_TEMP_RANGE_36 | unsigned long | Increment value for the temperature range 135 C &lt; t &lt;= 140 C |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-temp-verteilung-fot"></a>
### STATUS_TEMP_VERTEILUNG_FOT

Reads out the temperature histogram of the FOT unit.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MAX_TEMP | char | Maximum temperature that was measured up to 128 degrees |
| STAT_TEMP_RANGE_01 | unsigned long | Increment value for the temperature range -40 C &lt; t &lt;= -35 C |
| STAT_TEMP_RANGE_02 | unsigned long | Increment value for the temperature range -35 C &lt; t &lt;= -30 C |
| STAT_TEMP_RANGE_03 | unsigned long | Increment value for the temperature range -30 C &lt; t &lt;= -25 C |
| STAT_TEMP_RANGE_04 | unsigned long | Increment value for the temperature range -25 C &lt; t &lt;= -20 C |
| STAT_TEMP_RANGE_05 | unsigned long | Increment value for the temperature range -20 C &lt; t &lt;= -15 C |
| STAT_TEMP_RANGE_06 | unsigned long | Increment value for the temperature range -15 C &lt; t &lt;= -10 C |
| STAT_TEMP_RANGE_07 | unsigned long | Increment value for the temperature range -10 C &lt; t &lt;= -5 C |
| STAT_TEMP_RANGE_08 | unsigned long | Increment value for the temperature range -5 C &lt; t &lt;= 0 C |
| STAT_TEMP_RANGE_09 | unsigned long | Increment value for the temperature range 0 C &lt; t &lt;= 5 C |
| STAT_TEMP_RANGE_10 | unsigned long | Increment value for the temperature range 5 C &lt; t &lt;= 10 C |
| STAT_TEMP_RANGE_11 | unsigned long | Increment value for the temperature range 10 C &lt; t &lt;= 15 C |
| STAT_TEMP_RANGE_12 | unsigned long | Increment value for the temperature range 15 C &lt; t &lt;= 20 C |
| STAT_TEMP_RANGE_13 | unsigned long | Increment value for the temperature range 20 C &lt; t &lt;= 25 C |
| STAT_TEMP_RANGE_14 | unsigned long | Increment value for the temperature range 25 C &lt; t &lt;= 30 C |
| STAT_TEMP_RANGE_15 | unsigned long | Increment value for the temperature range 30 C &lt; t &lt;= 35 C |
| STAT_TEMP_RANGE_16 | unsigned long | Increment value for the temperature range 35 C &lt; t &lt;= 40 C |
| STAT_TEMP_RANGE_17 | unsigned long | Increment value for the temperature range 40 C &lt; t &lt;= 45 C |
| STAT_TEMP_RANGE_18 | unsigned long | Increment value for the temperature range 45 C &lt; t &lt;= 50 C |
| STAT_TEMP_RANGE_19 | unsigned long | Increment value for the temperature range 50 C &lt; t &lt;= 55 C |
| STAT_TEMP_RANGE_20 | unsigned long | Increment value for the temperature range 55 C &lt; t &lt;= 60 C |
| STAT_TEMP_RANGE_21 | unsigned long | Increment value for the temperature range 60 C &lt; t &lt;= 65 C |
| STAT_TEMP_RANGE_22 | unsigned long | Increment value for the temperature range 65 C &lt; t &lt;= 70 C |
| STAT_TEMP_RANGE_23 | unsigned long | Increment value for the temperature range 70 C &lt; t &lt;= 75 C |
| STAT_TEMP_RANGE_24 | unsigned long | Increment value for the temperature range 75 C &lt; t &lt;= 80 C |
| STAT_TEMP_RANGE_25 | unsigned long | Increment value for the temperature range 80 C &lt; t &lt;= 85 C |
| STAT_TEMP_RANGE_26 | unsigned long | Increment value for the temperature range 85 C &lt; t &lt;= 90 C |
| STAT_TEMP_RANGE_27 | unsigned long | Increment value for the temperature range 90 C &lt; t &lt;= 95 C |
| STAT_TEMP_RANGE_28 | unsigned long | Increment value for the temperature range 95 C &lt; t &lt;= 100 C |
| STAT_TEMP_RANGE_29 | unsigned long | Increment value for the temperature range 100 C &lt; t &lt;= 105 C |
| STAT_TEMP_RANGE_30 | unsigned long | Increment value for the temperature range 105 C &lt; t &lt;= 110 C |
| STAT_TEMP_RANGE_31 | unsigned long | Increment value for the temperature range 110 C &lt; t &lt;= 115 C |
| STAT_TEMP_RANGE_32 | unsigned long | Increment value for the temperature range 115 C &lt; t &lt;= 120 C |
| STAT_TEMP_RANGE_33 | unsigned long | Increment value for the temperature range 120 C &lt; t &lt;= 125 C |
| STAT_TEMP_RANGE_34 | unsigned long | Increment value for the temperature range 125 C &lt; t &lt;= 130 C |
| STAT_TEMP_RANGE_35 | unsigned long | Increment value for the temperature range 130 C &lt; t &lt;= 135 C |
| STAT_TEMP_RANGE_36 | unsigned long | Increment value for the temperature range 135 C &lt; t &lt;= 140 C |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-temp-verteilung-power-amplifier"></a>
### STATUS_TEMP_VERTEILUNG_POWER_AMPLIFIER

Reads out the temperature histogram of the power amplifier.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MAX_TEMP | char | Maximum temperature that was measured up to 128 degrees |
| STAT_TEMP_RANGE_1 | unsigned long | Increment value for the temperature range -40 C &lt; t &lt;= -35 C |
| STAT_TEMP_RANGE_2 | unsigned long | Increment value for the temperature range -35 C &lt; t &lt;= -30 C |
| STAT_TEMP_RANGE_3 | unsigned long | Increment value for the temperature range -30 C &lt; t &lt;= -25 C |
| STAT_TEMP_RANGE_4 | unsigned long | Increment value for the temperature range -25 C &lt; t &lt;= -20 C |
| STAT_TEMP_RANGE_5 | unsigned long | Increment value for the temperature range -20 C &lt; t &lt;= -15 C |
| STAT_TEMP_RANGE_6 | unsigned long | Increment value for the temperature range -15 C &lt; t &lt;= -10 C |
| STAT_TEMP_RANGE_7 | unsigned long | Increment value for the temperature range -10 C &lt; t &lt;= -5 C |
| STAT_TEMP_RANGE_8 | unsigned long | Increment value for the temperature range -5 C &lt; t &lt;= 0 C |
| STAT_TEMP_RANGE_9 | unsigned long | Increment value for the temperature range 0 C &lt; t &lt;= 5 C |
| STAT_TEMP_RANGE_10 | unsigned long | Increment value for the temperature range 5 C &lt; t &lt;= 10 C |
| STAT_TEMP_RANGE_11 | unsigned long | Increment value for the temperature range 10 C &lt; t &lt;= 15 C |
| STAT_TEMP_RANGE_12 | unsigned long | Increment value for the temperature range 15 C &lt; t &lt;= 20 C |
| STAT_TEMP_RANGE_13 | unsigned long | Increment value for the temperature range 20 C &lt; t &lt;= 25 C |
| STAT_TEMP_RANGE_14 | unsigned long | Increment value for the temperature range 25 C &lt; t &lt;= 30 C |
| STAT_TEMP_RANGE_15 | unsigned long | Increment value for the temperature range 30 C &lt; t &lt;= 35 C |
| STAT_TEMP_RANGE_16 | unsigned long | Increment value for the temperature range 35 C &lt; t &lt;= 40 C |
| STAT_TEMP_RANGE_17 | unsigned long | Increment value for the temperature range 40 C &lt; t &lt;= 45 C |
| STAT_TEMP_RANGE_18 | unsigned long | Increment value for the temperature range 45 C &lt; t &lt;= 50 C |
| STAT_TEMP_RANGE_19 | unsigned long | Increment value for the temperature range 50 C &lt; t &lt;= 55 C |
| STAT_TEMP_RANGE_20 | unsigned long | Increment value for the temperature range 55 C &lt; t &lt;= 60 C |
| STAT_TEMP_RANGE_21 | unsigned long | Increment value for the temperature range 60 C &lt; t &lt;= 65 C |
| STAT_TEMP_RANGE_22 | unsigned long | Increment value for the temperature range 65 C &lt; t &lt;= 70 C |
| STAT_TEMP_RANGE_23 | unsigned long | Increment value for the temperature range 70 C &lt; t &lt;= 75 C |
| STAT_TEMP_RANGE_24 | unsigned long | Increment value for the temperature range 75 C &lt; t &lt;= 80 C |
| STAT_TEMP_RANGE_25 | unsigned long | Increment value for the temperature range 80 C &lt; t &lt;= 85 C |
| STAT_TEMP_RANGE_26 | unsigned long | Increment value for the temperature range 85 C &lt; t &lt;= 90 C |
| STAT_TEMP_RANGE_27 | unsigned long | Increment value for the temperature range 90 C &lt; t &lt;= 95 C |
| STAT_TEMP_RANGE_28 | unsigned long | Increment value for the temperature range 95 C &lt; t &lt;= 100 C |
| STAT_TEMP_RANGE_29 | unsigned long | Increment value for the temperature range 100 C &lt; t &lt;= 105 C |
| STAT_TEMP_RANGE_30 | unsigned long | Increment value for the temperature range 105 C &lt; t &lt;= 110 C |
| STAT_TEMP_RANGE_31 | unsigned long | Increment value for the temperature range 110 C &lt; t &lt;= 115 C |
| STAT_TEMP_RANGE_32 | unsigned long | Increment value for the temperature range 115 C &lt; t &lt;= 120 C |
| STAT_TEMP_RANGE_33 | unsigned long | Increment value for the temperature range 120 C &lt; t &lt;= 125 C |
| STAT_TEMP_RANGE_34 | unsigned long | Increment value for the temperature range 125 C &lt; t &lt;= 130 C |
| STAT_TEMP_RANGE_35 | unsigned long | Increment value for the temperature range 130 C &lt; t &lt;= 135 C |
| STAT_TEMP_RANGE_36 | unsigned long | Increment value for the temperature range 135 C &lt; t &lt;= 140 C |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-temp-verteilung-sh4a"></a>
### STATUS_TEMP_VERTEILUNG_SH4A

Reads out the temperature histogram of the SH4A.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MAX_TEMP | char | Maximum temperature that was measured up to 128 degrees |
| STAT_TEMP_RANGE_01 | unsigned long | Increment value for the temperature range -40 C &lt; t &lt;= -35 C |
| STAT_TEMP_RANGE_02 | unsigned long | Increment value for the temperature range -35 C &lt; t &lt;= -30 C |
| STAT_TEMP_RANGE_03 | unsigned long | Increment value for the temperature range -30 C &lt; t &lt;= -25 C |
| STAT_TEMP_RANGE_04 | unsigned long | Increment value for the temperature range -25 C &lt; t &lt;= -20 C |
| STAT_TEMP_RANGE_05 | unsigned long | Increment value for the temperature range -20 C &lt; t &lt;= -15 C |
| STAT_TEMP_RANGE_06 | unsigned long | Increment value for the temperature range -15 C &lt; t &lt;= -10 C |
| STAT_TEMP_RANGE_07 | unsigned long | Increment value for the temperature range -10 C &lt; t &lt;= -5 C |
| STAT_TEMP_RANGE_08 | unsigned long | Increment value for the temperature range -5 C &lt; t &lt;= 0 C |
| STAT_TEMP_RANGE_09 | unsigned long | Increment value for the temperature range 0 C &lt; t &lt;= 5 C |
| STAT_TEMP_RANGE_10 | unsigned long | Increment value for the temperature range 5 C &lt; t &lt;= 10 C |
| STAT_TEMP_RANGE_11 | unsigned long | Increment value for the temperature range 10 C &lt; t &lt;= 15 C |
| STAT_TEMP_RANGE_12 | unsigned long | Increment value for the temperature range 15 C &lt; t &lt;= 20 C |
| STAT_TEMP_RANGE_13 | unsigned long | Increment value for the temperature range 20 C &lt; t &lt;= 25 C |
| STAT_TEMP_RANGE_14 | unsigned long | Increment value for the temperature range 25 C &lt; t &lt;= 30 C |
| STAT_TEMP_RANGE_15 | unsigned long | Increment value for the temperature range 30 C &lt; t &lt;= 35 C |
| STAT_TEMP_RANGE_16 | unsigned long | Increment value for the temperature range 35 C &lt; t &lt;= 40 C |
| STAT_TEMP_RANGE_17 | unsigned long | Increment value for the temperature range 40 C &lt; t &lt;= 45 C |
| STAT_TEMP_RANGE_18 | unsigned long | Increment value for the temperature range 45 C &lt; t &lt;= 50 C |
| STAT_TEMP_RANGE_19 | unsigned long | Increment value for the temperature range 50 C &lt; t &lt;= 55 C |
| STAT_TEMP_RANGE_20 | unsigned long | Increment value for the temperature range 55 C &lt; t &lt;= 60 C |
| STAT_TEMP_RANGE_21 | unsigned long | Increment value for the temperature range 60 C &lt; t &lt;= 65 C |
| STAT_TEMP_RANGE_22 | unsigned long | Increment value for the temperature range 65 C &lt; t &lt;= 70 C |
| STAT_TEMP_RANGE_23 | unsigned long | Increment value for the temperature range 70 C &lt; t &lt;= 75 C |
| STAT_TEMP_RANGE_24 | unsigned long | Increment value for the temperature range 75 C &lt; t &lt;= 80 C |
| STAT_TEMP_RANGE_25 | unsigned long | Increment value for the temperature range 80 C &lt; t &lt;= 85 C |
| STAT_TEMP_RANGE_26 | unsigned long | Increment value for the temperature range 85 C &lt; t &lt;= 90 C |
| STAT_TEMP_RANGE_27 | unsigned long | Increment value for the temperature range 90 C &lt; t &lt;= 95 C |
| STAT_TEMP_RANGE_28 | unsigned long | Increment value for the temperature range 95 C &lt; t &lt;= 100 C |
| STAT_TEMP_RANGE_29 | unsigned long | Increment value for the temperature range 100 C &lt; t &lt;= 105 C |
| STAT_TEMP_RANGE_30 | unsigned long | Increment value for the temperature range 105 C &lt; t &lt;= 110 C |
| STAT_TEMP_RANGE_31 | unsigned long | Increment value for the temperature range 110 C &lt; t &lt;= 115 C |
| STAT_TEMP_RANGE_32 | unsigned long | Increment value for the temperature range 115 C &lt; t &lt;= 120 C |
| STAT_TEMP_RANGE_33 | unsigned long | Increment value for the temperature range 120 C &lt; t &lt;= 125 C |
| STAT_TEMP_RANGE_34 | unsigned long | Increment value for the temperature range 125 C &lt; t &lt;= 130 C |
| STAT_TEMP_RANGE_35 | unsigned long | Increment value for the temperature range 130 C &lt; t &lt;= 135 C |
| STAT_TEMP_RANGE_36 | unsigned long | Increment value for the temperature range 135 C &lt; t &lt;= 140 C |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-test-antenne"></a>
### STATUS_TEST_ANTENNE

Returns the results of the impedance measurements performed with steuern_test_antenne

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANTENNE | unsigned long | Antennas that have been tested values from table TAntenne |
| STAT_ANTENNE_TEXT | string | Antenna that have been tested Values from table TAntenne |
| STAT_TEST_ANTENNE | unsigned char | Status of the test values from table TTestStatus |
| STAT_TEST_ANTENNE_TEXT | string | Status of the test values from table TTestStatus |
| STAT_ANZAHL_FEHLERHAFTE_ANTENNEN_WERT | unsigned char | Number of the faulty antennas  In the following you see only first antenna the other results STAT_FEHLER_2-16_... are created dynamically |
| STAT_FEHLER_1_ANTENNE | unsigned long | faulty antenna values from table TAntenne |
| STAT_FEHLER_1_ANTENNE_TEXT | string | faulty antenna values from table TAntenne |
| STAT_FEHLER_1_FEHLERART_ANTENNE | unsigned char | Type of error values from table TAntenneFehlerArt |
| STAT_FEHLER_1_FEHLERART_ANTENNE_TEXT | string | Type of error values from table TAntenneFehlerArt |
| STAT_FEHLER_1_MESSWERT_WIDERSTAND_WERT | unsigned int | impedance value measured 0x0001 = 0.1 kOhm, Max possible value: 0xC350 = 5 MOhm If the exact value cannot be returned, the value 0xFFFF is returned |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tmc"></a>
### STATUS_TMC

Returns the activation state of the TMC functionality

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TMC | unsigned char | TMC Activation state table TTmcActivationState |
| STAT_TMC_TEXT | string | TMC Activation state as text |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tmc-dab"></a>
### STATUS_TMC_DAB

Returns the activation state of the DAB TMC functionality.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TMC_DAB | unsigned char | Activation state values from table TDabTmcActivationState |
| STAT_TMC_DAB_TEXT | string | Activation state values from table TDabTmcActivationState |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tuner-codierung"></a>
### STATUS_TUNER_CODIERUNG

Reads all the coding data / flags which are correlated to the tuner.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LAENDERVARIANTE_TUNER | unsigned char | country variant with 0x00=ECE, 0x01=US, 0x02=Japan, 0x03=Oceania, 0x07=No Area |
| STAT_LAENDERVARIANTE_TUNER_TEXT | string | country variant |
| STAT_TP | unsigned char | TP status with 0x00=TP inactive, 0x01=TP active |
| STAT_TP_TEXT | string | TP status |
| STAT_RDS_AF | unsigned char | RDS / AF status with 0x00=RDS on, AF off / 0x01=RDS on, AF manual / 0x02=RDS on, AF automatic / 0x03=RDS off / 0x07=Not defined |
| STAT_RDS_AF_TEXT | string | RDS / AF status |
| STAT_PTY_TABELLE | unsigned char | PTY table with 0x00=PTY ECE / 0x01=PTY US |
| STAT_PTY_TABELLE_TEXT | string | PTY table |
| STAT_REGIONALISIERUNG | unsigned char | regional values with 0x00=value 0 / 0x01=value 1 / 0x02=value 2 |
| STAT_REGIONALISIERUNG_TEXT | string | regional values |
| STAT_HIGH_CUT | unsigned char | HighCut with 0x00=High / 0x01=Low / 0x02=Auto / 0x03=Notch |
| STAT_HIGH_CUT_TEXT | string | HighCut |
| STAT_SENDER_TAB | unsigned char | SenderTab with 0x00=HGL / 0x01=FMD |
| STAT_SENDER_TAB_TEXT | string | SenderTab |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tuner-codierung-dab"></a>
### STATUS_TUNER_CODIERUNG_DAB

Reads all the coding data / flags which are correlated to the tuner.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-version-most-controller"></a>
### STATUS_VERSION_MOST_CONTROLLER

Return Version of MOST Controller

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TRANSCEIVER_VERSION | string | Transceiver Version Format DDMMYY |
| STAT_NETSERVICES_VERSION | string | 3 Bytes Netservices Version |
| STAT_NETSERVICES_REVISION | string | 4 Byte Netservices Revision |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-versorgungsspannung"></a>
### STATUS_VERSORGUNGSSPANNUNG

Betriebsspannung am SG. Darstellung mit Millivolt-Auflösung.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MILLI_VOLT_WERT | unsigned int | Spannung in milliVolt |
| STAT_MILLI_VOLT_EINH | string | unit of the result |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-vertical-heading"></a>
### STATUS_VERTICAL_HEADING

Reads out all data related to the vertical heading of the car (acceleration sensor type, vertical delta heading and drift) and performs a comparison with the GPS vertical heading changes.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VERTICAL_DELTA_HEADING_WERT | unsigned int | Vertical heading changes measured by the acceleration sensor |
| STAT_ACCELERATION_SENSOR_TYPE | unsigned char | Type of acceleration sensor that is present in the car as integer |
| STAT_ACCELERATION_SENSOR_TYPE_TEXT | string | Type of acceleration sensor that is present in the car as table TAccelerationSensorType |
| STAT_ACCELERATION_SENSOR_DRIFT_WERT | unsigned int | Drift of the acceleration sensor in mV |
| STAT_GPS_CORRELATION | unsigned char | Correlation of the vertical heading changes measured by the acceleration sensor with the vertical heading changes measured via GPS as integer |
| STAT_GPS_CORRELATION_TEXT | string | Correlation of the vertical heading changes measured by the acceleration sensor with the vertical heading changes measured via GPS as table TGpsCorrelationHeading |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-volumeaudio"></a>
### STATUS_VOLUMEAUDIO

Abfragen der Audio-Lautstaerke

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_AUDIO_SIGNAL | unsigned char | Adjusts the volume of a definite audio signal from table TAudioSignal Default, 0x00 Entertainment |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LEVEL_WERT | unsigned char | VolumeLevel of the selected audio signal |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-wakeup-status"></a>
### STATUS_WAKEUP_STATUS

Gibt an, ob das SG den MOST-Ring geweckt hat oder geweckt wurde.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WAKEUP_STATUS | int | 0 = nicht initialisiert, 1 = SG hat geweckt,  2= SG wurde geweckt from table TWakeupStatus WERT |
| STAT_WAKEUP_STATUS_TEXT | string | 0 = nicht initialisiert, 1 = SG hat geweckt,  2= SG wurde geweckt from table TWakeupStatus TEXT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-wakeup-abstime"></a>
### STATUS_WAKEUP_ABSTIME

7 bytes Zeitpunkt, zu dem das SG den Weckbefehl gegeben hat Bytes werden als Datum interpretiert Beispiel: '20060508131210' in der Reihenfolge YYYYMMDDHHMMSS. Falls das SG nie geweckt hat wird '00000000000000' zurückgegeben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WAKE_UP_ABSTIME | string | Zeitpunkt im Format YYYYMMDDHHMMSS wann das SG den WakeUp-befehl gegeben hat |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-waveband"></a>
### STATUS_WAVEBAND

Returns the waveband that is currently active.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WAVEBAND | unsigned char | Waveband that is currently active from Table TWaveband WERT |
| STAT_WAVEBAND_TEXT | string | Waveband that is currently active from Table TWaveband TEXT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ability-to-wake"></a>
### STEUERN_ABILITY_TO_WAKE

Gibt an, ob das SG den MOST-Ring wecken darf.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_ABILITY_TO_WAKE | int | 0=off 1=on 2=critical |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ant-eigen-diag"></a>
### STEUERN_ANT_EIGEN_DIAG

Starts antenna diagnostics cycle for the respective antenna specification

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ant-scan"></a>
### STEUERN_ANT_SCAN

Creates an 8 Volt peek (if diversity diagnosis modus is active done by steuern_ant_eigen_diagnose) to switch through the FM antennas of the diversity or to switch back to normal operation mode into the AM band with the AM amplifier being active

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_SCAN | unsigned char | Operation to be performed 0x00 switch to AM, 0x01 switch to next FM (create a peek) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-audiokanaele"></a>
### STEUERN_AUDIOKANAELE

Ansteuern eines AudioKanals

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_KANAL | long | is the desired  BIT combination of the following values from table TAudiokanal WERT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-clear-ckmdata"></a>
### STEUERN_CLEAR_CKMDATA

Restores the delivery state (resets the PIA settings to their default settings) for the desired key/car.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_NR_KEY | unsigned char | Key number or car for which the delivery state must be restored |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-clear-ckmdata"></a>
### STATUS_CLEAR_CKMDATA

Status des Löschens der Car-Key-PIA Daten eines oder aller Schlüssel.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CLEAR_CKMDATA | unsigned char | Gibt den Status des Löschens wieder. Werte aus table TProcessStatus |
| STAT_CLEAR_CKMDATA_TEXT | string | Gibt den Status des Löschens wieder. Werte aus table TProcessStatus |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-clear-temp-verteilung"></a>
### STEUERN_CLEAR_TEMP_VERTEILUNG

Deletes the desired temperature histogram.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_LIST | unsigned char | Component from which the temperature histogram must be deleted 0x00 FOT, 0x01 DVD, 0x02 HDD, 0x03 Power, 0x04 SH4 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-codierung-master-bereich"></a>
### STEUERN_CODIERUNG_MASTER_BEREICH

Copy the content of the coding working domain into the very secured coding master domain.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-codierung-referenz-crc"></a>
### STEUERN_CODIERUNG_REFERENZ_CRC

Calculates the CRC of the coding data that are stored into the coding master domain and stores it into a very secured memory domain.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-copy-ckmdata"></a>
### STEUERN_COPY_CKMDATA

Copies the PIA data from key X to key Y.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_NR_KEY_SOURCE | unsigned char | Source key number without "all" 0x00	Profile 1 0x01	Profile 2 0x02	Profile 3 0x0A	Guest 0x0F	Dealership 0x10	Car 0xEF	All |
| ARG_NR_KEY_DEST | unsigned char | Destination key number also with "all" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-delete-cookies"></a>
### STEUERN_DELETE_COOKIES

Deletes all cookies inside all http stacks.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-demute"></a>
### STEUERN_DEMUTE

Controls the mute status of the current entertainment source.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_DEMUTE | unsigned char | Desired state of radio, 0x00 off, 0x01 on |
| ARG_HEADPHONES | unsigned char | Only for RSE needed  (for HeadUnit this is always 0x00 0x00 not used / no operation (used by HeadUnit) 0x01 left Headphones 0x02 right Headphones 0x03 both Headphones |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-eject"></a>
### STEUERN_EJECT

Ejects the media of the selected drives.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_DRIVE | int | Drives from which the media must be ejected Integer values from table TLaufwerk |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-emergency-eject"></a>
### STEUERN_EMERGENCY_EJECT

Ejects the media of the selected drives.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_DRIVE | unsigned char | Drives from which the media must be 0x02 CD 0x04 DVD (default) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fb-reset"></a>
### STEUERN_FB_RESET

This job resets/restarts the bezel.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fband-scan"></a>
### STEUERN_FBAND_SCAN

Start FBand scan

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_BAND | string | select the Waveband table TWaveband TEXT |
| ARG_WAIT | unsigned char | Startverzögerung in sekunden |
| ARG_FREQ_START | unsigned long | Startfrequenz (kHz) |
| ARG_FREQ_STOP | unsigned long | letzte zu prüfende Frequenz (kHz) |
| ARG_FREQ_STEP | unsigned long | Frequenzschrittweite (kHz) |
| ARG_BANDWIDTH | unsigned long | Bandbreite |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fband-scan-stop"></a>
### STEUERN_FBAND_SCAN_STOP

Stoped FBand scan

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-find-best-station"></a>
### STEUERN_FIND_BEST_STATION

Triggers the search in the current waveband of the best station (station with the best reception). When the best station has been detected, the head-unit switches to this best station.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-find-best-station-dab"></a>
### STEUERN_FIND_BEST_STATION_DAB

Triggers the search of the best DAB ensemble (ensemble with the lowest bit error rate). When the best DAB ensemble has been detected, the head-unit switches to this best ensemble (to the 1st service of the ensemble).

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-find-best-tmc-station"></a>
### STEUERN_FIND_BEST_TMC_STATION

Triggers the search in the current waveband of the best TMC station (station with the best reception). When the best TMC station has been detected, the head-unit switches to this best station.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-find-best-tmc-station-dab"></a>
### STEUERN_FIND_BEST_TMC_STATION_DAB

Triggers the search of the best DAB TMC station (station with the best reception). When the best DAB TMC station has been detected, the head-unit switches to this best station.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-flottenmodus"></a>
### STEUERN_FLOTTENMODUS

Set the desired Flottenmodus (mode of the NAVI DVD lock).

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_MODUS | unsigned char | Flottenmodus that must be activated |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-frequenz"></a>
### STEUERN_FREQUENZ

Set the tuner frequency.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_FREQUENZ | unsigned long | Frequency that must be set like: 94400 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klangzeichen"></a>
### STEUERN_KLANGZEICHEN

Ausloesen eines Klangzeichens

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_KLANGZEICHEN | unsigned char | Wert table TKlangzeichen WERT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-linear"></a>
### STEUERN_LINEAR

This job resets the tone controls such as bass treble, fader, balance, surround to the default values

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-logistic-nr"></a>
### STEUERN_LOGISTIC_NR

Stores the logistic number Lieferumfangsnummer = number that characterizes the Anliefervariante

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_LOGISTIC_NUMBER | string | Logistic Number |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-most-3db"></a>
### STEUERN_MOST_3DB

3dB Leistungsabsenkung der MOST FOTs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-navi-map"></a>
### STEUERN_NAVI_MAP

Enables to deactivate or to erase the customer navigation map.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_ACTION | unsigned char | Action to perform 0x00 Deactivate customer navigation map 0x01 Erase customer navigation map |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-navi-simulation"></a>
### STEUERN_NAVI_SIMULATION

Activates or deactivates the navi simulation mode

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_ACTIVATION | unsigned char | 0x00 Deactivates navi simulation mode 0x01 Activates navi simulation mode |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-navi-simulation"></a>
### STATUS_NAVI_SIMULATION

Activation state of the navi simulation mode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NAVI_SIMULATION | unsigned char | 0x00 Navi simulation mode deactivated 0x01 Navi simulation mode activated |
| STAT_NAVI_SIMULATION_TEXT | string | values from table TNaviSimulationModeActivationStatus Navi simulation mode deactivated Navi simulation mode activated |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-navi-speech"></a>
### STEUERN_NAVI_SPEECH

Enables to test the navi speech output in the language that is currently set.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_COMMAND | unsigned int | Command that must be spoken out |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-next-entsource"></a>
### STEUERN_NEXT_ENTSOURCE

Enables to switch to the next or to a specified entertainment source.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_ENTSOURCE | unsigned char | Entertainment source to be set Values from table TEntSource |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-pdc"></a>
### STEUERN_PDC

Simulates the tone that is hearable at a definite distance to an obstacle

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_PDC_SIGNAL | unsigned char | Type of the PDC signal Values are 0x1 Front Tone 0x2 Rear Tone 0x3 Off |
| ARG_AUDIO_STEP | unsigned char | Audio step that corresponds to the tone that is hearable at a definite distance to the next obstacle Range from 0 (mute) to 82 (continuous tone) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-provisioning"></a>
### STEUERN_PROVISIONING

Initiates provisioning request.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-radon"></a>
### STEUERN_RADON

Sets the RADON control lead to logical High or Low.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_RADON | unsigned char | Logical value of the RAD ON lead that must be set |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-rds"></a>
### STEUERN_RDS

Enables to control the activation state of the RDS and of the TP functionalities.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_TP | unsigned char | Activation state of TP 0 TP aus, 1 TP ein, 2 TP keine Änderung |
| ARG_RDS | unsigned char | Activation state of RDS 0 RDS aus, 1 RDS ein, 2 RDS keine Änderung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ringbruch-diagnose"></a>
### STEUERN_RINGBRUCH_DIAGNOSE

Ringbruchdiagnose soll gestartet werden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sdars-ber-mode"></a>
### STEUERN_SDARS_BER_MODE

Sets the selected SDARS BER mode.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_SDARS_BER_MODE | unsigned char | BER mode that must be set values from table TSdarsBerMode |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sdars-channel"></a>
### STEUERN_SDARS_CHANNEL

Sets a definite SDARS channel.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_SDARS_CHANNEL | unsigned char | Channel that must be tuned |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sdars-factory-defaults"></a>
### STEUERN_SDARS_FACTORY_DEFAULTS

Restores the factory defaults of the SDARS tuner.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sdars-generator-frequency"></a>
### STEUERN_SDARS_GENERATOR_FREQUENCY

Sets the sine generator frequency respectively for the left and right channels.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_SDARS_GENERATOR_FREQUENCY_LEFT_WERT | unsigned int | Frequency that must be set on the left channel range 1 to 1599 (Hz*10) default 40 (400 Hz) |
| ARG_SDARS_GENERATOR_FREQUENCY_RIGHT_WERT | unsigned int | Frequency that must be set on the right channel range 1 to 1599 (Hz*10) default 100 (1000 Hz) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sdars-tuner-mode"></a>
### STEUERN_SDARS_TUNER_MODE

Sets the SDARS tuner in the selected mode.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_SDARS_TUNER_MODE | unsigned char | Mode of the SDARS tuner that must be set values from table TSdarsTunerMode |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sensor-temp"></a>
### STEUERN_SENSOR_TEMP

Simulates the temperature of a definite sensor.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_SENSOR | unsigned char | Sensor for which the temperature must be simulated |
| ARG_TEMPERATURE | char | Temperature that must be simulated |
| ARG_DURATION | unsigned char | Duration of the temperature simulation |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sinusgenerator-aus"></a>
### STEUERN_SINUSGENERATOR_AUS

Ausschalten des Sinusgenerators

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sinusgenerator-ein"></a>
### STEUERN_SINUSGENERATOR_EIN

Aktivieren des Sinusgenerators und Ausgabe auf allen ausgewählten Lautsprechern

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_FREQUENZ | unsigned int | desired frequency in Hz |
| ARG_LEVEL | unsigned char | Volumelevel 0x00-0x3F |
| ARG_KANAL | long | Bit combination of desired speakers values from table TAudioKanal |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-start-navicheck"></a>
### STEUERN_START_NAVICHECK

Initiates the special modus to check the plausibility of the navigation subsystem.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_NOTIMEOUT | unsigned char | If ARG_NOTIMEOUT = 0x00 or empty (default), |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-stop-navicheck"></a>
### STEUERN_STOP_NAVICHECK

This job stops the NAVICHECK subsystem.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-tda-atm"></a>
### STEUERN_TDA_ATM

Configures the automatic trigger of a TDA call.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_STARTTIME | unsigned char | Hour when mechanism should start (0-24) |
| ARG_INTERVALL | unsigned char | Minutes between the test calls |
| ARG_CALLID | unsigned char | 0x01, 0x02, 0x04… |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-test-antenne"></a>
### STEUERN_TEST_ANTENNE

Performs an impedance measurement of one, some or all antennas

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_ANTENNE | unsigned long | Bitcombination of antennas to be tested values from table TAntenne |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-tmc"></a>
### STEUERN_TMC

Controls the activation state (on/off) of the TMC functionality.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_TMC | unsigned char | TMC activation state that should become active. values from table TTMC |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-tmc-dab"></a>
### STEUERN_TMC_DAB

Controls the activation state (on/off) of the DAB TMC functionality.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_TMC_DAB | unsigned char | Activation state values from table TDabTmcActivationState |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-track-number"></a>
### STEUERN_TRACK_NUMBER

Sets the track number

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_TRACK | int | Track number that must be set |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-tuner-suchlauf"></a>
### STEUERN_TUNER_SUCHLAUF

Starts station search of tuner in the actual selected waveband.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_SUCHLAUF | unsigned char | Direction of the search 0x00	Descending, 0x01	Ascending, 0x02	Stop |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-usb-test"></a>
### STEUERN_USB_TEST

Stores VendorID and ProductID for diagnosis of USB mass storage recognition. Internal preparation of control unit for USB recognition (optional).

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_PRODUCTID | string | Format should be '0000' If empty then default 0000 is written. |
| ARG_VENDORID | string | Format should be '0000' If empty then default 0000 is written. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-usb-test"></a>
### STATUS_USB_TEST

Returns status of USB mass storage recognition

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_USB_TEST | unsigned char | Status of the USB test from table TUsbTestStatus WERT |
| STAT_USB_TEST_TEXT | string | Status of the USB test from table TUsbTestStatus TEXT |
| STAT_VENDORID_INT | string | VendorID stored in HeadUnit by steuern_usb_test |
| STAT_PRODUCTID_INT | string | ProductID stored in HeadUnit by steuern_usb_test |
| STAT_VENDORID_REC | string | VendorID which was detected |
| STAT_PRODUCTID_REC | string | ProductID which was detected |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-usb-hub-test"></a>
### STATUS_USB_HUB_TEST

Returns if a USB HUB is built in

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_USB_HUB_TEST_PORT_1 | unsigned char | Status of the HUB connection of the 1st USB port value from table THubConnectionState |
| STAT_USB_HUB_TEST_PORT_1_TEXT | string | Status of the HUB connection of the 1st USB port value from table THubConnectionState |
| STAT_USB_HUB_TEST_PORT_2 | unsigned char | Status of the HUB connection of the 2nd USB port value from table THubConnectionState |
| STAT_USB_HUB_TEST_PORT_2_TEXT | string | Status of the HUB connection of the 2nd USB port value from table THubConnectionState |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-test-usb-tel"></a>
### STATUS_TEST_USB_TEL

Returns status of USB mass storage recognition for USB Interface (KDZ) OR Tele-phone Snap In Adapter (SIA)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-respone from ECU |
| STAT_USB_TEST_KDZ | unsigned char | test result of KDZ |
| STAT_USB_TEST_TEXT_KDZ | string | test result KDZ text |
| STAT_VENDORID_INT_KDZ | unsigned int | vendorID KDZ |
| STAT_PRODUCTID_INT_KDZ | unsigned int | ProductID KDZ |
| STAT_VENDORID_REC_KDZ | unsigned int | rec VendorID KDZ |
| STAT_VENDORSTRING_KDZ_REC | string | rec VendorID string KDZ |
| STAT_PRODUCTID_REC_KDZ | unsigned int | rec ProductID KDZ |
| STAT_USB_TEST_SIA | unsigned char | test result of KDZ |
| STAT_USB_TEST_TEXT_SIA | string | test result KDZ text |
| STAT_VENDORID_INT_SIA | unsigned int | vendorID KDZ |
| STAT_PRODUCTID_INT_SIA | unsigned int | ProductID KDZ |
| STAT_VENDORID_REC_SIA | unsigned int | rec VendorID KDZ |
| STAT_VENDORSTRING_SIA_REC | string | rec VendorID string KDZ |
| STAT_PRODUCTID_REC_SIA | unsigned int | rec ProductID KDZ |

<a id="job-steuern-test-usb-tel"></a>
### STEUERN_TEST_USB_TEL

Stores VendorID and ProductID for diagnosis of USB mass storage recognition for USB Interface (KDZ = Kundenzugang in der Mittelkonsole) or and Telephone Snap In Adapter (SIA)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_VENDORID_KDZ | string | referenz VendorID Kundenzugang Hexvalue as string without 0x sample 0x1912 then argument is 1912 |
| ARG_PRODUCTID_KDZ | string | referenz ProduktID Kundenzugang Hexvalue as string without 0x sample 0x1912 then argument is 1912 |
| ARG_VENDORID_SIA | string | referenz VendorID SNAPIn Hexvalue as string without 0x sample 0x1912 then argument is 1912 |
| ARG_PRODUCTID_SIA | string | referenz ProduktID SNAPIn Hexvalue as string without 0x sample 0x1912 then argument is 1912 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-respone from ECU |

<a id="job-status-usb-stack-info-for-device"></a>
### STATUS_USB_STACK_INFO_FOR_DEVICE

Reads out logistical information about the four last connected USB devices four last connected IPOD Players, four last connected MTP Players and four last unrecognized USB devices

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_TYPE | unsigned char | UMS-type of requested Info 0x01 USB Stick 0x02 IPOD 0x03 MTP Player 0x04 UNKNOWN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_1_VENDORID_WERT | string | Vendor ID |
| STAT_1_PRODUCTID_WERT | string | Product ID |
| STAT_1_CLASSID_WERT | string | Class ID |
| STAT_1_SUBCLASSID_WERT | string | Subclass ID |
| STAT_1_KM_FIRST_CONNECT_WERT | unsigned long | km Stand beim ersten Connect |
| STAT_1_KM_FIRST_DISCONNECT_WERT | unsigned long | km Stand beim ersten Disconnect |
| STAT_1_KM_LAST_CONNECT_WERT | unsigned long | km Stand beim letzten Connect |
| STAT_1_KM_LAST_DISCONNECT_WERT | unsigned long | km Stand beim letzten Disconnect |
| STAT_1_CONNECTIONS_WERT | unsigned int | Anzahl der Connections |
| STAT_1_CONNECT_STATE | unsigned char | Aktueller Zustand der Connection |
| STAT_1_CONNECT_STATE_TEXT | string | Aktueller Zustand der Connection |
| STAT_1_USED_PORT | unsigned char | Port Info |
| STAT_2_VENDORID_WERT | string | Vendor ID |
| STAT_2_PRODUCTID_WERT | string | Product ID |
| STAT_2_CLASSID_WERT | string | Vendor ID |
| STAT_2_SUBCLASSID_WERT | string | Product ID |
| STAT_2_KM_FIRST_CONNECT_WERT | unsigned long | km Stand beim ersten Connect |
| STAT_2_KM_FIRST_DISCONNECT_WERT | unsigned long | km Stand beim ersten Disconnect |
| STAT_2_KM_LAST_CONNECT_WERT | unsigned long | km Stand beim letzten Connect |
| STAT_2_KM_LAST_DISCONNECT_WERT | unsigned long | km Stand beim letzten Disconnect |
| STAT_2_CONNECTIONS_WERT | unsigned int | Anzahl der Connections |
| STAT_2_CONNECT_STATE | unsigned char | Aktueller Zustand der Connection |
| STAT_2_CONNECT_STATE_TEXT | string | Aktueller Zustand der Connection |
| STAT_2_USED_PORT | unsigned char | Port Info |
| STAT_3_VENDORID_WERT | string | Vendor ID |
| STAT_3_PRODUCTID_WERT | string | Product ID |
| STAT_3_CLASSID_WERT | string | Vendor ID |
| STAT_3_SUBCLASSID_WERT | string | Product ID |
| STAT_3_KM_FIRST_CONNECT_WERT | unsigned long | km Stand beim ersten Connect |
| STAT_3_KM_FIRST_DISCONNECT_WERT | unsigned long | km Stand beim ersten Disconnect |
| STAT_3_KM_LAST_CONNECT_WERT | unsigned long | km Stand beim letzten Connect |
| STAT_3_KM_LAST_DISCONNECT_WERT | unsigned long | km Stand beim letzten Disconnect |
| STAT_3_CONNECTIONS_WERT | unsigned int | Anzahl der Connections |
| STAT_3_CONNECT_STATE | unsigned char | Aktueller Zustand der Connection |
| STAT_3_CONNECT_STATE_TEXT | string | Aktueller Zustand der Connection |
| STAT_3_USED_PORT | unsigned char | Port Info |
| STAT_4_VENDORID_WERT | string | Vendor ID |
| STAT_4_PRODUCTID_WERT | string | Product ID |
| STAT_4_CLASSID_WERT | string | Vendor ID |
| STAT_4_SUBCLASSID_WERT | string | Product ID |
| STAT_4_KM_FIRST_CONNECT_WERT | unsigned long | km Stand beim ersten Connect |
| STAT_4_KM_FIRST_DISCONNECT_WERT | unsigned long | km Stand beim ersten Disconnect |
| STAT_4_KM_LAST_CONNECT_WERT | unsigned long | km Stand beim letzten Connect |
| STAT_4_KM_LAST_DISCONNECT_WERT | unsigned long | km Stand beim letzten Disconnect |
| STAT_4_CONNECTIONS_WERT | unsigned int | Anzahl der Connections |
| STAT_4_CONNECT_STATE | unsigned char | Aktueller Zustand der Connection |
| STAT_4_CONNECT_STATE_TEXT | string | Aktueller Zustand der Connection |
| STAT_4_USED_PORT | unsigned char | Port Info |
| JOB_STATUS | string | OKAY, if without errors table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-daten from ECU |

<a id="job-steuern-volumeaudio"></a>
### STEUERN_VOLUMEAUDIO

Adjusts the volume of a definite audio signal

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_LEVEL | char | Desired Volumelevel (Range 0 to 63) or OffsetEntertainment (Range -11 to 11) |
| ARG_AUDIO_SIGNAL | unsigned char | Adjusts the volume (only 0x00, 0x0B, 0x0C) or OffsetEntertainment (only 0x01 .. 0x0A) of a definite audio signal from table TAudioSignal |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-volumeaudio-default"></a>
### STEUERN_VOLUMEAUDIO_DEFAULT

Set Volumeaudio default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-watchdog-trigger-stop"></a>
### STEUERN_WATCHDOG_TRIGGER_STOP

Unterbindet das regelmäßige Rücksetzen des Applikations-Watchdogs nach ARG_TIME_WATCHDOG Sekunden. Wenn ARG_TIME_WATCHDOG nicht angegeben wird, wird der Wert 0 benutzt.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_TIME_WATCHDOG | unsigned int | Beschreibung: z.B. ARG_TIME_WATCHDOG = 4 bedeutet Abschalten des Watchdog-Triggers nach 4 Sekunden. nur positiven Zahlen und die 0. Skalierung: 1 entspricht 1 Sekunde |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-waveband"></a>
### STEUERN_WAVEBAND

Activates the desired waveband.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_WAVEBAND | unsigned char | see table TWaveband |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-zentrale-registry-sollkonfiguration"></a>
### STEUERN_ZENTRALE_REGISTRY_SOLLKONFIGURATION

Die aktuelle Registry wird als Default Registry gespeichert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DELAY_WERT | unsigned char | Zeit in Sekunden wann Job wieder ausgeführt werden kann |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-test-microphone"></a>
### STATUS_TEST_MICROPHONE

Returns the result of the microphone test performed with steuern_test_microphone.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MICROPHONE | unsigned char | Microphone that has been tested values from table TMicrophone |
| STAT_MICROPHONE_TEXT | string | Microphone that has been tested values from table TMicrophone |
| STAT_TEST_MICROPHONE | unsigned char | Status of the test values from table TTestStatus |
| STAT_TEST_MICROPHONE_TEXT | string | Status of the test values from table TTestStatus |
| STAT_DETECTED_LEVEL_WERT | unsigned char | Level that has been detected Range 0x00 to 0x3F |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-test-videoeingang"></a>
### STATUS_TEST_VIDEOEINGANG

Returns the results of the signal tests performed with steuern_test_videoeingang.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_QUELLE | unsigned long | Video source from which the signal has been tested values from table TVideoQuelle or combination of the values |
| STAT_TEST_VIDEOEINGANG | unsigned char | Status of the test values from table TTestStatus |
| STAT_TEST_VIDEOEINGANG_TEXT | string | Status of the test values from table TTestStatus |
| STAT_ANZAHL_FEHLERHAFTE_SIGNALE_WERT | unsigned char | Number of the faulty input signals |
| STAT_FEHLER_1_QUELLE | unsigned long | Xth faulty source (=incoming signal) values from table TVideoQuelle |
| STAT_FEHLER_1_QUELLE_TEXT | string | Xth faulty source (=incoming signal) values from table TVideoQuelle |
| STAT_FEHLER_1_FEHLERART_SIGNAL | unsigned char | Type of error of the Xth faulty incoming signal values from table TVideoeingangFehlerArt |
| STAT_FEHLER_1_FEHLERART_SIGNAL_TEXT | string | Type of error of the Xth faulty incoming signal values from table TVideoeingangFehlerArt |
| STAT_FEHLER_1_EINGANG | unsigned long | FBAS input on which the faulty signal has been received values from table TFBasEingang |
| STAT_FEHLER_1_EINGANG_TEXT | string | FBAS input on which the faulty signal has been received values from table TFBasEingang |
| STAT_FEHLER_1_VIDEOSWITCH_EINGANG | unsigned int | Input of the video switch on which the faulty signal has been routed values from table TEingangVideoSwitch |
| STAT_FEHLER_1_VIDEOSWITCH_EINGANG_TEXT | string | Input of the video switch on which the faulty signal has been routed values from table TEingangVideoSwitch |
| STAT_FEHLER_1_VIDEOSWITCH_AUSGANG | unsigned int | Output of the video switch on which the faulty signal has been routed values from table TAusgangVideoSwitch |
| STAT_FEHLER_1_VIDEOSWITCH_AUSGANG_TEXT | string | Output of the video switch on which the faulty signal has been routed values from table TAusgangVideoSwitch |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-videoverbindung"></a>
### STATUS_VIDEOVERBINDUNG

Returns if a video connection is active and if yes which

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HERSTELLUNG_VIDEOVERBINDUNG | unsigned char | Status of the connection establishing values from table THerstellungStatus |
| STAT_HERSTELLUNG_VIDEOVERBINDUNG_TEXT | string | Status of the connection establishing values from table THerstellungStatus |
| STAT_HERSTELLUNG_FEHLER | unsigned char | Error of the connection establishing values from table THerstellungFehler |
| STAT_HERSTELLUNG_FEHLER_TEXT | string | Error of the connection establishing values from table THerstellungFehler |
| STAT_QUELLE | long | Video source of the current video connection values from table TVideoQuelle |
| STAT_QUELLE_TEXT | string | Video source of the current video connection values from table TVideoQuelle |
| STAT_SENKEN | unsigned int | Video sinks of the current video connection values from table TVideoSenke |
| STAT_SENKEN_TEXT | string | Video sinks of the current video connection values from table TVideoSenke |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-aktives-sprachpaket"></a>
### STATUS_AKTIVES_SPRACHPAKET

Reads out which language for speech recognition system is currently stored into the flash memory

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AKTIVES_SPRACHPAKET | unsigned char | Language for speech recognition system that is currently stored into the flash memory values from table TLanguage |
| STAT_AKTIVES_SPRACHPAKET_TEXT | string | Language for speech recognition system that is currently stored into the flash memory values from table TLanguage |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-cpu-auslastung"></a>
### STATUS_CPU_AUSLASTUNG

Reads out the current system load of the CPU(s) in per cent.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CPU1_WERT | unsigned char | Current load of CPU1 in per cent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ethernet-connection-state"></a>
### STATUS_ETHERNET_CONNECTION_STATE

Returns the activation state of all Ethernet connections

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FLASH_ETHERNET_CONNECTION_STATE | unsigned char | State of the Ethernet connection for flash process values from table TEthernetActivationState |
| STAT_FLASH_ETHERNET_CONNECTION_STATE_TEXT | string | State of the Ethernet connection for flash process values from table TEthernetActivationState |
| STAT_RSE_ETHERNET_CONNECTION_STATE | unsigned char | State of the Ethernet connection for flash process values from table TEthernetActivationState |
| STAT_RSE_ETHERNET_CONNECTION_STATE_TEXT | string | State of the Ethernet connection for flash process values from table TEthernetActivationState |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-get-ipconfig"></a>
### STATUS_GET_IPCONFIG

Reads out the actual ipconfig of the Ethernet interface of the HeadUnit.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FORMAT | unsigned char | 0x00  IPv4, 0x01  IPv6 |
| STAT_IPADDRESS | string | IP Adress e.g. 10.230.1.60 |
| STAT_NETMASK | string | Netmask e.g. 255.255.255.0 |
| STAT_GATEWAY | string | default Gateway Adress e.g. 10.230.1.1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lade-sprachpaket"></a>
### STATUS_LADE_SPRACHPAKET

Returns the status of the loading process started with the job steuern_lade_sprachpaket.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LADEVORGANG_SPRACHPAKET | unsigned char | Status of the loading process values from table TLadeVorgangSprachpaket |
| STAT_LADEVORGANG_SPRACHPAKET_TEXT | string | Status of the loading process values from table TLadeVorgangSprachpaket |
| STAT_PERCENT_COMPLETE_WERT | unsigned char | Completion percentage in percent of the loading process |
| STAT_FEHLERURSACHE | unsigned char | Error cause values from table TFehlerursacheSprachpaket |
| STAT_FEHLERURSACHE_TEXT | string | Error cause values from table TFehlerursacheSprachpaket |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-language"></a>
### STATUS_LANGUAGE

Reads out the languag that is currently active.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LANGUAGE | unsigned char | Language that is currently active values from table TLanguage |
| STAT_LANGUAGE_TEXT | string | Language that is currently active values from table TLanguage |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-menu"></a>
### STATUS_MENU

Reads out the menu that is currently active

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MENU_WERT | long | ID of the menu that is currently active (for RSE left display) |
| STAT_MENU_RSE_RIGHT_WERT | long | ID of the menu that is currently active (for RSE right display). (00000000 for head-unit) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-selbsttest"></a>
### STATUS_SELBSTTEST

Returns the mute status of the current entertainment source.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SELBSTTEST_ROUTINE | long | Routine that is being or that has been performed values from Table TSelbsttestRoutine |
| STAT_SELBSTTEST | unsigned char | Status of the test values from table TTestStatus |
| STAT_SELBSTTEST_TEXT | string | Status of the test values from table TTestStatus |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-test-auxverbindung"></a>
### STATUS_TEST_AUXVERBINDUNG

Returns the results of the impedance measurement performed with steuern_test_aux_verbindung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VERBINDUNG | unsigned int | Aux connection that has been tested Values from table TAuxVerbindung |
| STAT_TEST_AUXVERBINDUNG | unsigned char | Status of the test as integer Integer values from table TTestStatus |
| STAT_TEST_AUXVERBINDUNG_TEXT | string | Status of the test as text Integer values from table TTestStatus |
| STAT_ANZAHL_FEHLERHAFTE_VERBINDUNGEN_WERT | unsigned char | Number of the faulty aux connections |
| STAT_FEHLER_1_VERBINDUNG | unsigned int | Xth faulty connection values from table TAuxVerbindung |
| STAT_FEHLER_1_VERBINDUNG_TEXT | string | Xth faulty connection values from table TAuxVerbindung |
| STAT_FEHLER_1_FEHLERART_VERBINDUNG | unsigned char | Type of error values from table TVerbindungFehlerArt |
| STAT_FEHLER_1_FEHLERART_VERBINDUNG_TEXT | string | Type of error values from table TVerbindungFehlerArt |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-test-verbau"></a>
### STATUS_TEST_VERBAU

Returns the result of the test of external interfaces performed with steuern_test_verbau

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VERBAU_ROUTINE | long | Routine that has been tested values from table TVerbauRoutine |
| STAT_VERBAU_ROUTINE_TEXT | string | Routine that has been tested values from table TVerbauRoutine only well known bitcombinations are shown |
| STAT_TEST_VERBAU | unsigned char | Status of the test values from table TTestStatus |
| STAT_TEST_VERBAU_TEXT | string | Status of the test values from table TTestStatus |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-clear-fault-tracking"></a>
### STEUERN_CLEAR_FAULT_TRACKING

Clears down to zero the whole area where the extended fault tracking datasets are stored. It also removes the DTC Error_Software from the secondary error memory.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ethernet-connection-state"></a>
### STEUERN_ETHERNET_CONNECTION_STATE

Enables to control the activation state of the selected Ethernet connection.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_ETHERNET_CONNECTION | unsigned char | Ethernet connection that must be activated/deactivated values from table TEthernetConnection |
| ARG_ACTIVATION_STATE | unsigned char | Activation state of the Ethernet connection values from table TEthernetActivationState |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-internal-reset"></a>
### STEUERN_INTERNAL_RESET

Resets the head-unit with following properties The applications are stored properly before performing the reset The MOST light remains on

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lade-sprachpaket"></a>
### STEUERN_LADE_SPRACHPAKET

Enables to load the language for speech recognition system and perhaps the speech for the Navi out from the HDD into the Flash memory.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_SPRACHPAKET | unsigned char | Language that must be loaded values from table TLanguage |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-language"></a>
### STEUERN_LANGUAGE

Activates the desired languag.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_LANGUAGE | unsigned char | Language that must be activated values from table TLanguage |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lautsprecher-impedanzmessung"></a>
### STEUERN_LAUTSPRECHER_IMPEDANZMESSUNG

Enables to test a loudspeaker connection by performing an impedance measurement.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_FREQUENZ | unsigned int | Frequency used for the impedance measurement Range: 20 – 20000 Hz |
| ARG_LEVEL | unsigned char | Level of the signal used for the impedance measurement Increment value, expressed in hexadecimal |
| ARG_KANAL | long | Channel(s) on which the impedance measurement must be performed Integer values from table TAudioKanal |
| ARG_MESSDAUER | unsigned int | Duration of the measurement Range: 50 – 1000 ms |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-menu"></a>
### STEUERN_MENU

Activates the desired menu.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_MENU | long | ID of the menu that must be activated (for RSE: left display) |
| ARG_MENU_RSE_RIGHT | long | ID of the menu that must be activated on the 2nd RSE HMI (right display) 00000000 if head-unit |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-selbsttest"></a>
### STEUERN_SELBSTTEST

Performs a test of internal functions and components.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_SELBSTTEST_ROUTINE | long | Routine that must be performed values from table TSelbsttestRoutine |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-signalausgabe"></a>
### STEUERN_SIGNALAUSGABE

Modifies the video output signal

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_SIGNALART | unsigned char | Type of signal to give out values from table TSignalArt |
| ARG_AUSGANG | unsigned int | Output on which the signal has to be given out values from table TVideoAusgang or combination of the values |
| ARG_TIMEOUT | unsigned char | Duration of the signal in seconds When the timer expires, the Head-Unit must return to normal operation mode Allowed values: [0,…,30] and 255 0 = return to normal operation mode for the corresponding output 255 = no timeout |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-signalausgabe-aus"></a>
### STEUERN_SIGNALAUSGABE_AUS

Ends the output of the signal that was generated with steuern_signalausgabe

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_AUSGANG | unsigned int | Output on which the signal output has to be ended values from table TVideoAusgang or combination of the values |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-test-auxverbindung"></a>
### STEUERN_TEST_AUXVERBINDUNG

Performs an impedance measurement of one or all auxiliary connections

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_VERBINDUNG | unsigned int | Connection to be tested values from table TAuxVerbindung (Each channel is defined as a special Bit) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-test-microphone"></a>
### STEUERN_TEST_MICROPHONE

Enables to test a definite microphone by generating a sine tone and starting in parallel the recording mode of the microphone

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_MICROPHONE | unsigned char | Microphone that must be tested values from table TMicrophone |
| ARG_DURATION | unsigned char | Duration in seconds for which the sine tone is generated and the recording mode is active. Default 3 seconds |
| ARG_LEVEL | unsigned char | Level of the sine signal range 0x10 to 0x3F, default 0x18 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-test-verbau"></a>
### STEUERN_TEST_VERBAU

Performs a test of one, some or all external interfaces

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_VERBAU_ROUTINE | long | Routine that must be tested values from table TVerbauRoutine |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-test-videoeingang"></a>
### STEUERN_TEST_VIDEOEINGANG

Tests the signal(s) from one (some) definite video source(s).

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_QUELLE | long | Video source from which the signal will be tested values from Table TVideoQuelle |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-very-hard-reset"></a>
### STEUERN_VERY_HARD_RESET

Resets the head-unit analogue to a battery reset.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-videoverbindung"></a>
### STEUERN_VIDEOVERBINDUNG

Establishes a video connection between a video source and some video sinks

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_QUELLE | long | Video source from which the signal will be given out Values from table TVideoQuelle |
| ARG_SENKEN | unsigned int | Sink(s) on which the signal will be given out Values from table TVideoSenke |
| ARG_TIMEOUT | unsigned char | Duration of the signal in seconds When the timer expires, the connection that was active before the diagnosis test must be restored. Allowed values: [0,…,30] and 255 0 = return to normal operation mode for the corresponding output 255 = no timeout |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-videoverbindung-aus"></a>
### STEUERN_VIDEOVERBINDUNG_AUS

Ends the connection that has been established with the job steuern_videoverbindung and restores the normal operation mode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fan-history"></a>
### STATUS_FAN_HISTORY

Reads out the fan histogram.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TIME_FAN_ALL | long | Whole operating time of the fan in seconds |
| STAT_OCCURENCES_FAN_SWITCH_ON | long | Number of switch ON occurrences |
| STAT_TIME_FAN_OFF | long | Time in seconds the fan is not running |
| STAT_TIME_FAN_FREQUENCY_RANGE1 | long | Time in seconds the fan is running at frequency 0Hz &lt; f1 &lt;= 5Hz |
| STAT_TIME_FAN_FREQUENCY_RANGE2 | long | Time in seconds the fan is running at frequency 5Hz &lt; f1 &lt;= 10Hz |
| STAT_TIME_FAN_FREQUENCY_RANGE3 | long | Time in seconds the fan is running at frequency 10Hz &lt; f1 &lt;= 15Hz |
| STAT_TIME_FAN_FREQUENCY_RANGE4 | long | Time in seconds the fan is running at frequency 15Hz &lt; f1 &lt;= 20Hz |
| STAT_TIME_FAN_FREQUENCY_RANGE5 | long | Time in seconds the fan is running at frequency 20Hz &lt; f1 &lt;= 25Hz |
| STAT_TIME_FAN_FREQUENCY_RANGE6 | long | Time in seconds the fan is running at frequency 25Hz &lt; f1 &lt;= 30Hz |
| STAT_TIME_FAN_FREQUENCY_RANGE7 | long | Time in seconds the fan is running at frequency 30Hz &lt; f1 &lt;= 35Hz |
| STAT_TIME_FAN_FREQUENCY_RANGE8 | long | Time in seconds the fan is running at frequency 35Hz &lt; f1 &lt;= 40Hz |
| STAT_TIME_FAN_FREQUENCY_RANGE9 | long | Time in seconds the fan is running at frequency 40Hz &lt; f1 &lt;= 45Hz |
| STAT_TIME_FAN_FREQUENCY_RANGE10 | long | Time in seconds the fan is running at frequency 45Hz &lt; f1 &lt;= 50Hz |
| STAT_TIME_FAN_FREQUENCY_RANGE11 | long | Time in seconds the fan is running at frequency 50Hz &lt; f1 &lt;= 55Hz |
| STAT_TIME_FAN_FREQUENCY_RANGE12 | long | Time in seconds the fan is running at frequency 55Hz &lt; f1 &lt;= 60Hz |
| STAT_TIME_FAN_FREQUENCY_RANGE13 | long | Time in seconds the fan is running at frequency 60Hz &lt; f1 &lt;= 65Hz |
| STAT_TIME_FAN_FREQUENCY_RANGE14 | long | Time in seconds the fan is running at frequency 65Hz &lt; f1 &lt;= 70Hz |
| STAT_TIME_FAN_FREQUENCY_RANGE15 | long | Time in seconds the fan is running at frequency 70Hz &lt; f1 &lt;= 75Hz |
| STAT_TIME_FAN_FREQUENCY_RANGE16 | long | Time in seconds the fan is running at frequency 75Hz &lt; f1 &lt;= 80Hz |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-luefter"></a>
### STATUS_LUEFTER

Returns if and at which speed the fan is running.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LUEFTER | unsigned char | Status of the fan values from table TLuefterStatus |
| STAT_LUEFTER_TEXT | string | Status of the fan values from table TLuefterStatus |
| STAT_LUEFTER_DREHZAHL_WERT | unsigned int | Current frequency of fan in Hz |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-luefter-control-data"></a>
### STATUS_LUEFTER_CONTROL_DATA

Reads out the current control parameters of the fan

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_POWER_AMPLIFIER_THRESHOLD1 | unsigned char | Power amplifier temperature threshold 1 in Celsius |
| STAT_POWER_AMPLIFIER_THRESHOLD2 | unsigned char | Power amplifier temperature threshold 2 in Celsius |
| STAT_POWER_AMPLIFIER_THRESHOLD3 | unsigned char | Power amplifier temperature threshold 3 in Celsius |
| STAT_FOT_THRESHOLD1 | unsigned char | FOT unit temperature threshold 1 in Celsius |
| STAT_FOT_THRESHOLD2 | unsigned char | FOT unit temperature threshold 2 in Celsius |
| STAT_FOT_THRESHOLD3 | unsigned char | FOT unit temperature threshold 3 in Celsius |
| STAT_GYRO_THRESHOLD1 | unsigned char | Gyro temperature threshold 1 in Celsius |
| STAT_GYRO_THRESHOLD2 | unsigned char | Gyro temperature threshold 2 in Celsius |
| STAT_GYRO_THRESHOLD3 | unsigned char | Gyro temperature threshold 3 in Celsius |
| STAT_SH4A_THRESHOLD1 | unsigned char | SH4A temperature threshold 1 in Celsius |
| STAT_SH4A_THRESHOLD2 | unsigned char | SH4A temperature threshold 2 in Celsius |
| STAT_SH4A_THRESHOLD3 | unsigned char | SH4A temperature threshold 3 in Celsius |
| STAT_HDD_THRESHOLD1 | unsigned char | HDD temperature threshold 1 in Celsius |
| STAT_HDD_THRESHOLD2 | unsigned char | HDD temperature threshold 2 in Celsius |
| STAT_HDD_THRESHOLD3 | unsigned char | HDD temperature threshold 3 in Celsius |
| STAT_DVD_THRESHOLD1 | unsigned char | DVD temperature threshold 1 in Celsius |
| STAT_DVD_THRESHOLD2 | unsigned char | DVD temperature threshold 2 in Celsius |
| STAT_DVD_THRESHOLD3 | unsigned char | DVD temperature threshold 3 in Celsius |
| STAT_FAN_QUIETMODE_SPEED | unsigned int | Fan rotation speed in Hz of the quietmode (= minimal fan rotation speed of the fan) |
| STAT_FAN_MAXIMAL_SPEED | unsigned int | Maximal fan rotation speed in Hz |
| STAT_TEMPERATURE_HYSTERESIS | unsigned char | Hysteresis of the temperature thresholds |
| STAT_DELAY_TEMP_MEASUREMENT | unsigned int | Delay in seconds between 2 temperature measurements that are used for generating the sensor histograms Default: 60 seconds (refer to the histogram jobs) |
| STAT_DELAY_WRITING_NON_VOLATILE_MEMORY | unsigned int | Delay in seconds between 2 occurrences of the non-volatile memory writing event 0xFFFF = once at rundown Default 0xFFFF = once at rundown Delivery state 0xFFFF = once at rundown |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-clear-fan-history"></a>
### STEUERN_CLEAR_FAN_HISTORY

Clears the fan histogram

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-luefter"></a>
### STEUERN_LUEFTER

Triggers the fan rotation at its maximal rotation speed

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_DURATION | unsigned char | Duration in seconds for which the fan will rotate Range 0…30 seconds |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-luefter-control-data"></a>
### STEUERN_LUEFTER_CONTROL_DATA

Enables to modify one or some control parameters of the fan

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_POWER_AMPLIFIER_THRESHOLD1 | unsigned char | Power amplifier temperature threshold 1 in Celsius |
| ARG_POWER_AMPLIFIER_THRESHOLD2 | unsigned char | Power amplifier temperature threshold 2 in Celsius |
| ARG_POWER_AMPLIFIER_THRESHOLD3 | unsigned char | Power amplifier temperature threshold 3 in Celsius |
| ARG_FOT_THRESHOLD1 | unsigned char | FOT unit temperature threshold 1 in Celsius |
| ARG_FOT_THRESHOLD2 | unsigned char | FOT unit temperature threshold 2 in Celsius |
| ARG_FOT_THRESHOLD3 | unsigned char | FOT unit temperature threshold 3 in Celsius |
| ARG_GYRO_THRESHOLD1 | unsigned char | Gyro temperature threshold 1 in Celsius |
| ARG_GYRO_THRESHOLD2 | unsigned char | Gyro temperature threshold 2 in Celsius |
| ARG_GYRO_THRESHOLD3 | unsigned char | Gyro temperature threshold 3 in Celsius |
| ARG_SH4A_THRESHOLD1 | unsigned char | SH4A temperature threshold 1 in Celsius |
| ARG_SH4A_THRESHOLD2 | unsigned char | SH4A temperature threshold 2 in Celsius |
| ARG_SH4A_THRESHOLD3 | unsigned char | SH4A temperature threshold 3 in Celsius |
| ARG_HDD_THRESHOLD1 | unsigned char | HDD temperature threshold 1 in Celsius |
| ARG_HDD_THRESHOLD2 | unsigned char | HDD temperature threshold 2 in Celsius |
| ARG_HDD_THRESHOLD3 | unsigned char | HDD temperature threshold 3 in Celsius |
| ARG_DVD_THRESHOLD1 | unsigned char | DVD temperature threshold 1 in Celsius |
| ARG_DVD_THRESHOLD2 | unsigned char | DVD temperature threshold 2 in Celsius |
| ARG_DVD_THRESHOLD3 | unsigned char | DVD temperature threshold 3 in Celsius |
| ARG_FAN_QUIETMODE_SPEED | unsigned int | Fan rotation speed in Hz of the quietmode (= minimal fan rotation speed of the fan) |
| ARG_FAN_MAXIMAL_SPEED | unsigned int | Maximal fan rotation speed in Hz |
| ARG_TEMPERATURE_HYSTERESIS | unsigned char | Hysteresis of the temperature thresholds |
| ARG_DELAY_TEMP_MEASUREMENT | unsigned int | Delay in seconds between 2 temperature measurements that are used for generating the sensor histograms Default: 60 seconds (refer to the histogram jobs) |
| ARG_DELAY_WRITING_NON_VOLATILE_MEMORY | unsigned int | Delay in seconds between 2 occurrences of the non-volatile memory writing event 0xFFFF = once at rundown Default 0xFFFF = once at rundown Delivery state 0xFFFF = once at rundown |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-af-tp-dab"></a>
### STATUS_AF_TP_DAB

Reads out the activation state of the TP, RDS and AF functionalities.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FOLLOWING_DAB_FM | unsigned char | Activation state of Following DAB FM Values from table TFollowingDabFm |
| STAT_FOLLOWING_DAB_FM_TEXT | string | Activation state of Following DAB FM Values from table TFollowingDabFm |
| STAT_FOLLOWING_DAB_DAB | unsigned char | Activation state of Following DAB DAB Values from table TFollowingDabDab |
| STAT_FOLLOWING_DAB_DAB_TEXT | string | Activation state of Following DAB DAB Values from table TFollowingDabDab |
| STAT_TP_DAB | unsigned char | Activation state of TP DAB Values from table TTpDab |
| STAT_TP_DAB_TEXT | string | Activation state of TP DAB Values from table TTpDab |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-aktive-antenne-dab"></a>
### STATUS_AKTIVE_ANTENNE_DAB

Reads out which DAB antenna is currently active.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AKTIVE_ANTENNE_DAB | unsigned char | Antenna that is currently active Values from table TAktiveAntenneDAB |
| STAT_AKTIVE_ANTENNE_DAB_TEXT | string | Antenna that is currently active Values from table TAktiveAntenneDAB |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bit-error-rate-dab"></a>
### STATUS_BIT_ERROR_RATE_DAB

Measures the quality of the reception of the current DAB ensemble.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BIT_ERROR_RATE_DAB | long | Reception quality of the current DAB ensemble expressed in bit error rate |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-frequenz-dab"></a>
### STATUS_FREQUENZ_DAB

Get back the currently active DAB frequency

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FREQUENZ_DAB | string | Current DAB frequency 3 Bytes are needed for this result |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-signal-dab"></a>
### STATUS_SIGNAL_DAB

Reads out if a valid DAB signal is available.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SIGNAL_DAB | unsigned char | Status of the current DAB signal as integer Integer values from table TSignalDab |
| STAT_SIGNAL_DAB_TEXT | string | Status of the current DAB signal as integer Integer values from table TSignalDab |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-af-tp-dab"></a>
### STEUERN_AF_TP_DAB

Enables to control the activation state of the RDS and of the TP functionalities.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_FOLLOWING_DAB_FM | unsigned char | Activation state of Following DAB FM Values from table TFollowingDabFm |
| ARG_FOLLOWING_DAB_DAB | unsigned char | Activation state of Following DAB DAB Values from table TFollowingDabDab |
| ARG_TP_DAB | unsigned char | Activation state of TP DAB Values from table TTpDab |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-aktive-antenne-dab"></a>
### STEUERN_AKTIVE_ANTENNE_DAB

Enables to control the activation state of both DAB antennae

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_AKTIVE_ANTENNE_DAB | unsigned char | Antenna(e) that should be activated Values from table TAktiveAntenneDAB default ist 0x03 Both antennas |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-frequenz-dab"></a>
### STEUERN_FREQUENZ_DAB

Set the DAB frequency.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_FREQUENZ_DAB | string | Frequency to be set. 3 ASCII Bytes are needed for this argument sample ABC |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-initialisierung"></a>
### STATUS_INITIALISIERUNG

Gibt wieder, ob das komplette Steuergerät initialisiert wurde

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_INITIALISIERUNG | unsigned char | Status der Initialisierung 0   Nicht initialisiert 1   IO initialisiert 255 NIO initialisiert |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-rescue-mode"></a>
### STEUERN_RESCUE_MODE

Resets the HeadUnit in a stable bootloadermode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-individualdata-liste"></a>
### LESEN_INDIVIDUALDATA_LISTE

Lesen eines Listeneintrags der Individualisierungsdaten KWP2000: $31 ReadDataByLocalIdentifier $80 recordLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_LISTENTRY | unsigned int | Nummer des angeforderten Listenelements (0,1,2,...) 0x0000 = Anforderung, das 1. Listelement zu senden 0x0001 = Anforderung, das 2. Listelement zu senden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RET_ENTRYNR | unsigned int | Nummer des zurückgegebenen Listenelements (0,1,2,...) |
| RET_STATUS | unsigned char | Information ob aktuelles Listenelement das Letzte ist 0xFF	letztes Listenelement 0xFE	Listenelement nicht gefunden 0x00 	nicht letztes Listenelement |
| RET_FROMWHERE | unsigned char | Individualdaten müssen via CAN oder MOST oder XY angesprochen werden. 0x00	via CAN 0x01	via MOST 0x02  via CAN-PIADiensteanfrage 0x03  via Naviadressbuchanfrage ...	via XY... |
| RET_DATA | binary | Listentry zur Individualdaten-Abfrage 1.Byte, Diagnoseadresse (for future use), diese gibt Auskunft von welchem SG die Individualdaten verwaltet werden. z.B. 0x63  2.Byte:	Sind die Daten Car- oder Key- Memory relevant? 0x01	CarMemory relevant 0x02	KeyMemory relevant 0x03	CarMemory relevant und KeyMemory relevant  3.Byte:	Individualdaten können via CAN oder MOST oder XY erreicht werden. 0x00	via CAN 0x01	via MOST 0x02  via CAN-PIADiensteanfrage 0x03  via Naviadressbuchanfrage ...	via XY...  4.Byte und Folgende siehe Spec Datenrettung  |
| RET_COMMENT | string | Kommentarspalte des Entries |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-lese-individualdata"></a>
### LESE_INDIVIDUALDATA

Lesen von Individualisierungsdaten Modus   : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_KEYID | unsigned char | 0x00       CarMemory 0x01..0x04 Schlüsselnummer dem der RET_DATA zugeordnet ist 0xFF	   Aktuell gesteckter Schlüssel ist RET_DATA zugeordnet actual not used by CICR |
| ARG_BLOCKNR | unsigned long | Zu übertragende Blocknummer (Zähler) bei langen Datenstreams z.B. 0x01020304 (4 Bytes) falls nicht verwendet als Dummy mitschleifen |
| ARG_FROMWHERE | unsigned char | Strategie switch actual must be 1 |
| ARG_INQY_LEN | unsigned char | Länge des folgenden Anfragedatenstreams z.B. 0x02 für 2 Byte |
| ARG_INQY_DATA | string | ASCII-codiert Anfrage Individualdatenstream in CICR ist es der memObjectidentifier z.B. 100200001000 |
| ARG_RESP_LEN | unsigned char | Länge der folgenden Information wie die Antwort erhalten wird. not used by CICR |
| ARG_RESP_DATA | string | ASCII-codiert Information wie die Antwort erhalten wird: not used by CICR |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RET_STATUS | unsigned char | 0xFF letztes oder einziges element des Datenstreams 0x00 es folgen weitere Datenstreamstücke 0x01 komplette Wiederholung erforderlich nötig wegen 1k Grenze der Ediabas-results |
| RET_BLOCKNR | unsigned long | Übertragende Blocknummer (Zähler) bei langen Datenstreams z.B. 0x01020304 falls nicht verwendet als Dummy mitschleifen not used by CICR |
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
| ARG_KEYID | unsigned char | 0x00       CarMemory 0x01..0x04 Schlüsselnummer dem der ARG_DATA zugeordnet ist 0xFF	   Aktuell gesteckter Schlüssel ist ARG_DATA zugeordnet actual not used by CICR |
| ARG_BLOCKNR | unsigned long | Zu übertragende Blocknummer (Zähler) bei langen Datenstreams z.B. 0x01020304 (4 Bytes) falls nicht verwendet als Dummy mitschleifen |
| ARG_FROMWHERE | unsigned char | Strategie switch actual must be 1 |
| ARG_STATUS | unsigned char | 0xFF letztes oder einziges element des Datenstreams 0x00 es folgen weitere Datenstreamstücke |
| ARG_WRITE_LEN | unsigned char | Länge des folgenden Schreibauftrags z.B. 0x02 für 2 Byte |
| ARG_WRITE_DATA | string | ASCII-codiert Schreibauftrag für Individualdatenstream in CICR ist es der memObjectidentifier z.B. 100200001000 |
| ARG_W_RESP_LEN | unsigned char | Optional, Laenge des folgenden Antwortfilters not used by CICR |
| ARG_W_RESP_DATA | string | ASCII-codiert, Optional, Antwortfilter des Schreibauftrags not used by CICR |
| ARG_LEN | int | Länge des Individualisierungs Datenstream oder -streamstücks |
| ARG_DATA | string | ASCII-codiert Datenstream |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RET_STATUS | unsigned char | Rückmeldungen, Fehlercodes z.B. OK 0x00 oder NOTOK 0x01 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-baureihe"></a>
### STEUERN_BAUREIHE

Sets the HeadUnit to a desired Baureihe of the Gateway table

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_BAUREIHE | unsigned char | the desired Baureihe of the Gateway table as uchar 0x01 (L1),0x02 (L2),0x04 (L4),0x06 (L6), 0xFF (FF) 'FF' means all Baureihen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-baureihe"></a>
### STATUS_BAUREIHE

Reads out the actual Baureihe of the Gateway table

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BAUREIHE | string | the actual Baureihe of the Gateway table as string 'L1','L2','L4','L6','FF' 'FF' means all Baureihen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-nwm-config-notok"></a>
### STEUERN_NWM_CONFIG_NOTOK

Sends a Config.NotOk on the MOST Bus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NOTOK | unsigned char | 0x00  = Nachricht wird versendet 0xFF = Nachricht kann nicht versendet werden, Grund unbekannt |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _RESPONSE | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hmi-version"></a>
### STATUS_HMI_VERSION

Reads out the flashed Buildname

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HMI_VERSION | string | Present HMI version like shown in the developer menue |
| STAT_SVS_VERSION | string | Present SVS version like shown in the developer menue |
| STAT_TEXT_VERSION | string | Present TEXT version like shown in the developer menue |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-komp-id"></a>
### STATUS_KOMP_ID

Liefert die HDD Download Kompatibilitätskennung gemäß der HW-Variante

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KOMP_ID | string | Kompatibilitätskennung für HDD Downloadsystem 'HU_CICM-HB' (ECE) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-hddownload-mode"></a>
### START_HDDOWNLOAD_MODE

Start des HDDownload KWP2000: $108A StartHDDownloadMode Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| RESPONSE_CODE | int | Fehlercode |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-write-data-server-address"></a>
### WRITE_DATA_SERVER_ADDRESS

Adresse (URL) des Download-Servers KWP2000: $2E $2507 WriteDataserverAddress Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SERVER_ADRESSE | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| RESPONSE_CODE | int | Fehlercode |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-hddownload-kennung"></a>
### READ_HDDOWNLOAD_KENNUNG

Auslesen der kompletten HDDownload-Kennung KWP2000: $22 $2501 ReadHDDownloadkennung Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| VERSION | unsigned int | HD-Download-Kennung-Version |
| ANZAHL_SWE | unsigned int | Anzahl der vorhandenen SGBM-IDs |
| SGBM_ID_RECORD | binary | Feld der SGBM-IDs [0..ANZAHL_SWE-1] 8 Byte pro SGBM-ID |
| LAENGE_MAPINFO | unsigned int | Anzahl Bytes der Map-Info HD-Download-Kennung-Version |
| MAPINFO | string | Map-Info in ASCII |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-hddownload-timing-parameter"></a>
### READ_HDDOWNLOAD_TIMING_PARAMETER

Auslesen aller HDDownload-Timing-Parameter KWP2000: $22 $250A ReadHDDownloadTimingParameter Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| RESPONSE_CODE | int | Fehlercode |
| START_TIME | unsigned int |  |
| STOP_TIME | unsigned int |  |
| SIG_TIME | unsigned int |  |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-hddownload-status"></a>
### READ_HDDOWNLOAD_STATUS

Auslesen des aktuellen HDDownload-Status KWP2000: $22 $250B ReadHDDownloadObjectStatus Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| RESPONSE_CODE | int | Fehlercode |
| STATUS | int |  |
| EXT_STATUS | unsigned int |  |
| MESSAGE | string |  |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-read-hddownload-time-to-completion"></a>
### READ_HDDOWNLOAD_TIME_TO_COMPLETION

Verbleibende HDDownload-Zeit KWP2000: $22 $250C ReadHDDownloadTimeToCompletion Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| RESPONSE_CODE | int | Fehlercode |
| TIME_TO_COMPLETION | unsigned long | TIME_TO_COMPLETION &gt;&gt; 16 |
| TIME_TO_COMPLETION_HI | unsigned int | TIME_TO_COMPLETION & 0xffff |
| TIME_TO_COMPLETION_LO | unsigned int |  |
| TIME_TO_COMPLETION_D | string | als Dezimalzahl (String von Dezimalziffern) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-hddownload-routine"></a>
### START_HDDOWNLOAD_ROUTINE

Starte Download einer SWE KWP2000: $3110 StartHDDownloadRoutine Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SGBM_ID | binary | SGBM-ID einer einzelnen SWE, 8 Byte |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| RESPONSE_CODE | int | Fehlercode |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-hddownload-routine-a"></a>
### START_HDDOWNLOAD_ROUTINE_A

Starte Download einer SWE KWP2000: $3110 StartHDDownloadRoutine Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SGBM_ID | string | SGBM-ID einer einzelnen SWE, Hexdump 16 Byte |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| RESPONSE_CODE | int | Fehlercode |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-hddownload-routine"></a>
### STOP_HDDOWNLOAD_ROUTINE

Starte Download einer SWE KWP2000: $3210 StopHDDownloadRoutine KWP2000: $3E TesterPresent Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| RESPONSE_CODE | int | Fehlercode |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-test-data-argument"></a>
### TEST_DATA_ARGUMENT

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADATEN | binary |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| RDATEN | binary |  |
| ADATENL | int |  |
| RDATENL | int |  |

<a id="job-test-xdump-argument"></a>
### TEST_XDUMP_ARGUMENT

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADATEN | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| RDATEN | binary |  |
| ADATENL | int |  |
| RDATENL | int |  |

<a id="job-ng-authentisierung-start"></a>
### NG_AUTHENTISIERUNG_START

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

<a id="job-interfacetype"></a>
### INTERFACETYPE

Interface-Typ bestimmen und ausgeben Es wird der Name des Interfaces übergeben Wichtig für Baudratenumschaltung weil bei ADS, EADS und OBD sind nur 115200 Baud möglich, bei EDIC nur 125000 Baud möglich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| INTERFACE_TYP | string | Rueckmeldung des Interface-Typs |

<a id="job-ng-flash-loeschen"></a>
### NG_FLASH_LOESCHEN

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

<a id="job-ng-signatur-pruefen"></a>
### NG_SIGNATUR_PRUEFEN

Flash Signatur pruefen KWP2000: $31 StartRoutineByLocalIdentifier $09 CheckSignature Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BEREICH | string | 'Programm' 'Daten' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-gettickcount"></a>
### GETTICKCOUNT

systeminterner Zählerwert in Milli-Sekunden zurückgeben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| TICKS | unsigned int | systeminterner Zählerwert in Milli-Sekunden VORSICHT: der Zähler läuft alle 64 Sekunden über! |

<a id="job-steuern-kartenupdate-usb"></a>
### STEUERN_KARTENUPDATE_USB

Update der Kartendaten für die Navigation über USB

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_KARTENUPDATE | unsigned char | 0 = Kartenupdate mit USB ab 10 km/h möglich 1 = Kartenupdate im Stillstand mit USB möglich |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kartenupdate-usb"></a>
### STATUS_KARTENUPDATE_USB

Update der Kartendaten für die Navigation über USB

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KARTENUPDATE | unsigned char | 0 = Kartenupdate mit USB ab 10 km/h möglich 1 = Kartenupdate im Stillstand mit USB möglich |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mnand-repair"></a>
### STEUERN_MNAND_REPAIR

Formatsequenz für korruptes MNAND

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| _RESPONSE2 | binary | Hex-Antwort von SG |

<a id="job-steuern-navimetadb-patch"></a>
### STEUERN_NAVIMETADB_PATCH

Repairs the navigation metadata database

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _RESPONSE_0 | binary | Hex-Antwort von SG |
| _RESPONSE_1 | binary | Hex-Antwort von SG |
| _RESPONSE_A | binary | Hex-Antwort von SG |
| _RESPONSE_2 | binary | Hex-Antwort von SG |
| _RESPONSE_3 | binary | Hex-Antwort von SG |
| _RESPONSE_4 | binary | Hex-Antwort von SG |
| _RESPONSE_5 | binary | Hex-Antwort von SG |
| _RESPONSE_6 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-atc-version"></a>
### STATUS_ATC_VERSION

Reads out the capability of the ATC diagnosis

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ATC_TEXT | string | capability of the ATC diagnosis 0 no ATC diagnosis possible 1 ATC diagnosis with track 12 measurement 2 ATC diagnosis with jitter measurement |
| STAT_ATC | int | capability of the ATC diagnosis 0 no ATC diagnosis possible 1 ATC diagnosis with track 12 measurement 2 ATC diagnosis with jitter measurement |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-tuner-fix"></a>
### STEUERN_TUNER_FIX

Repairs the tuner coding problem ECE Target-&gt;SouthAmerica

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _RESPONSE_0 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mmedb-erase"></a>
### STEUERN_MMEDB_ERASE

Repairs the navigation metadata database

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _RESPONSE_0 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hmi-license-file"></a>
### STATUS_HMI_LICENSE_FILE

Repairs the navigation metadata database

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _RESPONSE_0 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hmi-license-file"></a>
### STEUERN_HMI_LICENSE_FILE

Repairs the gpl license file

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _RESPONSE_0 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tda-aktivierung"></a>
### STATUS_TDA_AKTIVIERUNG

Reads out the actual Baureihe of the Gateway table

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TDA | unsigned char | Returns the status of activation of BMW services by the user xx values from table TDAActivationState |
| STAT_TDA_TEXT | string | Returns the status of activation of BMW services by the user xx values from table TDAActivationState |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-format-hdd"></a>
### STEUERN_FORMAT_HDD

Formats one or all partition(s) of the Hard Disk Drive.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_PARTITION | unsigned char | Partition that must be formatted |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ard-fix"></a>
### STEUERN_ARD_FIX

Switch off ARD in dependence of software (only H,I) and modell (only Basis)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-steuern-ipsafe-forhddupdate"></a>
### STEUERN_IPSAFE_FORHDDUPDATE

Saves IP for HDD update against Onlineactivation of MULF TCU

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _RESPONSE_0 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ipsafe-forhddupdate-cbx1"></a>
### STEUERN_IPSAFE_FORHDDUPDATE_CBX1

Some special stuff number 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ipsafe-forhddupdate-cbx2"></a>
### STEUERN_IPSAFE_FORHDDUPDATE_CBX2

Some special stuff number 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-no-hmi-watchdog"></a>
### STEUERN_NO_HMI_WATCHDOG

Prevents HMI Hang

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-gps-repair"></a>
### STEUERN_GPS_REPAIR

Repariert: 'Keine Provisionierung möglich, wegen falschem GPS Datum'

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-del-cert"></a>
### STEUERN_DEL_CERT

removes cert to trigger download of new one

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _RESPONSE_0 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sdars-activation"></a>
### STEUERN_SDARS_ACTIVATION

Schaltet das SDARS Modul ein und aus

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_SDARS_ACTIVATION | unsigned char | 0x00 AUS, 0x01 EIN, 0xFF NICHT DEFINIERT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sdars-activation"></a>
### STATUS_SDARS_ACTIVATION

Reads out the actual status of sdars modul

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SDARS_ACTIVATION_WERT | unsigned char | actual status of sdars modul 0x00 AUS, 0x01 EIN, 0xFF NICHT DEFINIERT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (125 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (47 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (59 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (18 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (14 × 9)
- [TFREQUENZSINUSGENERATOR](#table-tfrequenzsinusgenerator) (57 × 2)
- [TGALKURVE](#table-tgalkurve) (8 × 2)
- [TCONNECTIONTABLE](#table-tconnectiontable) (132 × 2)
- [TCONNECTIONSTATUS](#table-tconnectionstatus) (4 × 2)
- [TFBLOCKIDTEXTE](#table-tfblockidtexte) (81 × 2)
- [TMOSTLIGHT](#table-tmostlight) (2 × 2)
- [TWAKEUPSTATUS](#table-twakeupstatus) (3 × 3)
- [TFBANDSCANSTATUS](#table-tfbandscanstatus) (4 × 2)
- [TFBANDSCANFEHLER](#table-tfbandscanfehler) (3 × 2)
- [TTVREGION](#table-ttvregion) (13 × 2)
- [FORTTEXTE](#table-forttexte) (131 × 2)
- [IORTTEXTE](#table-iorttexte) (50 × 2)
- [TNODETYPE](#table-tnodetype) (6 × 2)
- [TPRE_PRO_SWI_STATE](#table-tpre-pro-swi-state) (4 × 2)
- [TINC_GW_TAB](#table-tinc-gw-tab) (4 × 2)
- [TRADIOEINAUSSTATUS](#table-tradioeinausstatus) (3 × 2)
- [TLADEVORGANGSPRACHPAKET](#table-tladevorgangsprachpaket) (6 × 2)
- [TFEHLERURSACHESPRACHPAKET](#table-tfehlerursachesprachpaket) (2 × 2)
- [TFLOTTENMODUS](#table-tflottenmodus) (4 × 2)
- [TGPSTIMEVALIDITY](#table-tgpstimevalidity) (3 × 2)
- [TUSBTESTSTATUS](#table-tusbteststatus) (6 × 2)
- [TINTERNALACCELERATIONSENSORSTATUS](#table-tinternalaccelerationsensorstatus) (3 × 2)
- [TAB_TEST_STATUS](#table-tab-test-status) (4 × 2)
- [TINTERNALGYROSTATUS](#table-tinternalgyrostatus) (3 × 2)
- [TVIDEOEINGANGFEHLERART](#table-tvideoeingangfehlerart) (4 × 2)
- [TFBASEINGANG](#table-tfbaseingang) (180 × 2)
- [TEINGANGVIDEOSWITCH](#table-teingangvideoswitch) (513 × 2)
- [TAUSGANGVIDEOSWITCH](#table-tausgangvideoswitch) (33 × 2)
- [TSDARSSIGNALQUALITY](#table-tsdarssignalquality) (5 × 2)
- [TSDARSSIGNALQUALITYGLOBALSTATUS](#table-tsdarssignalqualityglobalstatus) (3 × 2)
- [TPDCSIGNAL](#table-tpdcsignal) (4 × 2)
- [TSDARSBERMODE](#table-tsdarsbermode) (3 × 2)
- [THERSTELLUNGSTATUS](#table-therstellungstatus) (6 × 2)
- [THERSTELLUNGFEHLER](#table-therstellungfehler) (3 × 2)
- [TVIDEOQUELLE](#table-tvideoquelle) (262 × 2)
- [TVIDEOSENKE](#table-tvideosenke) (9 × 2)
- [TAKTIVEANTENNEDAB](#table-taktiveantennedab) (5 × 2)
- [TBROWSERACTIVATIONSTATE](#table-tbrowseractivationstate) (3 × 2)
- [TINPUTNECESSARY](#table-tinputnecessary) (3 × 2)
- [TONLINECODED](#table-tonlinecoded) (3 × 2)
- [TTMCACTIVATIONSTATE](#table-ttmcactivationstate) (3 × 2)
- [TTELMUTE](#table-ttelmute) (3 × 2)
- [TWAVEBAND](#table-twaveband) (7 × 2)
- [TGPSSTATUS](#table-tgpsstatus) (14 × 2)
- [TINITIALISIERUNG](#table-tinitialisierung) (3 × 2)
- [TLUEFTERSTATUS](#table-tluefterstatus) (5 × 2)
- [TTESTMAPACTIVATIONSTATUS](#table-ttestmapactivationstatus) (12 × 2)
- [TTESTMAPSTATUS](#table-ttestmapstatus) (15 × 2)
- [TETHERNETCONNECTION](#table-tethernetconnection) (4 × 2)
- [TETHERNETACTIVATIONSTATE](#table-tethernetactivationstate) (3 × 2)
- [TGPSPOSITIONVALIDITY](#table-tgpspositionvalidity) (3 × 2)
- [TFBTASTENUMMER](#table-tfbtastenummer) (9 × 2)
- [TFBTASTESTATUS](#table-tfbtastestatus) (3 × 2)
- [TLANGUAGE](#table-tlanguage) (29 × 2)
- [TTUNERSUCHLAUF](#table-ttunersuchlauf) (4 × 2)
- [TKLANGZEICHEN](#table-tklangzeichen) (22 × 2)
- [TDEMUTESTATUS](#table-tdemutestatus) (3 × 2)
- [TDEMUTESOURCE](#table-tdemutesource) (5 × 2)
- [TSOURCEDEMUTESTATUS](#table-tsourcedemutestatus) (7 × 2)
- [TEXTGYROSIGNAL](#table-textgyrosignal) (3 × 2)
- [TFOLLOWINGDABFM](#table-tfollowingdabfm) (4 × 2)
- [TFOLLOWINGDABDAB](#table-tfollowingdabdab) (4 × 2)
- [TTPDAB](#table-ttpdab) (4 × 2)
- [TAPPLICATION](#table-tapplication) (14 × 2)
- [TAPPLICATIONRUNNINGSTATUS](#table-tapplicationrunningstatus) (3 × 2)
- [TAPPLICATIONACTIVATIONSTATUS](#table-tapplicationactivationstatus) (12 × 2)
- [TANTSCAN](#table-tantscan) (3 × 2)
- [TENTSOURCE](#table-tentsource) (27 × 2)
- [TENTSOURCESTATUS](#table-tentsourcestatus) (3 × 2)
- [TTASTE](#table-ttaste) (11 × 2)
- [TAUXVERBINDUNG](#table-tauxverbindung) (10 × 2)
- [TVERBINDUNGFEHLERART](#table-tverbindungfehlerart) (4 × 2)
- [TSATELLITESTATUS](#table-tsatellitestatus) (3 × 2)
- [TNAVIOUTPUT](#table-tnavioutput) (4 × 2)
- [TSDARSTUNERMODE](#table-tsdarstunermode) (4 × 2)
- [TVERBAUROUTINE](#table-tverbauroutine) (20 × 2)
- [TTUNERRI](#table-ttunerri) (5 × 2)
- [TAUDIOSIGNAL](#table-taudiosignal) (11 × 2)
- [TLAUFWERK](#table-tlaufwerk) (129 × 2)
- [TANTENNE](#table-tantenne) (75 × 2)
- [TANTENNEFEHLERART](#table-tantennefehlerart) (5 × 2)
- [TNAVICALIBRATION](#table-tnavicalibration) (3 × 2)
- [TKEYNR](#table-tkeynr) (16 × 2)
- [TSDARSCHANNELTUNESUCCESS](#table-tsdarschanneltunesuccess) (5 × 2)
- [TFORMATTINGSTATUS](#table-tformattingstatus) (5 × 2)
- [THDDPARTITION](#table-thddpartition) (8 × 2)
- [TAUDIOSYSTEM](#table-taudiosystem) (5 × 2)
- [TSEARCHINGPROCESS](#table-tsearchingprocess) (6 × 2)
- [TMICROPHONE](#table-tmicrophone) (3 × 2)
- [TMICROPHONETEST](#table-tmicrophonetest) (6 × 2)
- [TSDARSFACTORYSUCCESSFUL](#table-tsdarsfactorysuccessful) (5 × 2)
- [TINSERTEDMEDIUM](#table-tinsertedmedium) (6 × 2)
- [TACTIVATIONSTATEVICSBEACONDIAGNOSIS](#table-tactivationstatevicsbeacondiagnosis) (3 × 2)
- [TANTENNADIAG](#table-tantennadiag) (3 × 2)
- [THWLIEFERANT](#table-thwlieferant) (7 × 2)
- [THWEINHEIT](#table-thweinheit) (1 × 2)
- [TRADONLEAD](#table-tradonlead) (3 × 2)
- [TTESTSTATUS](#table-tteststatus) (6 × 2)
- [TAUDIOKANAL](#table-taudiokanal) (27 × 2)
- [TKANALFEHLERART](#table-tkanalfehlerart) (5 × 2)
- [TSIGNALDAB](#table-tsignaldab) (3 × 2)
- [TSIGNALART](#table-tsignalart) (9 × 2)
- [TVIDEOAUSGANG](#table-tvideoausgang) (33 × 2)
- [TTP](#table-ttp) (4 × 2)
- [TAF](#table-taf) (4 × 2)
- [TRDS](#table-trds) (4 × 2)
- [TONLINESTATETABLE](#table-tonlinestatetable) (3 × 2)
- [THDDSMARTVALUES](#table-thddsmartvalues) (15 × 2)
- [TNAVIMAPSTATUS](#table-tnavimapstatus) (6 × 2)
- [TGEARTYPE](#table-tgeartype) (4 × 2)
- [TDIRECTIONSOURCE](#table-tdirectionsource) (2 × 2)
- [TPROVISIONINGSTATUS](#table-tprovisioningstatus) (4 × 2)
- [TPROCESSSTATUS](#table-tprocessstatus) (6 × 2)
- [TNAVISIMULATIONMODEACTIVATIONSTATUS](#table-tnavisimulationmodeactivationstatus) (3 × 2)
- [TAB_EXCHANGINGSTATUS](#table-tab-exchangingstatus) (5 × 2)
- [TROUTEDOWNLOAD](#table-troutedownload) (6 × 2)
- [TPOIDOWNLOAD](#table-tpoidownload) (6 × 2)
- [TATCVERSION](#table-tatcversion) (4 × 2)
- [THWVAR_DEVICE](#table-thwvar-device) (13 × 2)
- [THWVAR_FUNCTION](#table-thwvar-function) (13 × 2)
- [TINDIVIDUALDATALISTE](#table-tindividualdataliste) (6 × 17)
- [TWAKEUPSOURCE](#table-twakeupsource) (6 × 2)
- [TGPSCORRELATIONHEADING](#table-tgpscorrelationheading) (3 × 2)
- [TGYROTYPE](#table-tgyrotype) (3 × 2)
- [TACCELERATIONSENSORTYPE](#table-taccelerationsensortype) (3 × 2)
- [TMAPUPDATE](#table-tmapupdate) (6 × 2)
- [TDABTMCACTIVATIONSTATE](#table-tdabtmcactivationstate) (3 × 2)
- [THUBCONNECTIONSTATE](#table-thubconnectionstate) (4 × 2)
- [TDAACTIVATIONSTATE](#table-tdaactivationstate) (5 × 2)

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

Dimensions: 125 rows × 2 columns

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
| 0x72 | AISIN AW CO.LTD |
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
| 0x85 | AKsys GmbH |
| 0x86 | META System |
| 0x87 | Hülsbeck & Fürst GmbH & Co KG |
| 0x88 | Mann & Hummel Automotive GmbH |
| 0x89 | Brose Fahrzeugteile GmbH & Co |
| 0x90 | Keihin |
| 0x91 | Vimercati S.p.A. |
| 0x92 | CRH |
| 0x93 | TPO Display Corp. |
| 0x94 | KÜSTER Automotive Control |
| 0x95 | Hitachi Automotive |
| 0x96 | Continental Automotive |
| 0x97 | TI-Automotive |
| 0x98 | Hydro |
| 0x99 | Johnson Controls |
| 0x9A | Takata- Petri |
| 0x9B | Mitsubishi Electric B.V. (Melco) |
| 0x9C | Autokabel |
| 0x9D | GKN-Driveline |
| 0x9E | Zollner Elektronik AG |
| 0x9F | PEIKER acustics GmbH |
| 0xA0 | Bosal-Oris |
| 0xA1 | Cobasys |
| 0xA2 | Lighting Reutlingen GmbH |
| 0xA3 | CONTI VDO |
| 0xA4 | ADC Automotive Distance Control Systems GmbH |
| 0xA5 | Funkwerk Dabendorf GmbH |
| 0xA6 | Lame |
| 0xA7 | Magna/Closures |
| 0xA8 | Wanyu |
| 0xA9 | Thyssen Krupp Presta |
| 0xAA | ArvinMeritor |
| 0xAB | Kongsberg Automotive GmbH |
| 0xAC | SMR Automotive Mirrors |
| 0xAD | So.Ge.Mi. |
| 0xAE | MTA |
| 0xAF | Alfmeier |
| 0xB0 | ELTEK VALERE DEUTSCHLAND GMBH |
| 0xB1 | Omron Automotive Electronics Europe Group |
| 0xB2 | ASK |
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

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
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
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 47 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0xC560 | 0x4224 | - | - | - |
| 0xC561 | 0x4224 | - | - | - |
| 0xC562 | 0x4224 | - | - | - |
| 0xC563 | 0x4224 | - | - | - |
| 0xC564 | 0x4224 | - | - | - |
| 0xC565 | 0x4224 | - | - | - |
| 0xC573 | 0x4208 | - | - | - |
| 0xC576 | 0x4208 | - | - | - |
| 0xC57A | 0x422A | 0x4229 | - | - |
| 0xC580 | 0x4220 | - | - | - |
| 0xC583 | 0x4223 | - | - | - |
| 0xC585 | 0x422B | - | - | - |
| 0xC588 | 0x170C | - | - | - |
| 0xC589 | 0x170C | - | - | - |
| 0x9310 | 0x1709 | - | - | - |
| 0xE1D0 | 0x170B | - | - | - |
| 0xE1D2 | 0x1707 | - | - | - |
| 0xE1CC | 0x1707 | - | - | - |
| 0x930F | 0x1707 | - | - | - |
| 0xE1CF | 0x1707 | - | - | - |
| 0xC58D | 0x420D | 0x4232 | - | - |
| 0xC58E | 0x420E | 0x420F | 0x4210 | - |
| 0xC58F | 0x420E | 0x420F | 0x4210 | - |
| 0xC590 | 0x420E | 0x420F | 0x4210 | 0x4211 |
| 0xC592 | 0x420D | 0x4212 | - | - |
| 0xC594 | 0x420E | 0x4212 | - | - |
| 0xC595 | 0x420E | 0x4212 | - | - |
| 0xE1EB | 0x420D | 0x4214 | - | - |
| 0xC597 | 0x420D | 0x4215 | - | - |
| 0xC598 | 0x4216 | - | - | - |
| 0xC599 | 0x4216 | - | - | - |
| 0xC59A | 0x4216 | - | - | - |
| 0xC59B | 0x4216 | - | - | - |
| 0xC59C | 0x4216 | 0x4217 | - | - |
| 0xC59D | 0x4216 | 0x4218 | - | - |
| 0xC59E | 0x4216 | 0x4219 | 0x420D | - |
| 0xC5A1 | 0x4208 | - | - | - |
| 0xC5A2 | 0x4228 | - | - | - |
| 0xC56C | 0x4224 | 0x4226 | - | - |
| 0xC517 | - | - | - | - |
| 0xC587 | 0x1715 | 0x422E | 0x1707 | - |
| 0xC59F | 0x420C | - | - | - |
| 0xE1E8 | 0x422D | - | - | - |
| 0xC5BB | 0x4234 | - | - | - |
| 0xC5BC | 0x4234 | - | - | - |
| 0xC5BD | 0x4235 | 0x4236 | - | - |
| 0xFFFF | - | - | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 59 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x4200 | AmpTemp | Grad C | high | signed int | - | - | - | - |
| 0x4201 | GyroTemp | Grad C | - | signed char | - | - | - | - |
| 0x4202 | CPU Temp | Grad C | - | signed char | - | - | - | - |
| 0x4203 | HDD Temp | Grad C | - | signed char | - | - | - | - |
| 0x4204 | DVD Temp | Grad C | - | signed char | - | - | - | - |
| 0x4205 | Audioquelle | text | - | 3 | - | - | - | - |
| 0x4206 | SMART Attributes | text | - | 30 | - | - | - | - |
| 0x4207 | HDD ErrorCode | hex | - | unsigned char | - | - | - | - |
| 0x4208 | Allgemeine Secondary DTC ID | hex | - | unsigned int | - | - | - | - |
| 0x4209 | AMFM Tuner SW Version | text | - | 3 | - | - | - | - |
| 0x420A | DAB Tuner SW Version | text | - | 3 | - | - | - | - |
| 0x420B | Audio Label | hex | - | unsigned char | - | - | - | - |
| 0x420C | Coding Inconsistency Address | hex | high | signed long | - | - | - | - |
| 0x420D | PIA Process | hex | - | unsigned char | - | - | - | - |
| 0x420E | PIA Medium | hex | - | unsigned char | - | - | - | - |
| 0x420F | PIA Profilname | text | high | 24 | - | - | - | - |
| 0x4210 | PIA IStufenbezeichner | text | high | 17 | - | - | - | - |
| 0x4211 | PIA Version | hex | - | unsigned char | - | - | - | - |
| 0x4212 | PIA Errortext | hex | - | unsigned char | - | - | - | - |
| 0x4213 | PIA LowMemory | text | - | 8 | - | - | - | - |
| 0x4214 | PIA Profilnummer | hex | - | unsigned char | - | - | - | - |
| 0x4215 | PIA Profilcompare | text | - | 2 | - | - | - | - |
| 0x4216 | PIA FunctionID | text | - | 3 | - | - | - | - |
| 0x4217 | PIA configuration attributes | text | - | 4 | - | - | - | - |
| 0x4218 | PIA configuration attributes compare | text | - | 8 | - | - | - | - |
| 0x4219 | PIA Profilnumbers  function and master | text | - | 2 | - | - | - | - |
| 0x4220 | FB Defect Error | hex | - | unsigned char | - | - | - | - |
| 0x4221 | FB_Software_Error | hex | - | unsigned char | - | - | - | - |
| 0x4222 | Interne 5V Spannung | mVolt | high | signed int | - | - | - | - |
| 0x4223 | Grund des Lüfterfehlers | hex | - | unsigned char | - | - | - | - |
| 0x1707 | DiagAdr | hex | - | unsigned char | - | - | - | - |
| 0x1708 | Klemmenstatus | hex | - | unsigned char | - | - | - | - |
| 0x1709 | MOST Message Header | text | - | 6 | - | - | - | - |
| 0x170A | FOT Temp | Grad C | - | signed char | - | - | - | - |
| 0x170B | NPR | hex | - | unsigned char | - | 1 | 1 | 0 |
| 0x170C | UBat | mVolt | high | unsigned int | - | - | - | - |
| 0x170D | MemMirror | text | - | 74 | - | - | - | - |
| 0x1721 | ResetReason | hex | - | unsigned int | - | - | - | - |
| 0x4224 | Videoquelle | hex | - | unsigned char | - | - | - | - |
| 0x4225 | VideoSink | hex | - | unsigned char | - | - | - | - |
| 0x4226 | Video Watchdog info | text | - | 4 | - | - | - | - |
| 0x4227 | Media Type | hex | - | unsigned char | - | - | - | - |
| 0x4228 | Address | text | - | 8 | - | - | - | - |
| 0x4229 | ATC Test CD ID | text | - | 8 | - | - | - | - |
| 0x422A | Quality Level ATC CD | hex | - | unsigned char | - | - | - | - |
| 0x422B | Amp, Gyro, CPU, HDD, DVD Temp | text | - | 5 | - | - | - | - |
| 0x1701 | Systemzeit | sec | high | signed long | - | - | - | - |
| 0x1715 | WakeUp Source | hex | - | unsigned char | - | - | - | - |
| 0x422C | PDC Internal Error | hex | - | unsigned char | - | - | - | - |
| 0x422D | MileageErrorCause | hex | - | unsigned char | - | - | - | - |
| 0x422E | Einschlafverhinderung | hex | - | unsigned char | - | - | - | - |
| 0x422F | Kartenmaterial | hex | - | unsigned char | - | - | - | - |
| 0x4230 | VideoSwitch | hex | - | unsigned char | - | - | - | - |
| 0x4231 | Interner Spannungs Sensor | hex | - | unsigned char | - | - | - | - |
| 0x4232 | Fahrzeugzustand | hex | - | unsigned char | - | - | - | - |
| 0x4233 | Communication Failure to Tuner HW | hex | - | unsigned char | - | - | - | - |
| 0x4234 | Reason for mounting the NAND writable | hex | - | unsigned char | - | - | - | - |
| 0x4235 | Systemzeit in Sekunden seit Startup bis zur Unterspannung | hex | high | signed long | - | - | - | - |
| 0x4236 | Bootloader oder Applikation | hex | - | unsigned char | - | - | - | - |

<a id="table-horttexte"></a>
### HORTTEXTE

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
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 18 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x1040 | 0x4206 | - | - | - |
| 0x1041 | 0x4206 | 0x4207 | - | - |
| 0x1042 | 0x4206 | - | - | - |
| 0x1080 | 0x4227 | - | - | - |
| 0x1093 | 0x4221 | - | - | - |
| 0x930A | - | - | - | - |
| 0x9311 | - | - | - | - |
| 0x930B | 0x1707 | - | - | - |
| 0x10A3 | 0x4209 | - | - | - |
| 0x10A4 | 0x420A | 0x4233 | - | - |
| 0x930F | 0x1707 | - | - | - |
| 0x9310 | 0x1709 | - | - | - |
| 0x1150 | 0x4216 | - | - | - |
| 0x1151 | 0x4216 | - | - | - |
| 0x1152 | 0x4216 | - | - | - |
| 0x1153 | 0x4216 | 0x4217 | - | - |
| 0x1154 | 0x4216 | 0x4218 | - | - |
| 0xFFFF | - | - | - | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 14 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x4206 | SMART Attributes | text | - | 30 | - | - | - | - |
| 0x4207 | HDD ErrorCode | hex | - | unsigned char | - | - | - | - |
| 0x4227 | Media Type | hex | - | unsigned char | - | - | - | - |
| 0x4221 | FB_Software_Error | hex | - | unsigned char | - | - | - | - |
| 0x170C | UBat | mVolt | high | unsigned int | - | - | - | - |
| 0x1707 | DiagAdr | hex | - | unsigned char | - | - | - | - |
| 0x4209 | AMFM Tuner SW Version | text | - | 3 | - | - | - | - |
| 0x420A | DAB Tuner SW Version | text | - | 3 | - | - | - | - |
| 0x1701 | Systemzeit | sec | high | signed long | - | - | - | - |
| 0x1709 | MOST Message Header | text | - | 6 | - | - | - | - |
| 0x4233 | Communication Failure to Tuner HW | hex | - | unsigned char | - | - | - | - |
| 0x4216 | PIA FunctionID | text | - | 3 | - | - | - | - |
| 0x4217 | PIA configuration attributes | text | - | 4 | - | - | - | - |
| 0x4218 | PIA configuration attributes compare | text | - | 8 | - | - | - | - |

<a id="table-tfrequenzsinusgenerator"></a>
### TFREQUENZSINUSGENERATOR

Dimensions: 57 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 20 | 20 |
| 28 | 28 |
| 40 | 40 |
| 50 | 50 |
| 56 | 56 |
| 63 | 63 |
| 71 | 71 |
| 89 | 89 |
| 100 | 100 |
| 112 | 112 |
| 125 | 125 |
| 140 | 140 |
| 160 | 160 |
| 180 | 180 |
| 200 | 200 |
| 220 | 220 |
| 250 | 250 |
| 280 | 280 |
| 315 | 315 |
| 355 | 355 |
| 400 | 400 |
| 445 | 445 |
| 500 | 500 |
| 560 | 560 |
| 630 | 630 |
| 710. | 710. |
| 800 | 800 |
| 890 | 890 |
| 1000 | 1000 |
| 1120 | 1120 |
| 1250 | 1250 |
| 1400 | 1400 |
| 1600 | 1600 |
| 1800 | 1800 |
| 2000 | 2000 |
| 2200 | 2200 |
| 2500 | 2500 |
| 2800 | 2800 |
| 3150 | 3150 |
| 3550 | 3550 |
| 4000 | 4000 |
| 4450 | 4450 |
| 5000 | 5000 |
| 5600 | 5600 |
| 6300 | 6300 |
| 7100 | 7100 |
| 8000 | 8000 |
| 8900 | 8900 |
| 10000 | 10000 |
| 11200 | 11200 |
| 12500 | 12500 |
| 14000 | 14000 |
| 16000 | 16000 |
| 18000 | 180000 |
| 20000 | 20000 |
| 22000 | 22000 |
| 0xFFFF | Nicht definiert |

<a id="table-tgalkurve"></a>
### TGALKURVE

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | GAL-Kurve 0 |
| 0x01 | GAL-Kurve 1 |
| 0x02 | GAL-Kurve 2 |
| 0x03 | GAL-Kurve 3 |
| 0x04 | GAL-Kurve 4 |
| 0x05 | GAL-Kurve 5 |
| 0x06 | GAL-Kurve 6 |
| 0xFF | Nicht definiert |

<a id="table-tconnectiontable"></a>
### TCONNECTIONTABLE

Dimensions: 132 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | AmFmTuner/AudioAmplifier = 0x01  |
| 2 | AmFmTuner/HeadPhoneAmplifier = 0x02  |
| 3 | AmFmTuner/HeadPhoneAmplifier = 0x03  |
| 8 | Null device/AudioAmplifier = 0x08  |
| 9 | Null device/HeadPhoneAmplifier = 0x09  |
| 16 | AmFmTuner/HeadPhoneAmplifier = 0x10  |
| 24 | AudioDiscPlayer/AudioAmplifier = 0x18  |
| 25 | AudioDiscPlayer/HeadPhoneAmplifier = 0x19  |
| 32 | AudioDiscPlayer/AudioAmplifier = 0x20  |
| 33 | AudioDiscPlayer/HeadPhoneAmplifier = 0x21  |
| 34 | AudioDiscPlayer/HeadPhoneAmplifier = 0x22  |
| 40 | MultiMediaPlayer/AudioAmplifier = 0x28  |
| 48 | SVS/AudioAmplifier = 0x30  |
| 64 | Telephone/AudioAmplifier = 0x40  |
| 106 | DABTuner/HeadPhoneAmplifier = 0x6A |
| 80 | TVTuner/AudioAmplifier = 0x50  |
| 81 | TVTuner/HeadPhoneAmplifier = 0x51  |
| 82 | TVTuner/HeadPhoneAmplifier = 0x52  |
| 88 | Navigation/AudioAmplifier = 0x58  |
| 114 | Browser/HeadPhoneAmplifier = 0x72  |
| 56 | AmFmTuner/AudioAmplifier = 0x38  |
| 72 | TelematikTCU/AudioAmplifier = 0x48 |
| 117 | AuxilaryInput/HeadPhoneAmplifier = 0x75  |
| 118 | AuxilaryInput/HeadPhoneAmplifier = 0x76  |
| 119 | AuxilaryInput/AudioAmplifier = 0x77  |
| 120 | AuxilaryInput/HeadPhoneAmplifier = 0x78  |
| 121 | AuxilaryInput/HeadPhoneAmplifier = 0x79  |
| 128 | AuxilaryInput/AudioAmplifier = 0x80  |
| 129 | AuxilaryInput/HeadPhoneAmplifier = 0x81  |
| 130 | AuxilaryInput/HeadPhoneAmplifier = 0x82  |
| 134 | MultiMediaPlayer/AudioAmplifier = 0x86  |
| 132 | PDC/AudioAmplifier = 0x84 |
| 133 | Jingle/AudioAmplifier = 0x85  |
| 4 | AmFmTuner/AudioAmplifier = 0x04  |
| 5 | AmFmTuner/HeadPhoneAmplifier = 0x05  |
| 6 | AmFmTuner/HeadPhoneAmplifier = 0x06  |
| 36 | MultiMediaPlayer/AudioAmplifier = 0x24  |
| 37 | MultiMediaPlayer/HeadPhoneAmplifier = 0x25  |
| 38 | MultiMediaPlayer/HeadPhoneAmplifier = 0x26  |
| 39 | MultiMediaPlayer/AudioAmplifier = 0x27  |
| 41 | MultiMediaPlayer/HeadPhoneAmplifier = 0x29  |
| 67 | Telephone/HeadPhoneAmplifier = 0x43  |
| 68 | Telephone/HeadPhoneAmplifier = 0x44  |
| 69 | Telephone/AudioAmplifier = 0x45  |
| 70 | Telephone/HeadPhoneAmplifier = 0x46  |
| 71 | Telephone/HeadPhoneAmplifier = 0x47  |
| 73 | TelematikTCU/HeadPhoneAmplifier = 0x49  |
| 83 | TVTuner/AudioAmplifier = 0x53  |
| 84 | TVTuner/HeadPhoneAmplifier = 0x54  |
| 85 | TVTuner/HeadPhoneAmplifier = 0x55  |
| 112 | DABTuner/HeadPhoneAmplifier = 0x70  |
| 113 | Browser/AudioAmplifier = 0x71  |
| 115 | Browser/HeadPhoneAmplifier = 0x73  |
| 116 | AuxilaryInput/AudioAmplifier = 0x74  |
| 10 | Null device/HeadPhoneAmplifier = 0x0A  |
| 11 | AmFmTuner/AudioAmplifier = 0x0B  |
| 12 | AmFmTuner/HeadPhoneAmplifier = 0x0C  |
| 14 | AmFmTuner/AudioAmplifier = 0x0E  |
| 15 | AmFmTuner/HeadPhoneAmplifier = 0x0F  |
| 26 | AudioDiscPlayer/HeadPhoneAmplifier = 0x1A  |
| 28 | AudioDiscPlayer/HeadPhoneAmplifier = 0x1C  |
| 29 | AudioDiscPlayer/HeadPhoneAmplifier = 0x1D  |
| 42 | MultiMediaPlayer/HeadPhoneAmplifier = 0x2A  |
| 44 | MicrophoneInput/SVS = 0x2C  |
| 45 | MicrophoneInput/Telephone = 0x2D  |
| 74 | TelematikTCU/HeadPhoneAmplifier = 0x4A  |
| 107 | SatRadio/AudioAmplifier = 0x6B  |
| 108 | SatRadio/HeadPhoneAmplifier = 0x6C  |
| 109 | SatRadio/HeadPhoneAmplifier = 0x6D  |
| 110 | DABTuner/AudioAmplifier = 0x6E  |
| 111 | DABTuner/HeadPhoneAmplifier = 0x6F  |
| 122 | AuxilaryInput/AudioAmplifier = 0x7A  |
| 123 | AuxilaryInput/HeadPhoneAmplifier = 0x7B  |
| 124 | AuxilaryInput/HeadPhoneAmplifier = 0x7C  |
| 125 | AuxilaryInput/AudioAmplifier = 0x7D  |
| 126 | AuxilaryInput/HeadPhoneAmplifier = 0x7E  |
| 127 | AuxilaryInput/HeadPhoneAmplifier = 0x7F  |
| 154 | AuxilaryInput/AudioAmplifier = 0x9A  |
| 155 | AuxilaryInput/HeadPhoneAmplifier = 0x9B  |
| 156 | AuxilaryInput/HeadPhoneAmplifier = 0x9C  |
| 157 | AuxilaryInput/AudioAmplifier = 0x9D  |
| 158 | AuxilaryInput/HeadPhoneAmplifier = 0x9E  |
| 159 | AuxilaryInput/HeadPhoneAmplifier = 0x9F  |
| 160 | AuxilaryInput/AudioAmplifier = 0xA0  |
| 161 | AuxilaryInput/HeadPhoneAmplifier = 0xA1  |
| 162 | AuxilaryInput/HeadPhoneAmplifier = 0xA2  |
| 163 | AuxilaryInput/AudioAmplifier = 0xA3  |
| 164 | AuxilaryInput/HeadPhoneAmplifier = 0xA4  |
| 165 | AuxilaryInput/HeadPhoneAmplifier = 0xA5  |
| 166 | AuxilaryInput/AudioAmplifier = 0xA6  |
| 167 | AuxilaryInput/HeadPhoneAmplifier = 0xA7  |
| 168 | AuxilaryInput/HeadPhoneAmplifier = 0xA8  |
| 169 | AuxilaryInput/AudioAmplifier = 0xA9  |
| 170 | AuxilaryInput/HeadPhoneAmplifier = 0xAA  |
| 171 | AuxilaryInput/HeadPhoneAmplifier = 0xAB  |
| 172 | EntertainmentServer/AudioAmplifier = 0xAC  |
| 173 | EntertainmentServer/HeadPhoneAmplifier = 0xAD  |
| 174 | EntertainmentServer/HeadPhoneAmplifier = 0xAE  |
| 176 | EntertainmentServer/AudioAmplifier = 0xB0  |
| 177 | EntertainmentServer/HeadPhoneAmplifier = 0xB1  |
| 178 | EntertainmentServer/HeadPhoneAmplifier = 0xB2  |
| 179 | EntertainmentServer/AudioAmplifier = 0xB3  |
| 180 | MultiMediaPlayer/AudioAmplifier = 0xB4  |
| 181 | MultiMediaPlayer/HeadPhoneAmplifier = 0xB5  |
| 182 | MultiMediaPlayer/HeadPhoneAmplifier = 0xB6  |
| 183 | MultiMediaPlayer/AudioAmplifier = 0xB7  |
| 184 | Browser/AudioAmplifier = 0xB8  |
| 185 | Browser/HeadPhoneAmplifier = 0xB9  |
| 13 | AmFmTuner/HeadPhoneAmplifier = 0x0D  |
| 27 | AudioDiscPlayer/AudioAmplifier = 0x1B  |
| 18 | Null device/AudioAmplifier = 0x12 |
| 19 | Null device/HeadPhoneAmplifier = 0x13 |
| 20 | Null device/HeadPhoneAmplifier = 0x14 |
| 49 | iSpeechl/AudioAmplifier = 0x31 |
| 50 | iSpeech/AudioAmplifier = 0x32 |
| 104 | DABTuner/AudioAmplifier = 0x68 |
| 105 | DABTuner/HeadPhoneAmplifier = 0x69 |
| 187 | AuxilaryInput/AudioAmplifier = 0xBB |
| 188 | AuxilaryInput/HeadPhoneAmplifier = 0xBC |
| 189 | AuxilaryInput/HeadPhoneAmplifier = 0xBD |
| 46 | MicrophoneInput/iSpeech = 0x2E |
| 47 | MicrophoneInput/iSpeech = 0x2F |
| 186 | Browser/HeadPhoneAmplifier = 0xBA |
| 190 | AuxilaryInput/AudioAmplifier = 0xBE |
| 191 | AuxilaryInput/HeadPhoneAmplifier = 0xBF |
| 192 | AuxilaryInput/HeadPhoneAmplifier = 0xC0 |
| 193 | AuxilaryInput/AudioAmplifier = 0xC1 |
| 194 | AuxilaryInput/HeadPhoneAmplifier = 0xC2 |
| 195 | AuxilaryInput/HeadPhoneAmplifier = 0xC3 |
| 196 | AuxilaryInput/AudioAmplifier = 0xC4 |
| 197 | AuxilaryInput/HeadPhoneAmplifier = 0xC5 |
| 198 | AuxilaryInput/HeadPhoneAmplifier = 0xC6 |

<a id="table-tconnectionstatus"></a>
### TCONNECTIONSTATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Demuted |
| 0x01 | All.a.Con.a.SAPause.OR.Con.In.Mem. |
| 0x07 | Connection does't exist |
| 0xFF | Unknown |

<a id="table-tfblockidtexte"></a>
### TFBLOCKIDTEXTE

Dimensions: 81 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x02 | NetworkMaster=0x02 |
| 0x03 | ConnectionMaster=0x03 |
| 0x04 | PowerMaster=0x04 |
| 0x05 | Vehicle=0x05 |
| 0x06 | Diagnose=0x06 |
| 0x07 | VideoSwitch=0x07 |
| 0x10 | ManMachineInterface=0x10 |
| 0x11 | Sprachverarbeitungssystem=0x11 |
| 0x14 | BCStatistic=0x14 |
| 0x15 | ControlElements=0x15 |
| 0x20 | AudioMaster=0x20 |
| 0x22 | AudioAmplifier=0x22 |
| 0x23 | HeadPhoneAmplifier=0x23 |
| 0x24 | AuxilliaryInput=0x24 |
| 0x26 | MicrophoneInput=0x26 |
| 0x2E | AudioSinkRouter=0x2E |
| 0x2F | AudioSourceRouter=0x2F |
| 0x30 | AudioTapePlayer=0x30 |
| 0x31 | AudioDiscPlayer=0x31 |
| 0x32 | MultiMediaChanger=0x32 |
| 0x40 | AM/FM Tuner=0x40 |
| 0x41 | TMC Tuner=0x41 |
| 0x42 | TVTuner=0x42 |
| 0x43 | DABTuner=0x43 |
| 0x44 | SatRadio=0x44 |
| 0x50 | Telephone=0x50 |
| 0x51 | GeneralPhoneBook=0x51 |
| 0x52 | Navigationssystem=0x52 |
| 0x54 | Bluetooth=0x54 |
| 0x64 | TripMemory=0x64 |
| 0x6F | Monitor=0x6F |
| 0x70 | ParkDistanceControl=0x70 |
| 0x71 | Climate=0x71 |
| 0x74 | EBA/Services=0x74 |
| 0x80 | MMI_Terminal=0x80 |
| 0x81 | KOMBI_Terminal=0x81 |
| 0x82 | HUD_Terminal=0x82 |
| 0x90 | Telematik=0x90 |
| 0x91 | InternalAudioSource=0x91 |
| 0x92 | InternalAudioSink=0x92 |
| 0xAB | TollCollect=0xAB |
| 0xBE | Browser=0xBE |
| 0xC0 | CANDevices=0xC0 |
| 0xC9 | Services=0xC9 |
| 0xCA | KombiMiscFkts=0xCA |
| 0xCB | Bordcomputer=0xCB |
| 0xCC | ADASInterface=0xCC |
| 0xCD | NavigationInfo=0xCD |
| 0xCE | iSpeech=0xCE |
| 0xCF | HMIControl=0xCF |
| 0xD0 | Security=0xD0 |
| 0xD1 | SystemFunction=0xD1 |
| 0xD2 | MultiMediaServer=0xD2 |
| 0xD3 | MassStorageControl=0xD3 |
| 0xD4 | SWUpdate=0xD4 |
| 0xD5 | VirtualControlElements=0xD5 |
| 0xD6 | Vehicle2=0xD6 |
| 0xD7 | VideoConnectionMaster=0xD7 |
| 0xD8 | VideoSink=0xD8 |
| 0xD9 | EarlyVideoControl=0xD9 |
| 0xDA | MapControl=0xDA |
| 0xDB | Telematics=0xDB |
| 0xDC | DataComIP=0xDC |
| 0xDD | DownloadUploadMessagingManager=0xDD |
| 0xDE | TelematicAssist=0xDE |
| 0xDF | TeleX=0xDF |
| 0xE0 | KombiInterface=0xE0 |
| 0xE1 | HUDInterface=0xE1 |
| 0xE2 | Camera=0xE2 |
| 0xE3 | MOSTFileSystem=0xE3 |
| 0xE4 | SoundApplications=0xE4 |
| 0xE5 | CentralControlUnit=0xE5 |
| 0xE6 | TripMemory=0xE6 |
| 0xE7 | RemoteApplication=0xE7 |
| 0xE8 | VideoOutSettings=0xE8 |
| 0xE9 | SoundSIgnalService=0xE9 |
| 0xEA | ParkDistanceControl=0xEA |
| 0xEB | DebugApplication=0xEB |
| 0xED | PersonalInformationManagement=0xED |
| 0xEE | DataCommunication=0xEE |
| 0xFF | Nicht definiert |

<a id="table-tmostlight"></a>
### TMOSTLIGHT

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Lichtleistung abgesenkt |
| 1 | Volle Lichtleistung |

<a id="table-twakeupstatus"></a>
### TWAKEUPSTATUS

Dimensions: 3 rows × 3 columns

| WERT | TEXT | TEXT2 |
| --- | --- | --- |
| 0 | not initialised | off |
| 1 | SG will be waked up | on |
| 2 | SG are waked up | critical |

<a id="table-tfbandscanstatus"></a>
### TFBANDSCANSTATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Test läuft noch |
| 0x01 | Test beendet, Resultrückgabe |
| 0x02 | Test abgebrochen, Resultrückgabe |
| 0xFF | Fehlerbericht |

<a id="table-tfbandscanfehler"></a>
### TFBANDSCANFEHLER

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | FBandScan Fehler 0 |
| 0x0001 | FBandScan Fehler 1 |
| 0x0002 | FBandScan Fehler 2 |

<a id="table-ttvregion"></a>
### TTVREGION

Dimensions: 13 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Nordamerika |
| 0x02 | Mittelamerika |
| 0x03 | Südamerika |
| 0x04 | Karibik |
| 0x05 | Europa |
| 0x06 | Frankreich |
| 0x07 | Russland |
| 0x08 | Afrika |
| 0x09 | Naher Osten |
| 0x0A | Asien |
| 0x0B | Pazifik |
| 0x0C | Ozeanien/Australien |
| 0xFF | Nicht definiert |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 131 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xC508 | Verbindung Head-Unit zum Diversity: Leitungsunterbrechung |
| 0xC509 | Verbindung Head-Unit zum Diversity: Kurzschluss nach Plus |
| 0xC50A | Verbindung Head-Unit zum Diversity: Kurzschluss nach Masse |
| 0xC50C | Verbindung Diversity zu den Antennen: Leitungsunterbrechung |
| 0xC50D | Verbindung Head-Unit zum DAB L-Band Antennenfuß: Leitungsunterbrechung |
| 0xC50F | Verbindung Head-Unit zum DAB L-Band Antennenfuß: Kurzschluss |
| 0xC511 | Verbindung Head-Unit zum DAB Band III Antennenfuß: Leitungsunterbrechung |
| 0xC513 | Verbindung Head-Unit zum DAB Band III Antennenfuß: Kurzschluss |
| 0xC5AE | Verbindung Head-Unit zum SDARS Antennenfuß: Leitungsunterbrechung |
| 0xC5AF | Verbindung Head-Unit zum SDARS Antennenfuß: Kurzschluss |
| 0xC5B0 | SDARS Modul: Sicherheitssektor wurde gelöscht |
| 0xC517 | Verbindung Head-Unit zum GPS-Antennenfuß: Leitungsunterbrechung |
| 0xC518 | Verbindung Head-Unit zum GPS-Antennenfuß: Kurzschluss nach Plus |
| 0xC519 | Verbindung Head-Unit zum GPS-Antennenfuß: Kurzschluss nach Masse |
| 0xC51D | Verbindung Head-Unit zum VICS Beacon Antennenfuß: Leitungsunterbrechung |
| 0xC51E | Verbindung Head-Unit zum VICS Beacon Antennenfuß: Kurzschluss |
| 0xC51F | GPS Empfänger: defekt |
| 0xC5AC | GPS Empfänger: Firmware Fehler |
| 0xC520 | Gyro: defekt |
| 0xC521 | Beschleunigungssensor: defekt |
| 0xC522 | HDD Kartenmaterial: nicht verfügbar |
| 0xC523 | HDD Kartenmaterial: überhaupt nicht lesbar |
| 0xC524 | HDD Kartenmaterial: korrupt |
| 0xC525 | DVD Kartenmaterial: nicht verfügbar |
| 0xC526 | DVD Kartenmaterial: überhaupt nicht lesbar |
| 0xC527 | DVD Kartenmaterial: korrupt |
| 0xC528 | DVD Kartenmaterial: zeitaufwendige Lesefehler |
| 0xC529 | Kein GPS Empfang in den letzten 20 Kilometern |
| 0xC52A | Positionierung über TBD Zeitfenster nicht möglich |
| 0xE1E0 | Signal Drehgeschwindigkeit des Rades: nicht vorhanden |
| 0xE1E1 | Signal Drehgeschwindigkeit des Rades: unplausibel |
| 0xE1E2 | Signal Rückwertsgang: unplausibel |
| 0xE1E3 | Signal Rückwertsgang: nicht vorhanden |
| 0xC52F | Internes Signal bezüglich horizontaler Fahrtrichtung: unplausibel |
| 0xC530 | Internes Signal bezüglich vertikaler Fahrtrichtung: unplausibel |
| 0xE1E4 | Externes Signal bezüglich horizontaler Fahrtrichtung: unplausibel |
| 0xE1E5 | Externes Signal bezüglich horizontaler Fahrtrichtung: nicht vorhanden |
| 0xE1E6 | Externes Signal bezüglich vertikaler Fahrtrichtung: unplausibel |
| 0xE1E7 | Externes Signal bezüglich vertikaler Fahrtrichtung: nicht vorhanden |
| 0xC535 | Route/Reise Speicherbereich auf der HDD: korrupt |
| 0xC536 | Meine POI Speicherbereich auf der HDD: korrupt |
| 0xC537 | Ziele Speicherbereich auf der HDD: korrupt |
| 0xC538 | Adressbuch Speicherbereich auf der HDD: korrupt |
| 0xC53A | Berechnungsfehler von dem Navigationsrechner |
| 0xE1E8 | Signal Kilometerstand: unplausibel |
| 0xC53F | Top-HiFi Amplifier Kommunikationsfehler |
| 0xC540 | Lautsprecherausgangsleitungen vorne links: Leitungsunterbrechung |
| 0xC541 | Lautsprecherausgangsleitungen vorne links: Kurzschluss nach Plus |
| 0xC542 | Lautsprecherausgangsleitungen vorne links: Kurzschluss nach Masse |
| 0xC543 | Lautsprecherausgangsleitungen vorne links: Kurzschluss zwischen den 2 Leitungen |
| 0xC544 | Lautsprecherausgangsleitungen vorne rechts: Leitungsunterbrechung |
| 0xC545 | Lautsprecherausgangsleitungen vorne rechts: Kurzschluss nach Plus |
| 0xC546 | Lautsprecherausgangsleitungen vorne rechts: Kurzschluss nach Masse |
| 0xC547 | Lautsprecherausgangsleitungen vorne rechts: Kurzschluss zwischen den 2 Leitungen |
| 0xC548 | Lautsprecherausgangsleitungen hinten links: Leitungsunterbrechung |
| 0xC549 | Lautsprecherausgangsleitungen hinten links: Kurzschluss nach Plus |
| 0xC54A | Lautsprecherausgangsleitungen hinten links: Kurzschluss nach Masse |
| 0xC54B | Lautsprecherausgangsleitungen hinten links: Kurzschluss zwischen den 2 Leitungen |
| 0xC54C | Lautsprecherausgangsleitungen hinten rechts: Leitungsunterbrechung |
| 0xC54D | Lautsprecherausgangsleitungen hinten rechts: Kurzschluss nach Plus |
| 0xC54E | Lautsprecherausgangsleitungen hinten rechts: Kurzschluss nach Masse |
| 0xC54F | Lautsprecherausgangsleitungen hinten rechts: Kurzschluss zwischen den 2 Leitungen |
| 0xC560 | FBAS-Eingang 1: kein Video- oder Sync-Signal vorhanden |
| 0xC561 | FBAS-Eingang 2: kein Video- oder Sync-Signal vorhanden |
| 0xC562 | FBAS-Eingang 3: kein Video- oder Sync-Signal vorhanden |
| 0xC563 | FBAS-Eingang 1: Signal außerhalb Toleranz |
| 0xC564 | FBAS-Eingang 2: Signal außerhalb Toleranz |
| 0xC565 | FBAS-Eingang 3: Signal außerhalb Toleranz |
| 0xC568 | RAD ON Leitung: Kurzschluss nach Plus |
| 0xC569 | RAD ON Leitung: Kurzschluss nach Masse |
| 0xC56C | Video Watch Dog wurde ausgelöst |
| 0xC5AA | Video Verbindung: keine oder ungültige Codierdaten-Informationen für die angeforderte Verbindung Quelle %s zu Senke %s. Verbindung nicht hergestellt |
| 0xC5AB | Video Verbindung: Fehler vom Video Switch %i beim Verbindungsversuch Quelle %s zu Senke %s. Verbindung nicht hergestellt |
| 0xC56D | Verbindung Head-Unit zum Mikrophon 1: Leitungsunterbrechung |
| 0xC56E | Verbindung Head-Unit zum Mikrophon 1: Kurzschluss nach Plus |
| 0xC56F | Verbindung Head-Unit zum Mikrophon 1: Kurzschluss nach Masse |
| 0xC573 | Festplattenlaufwerk Hardware Fehler |
| 0xC576 | DVD Laufwerk Hardware Fehler |
| 0xC57F | FB Kommunikationsfehler |
| 0xC580 | FB Hardware Fehler |
| 0xC581 | Keine Reaktion des ETC Moduls auf Anfrage-Nachrichten |
| 0xC583 | Lüfter Fehler |
| 0xC585 | Interner Temperatursfehler |
| 0xC587 | Das Einschlafen von dem GW wird verhindert |
| 0xC588 | Externe Unterspannung |
| 0xC589 | Externe Überspannung |
| 0xE1CC | Device hat die Monitoringnachricht nicht abgenommen oder bestaetigt (Error_Monitoring) |
| 0xE1CD | Weckendes Device hat 3 mal erfolglos versucht das Netzwerk zu wecken (Error_WakeUp_Failed) |
| 0xE1CE | Obwohl Shutdown(Execute) geschickt wurde ging das Licht nicht aus (Error_Light_Not_Off) |
| 0xE1CF | Zentrale Registry stimmt nicht mit der Sollkonfiguration ueberein (Error_Registry_New) |
| 0xE1D0 | Ringbruchdiagnose wurde durchgefuehrt (Error_Ring_Diagnose) |
| 0xE1D2 | Ein Device hat sich wegen Uebertemperatur abgeschaltet (Error_Temp_Shutdown) |
| 0xE1C4 | K-CAN Leitungsfehler |
| 0xE1C7 | K-CAN Kommunikationsfehler |
| 0xE1E9 | Ausfall von dem vorderen Bildschirm |
| 0xC58A | Flash Ethernet Verbindung: Link Status von dem Ethernet Treiber nicht ok |
| 0xC58C | USB-VBUS Verbindung Head-Unit zur USB Benutzer Schnittstelle: Kurzschluss nach Masse |
| 0xC58D | Abbruch des laufenden PIA-Ablaufs wegen Fahrzeugzustandsänderung |
| 0xC58E | Signatur der zu importierenden Portierungsdatei korrupt |
| 0xC58F | Dateistruktur der zu importierenden Portierungsdatei korrupt |
| 0xC590 | Version der zu importierenden Portierungsdatei unbekannt |
| 0xC591 | Abbruch des laufenden PIA-Ablaufs durch Benutzerinteraktion |
| 0xC592 | PIA Software Fehler |
| 0xC593 | Nicht genügend speicher auf externem Speichermedium |
| 0xC594 | Fehler beim Schreiben auf externes Speichermedium |
| 0xC595 | Fehler beim Lesen vom externen Speichermedium |
| 0xE1EB | Die Head Unit hat das Telegramm Status_Funkschlüssel vom CAS-Steuergerät nicht erhalten |
| 0xC597 | Das Telegramm Status_Funkschlüssel vom CAS-Steuergerät enthält nicht die von der Head Unit angeforderte Profilnummer |
| 0xC598 | Eine verbaute PIA-Funktion hat die Anfrage nach ihrem Einstellwert nicht beantwortet |
| 0xC599 | Eine PIA-Funktion, die bei der Konfigurationsanfrage nicht gefunden wurde, hat einen Einstellwert geschickt |
| 0xC59A | Eine verbaute PIA-Funktion hat das Setzen ihres Einstellwerts nicht bestätigt |
| 0xC59B | Eine PIA-Funktion meldet ihre Konfigurationsinformationen obwohl sie nicht dazu aufgefordert wurde |
| 0xC59C | Eine PIA-Funktion liefert korrupte Konfigurationsinformationen |
| 0xC59D | Für eine PIA-ID wurden mehrere Telegramme mit unterschiedlichen Konfigurationsinformationen geliefert |
| 0xC59E | Die von einer PIA-Funktion gelieferte aktuelle Profilnummer unterscheidet sich von der in der Head Unit vermerkten |
| 0xC59F | Codierungsfehler Arbeitsbereich |
| 0xC5A0 | Codierunsfehler Master Bereich |
| 0xC5A1 | Hauptplatine Hardware Fehler |
| 0xC5A2 | Flash File System fehlerhaft |
| 0xC5A3 | Schwerwiegender Software Fehler: Software neu flashen |
| 0xC5B6 | CD Laufwerk Hardware Fehler |
| 0xC5B7 | Medium Fehler im CD Laufwerk |
| 0xC5B8 | ATC Test negativ: CD Laufwerk defekt |
| 0xC5BB | NAND_CORRUPT_THIS_LC |
| 0xC5BC | NAND_WILL_BE_FORMATED |
| 0xC5BD | CIRTICAL_UNDERVOLTAGE_DURING_FLASH_THIS_LC |
| 0xC5BE | CIRTICAL_UNDERVOLTAGE_DURING_ANY_LC |
| 0xC5BF | SDARS Module nicht aktiv |
| 0x10E0 | Error_Software_Fault |
| 0xE1EA | PDC Signal: unplausibel |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 50 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x10F0 | SDARS Modul: interner Reset |
| 0x10F1 | SDARS Modul: Kommunikationsfehler |
| 0x1040 | Ursache Festplattenfehler |
| 0x1041 | Ursache Initialisierungsfehler der Festplatte |
| 0x1042 | HDD: SMART Status nah vom kritischen Zustand |
| 0x1120 | Ursache CD Laufwerk Fehler |
| 0x1060 | Ursache DVD Laufwerk Fehler |
| 0x1061 | Ursache DVD Laufwerk Initianilisierungsfehler |
| 0x1062 | Ursache Lad- / Auswurffehler |
| 0x1121 | Ursache Lad- / Auswurffehler |
| 0x1130 | Ursache Medium Detektierungsfehler |
| 0x1090 | FB Protokollfehler |
| 0x1091 | FB Alive Fehler |
| 0x1093 | FB Softwarefehler |
| 0x9308 | Device bekam Reset (Error_Reset) |
| 0x9309 | Bis zum Auftreten des Timeouts konnte kein Licht bzw. kein stabiler Lock erkannt werden (Error_NSInit_Timeout) |
| 0x930A | Device ist im Zustand Normal Operation und das Licht am Eingang geht ohne Vorankuendigung aus (Error_Sudden_light_off) |
| 0x930B | Anfragendes Device bekommt keine Antwort obwohl Partner vorhanden ist (Error_Device_No_Answer) |
| 0x930C | Kurze Unlocks (Error_Unlock_Short) |
| 0x930F | Ein Device hat im laufenden Betrieb seinen Bypass All geschlossen (Error_NCE) |
| 0x9310 | Empfaenger hat eine Nachricht nicht abgenommen (Error_NAK) |
| 0x9311 | Lange und/oder haeufige Unlocks (Error_Unlock_Long) |
| 0x10A0 | Ursache V850 RAM Fehler |
| 0x10A1 | Ursache E2P Checksum Fehler |
| 0x10A2 | Ursache Videodecoder Fehler |
| 0x10A3 | Ursache keine Kommunikation mit der Tuner Hardware |
| 0x10A4 | Ursache keine Kommunikation mit der DAB Tuner Hardware |
| 0x10A5 | Ursache keine IPC Kommunikation möglich |
| 0x10C0 | Ursache FBlock NWM nicht vorhanden |
| 0x10D0 | PDC interner Fehler |
| 0x10D1 | Reset: Ursache ONOFF_ERROR |
| 0x10D2 | Reset: Ursache ONOFF_EMERGENCY_ERROR |
| 0x10D3 | Reset: Ursache HMI_DIED |
| 0x10D4 | Reset: Ursache ASN_NAVI_DIED |
| 0x10D5 | Reset: Ursache CHILD_DIED |
| 0x10D6 | Reset: Ursache THREAD_WATCHDOG |
| 0x10D7 | Reset: Ursache DSP_WATCHDOG |
| 0x10D8 | Reset: Ursache DSP_INIT_ERROR |
| 0x10D9 | Reset: Ursache LAYERMANAGER_DIED |
| 0x10E0 | Software Fehler, CoreDumps vorhanden |
| 0x1150 | Eine PIA-Funktion, die bei der Konfigurationsanfrage nicht gefunden wurde, hat einen Einstellwert geschickt |
| 0x1151 | Eine verbaute PIA-Funktion hat das Setzen ihres Einstellwerts nicht bestätigt |
| 0x1152 | Eine PIA-Funktion meldet ihre Konfigurationsinformationen obwohl sie nicht dazu aufgefordert wurde |
| 0x1153 | Eine PIA-Funktion liefert korrupte Konfigurationsinformationen |
| 0x1154 | Für eine PIA-ID wurden mehrere Telegramme mit unterschiedlichen Konfigurationsinformationen geliefert |
| 0x1155 | Positionierung über 10 Minuten nicht möglich |
| 0x1157 | Video Watch Dog wurde ausgelöst |
| 0x1158 | Abbruch des laufenden PIA-Ablaufs wegen Fahrzeugzustandsänderung |
| 0x1159 | NAND_PARTITION_NOT_AVILABLE |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-tnodetype"></a>
### TNODETYPE

Dimensions: 6 rows × 2 columns

| MASKE | TEXT |
| --- | --- |
| 0x00 | Virtual Function-Block |
| 0x01 | Local Function-Block |
| 0x02 | External Function-Block |
| 0x03 | Virtual Function-Block-Model |
| 0x04 | Local Function-Block-Model |
| 0x05 | External Function-Block-Model |

<a id="table-tpre-pro-swi-state"></a>
### TPRE_PRO_SWI_STATE

Dimensions: 4 rows × 2 columns

| NAME | MASKE |
| --- | --- |
| Classic | 0x00 |
| Compressed Intel | 0x01 |
| Compressed Motorola | 0x02 |
| Unknown | 0xXY |

<a id="table-tinc-gw-tab"></a>
### TINC_GW_TAB

Dimensions: 4 rows × 2 columns

| NAME | MASKE |
| --- | --- |
| Classic / Invalid | 0x00 |
| Compressed Intel | 0x01 |
| Compressed Motorola | 0x02 |
| Unknown | 0xXY |

<a id="table-tradioeinausstatus"></a>
### TRADIOEINAUSSTATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Radio aus |
| 0x01 | Radio ein |
| 0xFF | Nicht definiert |

<a id="table-tladevorgangsprachpaket"></a>
### TLADEVORGANGSPRACHPAKET

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Ladevorgang nicht gestartet |
| 0x01 | Ladevorgang läuft |
| 0x02 | Ladevorgang beendet ohne Fehler |
| 0x03 | Ladevorgang beendet mit Fehler |
| 0x04 | Ladevorgang abgebrochen |
| 0xFF | Nicht definiert |

<a id="table-tfehlerursachesprachpaket"></a>
### TFEHLERURSACHESPRACHPAKET

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0xFF | Nicht definiert |

<a id="table-tflottenmodus"></a>
### TFLOTTENMODUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Keine NAVI DVD Sperre |
| 1 | NAVI DVD Sperre mit PIN-Code |
| 2 | Permanente NAVI DVD Sperre |
| 255 | Nicht definiert |

<a id="table-tgpstimevalidity"></a>
### TGPSTIMEVALIDITY

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Zeit ist gueltig |
| 0x01 | Zeit ist nicht gueltig |
| 0xFF | Nicht definiert |

<a id="table-tusbteststatus"></a>
### TUSBTESTSTATUS

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kein Gerät angeschlossen |
| 0x01 | Gerät angeschlossen, Erkennung läuft |
| 0x02 | Gerät erkannt aber falsche ID |
| 0x03 | Gerät angeschlossen und richtige ID |
| 0xFE | Gerät angeschlossen aber kein Massenspeicher |
| 0xFF | Nicht definiert |

<a id="table-tinternalaccelerationsensorstatus"></a>
### TINTERNALACCELERATIONSENSORSTATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Beschleunigungssensor OK |
| 0x01 | Beschleunigungssensor defekt |
| 0xFF | Nicht definiert |

<a id="table-tab-test-status"></a>
### TAB_TEST_STATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Test laeuft noch |
| 0x01 | Test beendet, Resultrueckgabe |
| 0x02 | Test abgebrochen, Resultrueckgabe |
| 0xFF | Fehlerbericht |

<a id="table-tinternalgyrostatus"></a>
### TINTERNALGYROSTATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Gyro OK |
| 0x01 | Gyro defekt |
| 0xFF | Nicht definiert |

<a id="table-tvideoeingangfehlerart"></a>
### TVIDEOEINGANGFEHLERART

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | kein Video- oder Sync-Signal vorhanden |
| 0x01 | Signal außerhalb der Toleranz |
| 0x02 | Verbindung konnte nicht hergestellt werden |
| 0xFF | Nicht definiert |

<a id="table-tfbaseingang"></a>
### TFBASEINGANG

Dimensions: 180 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00000000 | Alle Eingänge |
| 0x00000001 | FBAS-Eingang 1 |
| 0x00000002 | FBAS-Eingang 2 |
| 0x00000003 | FBAS-Eingang 1 und 2 |
| 0x00000004 | FBAS-Eingang 3 |
| 0x00000005 | FBAS-Eingang 1 und 3 |
| 0x00000006 | FBAS-Eingang 2 und 3 |
| 0x00000007 | FBAS-Eingang 1, 2 und 3 |
| 0x00000008 | FBAS-Eingang 4 |
| 0x00000009 | FBAS-Eingang 1 und 4 |
| 0x0000000A | FBAS-Eingang 2 und 4 |
| 0x0000000B | FBAS-Eingang 1, 2 und 4 |
| 0x0000000C | FBAS-Eingang 3 und 4 |
| 0x0000000D | FBAS-Eingang 1, 2 und 4 |
| 0x0000000E | FBAS-Eingang 2, 3 und 4 |
| 0x0000000F | FBAS-Eingang 1, 2, 3 und 4 |
| 0x00000010 | FBAS-Eingang 5 |
| 0x00000011 | FBAS-Eingang 1 und 5 |
| 0x00000012 | FBAS-Eingang 2 und 5 |
| 0x00000013 | FBAS-Eingang 1,2 und 5 |
| 0x00000014 | FBAS-Eingang 3 und 5 |
| 0x00000015 | FBAS-Eingang 1,3 und 5 |
| 0x00000016 | FBAS-Eingang 2,3 und 5 |
| 0x00000017 | FBAS-Eingang 1, 2 und 3 und 5 |
| 0x00000018 | FBAS-Eingang 4 und 5 |
| 0x00000019 | FBAS-Eingang 1, 4 und 5 |
| 0x0000001A | FBAS-Eingang 2, 4 und 5 |
| 0x0000001B | FBAS-Eingang 1, 2, 4 und 5 |
| 0x0000001C | FBAS-Eingang 3, 4 und 5 |
| 0x0000001D | FBAS-Eingang 1, 2, 4 und 5 |
| 0x0000001E | FBAS-Eingang 2, 3, 4 und 5 |
| 0x0000001F | FBAS-Eingang 1, 2, 3, 4 und 5 |
| 0x00000020 | FBAS-Eingang 6 |
| 0x00000021 | FBAS-Eingang 1 und 6 |
| 0x00000022 | FBAS-Eingang 2 und 6 |
| 0x00000023 | FBAS-Eingang 1, 2 und 6 |
| 0x00000024 | FBAS-Eingang 3 und 6 |
| 0x00000025 | FBAS-Eingang 1, 3 und 6 |
| 0x00000026 | FBAS-Eingang 2, 3 und 6 |
| 0x00000027 | FBAS-Eingang 1, 2, 3 und 6 |
| 0x00000028 | FBAS-Eingang 4 und 6 |
| 0x00000029 | FBAS-Eingang 1, 4 und 6 |
| 0x0000002A | FBAS-Eingang 2, 4 und 6 |
| 0x0000002B | FBAS-Eingang 1, 2, 4 und 6 |
| 0x0000002C | FBAS-Eingang 3, 4 und 6 |
| 0x0000002D | FBAS-Eingang 1, 2, 4 und 6 |
| 0x0000002E | FBAS-Eingang 2, 3, 4 und 6 |
| 0x0000002F | FBAS-Eingang 1, 2, 3, 4 und 6 |
| 0x00000030 | FBAS-Eingang 5 und 6 |
| 0x00000031 | FBAS-Eingang 1, 5 und 6 |
| 0x00000032 | FBAS-Eingang 2, 5 und 6 |
| 0x00000033 | FBAS-Eingang 1,2, 5 und 6 |
| 0x00000034 | FBAS-Eingang 3, 5 und 6 |
| 0x00000035 | FBAS-Eingang 1,3, 5 und 6 |
| 0x00000036 | FBAS-Eingang 2,3, 5 und 6 |
| 0x00000037 | FBAS-Eingang 1, 2, 3, 5 und 6 |
| 0x00000038 | FBAS-Eingang 4, 5 und 6 |
| 0x00000039 | FBAS-Eingang 1, 4, 5 und 6 |
| 0x0000003A | FBAS-Eingang 2, 4, 5 und 6 |
| 0x0000003B | FBAS-Eingang 1, 2, 4, 5 und 6 |
| 0x0000003C | FBAS-Eingang 3, 4, 5 und 6 |
| 0x0000003D | FBAS-Eingang 1, 2, 4, 5 und 6 |
| 0x0000003E | FBAS-Eingang 2, 3, 4, 5 und 6 |
| 0x0000003F | FBAS-Eingang 1, 2, 3, 4, 5 und 6 |
| 0x00000040 | FBAS-Eingang 7 |
| 0x00000041 | FBAS-Eingang 1 und 7 |
| 0x00000042 | FBAS-Eingang 2 und 7 |
| 0x00000043 | FBAS-Eingang 1, 2 und 7 |
| 0x00000044 | FBAS-Eingang 3 und 7 |
| 0x00000045 | FBAS-Eingang 1, 3 und 7 |
| 0x00000046 | FBAS-Eingang 2, 3 und 7 |
| 0x00000047 | FBAS-Eingang 1, 2, 3 und 7 |
| 0x00000048 | FBAS-Eingang 4 und 7 |
| 0x00000049 | FBAS-Eingang 1, 4 und 7 |
| 0x0000004A | FBAS-Eingang 2, 4 und 7 |
| 0x0000004B | FBAS-Eingang 1, 2, 4 und 7 |
| 0x0000004C | FBAS-Eingang 3, 4 und 7 |
| 0x0000004D | FBAS-Eingang 1, 2, 4 und 7 |
| 0x0000004E | FBAS-Eingang 2, 3, 4 und 7 |
| 0x0000004F | FBAS-Eingang 1, 2, 3, 4 und 7 |
| 0x00000050 | FBAS-Eingang 5 und 7 |
| 0x00000051 | FBAS-Eingang 1, 5 und 7 |
| 0x00000052 | FBAS-Eingang 2, 5 und 7 |
| 0x00000053 | FBAS-Eingang 1,2, 5 und 7 |
| 0x00000054 | FBAS-Eingang 3, 5 und 7 |
| 0x00000055 | FBAS-Eingang 1,3, 5 und 7 |
| 0x00000056 | FBAS-Eingang 2,3, 5 und 7 |
| 0x00000057 | FBAS-Eingang 1, 2, 3, 5 und 7 |
| 0x00000058 | FBAS-Eingang 4, 5 und 7 |
| 0x00000059 | FBAS-Eingang 1, 4, 5 und 7 |
| 0x0000005A | FBAS-Eingang 2, 4, 5 und 7 |
| 0x0000005B | FBAS-Eingang 1, 2, 4, 5 und 7 |
| 0x0000005C | FBAS-Eingang 3, 4, 5 und 7 |
| 0x0000005D | FBAS-Eingang 1, 2, 4, 5 und 7 |
| 0x0000005E | FBAS-Eingang 2, 3, 4, 5 und 7 |
| 0x0000005F | FBAS-Eingang 1, 2, 3, 4, 5 und 7 |
| 0x00000060 | FBAS-Eingang 6 und 7 |
| 0x00000061 | FBAS-Eingang 1, 6 und 7 |
| 0x00000062 | FBAS-Eingang 2, 6 und 7 |
| 0x00000063 | FBAS-Eingang 1, 2, 6 und 7 |
| 0x00000064 | FBAS-Eingang 3, 6 und 7 |
| 0x00000065 | FBAS-Eingang 1, 3, 6 und 7 |
| 0x00000066 | FBAS-Eingang 2, 3, 6 und 7 |
| 0x00000067 | FBAS-Eingang 1, 2, 3, 6 und 7 |
| 0x00000068 | FBAS-Eingang 4, 6 und 7 |
| 0x00000069 | FBAS-Eingang 1, 4, 6 und 7 |
| 0x0000006A | FBAS-Eingang 2, 4, 6 und 7 |
| 0x0000006B | FBAS-Eingang 1, 2, 4, 6 und 7 |
| 0x0000006C | FBAS-Eingang 3, 4, 6 und 7 |
| 0x0000006D | FBAS-Eingang 1, 2, 4, 6 und 7 |
| 0x0000006E | FBAS-Eingang 2, 3, 4, 6 und 7 |
| 0x0000006F | FBAS-Eingang 1, 2, 3, 4, 6 und 7 |
| 0x00000070 | FBAS-Eingang 5, 6 und 7 |
| 0x00000071 | FBAS-Eingang 1, 5, 6 und 7 |
| 0x00000072 | FBAS-Eingang 2, 5, 6 und 7 |
| 0x00000073 | FBAS-Eingang 1,2, 5, 6 und 7 |
| 0x00000074 | FBAS-Eingang 3, 5, 6 und 7 |
| 0x00000075 | FBAS-Eingang 1,3, 5, 6 und 7 |
| 0x00000076 | FBAS-Eingang 2,3, 5, 6 und 7 |
| 0x00000077 | FBAS-Eingang 1, 2, 3, 5, 6 und 7 |
| 0x00000078 | FBAS-Eingang 4, 5, 6 und 7 |
| 0x00000079 | FBAS-Eingang 1, 4, 5, 6 und 7 |
| 0x0000007A | FBAS-Eingang 2, 4, 5, 6 und 7 |
| 0x0000007B | FBAS-Eingang 1, 2, 4, 5, 6 und 7 |
| 0x0000007C | FBAS-Eingang 3, 4, 5, 6 und 7 |
| 0x0000007D | FBAS-Eingang 1, 2, 4, 5, 6 und 7 |
| 0x0000007E | FBAS-Eingang 2, 3, 4, 5, 6 und 7 |
| 0x0000007F | FBAS-Eingang 1, 2, 3, 4, 5, 6 und 7 |
| 0x00000080 | FBAS-Eingang 8 |
| 0x00000081 | FBAS-Eingang 1 und 8 |
| 0x00000082 | FBAS-Eingang 2 und 8 |
| 0x00000083 | FBAS-Eingang 1, 2 und 8 |
| 0x00000084 | FBAS-Eingang 3 und 8 |
| 0x00000085 | FBAS-Eingang 1, 3 und 8 |
| 0x00000086 | FBAS-Eingang 2, 3 und 8 |
| 0x00000087 | FBAS-Eingang 1, 2, 3 und 8 |
| 0x00000088 | FBAS-Eingang 4 und 8 |
| 0x00000089 | FBAS-Eingang 1, 4 und 8 |
| 0x0000008A | FBAS-Eingang 2, 4 und 8 |
| 0x0000008B | FBAS-Eingang 1, 2, 4 und 8 |
| 0x0000008C | FBAS-Eingang 3, 4 und 8 |
| 0x0000008D | FBAS-Eingang 1, 2, 4 und 8 |
| 0x0000008E | FBAS-Eingang 2, 3, 4 und 8 |
| 0x0000008F | FBAS-Eingang 1, 2, 3, 4 und 8 |
| 0x00000090 | FBAS-Eingang 5 und 8 |
| 0x00000091 | FBAS-Eingang 1, 5 und 8 |
| 0x00000092 | FBAS-Eingang 2, 5 und 8 |
| 0x00000093 | FBAS-Eingang 1,2, 5 und 8 |
| 0x00000094 | FBAS-Eingang 3, 5 und 8 |
| 0x00000095 | FBAS-Eingang 1,3, 5 und 8 |
| 0x00000096 | FBAS-Eingang 2,3, 5 und 8 |
| 0x00000097 | FBAS-Eingang 1, 2, 3, 5 und 8 |
| 0x00000098 | FBAS-Eingang 4, 5 und 8 |
| 0x00000099 | FBAS-Eingang 1, 4, 5 und 8 |
| 0x0000009A | FBAS-Eingang 2, 4, 5 und 8 |
| 0x0000009B | FBAS-Eingang 1, 2, 4, 5 und 8 |
| 0x0000009C | FBAS-Eingang 3, 4, 5 und 8 |
| 0x0000009D | FBAS-Eingang 1, 2, 4, 5 und 8 |
| 0x0000009E | FBAS-Eingang 2, 3, 4, 5 und 8 |
| 0x0000009F | FBAS-Eingang 1, 2, 3, 4, 5 und 8 |
| 0x000000A0 | FBAS-Eingang 6 und 8 |
| 0x000000A1 | FBAS-Eingang 1, 6 und 8 |
| 0x000000A2 | FBAS-Eingang 2, 6 und 8 |
| 0x000000A3 | FBAS-Eingang 1, 2, 6 und 8 |
| 0x000000A4 | FBAS-Eingang 3, 6 und 8 |
| 0x000000A5 | FBAS-Eingang 1, 3, 6 und 8 |
| 0x000000A6 | FBAS-Eingang 2, 3, 6 und 8 |
| 0x000000A7 | FBAS-Eingang 1, 2, 3, 6 und 8 |
| 0x000000A8 | FBAS-Eingang 4, 6 und 8 |
| 0x000000A9 | FBAS-Eingang 1, 4, 6 und 8 |
| 0x000000AA | FBAS-Eingang 2, 4, 6 und 8 |
| 0x000000AB | FBAS-Eingang 1, 2, 4, 6 und 8 |
| 0x000000AC | FBAS-Eingang 3, 4, 6 und 8 |
| 0x000000AD | FBAS-Eingang 1, 2, 4, 6 und 8 |
| 0x000000AE | FBAS-Eingang 2, 3, 4, 6 und 8 |
| 0x000000AF | FBAS-Eingang 1, 2, 3, 4, 6 und 8 |
| 0x000000B0 | FBAS-Eingang 5, 6 und 8 |
| 0x000000B1 | FBAS-Eingang 1, 5, 6 und 8 |
| 0x000000B2 | FBAS-Eingang 2, 5, 6 und 8 |
| 0x000000B3 | FBAS-Eingang 1,2, 5, 6 und 8 |

<a id="table-teingangvideoswitch"></a>
### TEINGANGVIDEOSWITCH

Dimensions: 513 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | Kein VideoSwitch vorhanden bzw. verwendet |
| 0x0001 | Eingang 1 |
| 0x0002 | Eingang 2 |
| 0x0003 | Eingang 1 und 2 |
| 0x0004 | Eingang 3 |
| 0x0005 | Eingang 1 und 3 |
| 0x0006 | Eingang 2 und 3 |
| 0x0007 | Eingang 1, 2 und 3 |
| 0x0008 | Eingang 4 |
| 0x0009 | Eingang 1 und 4 |
| 0x000A | Eingang 2 und 4 |
| 0x000B | Eingang 1, 2 und 4 |
| 0x000C | Eingang 3 und 4 |
| 0x000D | Eingang 1, 2 und 4 |
| 0x000E | Eingang 2, 3 und 4 |
| 0x000F | Eingang 1, 2, 3 und 4 |
| 0x0010 | Eingang 5 |
| 0x0011 | Eingang 1 und 5 |
| 0x0012 | Eingang 2 und 5 |
| 0x0013 | Eingang 1,2 und 5 |
| 0x0014 | Eingang 3 und 5 |
| 0x0015 | Eingang 1,3 und 5 |
| 0x0016 | Eingang 2,3 und 5 |
| 0x0017 | Eingang 1, 2 und 3 und 5 |
| 0x0018 | Eingang 4 und 5 |
| 0x0019 | Eingang 1, 4 und 5 |
| 0x001A | Eingang 2, 4 und 5 |
| 0x001B | Eingang 1, 2, 4 und 5 |
| 0x001C | Eingang 3, 4 und 5 |
| 0x001D | Eingang 1, 2, 4 und 5 |
| 0x001E | Eingang 2, 3, 4 und 5 |
| 0x001F | Eingang 1, 2, 3, 4 und 5 |
| 0x0020 | Eingang 6 |
| 0x0021 | Eingang 1 und 6 |
| 0x0022 | Eingang 2 und 6 |
| 0x0023 | Eingang 1, 2 und 6 |
| 0x0024 | Eingang 3 und 6 |
| 0x0025 | Eingang 1, 3 und 6 |
| 0x0026 | Eingang 2, 3 und 6 |
| 0x0027 | Eingang 1, 2, 3 und 6 |
| 0x0028 | Eingang 4 und 6 |
| 0x0029 | Eingang 1, 4 und 6 |
| 0x002A | Eingang 2, 4 und 6 |
| 0x002B | Eingang 1, 2, 4 und 6 |
| 0x002C | Eingang 3, 4 und 6 |
| 0x002D | Eingang 1, 2, 4 und 6 |
| 0x002E | Eingang 2, 3, 4 und 6 |
| 0x002F | Eingang 1, 2, 3, 4 und 6 |
| 0x0030 | Eingang 5 und 6 |
| 0x0031 | Eingang 1, 5 und 6 |
| 0x0032 | Eingang 2, 5 und 6 |
| 0x0033 | Eingang 1,2, 5 und 6 |
| 0x0034 | Eingang 3, 5 und 6 |
| 0x0035 | Eingang 1,3, 5 und 6 |
| 0x0036 | Eingang 2,3, 5 und 6 |
| 0x0037 | Eingang 1, 2, 3, 5 und 6 |
| 0x0038 | Eingang 4, 5 und 6 |
| 0x0039 | Eingang 1, 4, 5 und 6 |
| 0x003A | Eingang 2, 4, 5 und 6 |
| 0x003B | Eingang 1, 2, 4, 5 und 6 |
| 0x003C | Eingang 3, 4, 5 und 6 |
| 0x003D | Eingang 1, 2, 4, 5 und 6 |
| 0x003E | Eingang 2, 3, 4, 5 und 6 |
| 0x003F | Eingang 1, 2, 3, 4, 5 und 6 |
| 0x0040 | Eingang 7 |
| 0x0041 | Eingang 1 und 7 |
| 0x0042 | Eingang 2 und 7 |
| 0x0043 | Eingang 1, 2 und 7 |
| 0x0044 | Eingang 3 und 7 |
| 0x0045 | Eingang 1, 3 und 7 |
| 0x0046 | Eingang 2, 3 und 7 |
| 0x0047 | Eingang 1, 2, 3 und 7 |
| 0x0048 | Eingang 4 und 7 |
| 0x0049 | Eingang 1, 4 und 7 |
| 0x004A | Eingang 2, 4 und 7 |
| 0x004B | Eingang 1, 2, 4 und 7 |
| 0x004C | Eingang 3, 4 und 7 |
| 0x004D | Eingang 1, 2, 4 und 7 |
| 0x004E | Eingang 2, 3, 4 und 7 |
| 0x004F | Eingang 1, 2, 3, 4 und 7 |
| 0x0050 | Eingang 5 und 7 |
| 0x0051 | Eingang 1, 5 und 7 |
| 0x0052 | Eingang 2, 5 und 7 |
| 0x0053 | Eingang 1,2, 5 und 7 |
| 0x0054 | Eingang 3, 5 und 7 |
| 0x0055 | Eingang 1,3, 5 und 7 |
| 0x0056 | Eingang 2,3, 5 und 7 |
| 0x0057 | Eingang 1, 2, 3, 5 und 7 |
| 0x0058 | Eingang 4, 5 und 7 |
| 0x0059 | Eingang 1, 4, 5 und 7 |
| 0x005A | Eingang 2, 4, 5 und 7 |
| 0x005B | Eingang 1, 2, 4, 5 und 7 |
| 0x005C | Eingang 3, 4, 5 und 7 |
| 0x005D | Eingang 1, 2, 4, 5 und 7 |
| 0x005E | Eingang 2, 3, 4, 5 und 7 |
| 0x005F | Eingang 1, 2, 3, 4, 5 und 7 |
| 0x0060 | Eingang 6 und 7 |
| 0x0061 | Eingang 1, 6 und 7 |
| 0x0062 | Eingang 2, 6 und 7 |
| 0x0063 | Eingang 1, 2, 6 und 7 |
| 0x0064 | Eingang 3, 6 und 7 |
| 0x0065 | Eingang 1, 3, 6 und 7 |
| 0x0066 | Eingang 2, 3, 6 und 7 |
| 0x0067 | Eingang 1, 2, 3, 6 und 7 |
| 0x0068 | Eingang 4, 6 und 7 |
| 0x0069 | Eingang 1, 4, 6 und 7 |
| 0x006A | Eingang 2, 4, 6 und 7 |
| 0x006B | Eingang 1, 2, 4, 6 und 7 |
| 0x006C | Eingang 3, 4, 6 und 7 |
| 0x006D | Eingang 1, 2, 4, 6 und 7 |
| 0x006E | Eingang 2, 3, 4, 6 und 7 |
| 0x006F | Eingang 1, 2, 3, 4, 6 und 7 |
| 0x0070 | Eingang 5, 6 und 7 |
| 0x0071 | Eingang 1, 5, 6 und 7 |
| 0x0072 | Eingang 2, 5, 6 und 7 |
| 0x0073 | Eingang 1,2, 5, 6 und 7 |
| 0x0074 | Eingang 3, 5, 6 und 7 |
| 0x0075 | Eingang 1,3, 5, 6 und 7 |
| 0x0076 | Eingang 2,3, 5, 6 und 7 |
| 0x0077 | Eingang 1, 2, 3, 5, 6 und 7 |
| 0x0078 | Eingang 4, 5, 6 und 7 |
| 0x0079 | Eingang 1, 4, 5, 6 und 7 |
| 0x007A | Eingang 2, 4, 5, 6 und 7 |
| 0x007B | Eingang 1, 2, 4, 5, 6 und 7 |
| 0x007C | Eingang 3, 4, 5, 6 und 7 |
| 0x007D | Eingang 1, 2, 4, 5, 6 und 7 |
| 0x007E | Eingang 2, 3, 4, 5, 6 und 7 |
| 0x007F | Eingang 1, 2, 3, 4, 5, 6 und 7 |
| 0x0080 | Eingang 8 |
| 0x0081 | Eingang 1 und 8 |
| 0x0082 | Eingang 2 und 8 |
| 0x0083 | Eingang 1, 2 und 8 |
| 0x0084 | Eingang 3 und 8 |
| 0x0085 | Eingang 1, 3 und 8 |
| 0x0086 | Eingang 2, 3 und 8 |
| 0x0087 | Eingang 1, 2, 3 und 8 |
| 0x0088 | Eingang 4 und 8 |
| 0x0089 | Eingang 1, 4 und 8 |
| 0x008A | Eingang 2, 4 und 8 |
| 0x008B | Eingang 1, 2, 4 und 8 |
| 0x008C | Eingang 3, 4 und 8 |
| 0x008D | Eingang 1, 2, 4 und 8 |
| 0x008E | Eingang 2, 3, 4 und 8 |
| 0x008F | Eingang 1, 2, 3, 4 und 8 |
| 0x0090 | Eingang 5 und 8 |
| 0x0091 | Eingang 1, 5 und 8 |
| 0x0092 | Eingang 2, 5 und 8 |
| 0x0093 | Eingang 1,2, 5 und 8 |
| 0x0094 | Eingang 3, 5 und 8 |
| 0x0095 | Eingang 1,3, 5 und 8 |
| 0x0096 | Eingang 2,3, 5 und 8 |
| 0x0097 | Eingang 1, 2, 3, 5 und 8 |
| 0x0098 | Eingang 4, 5 und 8 |
| 0x0099 | Eingang 1, 4, 5 und 8 |
| 0x009A | Eingang 2, 4, 5 und 8 |
| 0x009B | Eingang 1, 2, 4, 5 und 8 |
| 0x009C | Eingang 3, 4, 5 und 8 |
| 0x009D | Eingang 1, 2, 4, 5 und 8 |
| 0x009E | Eingang 2, 3, 4, 5 und 8 |
| 0x009F | Eingang 1, 2, 3, 4, 5 und 8 |
| 0x00A0 | Eingang 6 und 8 |
| 0x00A1 | Eingang 1, 6 und 8 |
| 0x00A2 | Eingang 2, 6 und 8 |
| 0x00A3 | Eingang 1, 2, 6 und 8 |
| 0x00A4 | Eingang 3, 6 und 8 |
| 0x00A5 | Eingang 1, 3, 6 und 8 |
| 0x00A6 | Eingang 2, 3, 6 und 8 |
| 0x00A7 | Eingang 1, 2, 3, 6 und 8 |
| 0x00A8 | Eingang 4, 6 und 8 |
| 0x00A9 | Eingang 1, 4, 6 und 8 |
| 0x00AA | Eingang 2, 4, 6 und 8 |
| 0x00AB | Eingang 1, 2, 4, 6 und 8 |
| 0x00AC | Eingang 3, 4, 6 und 8 |
| 0x00AD | Eingang 1, 2, 4, 6 und 8 |
| 0x00AE | Eingang 2, 3, 4, 6 und 8 |
| 0x00AF | Eingang 1, 2, 3, 4, 6 und 8 |
| 0x00B0 | Eingang 5, 6 und 8 |
| 0x00B1 | Eingang 1, 5, 6 und 8 |
| 0x00B2 | Eingang 2, 5, 6 und 8 |
| 0x00B3 | Eingang 1,2, 5, 6 und 8 |
| 0x00B4 | Eingang 3, 5, 6 und 8 |
| 0x00B5 | Eingang 1,3, 5, 6 und 8 |
| 0x00B6 | Eingang 2,3, 5, 6 und 8 |
| 0x00B7 | Eingang 1, 2, 3, 5, 6 und 8 |
| 0x00B8 | Eingang 4, 5, 6 und 8 |
| 0x00B9 | Eingang 1, 4, 5, 6 und 8 |
| 0x00BA | Eingang 2, 4, 5, 6 und 8 |
| 0x00BB | Eingang 1, 2, 4, 5, 6 und 8 |
| 0x00BC | Eingang 3, 4, 5, 6 und 8 |
| 0x00BD | Eingang 1, 2, 4, 5, 6 und 8 |
| 0x00BE | Eingang 2, 3, 4, 5, 6 und 8 |
| 0x00BF | Eingang 1, 2, 3, 4, 5, 6 und 8 |
| 0x00C0 | Eingang 7 und 8 |
| 0x00C1 | Eingang 1, 7 und 8 |
| 0x00C2 | Eingang 2, 7 und 8 |
| 0x00C3 | Eingang 1, 2, 7 und 8 |
| 0x00C4 | Eingang 3, 7 und 8 |
| 0x00C5 | Eingang 1, 3, 7 und 8 |
| 0x00C6 | Eingang 2, 3, 7 und 8 |
| 0x00C7 | Eingang 1, 2, 3, 7 und 8 |
| 0x00C8 | Eingang 4, 7 und 8 |
| 0x00C9 | Eingang 1, 4, 7 und 8 |
| 0x00CA | Eingang 2, 4, 7 und 8 |
| 0x00CB | Eingang 1, 2, 4, 7 und 8 |
| 0x00CC | Eingang 3, 4, 7 und 8 |
| 0x00CD | Eingang 1, 2, 4, 7 und 8 |
| 0x00CE | Eingang 2, 3, 4, 7 und 8 |
| 0x00CF | Eingang 1, 2, 3, 4, 7 und 8 |
| 0x00D0 | Eingang 5, 7 und 8 |
| 0x00D1 | Eingang 1, 5, 7 und 8 |
| 0x00D2 | Eingang 2, 5, 7 und 8 |
| 0x00D3 | Eingang 1,2, 5, 7 und 8 |
| 0x00D4 | Eingang 3, 5, 7 und 8 |
| 0x00D5 | Eingang 1,3, 5, 7 und 8 |
| 0x00D6 | Eingang 2,3, 5, 7 und 8 |
| 0x00D7 | Eingang 1, 2, 3, 5, 7 und 8 |
| 0x00D8 | Eingang 4, 5, 7 und 8 |
| 0x00D9 | Eingang 1, 4, 5, 7 und 8 |
| 0x00DA | Eingang 2, 4, 5, 7 und 8 |
| 0x00DB | Eingang 1, 2, 4, 5, 7 und 8 |
| 0x00DC | Eingang 3, 4, 5, 7 und 8 |
| 0x00DD | Eingang 1, 2, 4, 5, 7 und 8 |
| 0x00DE | Eingang 2, 3, 4, 5, 7 und 8 |
| 0x00DF | Eingang 1, 2, 3, 4, 5, 7 und 8 |
| 0x00E0 | Eingang 6, 7 und 8 |
| 0x00E1 | Eingang 1, 6, 7 und 8 |
| 0x00E2 | Eingang 2, 6, 7 und 8 |
| 0x00E3 | Eingang 1, 2, 6, 7 und 8 |
| 0x00E4 | Eingang 3, 6, 7 und 8 |
| 0x00E5 | Eingang 1, 3, 6, 7 und 8 |
| 0x00E6 | Eingang 2, 3, 6, 7 und 8 |
| 0x00E7 | Eingang 1, 2, 3, 6, 7 und 8 |
| 0x00E8 | Eingang 4, 6, 7 und 8 |
| 0x00E9 | Eingang 1, 4, 6, 7 und 8 |
| 0x00EA | Eingang 2, 4, 6, 7 und 8 |
| 0x00EB | Eingang 1, 2, 4, 6, 7 und 8 |
| 0x00EC | Eingang 3, 4, 6, 7 und 8 |
| 0x00ED | Eingang 1, 2, 4, 6, 7 und 8 |
| 0x00EE | Eingang 2, 3, 4, 6, 7 und 8 |
| 0x00EF | Eingang 1, 2, 3, 4, 6, 7 und 8 |
| 0x00F0 | Eingang 5, 6, 7 und 8 |
| 0x00F1 | Eingang 1, 5, 6, 7 und 8 |
| 0x00F2 | Eingang 2, 5, 6, 7 und 8 |
| 0x00F3 | Eingang 1,2, 5, 6, 7 und 8 |
| 0x00F4 | Eingang 3, 5, 6, 7 und 8 |
| 0x00F5 | Eingang 1,3, 5, 6, 7 und 8 |
| 0x00F6 | Eingang 2,3, 5, 6, 7 und 8 |
| 0x00F7 | Eingang 1, 2, 3, 5, 6, 7 und 8 |
| 0x00F8 | Eingang 4, 5, 6, 7 und 8 |
| 0x00F9 | Eingang 1, 4, 5, 6, 7 und 8 |
| 0x00FA | Eingang 2, 4, 5, 6, 7 und 8 |
| 0x00FB | Eingang 1, 2, 4, 5, 6, 7 und 8 |
| 0x00FC | Eingang 3, 4, 5, 6, 7 und 8 |
| 0x00FD | Eingang 1, 2, 4, 5, 6, 7 und 8 |
| 0x00FE | Eingang 2, 3, 4, 5, 6, 7 und 8 |
| 0x00FF | Eingang 1, 2, 3, 4, 5, 6, 7 und 8 |
| 0x0100 | Eingang 9 |
| 0x0101 | Eingang 1 und 9 |
| 0x0102 | Eingang 2 und 9 |
| 0x0103 | Eingang 1, 2 und 9 |
| 0x0104 | Eingang 3 und 9 |
| 0x0105 | Eingang 1, 3 und 9 |
| 0x0106 | Eingang 2, 3 und 9 |
| 0x0107 | Eingang 1, 2, 3 und 9 |
| 0x0108 | Eingang 4 und 9 |
| 0x0109 | Eingang 1, 4 und 9 |
| 0x010A | Eingang 2, 4 und 9 |
| 0x010B | Eingang 1, 2, 4 und 9 |
| 0x010C | Eingang 3, 4 und 9 |
| 0x010D | Eingang 1, 2, 4 und 9 |
| 0x010E | Eingang 2, 3, 4 und 9 |
| 0x010F | Eingang 1, 2, 3, 4 und 9 |
| 0x0110 | Eingang 5 und 9 |
| 0x0111 | Eingang 1, 5 und 9 |
| 0x0112 | Eingang 2, 5 und 9 |
| 0x0113 | Eingang 1,2, 5 und 9 |
| 0x0114 | Eingang 3, 5 und 9 |
| 0x0115 | Eingang 1,3, 5 und 9 |
| 0x0116 | Eingang 2,3, 5 und 9 |
| 0x0117 | Eingang 1, 2, 3, 5 und 9 |
| 0x0118 | Eingang 4, 5 und 9 |
| 0x0119 | Eingang 1, 4, 5 und 9 |
| 0x011A | Eingang 2, 4, 5 und 9 |
| 0x011B | Eingang 1, 2, 4, 5 und 9 |
| 0x011C | Eingang 3, 4, 5 und 9 |
| 0x011D | Eingang 1, 2, 4, 5 und 9 |
| 0x011E | Eingang 2, 3, 4, 5 und 9 |
| 0x011F | Eingang 1, 2, 3, 4, 5 und 9 |
| 0x0120 | Eingang 6 und 9 |
| 0x0121 | Eingang 1, 6 und 9 |
| 0x0122 | Eingang 2, 6 und 9 |
| 0x0123 | Eingang 1, 2, 6 und 9 |
| 0x0124 | Eingang 3, 6 und 9 |
| 0x0125 | Eingang 1, 3, 6 und 9 |
| 0x0126 | Eingang 2, 3, 6 und 9 |
| 0x0127 | Eingang 1, 2, 3, 6 und 9 |
| 0x0128 | Eingang 4, 6 und 9 |
| 0x0129 | Eingang 1, 4, 6 und 9 |
| 0x012A | Eingang 2, 4, 6 und 9 |
| 0x012B | Eingang 1, 2, 4, 6 und 9 |
| 0x012C | Eingang 3, 4, 6 und 9 |
| 0x012D | Eingang 1, 2, 4, 6 und 9 |
| 0x012E | Eingang 2, 3, 4, 6 und 9 |
| 0x012F | Eingang 1, 2, 3, 4, 6 und 9 |
| 0x0130 | Eingang 5, 6 und 9 |
| 0x0131 | Eingang 1, 5, 6 und 9 |
| 0x0132 | Eingang 2, 5, 6 und 9 |
| 0x0133 | Eingang 1,2, 5, 6 und 9 |
| 0x0134 | Eingang 3, 5, 6 und 9 |
| 0x0135 | Eingang 1,3, 5, 6 und 9 |
| 0x0136 | Eingang 2,3, 5, 6 und 9 |
| 0x0137 | Eingang 1, 2, 3, 5, 6 und 9 |
| 0x0138 | Eingang 4, 5, 6 und 9 |
| 0x0139 | Eingang 1, 4, 5, 6 und 9 |
| 0x013A | Eingang 2, 4, 5, 6 und 9 |
| 0x013B | Eingang 1, 2, 4, 5, 6 und 9 |
| 0x013C | Eingang 3, 4, 5, 6 und 9 |
| 0x013D | Eingang 1, 2, 4, 5, 6 und 9 |
| 0x013E | Eingang 2, 3, 4, 5, 6 und 9 |
| 0x013F | Eingang 1, 2, 3, 4, 5, 6 und 9 |
| 0x0140 | Eingang 7 und 9 |
| 0x0141 | Eingang 1, 7 und 9 |
| 0x0142 | Eingang 2, 7 und 9 |
| 0x0143 | Eingang 1, 2, 7 und 9 |
| 0x0144 | Eingang 3, 7 und 9 |
| 0x0145 | Eingang 1, 3, 7 und 9 |
| 0x0146 | Eingang 2, 3, 7 und 9 |
| 0x0147 | Eingang 1, 2, 3, 7 und 9 |
| 0x0148 | Eingang 4, 7 und 9 |
| 0x0149 | Eingang 1, 4, 7 und 9 |
| 0x014A | Eingang 2, 4, 7 und 9 |
| 0x014B | Eingang 1, 2, 4, 7 und 9 |
| 0x014C | Eingang 3, 4, 7 und 9 |
| 0x014D | Eingang 1, 2, 4, 7 und 9 |
| 0x014E | Eingang 2, 3, 4, 7 und 9 |
| 0x014F | Eingang 1, 2, 3, 4, 7 und 9 |
| 0x0150 | Eingang 5, 7 und 9 |
| 0x0151 | Eingang 1, 5, 7 und 9 |
| 0x0152 | Eingang 2, 5, 7 und 9 |
| 0x0153 | Eingang 1,2, 5, 7 und 9 |
| 0x0154 | Eingang 3, 5, 7 und 9 |
| 0x0155 | Eingang 1,3, 5, 7 und 9 |
| 0x0156 | Eingang 2,3, 5, 7 und 9 |
| 0x0157 | Eingang 1, 2, 3, 5, 7 und 9 |
| 0x0158 | Eingang 4, 5, 7 und 9 |
| 0x0159 | Eingang 1, 4, 5, 7 und 9 |
| 0x015A | Eingang 2, 4, 5, 7 und 9 |
| 0x015B | Eingang 1, 2, 4, 5, 7 und 9 |
| 0x015C | Eingang 3, 4, 5, 7 und 9 |
| 0x015D | Eingang 1, 2, 4, 5, 7 und 9 |
| 0x015E | Eingang 2, 3, 4, 5, 7 und 9 |
| 0x015F | Eingang 1, 2, 3, 4, 5, 7 und 9 |
| 0x0160 | Eingang 6, 7 und 9 |
| 0x0161 | Eingang 1, 6, 7 und 9 |
| 0x0162 | Eingang 2, 6, 7 und 9 |
| 0x0163 | Eingang 1, 2, 6, 7 und 9 |
| 0x0164 | Eingang 3, 6, 7 und 9 |
| 0x0165 | Eingang 1, 3, 6, 7 und 9 |
| 0x0166 | Eingang 2, 3, 6, 7 und 9 |
| 0x0167 | Eingang 1, 2, 3, 6, 7 und 9 |
| 0x0168 | Eingang 4, 6, 7 und 9 |
| 0x0169 | Eingang 1, 4, 6, 7 und 9 |
| 0x016A | Eingang 2, 4, 6, 7 und 9 |
| 0x016B | Eingang 1, 2, 4, 6, 7 und 9 |
| 0x016C | Eingang 3, 4, 6, 7 und 9 |
| 0x016D | Eingang 1, 2, 4, 6, 7 und 9 |
| 0x016E | Eingang 2, 3, 4, 6, 7 und 9 |
| 0x016F | Eingang 1, 2, 3, 4, 6, 7 und 9 |
| 0x0170 | Eingang 5, 6, 7 und 9 |
| 0x0171 | Eingang 1, 5, 6, 7 und 9 |
| 0x0172 | Eingang 2, 5, 6, 7 und 9 |
| 0x0173 | Eingang 1,2, 5, 6, 7 und 9 |
| 0x0174 | Eingang 3, 5, 6, 7 und 9 |
| 0x0175 | Eingang 1,3, 5, 6, 7 und 9 |
| 0x0176 | Eingang 2,3, 5, 6, 7 und 9 |
| 0x0177 | Eingang 1, 2, 3, 5, 6, 7 und 9 |
| 0x0178 | Eingang 4, 5, 6, 7 und 9 |
| 0x0179 | Eingang 1, 4, 5, 6, 7 und 9 |
| 0x017A | Eingang 2, 4, 5, 6, 7 und 9 |
| 0x017B | Eingang 1, 2, 4, 5, 6, 7 und 9 |
| 0x017C | Eingang 3, 4, 5, 6, 7 und 9 |
| 0x017D | Eingang 1, 2, 4, 5, 6, 7 und 9 |
| 0x017E | Eingang 2, 3, 4, 5, 6, 7 und 9 |
| 0x017F | Eingang 1, 2, 3, 4, 5, 6, 7 und 9 |
| 0x0180 | Eingang 8 und 9 |
| 0x0181 | Eingang 1, 8 und 9 |
| 0x0182 | Eingang 2, 8 und 9 |
| 0x0183 | Eingang 1, 2, 8 und 9 |
| 0x0184 | Eingang 3, 8 und 9 |
| 0x0185 | Eingang 1, 3, 8 und 9 |
| 0x0186 | Eingang 2, 3, 8 und 9 |
| 0x0187 | Eingang 1, 2, 3, 8 und 9 |
| 0x0188 | Eingang 4, 8 und 9 |
| 0x0189 | Eingang 1, 4, 8 und 9 |
| 0x018A | Eingang 2, 4, 8 und 9 |
| 0x018B | Eingang 1, 2, 4, 8 und 9 |
| 0x018C | Eingang 3, 4, 8 und 9 |
| 0x018D | Eingang 1, 2, 4, 8 und 9 |
| 0x018E | Eingang 2, 3, 4, 8 und 9 |
| 0x018F | Eingang 1, 2, 3, 4, 8 und 9 |
| 0x0190 | Eingang 5, 8 und 9 |
| 0x0191 | Eingang 1, 5, 8 und 9 |
| 0x0192 | Eingang 2, 5, 8 und 9 |
| 0x0193 | Eingang 1,2, 5, 8 und 9 |
| 0x0194 | Eingang 3, 5, 8 und 9 |
| 0x0195 | Eingang 1,3, 5, 8 und 9 |
| 0x0196 | Eingang 2,3, 5, 8 und 9 |
| 0x0197 | Eingang 1, 2, 3, 5, 8 und 9 |
| 0x0198 | Eingang 4, 5, 8 und 9 |
| 0x0199 | Eingang 1, 4, 5, 8 und 9 |
| 0x019A | Eingang 2, 4, 5, 8 und 9 |
| 0x019B | Eingang 1, 2, 4, 5, 8 und 9 |
| 0x019C | Eingang 3, 4, 5, 8 und 9 |
| 0x019D | Eingang 1, 2, 4, 5, 8 und 9 |
| 0x019E | Eingang 2, 3, 4, 5, 8 und 9 |
| 0x019F | Eingang 1, 2, 3, 4, 5, 8 und 9 |
| 0x01A0 | Eingang 6, 8 und 9 |
| 0x01A1 | Eingang 1, 6, 8 und 9 |
| 0x01A2 | Eingang 2, 6, 8 und 9 |
| 0x01A3 | Eingang 1, 2, 6, 8 und 9 |
| 0x01A4 | Eingang 3, 6, 8 und 9 |
| 0x01A5 | Eingang 1, 3, 6, 8 und 9 |
| 0x01A6 | Eingang 2, 3, 6, 8 und 9 |
| 0x01A7 | Eingang 1, 2, 3, 6, 8 und 9 |
| 0x01A8 | Eingang 4, 6, 8 und 9 |
| 0x01A9 | Eingang 1, 4, 6, 8 und 9 |
| 0x01AA | Eingang 2, 4, 6, 8 und 9 |
| 0x01AB | Eingang 1, 2, 4, 6, 8 und 9 |
| 0x01AC | Eingang 3, 4, 6, 8 und 9 |
| 0x01AD | Eingang 1, 2, 4, 6, 8 und 9 |
| 0x01AE | Eingang 2, 3, 4, 6, 8 und 9 |
| 0x01AF | Eingang 1, 2, 3, 4, 6, 8 und 9 |
| 0x01B0 | Eingang 5, 6, 8 und 9 |
| 0x01B1 | Eingang 1, 5, 6, 8 und 9 |
| 0x01B2 | Eingang 2, 5, 6, 8 und 9 |
| 0x01B3 | Eingang 1,2, 5, 6, 8 und 9 |
| 0x01B4 | Eingang 3, 5, 6, 8 und 9 |
| 0x01B5 | Eingang 1,3, 5, 6, 8 und 9 |
| 0x01B6 | Eingang 2,3, 5, 6, 8 und 9 |
| 0x01B7 | Eingang 1, 2, 3, 5, 6, 8 und 9 |
| 0x01B8 | Eingang 4, 5, 6, 8 und 9 |
| 0x01B9 | Eingang 1, 4, 5, 6, 8 und 9 |
| 0x01BA | Eingang 2, 4, 5, 6, 8 und 9 |
| 0x01BB | Eingang 1, 2, 4, 5, 6, 8 und 9 |
| 0x01BC | Eingang 3, 4, 5, 6, 8 und 9 |
| 0x01BD | Eingang 1, 2, 4, 5, 6, 8 und 9 |
| 0x01BE | Eingang 2, 3, 4, 5, 6, 8 und 9 |
| 0x01BF | Eingang 1, 2, 3, 4, 5, 6, 8 und 9 |
| 0x01C0 | Eingang 7, 8 und 9 |
| 0x01C1 | Eingang 1, 7, 8 und 9 |
| 0x01C2 | Eingang 2, 7, 8 und 9 |
| 0x01C3 | Eingang 1, 2, 7, 8 und 9 |
| 0x01C4 | Eingang 3, 7, 8 und 9 |
| 0x01C5 | Eingang 1, 3, 7, 8 und 9 |
| 0x01C6 | Eingang 2, 3, 7, 8 und 9 |
| 0x01C7 | Eingang 1, 2, 3, 7, 8 und 9 |
| 0x01C8 | Eingang 4, 7, 8 und 9 |
| 0x01C9 | Eingang 1, 4, 7, 8 und 9 |
| 0x01CA | Eingang 2, 4, 7, 8 und 9 |
| 0x01CB | Eingang 1, 2, 4, 7, 8 und 9 |
| 0x01CC | Eingang 3, 4, 7, 8 und 9 |
| 0x01CD | Eingang 1, 2, 4, 7, 8 und 9 |
| 0x01CE | Eingang 2, 3, 4, 7, 8 und 9 |
| 0x01CF | Eingang 1, 2, 3, 4, 7, 8 und 9 |
| 0x01D0 | Eingang 5, 7, 8 und 9 |
| 0x01D1 | Eingang 1, 5, 7, 8 und 9 |
| 0x01D2 | Eingang 2, 5, 7, 8 und 9 |
| 0x01D3 | Eingang 1,2, 5, 7, 8 und 9 |
| 0x01D4 | Eingang 3, 5, 7, 8 und 9 |
| 0x01D5 | Eingang 1,3, 5, 7, 8 und 9 |
| 0x01D6 | Eingang 2,3, 5, 7, 8 und 9 |
| 0x01D7 | Eingang 1, 2, 3, 5, 7, 8 und 9 |
| 0x01D8 | Eingang 4, 5, 7, 8 und 9 |
| 0x01D9 | Eingang 1, 4, 5, 7, 8 und 9 |
| 0x01DA | Eingang 2, 4, 5, 7, 8 und 9 |
| 0x01DB | Eingang 1, 2, 4, 5, 7, 8 und 9 |
| 0x01DC | Eingang 3, 4, 5, 7, 8 und 9 |
| 0x01DD | Eingang 1, 2, 4, 5, 7, 8 und 9 |
| 0x01DE | Eingang 2, 3, 4, 5, 7, 8 und 9 |
| 0x01DF | Eingang 1, 2, 3, 4, 5, 7, 8 und 9 |
| 0x01E0 | Eingang 6, 7, 8 und 9 |
| 0x01E1 | Eingang 1, 6, 7, 8 und 9 |
| 0x01E2 | Eingang 2, 6, 7, 8 und 9 |
| 0x01E3 | Eingang 1, 2, 6, 7, 8 und 9 |
| 0x01E4 | Eingang 3, 6, 7, 8 und 9 |
| 0x01E5 | Eingang 1, 3, 6, 7, 8 und 9 |
| 0x01E6 | Eingang 2, 3, 6, 7, 8 und 9 |
| 0x01E7 | Eingang 1, 2, 3, 6, 7, 8 und 9 |
| 0x01E8 | Eingang 4, 6, 7, 8 und 9 |
| 0x01E9 | Eingang 1, 4, 6, 7, 8 und 9 |
| 0x01EA | Eingang 2, 4, 6, 7, 8 und 9 |
| 0x01EB | Eingang 1, 2, 4, 6, 7, 8 und 9 |
| 0x01EC | Eingang 3, 4, 6, 7, 8 und 9 |
| 0x01ED | Eingang 1, 2, 4, 6, 7, 8 und 9 |
| 0x01EE | Eingang 2, 3, 4, 6, 7, 8 und 9 |
| 0x01EF | Eingang 1, 2, 3, 4, 6, 7, 8 und 9 |
| 0x01F0 | Eingang 5, 6, 7, 8 und 9 |
| 0x01F1 | Eingang 1, 5, 6, 7, 8 und 9 |
| 0x01F2 | Eingang 2, 5, 6, 7, 8 und 9 |
| 0x01F3 | Eingang 1,2, 5, 6, 7, 8 und 9 |
| 0x01F4 | Eingang 3, 5, 6, 7, 8 und 9 |
| 0x01F5 | Eingang 1,3, 5, 6, 7, 8 und 9 |
| 0x01F6 | Eingang 2,3, 5, 6, 7, 8 und 9 |
| 0x01F7 | Eingang 1, 2, 3, 5, 6, 7, 8 und 9 |
| 0x01F8 | Eingang 4, 5, 6, 7, 8 und 9 |
| 0x01F9 | Eingang 1, 4, 5, 6, 7, 8 und 9 |
| 0x01FA | Eingang 2, 4, 5, 6, 7, 8 und 9 |
| 0x01FB | Eingang 1, 2, 4, 5, 6, 7, 8 und 9 |
| 0x01FC | Eingang 3, 4, 5, 6, 7, 8 und 9 |
| 0x01FD | Eingang 1, 2, 4, 5, 6, 7, 8 und 9 |
| 0x01FE | Eingang 2, 3, 4, 5, 6, 7, 8 und 9 |
| 0x01FF | Eingang 1, 2, 3, 4, 5, 6, 7, 8 und 9 |
| 0xFFFF | Nicht definiert |

<a id="table-tausgangvideoswitch"></a>
### TAUSGANGVIDEOSWITCH

Dimensions: 33 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | Kein VideoSwitch vorhanden bzw. verwendet |
| 0x0001 | Ausgang 1 |
| 0x0002 | Ausgang 2 |
| 0x0003 | Ausgang 1 und 2 |
| 0x0004 | Ausgang 3 |
| 0x0005 | Ausgang 1 und 3 |
| 0x0006 | Ausgang 2 und 3 |
| 0x0007 | Ausgang 1, 2 und 3 |
| 0x0008 | Ausgang 4 |
| 0x0009 | Ausgang 1 und 4 |
| 0x000A | Ausgang 2 und 4 |
| 0x000B | Ausgang 1, 2 und 4 |
| 0x000C | Ausgang 3 und 4 |
| 0x000D | Ausgang 1, 2 und 4 |
| 0x000E | Ausgang 2, 3 und 4 |
| 0x000F | Ausgang 1, 2, 3 und 4 |
| 0x0010 | Ausgang 5 |
| 0x0011 | Ausgang 1 und 5 |
| 0x0012 | Ausgang 2 und 5 |
| 0x0013 | Ausgang 1,2 und 5 |
| 0x0014 | Ausgang 3 und 5 |
| 0x0015 | Ausgang 1,3 und 5 |
| 0x0016 | Ausgang 2,3 und 5 |
| 0x0017 | Ausgang 1, 2 und 3 und 5 |
| 0x0018 | Ausgang 4 und 5 |
| 0x0019 | Ausgang 1, 4 und 5 |
| 0x001A | Ausgang 2, 4 und 5 |
| 0x001B | Ausgang 1, 2, 4 und 5 |
| 0x001C | Ausgang 3, 4 und 5 |
| 0x001D | Ausgang 1, 2, 4 und 5 |
| 0x001E | Ausgang 2, 3, 4 und 5 |
| 0x001F | Ausgang 1, 2, 3, 4 und 5 |
| 0xFFFF | Nicht definiert |

<a id="table-tsdarssignalquality"></a>
### TSDARSSIGNALQUALITY

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | kein Signal |
| 1 | schwaches Signal |
| 2 | gutes Signal |
| 3 | exzellentes Signal |
| 255 | nicht definiert |

<a id="table-tsdarssignalqualityglobalstatus"></a>
### TSDARSSIGNALQUALITYGLOBALSTATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Mute |
| 1 | Audio |
| 255 | nicht definiert |

<a id="table-tpdcsignal"></a>
### TPDCSIGNAL

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Vorderes Tonsignal |
| 0x02 | Hinteres Tonsignal |
| 0x03 | AUS |
| 0xFF | Nicht definiert |

<a id="table-tsdarsbermode"></a>
### TSDARSBERMODE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | unkorrigierter BER Modus |
| 1 | korrigierter BER Modus |
| 255 | nicht definiert |

<a id="table-therstellungstatus"></a>
### THERSTELLUNGSTATUS

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Keine Anfrage gestellt |
| 0x01 | Herstellung läuft |
| 0x02 | Herstellung beendet ohne Fehler |
| 0x03 | Herstellung beendet mit Fehler |
| 0x04 | Herstellung unterbrochen durch User-Interaktion |
| 0xFF | Nicht definiert |

<a id="table-therstellungfehler"></a>
### THERSTELLUNGFEHLER

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Physikalischer Fehler |
| 0xFF | Nicht definiert |

<a id="table-tvideoquelle"></a>
### TVIDEOQUELLE

Dimensions: 262 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00000000 | Alle Quellen |
| 0x00000001 | MMC |
| 0x00000002 | NiVi |
| 0x00000003 | MMC und NiVi |
| 0x00000004 | RFK |
| 0x00000005 | MMC und RFK |
| 0x00000006 | NiVi und RFK |
| 0x00000007 | MMC, NiVi und RFK |
| 0x00000008 | TV |
| 0x00000009 | MMC und TV |
| 0x0000000A | NiVi und TV |
| 0x0000000B | MMC, NiVi und TV |
| 0x0000000C | RFK und TV |
| 0x0000000D | MMC, RFK und TV |
| 0x0000000E | NiVi, RFK und TV |
| 0x0000000F | MMC, NiVi, RFK und TV |
| 0x00000010 | TopView |
| 0x00000011 | MMC und TopView |
| 0x00000012 | NiVi und TopView |
| 0x00000013 | MMC, NiVi und TopView |
| 0x00000014 | RFK und TopView |
| 0x00000015 | MMC, RFK und TopView |
| 0x00000016 | NiVi, RFK und TopView |
| 0x00000017 | MMC, NiVi, RFK und TopView |
| 0x00000018 | TV und TopView |
| 0x00000019 | MMC, TV und TopView |
| 0x0000001A | NiVi, TV und TopView |
| 0x0000001B | MMC, NiVi, TV und TopView |
| 0x0000001C | RFK, TV und TopView |
| 0x0000001D | MMC, RFK, TV und TopView |
| 0x0000001E | NiVi, RFK, TV und TopView |
| 0x0000001F | MMC, NiVi, RFK, TV und TopView |
| 0x00000020 | Entertainmentserver |
| 0x00000021 | MMC und Entertainmentserver |
| 0x00000022 | NiVi und Entertainmentserver |
| 0x00000023 | MMC, NiVi und Entertainmentserver |
| 0x00000024 | RFK und Entertainmentserver |
| 0x00000025 | MMC, RFK und Entertainmentserver |
| 0x00000026 | NiVi, RFK und Entertainmentserver |
| 0x00000027 | MMC, NiVi, RFK und Entertainmentserver |
| 0x00000028 | TV und Entertainmentserver |
| 0x00000029 | MMC, TV und Entertainmentserver |
| 0x0000002A | NiVi, TV und Entertainmentserver |
| 0x0000002B | MMC, NiVi, TV und Entertainmentserver |
| 0x0000002C | RFK, TV und Entertainmentserver |
| 0x0000002D | MMC, RFK, TV und Entertainmentserver |
| 0x0000002E | NiVi, RFK, TV und Entertainmentserver |
| 0x0000002F | MMC, NiVi, RFK, TV und Entertainmentserver |
| 0x00000030 | TopView und Entertainmentserver |
| 0x00000031 | MMC, TopView und Entertainmentserver |
| 0x00000032 | NiVi, TopView und Entertainmentserver |
| 0x00000033 | MMC, NiVi, TopView und Entertainmentserver |
| 0x00000034 | RFK, TopView und Entertainmentserver |
| 0x00000035 | MMC, RFK, TopView und Entertainmentserver |
| 0x00000036 | NiVi, RFK, TopView und Entertainmentserver |
| 0x00000037 | MMC, NiVi, RFK, TopView und Entertainmentserver |
| 0x00000038 | TV, TopView und Entertainmentserver |
| 0x00000039 | MMC, TV, TopView und Entertainmentserver |
| 0x0000003A | NiVi, TV, TopView und Entertainmentserver |
| 0x0000003B | MMC, NiVi, TV, TopView und Entertainmentserver |
| 0x0000003C | RFK, TV, TopView und Entertainmentserver |
| 0x0000003D | MMC, RFK, TV, TopView und Entertainmentserver |
| 0x0000003E | NiVi, RFK, TV, TopView und Entertainmentserver |
| 0x0000003F | MMC, NiVi, RFK, TV, TopView und Entertainmentserver |
| 0x00000040 | Headunit |
| 0x00000041 | MMC |
| 0x00000042 | NiVi |
| 0x00000043 | MMC und NiVi |
| 0x00000044 | RFK |
| 0x00000045 | MMC und RFK |
| 0x00000046 | NiVi und RFK |
| 0x00000047 | MMC, NiVi und RFK |
| 0x00000048 | TV |
| 0x00000049 | MMC und TV |
| 0x0000004A | NiVi und TV |
| 0x0000004B | MMC, NiVi und TV |
| 0x0000004C | RFK und TV |
| 0x0000004D | MMC, RFK und TV |
| 0x0000004E | NiVi, RFK und TV |
| 0x0000004F | MMC, NiVi, RFK und TV |
| 0x00000050 | TopView |
| 0x00000051 | MMC und TopView |
| 0x00000052 | NiVi und TopView |
| 0x00000053 | MMC, NiVi und TopView |
| 0x00000054 | RFK und TopView |
| 0x00000055 | MMC, RFK und TopView |
| 0x00000056 | NiVi, RFK und TopView |
| 0x00000057 | MMC, NiVi, RFK und TopView |
| 0x00000058 | TV und TopView |
| 0x00000059 | MMC, TV und TopView |
| 0x0000005A | NiVi, TV und TopView |
| 0x0000005B | MMC, NiVi, TV und TopView |
| 0x0000005C | RFK, TV und TopView |
| 0x0000005D | MMC, RFK, TV und TopView |
| 0x0000005E | NiVi, RFK, TV und TopView |
| 0x0000005F | MMC, NiVi, RFK, TV und TopView |
| 0x00000060 | Entertainmentserver |
| 0x00000061 | MMC und Entertainmentserver |
| 0x00000062 | NiVi und Entertainmentserver |
| 0x00000063 | MMC, NiVi und Entertainmentserver |
| 0x00000064 | RFK und Entertainmentserver |
| 0x00000065 | MMC, RFK und Entertainmentserver |
| 0x00000066 | NiVi, RFK und Entertainmentserver |
| 0x00000067 | MMC, NiVi, RFK und Entertainmentserver |
| 0x00000068 | TV und Entertainmentserver |
| 0x00000069 | MMC, TV und Entertainmentserver |
| 0x0000006A | NiVi, TV und Entertainmentserver |
| 0x0000006B | MMC, NiVi, TV und Entertainmentserver |
| 0x0000006C | RFK, TV und Entertainmentserver |
| 0x0000006D | MMC, RFK, TV und Entertainmentserver |
| 0x0000006E | NiVi, RFK, TV und Entertainmentserver |
| 0x0000006F | MMC, NiVi, RFK, TV und Entertainmentserver |
| 0x00000070 | TopView und Entertainmentserver |
| 0x00000071 | MMC, TopView und Entertainmentserver |
| 0x00000072 | NiVi, TopView und Entertainmentserver |
| 0x00000073 | MMC, NiVi, TopView und Entertainmentserver |
| 0x00000074 | RFK, TopView und Entertainmentserver |
| 0x00000075 | MMC, RFK, TopView und Entertainmentserver |
| 0x00000076 | NiVi, RFK, TopView und Entertainmentserve |
| 0x00000077 | MMC, NiVi, RFK, TopView und Entertainmentserver |
| 0x00000078 | TV, TopView und Entertainmentserver |
| 0x00000079 | MMC, TV, TopView und Entertainmentserver |
| 0x0000007A | NiVi, TV, TopView und Entertainmentserver |
| 0x0000007B | MMC, NiVi, TV, TopView und Entertainmentserver |
| 0x0000007C | RFK, TV, TopView und Entertainmentserver |
| 0x0000007D | MMC, RFK, TV, TopView und Entertainmentserver |
| 0x0000007E | NiVi, RFK, TV, TopView und Entertainmentserver |
| 0x0000007F | MMC, NiVi, RFK, TV, TopView und Entertainmentserver |
| 0x00000080 | RearSeatEntertainment |
| 0x00000081 | MMC und RearSeatEntertainment |
| 0x00000082 | NiVi und RearSeatEntertainment |
| 0x00000083 | MMC, NiVi und RearSeatEntertainment |
| 0x00000084 | RFK und RearSeatEntertainment |
| 0x00000085 | MMC, RFK und RearSeatEntertainment |
| 0x00000086 | NiVi, RFK und RearSeatEntertainment |
| 0x00000087 | MMC, NiVi, RFK und RearSeatEntertainment |
| 0x00000088 | TV und RearSeatEntertainment |
| 0x00000089 | MMC, TV und RearSeatEntertainment |
| 0x0000008A | NiVi, TV und RearSeatEntertainment |
| 0x0000008B | MMC, NiVi, TV und RearSeatEntertainment |
| 0x0000008C | RFK, TV und RearSeatEntertainment |
| 0x0000008D | MMC, RFK, TV und RearSeatEntertainment |
| 0x0000008E | NiVi, RFK, TV und RearSeatEntertainment |
| 0x0000008F | MMC, NiVi, RFK, TV und RearSeatEntertainment |
| 0x00000090 | TopView und RearSeatEntertainment |
| 0x00000091 | MMC, TopView und RearSeatEntertainment |
| 0x00000092 | NiVi, TopView und RearSeatEntertainment |
| 0x00000093 | MMC, NiVi, TopView und RearSeatEntertainment |
| 0x00000094 | RFK, TopView und RearSeatEntertainment |
| 0x00000095 | MMC, RFK, TopView und RearSeatEntertainment |
| 0x00000096 | NiVi, RFK, TopView und RearSeatEntertainment |
| 0x00000097 | MMC, NiVi, RFK, TopView und RearSeatEntertainment |
| 0x00000098 | TV, TopView und RearSeatEntertainment |
| 0x00000099 | MMC, TV, TopView und RearSeatEntertainment |
| 0x0000009A | NiVi, TV, TopView und RearSeatEntertainment |
| 0x0000009B | MMC, NiVi, TV, TopView und RearSeatEntertainment |
| 0x0000009C | RFK, TV, TopView und RearSeatEntertainment |
| 0x0000009D | MMC, RFK, TV, TopView und RearSeatEntertainment |
| 0x0000009E | NiVi, RFK, TV, TopView und RearSeatEntertainment |
| 0x0000009F | MMC, NiVi, RFK, TV, TopView und RearSeatEntertainment |
| 0x000000A0 | Entertainmentserver und RearSeatEntertainment |
| 0x000000A1 | MMC, Entertainmentserver und RearSeatEntertainment |
| 0x000000A2 | NiVi, Entertainmentserver und RearSeatEntertainment |
| 0x000000A3 | MMC, NiVi, Entertainmentserver und RearSeatEntertainment |
| 0x000000A4 | RFK, Entertainmentserver und RearSeatEntertainment |
| 0x000000A5 | MMC, RFK, Entertainmentserver und RearSeatEntertainment |
| 0x000000A6 | NiVi, RFK, Entertainmentserver und RearSeatEntertainment |
| 0x000000A7 | MMC, NiVi, RFK, Entertainmentserver und RearSeatEntertainment |
| 0x000000A8 | TV, Entertainmentserver und RearSeatEntertainment |
| 0x000000A9 | MMC, TV, Entertainmentserver und RearSeatEntertainment |
| 0x000000AA | NiVi, TV, Entertainmentserver und RearSeatEntertainment |
| 0x000000AB | MMC, NiVi, TV, Entertainmentserver und RearSeatEntertainment |
| 0x000000AC | RFK, TV, Entertainmentserver und RearSeatEntertainment |
| 0x000000AD | MMC, RFK, TV, Entertainmentserver und RearSeatEntertainment |
| 0x000000AE | NiVi, RFK, TV, Entertainmentserver und RearSeatEntertainment |
| 0x000000AF | MMC, NiVi, RFK, TV, Entertainmentserver und RearSeatEntertainment |
| 0x000000B0 | TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000B1 | MMC, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000B2 | NiVi, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000B3 | MMC, NiVi, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000B4 | RFK, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000B5 | MMC, RFK, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000B6 | NiVi, RFK, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000B7 | MMC, NiVi, RFK, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000B8 | TV, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000B9 | MMC, TV, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000BA | NiVi, TV, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000BB | MMC, NiVi, TV, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000BC | RFK, TV, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000BD | MMC, RFK, TV, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000BE | NiVi, RFK, TV, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000BF | MMC, NiVi, RFK, TV, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000C0 | Headunit und RearSeatEntertainment |
| 0x000000C1 | MMC und RearSeatEntertainment |
| 0x000000C2 | NiVi und RearSeatEntertainment |
| 0x000000C3 | MMC, NiVi und RearSeatEntertainment |
| 0x000000C4 | RFK und RearSeatEntertainment |
| 0x000000C5 | MMC, RFK und RearSeatEntertainment |
| 0x000000C6 | NiVi, RFK und RearSeatEntertainment |
| 0x000000C7 | MMC, NiVi, RFK und RearSeatEntertainment |
| 0x000000C8 | TV und RearSeatEntertainment |
| 0x000000C9 | MMC, TV und RearSeatEntertainment |
| 0x000000CA | NiVi, TV und RearSeatEntertainment |
| 0x000000CB | MMC, NiVi, TV und RearSeatEntertainment |
| 0x000000CC | RFK, TV und RearSeatEntertainment |
| 0x000000CD | MMC, RFK, TV und RearSeatEntertainment |
| 0x000000CE | NiVi, RFK, TV und RearSeatEntertainment |
| 0x000000CF | MMC, NiVi, RFK, TV und RearSeatEntertainment |
| 0x000000D0 | TopView und RearSeatEntertainment |
| 0x000000D1 | MMC, TopView und RearSeatEntertainment |
| 0x000000D2 | NiVi, TopView und RearSeatEntertainment |
| 0x000000D3 | MMC, NiVi, TopView und RearSeatEntertainment |
| 0x000000D4 | RFK, TopView und RearSeatEntertainment |
| 0x000000D5 | MMC, RFK, TopView und RearSeatEntertainment |
| 0x000000D6 | NiVi, RFK, TopView und RearSeatEntertainment |
| 0x000000D7 | MMC, NiVi, RFK, TopView und RearSeatEntertainment |
| 0x000000D8 | TV, TopView und RearSeatEntertainment |
| 0x000000D9 | MMC, TV, TopView und RearSeatEntertainment |
| 0x000000DA | NiVi, TV, TopView und RearSeatEntertainment |
| 0x000000DB | MMC, NiVi, TV, TopView und RearSeatEntertainment |
| 0x000000DC | RFK, TV, TopView und RearSeatEntertainment |
| 0x000000DD | MMC, RFK, TV, TopView und RearSeatEntertainment |
| 0x000000DE | NiVi, RFK, TV, TopView und RearSeatEntertainment |
| 0x000000DF | MMC, NiVi, RFK, TV, TopView und RearSeatEntertainment |
| 0x000000E0 | Entertainmentserver und RearSeatEntertainment |
| 0x000000E1 | MMC, Entertainmentserver und RearSeatEntertainment |
| 0x000000E2 | NiVi, Entertainmentserver und RearSeatEntertainment |
| 0x000000E3 | MMC, NiVi, Entertainmentserver und RearSeatEntertainment |
| 0x000000E4 | RFK, Entertainmentserver und RearSeatEntertainment |
| 0x000000E5 | MMC, RFK, Entertainmentserver und RearSeatEntertainment |
| 0x000000E6 | NiVi, RFK, Entertainmentserver und RearSeatEntertainment |
| 0x000000E7 | MMC, NiVi, RFK, Entertainmentserver und RearSeatEntertainment |
| 0x000000E8 | TV, Entertainmentserver und RearSeatEntertainment |
| 0x000000E9 | MMC, TV, Entertainmentserver und RearSeatEntertainment |
| 0x000000EA | NiVi, TV, Entertainmentserver und RearSeatEntertainment |
| 0x000000EB | MMC, NiVi, TV, Entertainmentserver und RearSeatEntertainment |
| 0x000000EC | RFK, TV, Entertainmentserver und RearSeatEntertainment |
| 0x000000ED | MMC, RFK, TV, Entertainmentserver und RearSeatEntertainment |
| 0x000000EE | NiVi, RFK, TV, Entertainmentserver und RearSeatEntertainment |
| 0x000000EF | MMC, NiVi, RFK, TV, Entertainmentserver und RearSeatEntertainment |
| 0x000000F0 | TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000F1 | MMC, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000F2 | NiVi, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000F3 | MMC, NiVi, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000F4 | RFK, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000F5 | MMC, RFK, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000F6 | NiVi, RFK, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000F7 | MMC, NiVi, RFK, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000F8 | TV, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000F9 | MMC, TV, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000FA | NiVi, TV, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000FB | MMC, NiVi, TV, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000FC | RFK, TV, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000FD | MMC, RFK, TV, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000FE | NiVi, RFK, TV, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x000000FF | MMC, NiVi, RFK, TV, TopView, Entertainmentserver und RearSeatEntertainment |
| 0x00000100 | SideView |
| 0x00000200 | AUX1 |
| 0x00000400 | AUX2 |
| 0x00000800 | AUX3 |
| 0x00001000 | AUX4 |
| 0xFFFFFFFF | Nicht definiert |

<a id="table-tvideosenke"></a>
### TVIDEOSENKE

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | Alle Bildschirme |
| 0x0001 | Bildschirm Headunit |
| 0x0002 | Linker oder einziger Bildschirm RearSeatEntertainment |
| 0x0003 | Linker oder einziger Bildschirm RearSeatEntertainment und Bildschirm Headunit |
| 0x0004 | Rechter  Bildschirm RearSeatEntertainment |
| 0x0005 | Bildschirm Headunit und Bildschirm RearSeatEntertainment |
| 0x0006 | Linker und Rechter Bildschirm RearSeatEntertainment |
| 0x0007 | Linker und Rechter Bildschirm RearSeatEntertainment und Bildschirm Headunit |
| 0xFFFF | Nicht definiert |

<a id="table-taktiveantennedab"></a>
### TAKTIVEANTENNEDAB

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Keine Antenne |
| 0x01 | L-Band Antenne |
| 0x02 | Band III Antenne |
| 0x03 | Beide Antennen |
| 0xFF | Nicht definiert |

<a id="table-tbrowseractivationstate"></a>
### TBROWSERACTIVATIONSTATE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Browser Applikation inaktiv |
| 0x01 | Browser Applikation aktiv |
| 0xFF | Nicht definiert |

<a id="table-tinputnecessary"></a>
### TINPUTNECESSARY

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Benutzereingang nicht erforderlich |
| 0x01 | Benutzereingang erforderlich |
| 0xFF | Nicht definiert |

<a id="table-tonlinecoded"></a>
### TONLINECODED

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Online nicht codiert |
| 0x01 | Online codiert |
| 0xFF | Nicht definiert |

<a id="table-ttmcactivationstate"></a>
### TTMCACTIVATIONSTATE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Nicht aktiviert |
| 0x01 | Aktiviert |
| 0xFF | Nicht definiert |

<a id="table-ttelmute"></a>
### TTELMUTE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Tel-Mute nicht aktiv |
| 0x01 | Tel-Mute aktiv |
| 0xFF | Nicht definiert |

<a id="table-twaveband"></a>
### TWAVEBAND

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | FM |
| 0x01 | LW |
| 0x02 | MW |
| 0x03 | KW |
| 0x04 | WB |
| 0x05 | TRF |
| 0x06 | Nicht definiert |

<a id="table-tgpsstatus"></a>
### TGPSSTATUS

Dimensions: 14 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Nicht unterstuetzt: Kein GPS |
| 0x01 | Nicht unterstuetzt: Kommunikationsfehler |
| 0x02 | Receiverfehler |
| 0x03 | Kein almanac |
| 0x04 | Suche Satelliten |
| 0x05 | Ortung Satellit 1 |
| 0x06 | Ortung Satellit 2 |
| 0x07 | Ortung Satellit 3 |
| 0x08 | Ortung Satellit 4 |
| 0x09 | Ortung Satellit 5 |
| 0x0A | Ortung Satellit 6 |
| 0x0B | 2D Position |
| 0x0C | 3D Position |
| 0xFF | Nicht definiert |

<a id="table-tinitialisierung"></a>
### TINITIALISIERUNG

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nicht initialisiert |
| 0x01 | IO initialisiert |
| 0xFF | NIO initialisiert |

<a id="table-tluefterstatus"></a>
### TLUEFTERSTATUS

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Lüfter steht |
| 0x01 | Lüfter läuft, aber nicht mit der erwarteteten Drehzahl |
| 0x02 | Lüfter läuft mit der erwarteteten Drehzahl |
| 0xFE | Lüfter läuft mit unbekannter Drehzahl |
| 0xFF | Nicht definiert |

<a id="table-ttestmapactivationstatus"></a>
### TTESTMAPACTIVATIONSTATUS

Dimensions: 12 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Testkarte deaktivieren |
| 0x01 | PrototypTestkarte aktivieren |
| 0x0A | Werkskarte München aktivieren |
| 0x0B | Werkskarte Dingolfing aktivieren |
| 0x0C | Werkskarte Regensburg aktivieren |
| 0x0D | Werkskarte Leipzig aktivieren |
| 0x0E | Werkskarte Rosslyn aktivieren |
| 0x0F | Werkskarte Spartanburg aktivieren |
| 0x10 | Werkskarte Goodwood aktivieren |
| 0x11 | Werkskarte China aktivieren |
| 0x12 | Werkskarte Oxford aktivieren |
| 0xFF | Nicht definiert |

<a id="table-ttestmapstatus"></a>
### TTESTMAPSTATUS

Dimensions: 15 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Testkarte aktivierbar aber derzeit deaktiviert |
| 0x01 | Prototyp Testkarte aktiviert |
| 0x02 | Testkarte nicht aktivierbar |
| 0x03 | Testkarte wird gerade aktiviert |
| 0x04 | Testkarte wird gerade deaktiviert |
| 0x0A | Werkskarte München aktiviert |
| 0x0B | Werkskarte Dingolfing aktiviert |
| 0x0C | Werkskarte Regensburg aktiviert |
| 0x0D | Werkskarte Leipzig aktiviert |
| 0x0E | Werkskarte Rosslyn aktiviert |
| 0x0F | Werkskarte Spartanburg aktiviert |
| 0x10 | Werkskarte Goodwood aktiviert |
| 0x11 | Werkskarte China aktiviert |
| 0x12 | Werkskarte Oxford aktiviert |
| 0xFF | Nicht definiert |

<a id="table-tethernetconnection"></a>
### TETHERNETCONNECTION

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Alle |
| 0x01 | Ethernet Verbindung für den Flash-Prozess |
| 0x02 | Ethernet Verbindung zum RSE |
| 0xFF | Nicht definiert |

<a id="table-tethernetactivationstate"></a>
### TETHERNETACTIVATIONSTATE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Deaktiviert |
| 0x01 | Aktiviert |
| 0xFF | Nicht definiert |

<a id="table-tgpspositionvalidity"></a>
### TGPSPOSITIONVALIDITY

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | GPS Position ist gueltig |
| 0x01 | GPS Position ist nicht gueltig |
| 0xFF | Nicht definiert |

<a id="table-tfbtastenummer"></a>
### TFBTASTENUMMER

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | FB-Taste 1 |
| 0x02 | FB-Taste 2 |
| 0x03 | FB-Taste 3 |
| 0x04 | FB-Taste 4 |
| 0x05 | FB-Taste 5 |
| 0x06 | FB-Taste 6 |
| 0x07 | FB-Taste 7 |
| 0x08 | FB-Taste 8 |
| 0xFF | Nicht definiert |

<a id="table-tfbtastestatus"></a>
### TFBTASTESTATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Taste berührt |
| 0x02 | Taste gedrückt |
| 0xFF | Nicht definiert |

<a id="table-tlanguage"></a>
### TLANGUAGE

Dimensions: 29 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | codierte Sprache |
| 0x01 | Deutsch |
| 0x02 | Englisch (UK) |
| 0x03 | Englisch (US) |
| 0x04 | Spanisch |
| 0x05 | Italienisch |
| 0x06 | Französisch |
| 0x07 | Flämisch |
| 0x08 | Niederländisch |
| 0x09 | Arabisch |
| 0x0A | Chinesisch Traditionell |
| 0x0B | Chinesisch Simpel |
| 0x0C | Koreanisch |
| 0x0D | Japanisch |
| 0x0E | Russisch |
| 0x0F | Franzoesisch CA |
| 0x10 | Spanisch US |
| 0x11 | Portugiesisch |
| 0x12 | Polnisch |
| 0x13 | Griechisch |
| 0x14 | Tuerkisch |
| 0x15 | Ungarisch |
| 0x16 | Rumänisch |
| 0x17 | Schwedisch |
| 0x18 | Portugiesisch BR |
| 0x19 | Kantonesisch Traditionell |
| 0x1A | Kantonesisch Simple |
| 0xFE | Kein Sprachpaket aktiv |
| 0xFF | Nicht definiert |

<a id="table-ttunersuchlauf"></a>
### TTUNERSUCHLAUF

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Absteigend |
| 0x01 | Aufsteigend |
| 0x02 | Stopp |
| 0xFF | Nicht definiert |

<a id="table-tklangzeichen"></a>
### TKLANGZEICHEN

Dimensions: 22 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Stoppen des aktiven Klangzeichens |
| 0x01 | ACC |
| 0x02 | CCG |
| 0x03 | DG |
| 0x04 | no longer present (Hour-Signal) |
| 0x05 | IMG_ON |
| 0x06 | IMG_OFF |
| 0x07 | HMI_FBM |
| 0x08 | Reverse_Gear_ON |
| 0x09 | Reverse_Gear_OFF |
| 0x0A | no longer present (HMI_Press) |
| 0x0B | no longer present (HMI_Slope) |
| 0x0C | maybe no longer present (HMI_Snap) (End of Slope) |
| 0x0D | TLC_Left_ON |
| 0x0E | TLC_Right_ON |
| 0x0F | TLC_OFF |
| 0x10 | IBrake |
| 0x11 | maybe no longer present (PDC_Sample ) |
| 0x12 | ETC1 |
| 0x13 | ETC2 |
| 0x14 | ETC3 |
| 0xFF | Nicht definiert |

<a id="table-tdemutestatus"></a>
### TDEMUTESTATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Stummschaltung ein |
| 0x01 | Stummschaltung aus |
| 0xFF | Nicht definiert |

<a id="table-tdemutesource"></a>
### TDEMUTESOURCE

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Nicht benutzt(Default in Headunit) |
| 0x01 | Kopfhörer links |
| 0x02 | Kopfhörer rechts |
| 0x03 | Beide Kopfhörer |
| 0xFF | Nicht definiert |

<a id="table-tsourcedemutestatus"></a>
### TSOURCEDEMUTESTATUS

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Head-Unit aus |
| 0x01 | Head-Unit ein |
| 0x02 | RSE Kopfhörer links aus |
| 0x03 | RSE Kopfhörer links ein |
| 0x04 | RSE Kopfhörer rechts aus |
| 0x05 | RSE Kopfhörer rechts ein |
| 0xFF | Nicht definiert |

<a id="table-textgyrosignal"></a>
### TEXTGYROSIGNAL

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Signal verfügbar |
| 0x01 | Signal nicht verfügbar |
| 0xFF | Nicht definiert |

<a id="table-tfollowingdabfm"></a>
### TFOLLOWINGDABFM

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | DAB FM Following aus |
| 0x01 | DAB FM Following ein |
| 0x02 | DAB FM Following keine Änderung |
| 0xFF | Nicht definiert |

<a id="table-tfollowingdabdab"></a>
### TFOLLOWINGDABDAB

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | DAB DAB Following aus |
| 0x01 | DAB DAB Following ein |
| 0x02 | DAB DAB Following keine Änderung |
| 0xFF | Nicht definiert |

<a id="table-ttpdab"></a>
### TTPDAB

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | TP DAB aus |
| 1 | TP DAB ein |
| 2 | TP DAB keine Änderung |
| 255 | Nicht definiert |

<a id="table-tapplication"></a>
### TAPPLICATION

Dimensions: 14 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Sprachverarbeitung |
| 0x01 | Navi Applikation |
| 0x02 | Navi Karte |
| 0x03 | Online Browser |
| 0x04 | AudioPlayer |
| 0x05 | Telefon Applikation |
| 0x06 | SDARS |
| 0x07 | A4A |
| 0x08 | Treiber update (KISU) |
| 0x09 | DAB |
| 0x0A | Video_in |
| 0x0B | Sprache arabisch |
| 0x0C | TextToSpeech |
| 0xFF | Nicht definiert |

<a id="table-tapplicationrunningstatus"></a>
### TAPPLICATIONRUNNINGSTATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Applikation nicht gestartet |
| 0x01 | Applikation gestartet |
| 0xFF | Nicht definiert |

<a id="table-tapplicationactivationstatus"></a>
### TAPPLICATIONACTIVATIONSTATUS

Dimensions: 12 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Deaktiviert durch Codierung |
| 0x02 | Aktiviert durch Codierung |
| 0x04 | Deaktiviert durch SWT |
| 0x05 | Deaktiviert durch Codierung und  Deaktiviert durch SWT |
| 0x06 | Aktiviert durch Codierung und Deaktiviert durch SWT |
| 0x08 | Aktiviert durch SWT |
| 0x0A | Aktiviert durch Codierung und Aktiviert durch SWT |
| 0x10 | Teilweise Aktiviert durch SWT |
| 0x12 | Aktiviert durch Codierung und Teilweise Aktiviert durch SWT |
| 0x20 | SWT Freischaltcode eingespielt |
| 0x22 | Aktiviert durch Codierung und SWT Freischaltcode eingespielt |
| 0xFF | Nicht definiert |

<a id="table-tantscan"></a>
### TANTSCAN

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Diagnosemodus des Diversitymoduls beenden |
| 1 | Auf nächste FM Antenne schalten |
| 255 | Nicht definiert |

<a id="table-tentsource"></a>
### TENTSOURCE

Dimensions: 27 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | nächste |
| 0x01 | FM |
| 0x02 | AM |
| 0x03 | internes CD Laufwerk |
| 0x04 | CDC |
| 0x05 | internes MD Laufwerk |
| 0x06 | WB (Weatherband) |
| 0x07 | SDARS |
| 0x08 | unbenutzt (vorher IBOC) |
| 0x09 | AUX IN intern oder extern |
| 0x0A | internes DVD Laufwerk |
| 0x0B | TV |
| 0x0C | unbenutzt (vorher VIDEOTXT) |
| 0x0D | Reserviert für AV-AUX IN |
| 0x0E | DAB |
| 0x0F | TRF |
| 0x10 | RSE-DVD |
| 0x11 | RSE-AVIN-LEFT |
| 0x12 | RSE-AVIN-RIGHT |
| 0x13 | USB extern 1 (USB Audio der MULF2 High/ComBox) |
| 0x14 | USB extern 2 (USB Telefon der MULF2 High/ComBox) |
| 0x15 | RSE analog (Audio) |
| 0x16 | MMC |
| 0x17 | Mono analog IN |
| 0x18 | USB intern |
| 0x19 | Entertainment server |
| 0xFF | Entertainmentquelle nicht definiert |

<a id="table-tentsourcestatus"></a>
### TENTSOURCESTATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Entertainmentquelle war nicht verfügbar |
| 0x01 | Entertainmentquelle war verfügbar |
| 0xFF | Nicht definiert |

<a id="table-ttaste"></a>
### TTASTE

Dimensions: 11 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Keine Taste gedrückt |
| 0x01 | Auswurf CD |
| 0x02 | Auswurf DVD |
| 0x03 | Entertainment Knopf |
| 0x04 | Suchlauf abwärts - Skip links |
| 0x05 | Suchlauf aufwärts - Skip rechts |
| 0x10 | RSE Einschaltknopf links |
| 0x11 | RSE Einschaltknopf rechts |
| 0x12 | RSE Auswurf DVD |
| 0x13 | MIODE-Taste |
| 0xFF | Nicht definiert |

<a id="table-tauxverbindung"></a>
### TAUXVERBINDUNG

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | Alle Aux Verbindungen |
| 0x0001 | Aux In Audio |
| 0x0100 | Aux In RSE links |
| 0x0200 | Aux In RSE rechts |
| 0x0300 | Aux In RSE links und rechts |
| 0x0400 | Aux In RSE BMW Individual |
| 0x0500 | Aux In RSE links und BMW Individual |
| 0x0600 | Aux In RSE rechts und BMW Individual |
| 0x0700 | Aux In RSE links, rechts und BMW Individual |
| 0xFFFF | Nicht definiert |

<a id="table-tverbindungfehlerart"></a>
### TVERBINDUNGFEHLERART

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kurzschluss nach Plus |
| 0x01 | Kurzschluss nach Masse |
| 0x02 | Leitungsunterbrechung |
| 0xFF | Nicht definiert |

<a id="table-tsatellitestatus"></a>
### TSATELLITESTATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Erkennbar |
| 0x01 | Aufgestoebert |
| 0xFF | Nicht definiert |

<a id="table-tnavioutput"></a>
### TNAVIOUTPUT

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0001 | Ansage 1... |
| 0x0002 | Ansage 2... |
| 0x0003 | Ansage 3... |
| 0xFFFF | Nicht definiert |

<a id="table-tsdarstunermode"></a>
### TSDARSTUNERMODE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Boradcast Modus |
| 1 | Sinusgenerator Modus |
| 2 | BER Messung Modus |
| 255 | nicht definiert |

<a id="table-tverbauroutine"></a>
### TVERBAUROUTINE

Dimensions: 20 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00000000 | Alle Routinen |
| 0x00000001 | Verbindung Head-Unit zum Diversity |
| 0x00000002 | Verbindung Diversity zu den Antennen |
| 0x00000004 | Verbindung Head-Unit zum DAB L-Band Antennenfu&#223; |
| 0x00000008 | Verbindung Head-Unit zum DAB Band III Antennenfu&#223; |
| 0x00000010 | Verbindung Head-Unit zum GPS-Antennenfu&#223; |
| 0x00000020 | Verbindung Head-Unit zum Aux-In Box |
| 0x00000040 | Lautsprecherausgangsleitungen (Stereo System) |
| 0x00000080 | Ausgangsleitungen zum HiFi Verstärker |
| 0x00000100 | RAD ON Leitung |
| 0x00000200 | Verbindung Head-Unit zum Mikrofon 1 |
| 0x00000400 | Verbindung Head-Unit zum Mikrofon 2 |
| 0x00000800 | Verbindung Head-Unit zum VICS FM Antennenfu&#223; |
| 0x00001000 | Verbindung Head-Unit zum VICS Beacon Antennenfu&#223; |
| 0x00002000 | Verbindung Head-Unit zum ETC-Spiegel |
| 0x00004000 | Ethernet-Verbindung Head-Unit zum ZGW |
| 0x00008000 | Ethernet-Verbindung Head-Unit zum RSE High |
| 0x00010000 | Verbindung Head-Unit zur USB Kunden-Schnittstelle |
| 0x00020000 | Verbindungen zu IR-Sendeeinheit |
| 0xFFFFFFFF | Nicht definiert |

<a id="table-ttunerri"></a>
### TTUNERRI

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Ri OK |
| 0x01 | Ri not OK |
| 0x02 | Kurzschluss nach Masse |
| 0x03 | Leitungsunterbrechung |
| 0xFF | Nicht definiert |

<a id="table-taudiosignal"></a>
### TAUDIOSIGNAL

Dimensions: 11 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Entertainment |
| 0x01 | Offset Verkehrsmeldungen |
| 0x02 | Offset Navigation |
| 0x03 | Telefon |
| 0x04 | Spracherkennung |
| 0x05 | PDC |
| 0x06 | Gong |
| 0x07 | Aux In |
| 0x10 | nur für RSE: Entertainment Kopfhörer linke Seite |
| 0x20 | nur für RSE: Entertainment Kopfhörer rechte Seite |
| 0xFF | Nicht definiert |

<a id="table-tlaufwerk"></a>
### TLAUFWERK

Dimensions: 129 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00000000 | Kein Laufwerk |
| 0x00000001 | Kassette |
| 0x00000002 | CD |
| 0x00000003 | Kassette und CD |
| 0x00000004 | DVD |
| 0x00000005 | Kassette und DVD |
| 0x00000006 | CD und DVD |
| 0x00000007 | Kasette, CD und DVD |
| 0x00000008 | MD |
| 0x00000009 | Kassette und MD |
| 0x0000000A | CD und MD |
| 0x0000000B | Kassette, CD und MD |
| 0x0000000C | DVD und MD |
| 0x0000000D | Kassette, DVD und MD |
| 0x0000000E | CD, DVD und MD |
| 0x0000000F | Kassette, CD, DVD und MD |
| 0x00000010 | HDD |
| 0x00000011 | Kassette und HDD |
| 0x00000012 | CD und HDD |
| 0x00000013 | Kassette, CD und HDD |
| 0x00000014 | DVD und HDD |
| 0x00000015 | Kassette, DVD und HDD |
| 0x00000016 | CD, DVD und HDD |
| 0x00000017 | Kasette, CD, DVD und HDD |
| 0x00000018 | MD und HDD |
| 0x00000019 | Kassette, MD und HDD |
| 0x0000001A | CD, MD und HDD |
| 0x0000001B | Kassette, CD, MD und HDD |
| 0x0000001C | DVD, MD und HDD |
| 0x0000001D | Kassette, DVD, MD und HDD |
| 0x0000001E | CD, DVD, MD und HDD |
| 0x0000001F | Kassette, CD, DVD, MD und HDD |
| 0x00000020 | USB |
| 0x00000021 | Kassette und USB |
| 0x00000022 | CD und USB |
| 0x00000023 | Kassette, CD und USB |
| 0x00000024 | DVD und USB |
| 0x00000025 | Kassette, DVD und USB |
| 0x00000026 | CD, DVD und USB |
| 0x00000027 | Kasette, CD, DVD und USB |
| 0x00000028 | MD und USB |
| 0x00000029 | Kassette, MD und USB |
| 0x0000002A | CD, MD und USB |
| 0x0000002B | Kassette, CD, MD und USB |
| 0x0000002C | DVD, MD und USB |
| 0x0000002D | Kassette, DVD, MD und USB |
| 0x0000002E | CD, DVD, MD und USB |
| 0x0000002F | Kassette, CD, DVD, MD und USB |
| 0x00000030 | HDD und USB |
| 0x00000031 | Kassette, HDD und USB |
| 0x00000032 | CD, HDD und USB |
| 0x00000033 | Kassette, CD, HDD und USB |
| 0x00000034 | DVD, HDD und USB |
| 0x00000035 | Kassette, DVD, HDD und USB |
| 0x00000036 | CD, DVD, HDD und USB |
| 0x00000037 | Kasette, CD, DVD, HDD und USB |
| 0x00000038 | MD, HDD und USB |
| 0x00000039 | Kassette, MD, HDD und USB |
| 0x0000003A | CD, MD, HDD und USB |
| 0x0000003B | Kassette, CD, MD, HDD und USB |
| 0x0000003C | DVD, MD, HDD und USB |
| 0x0000003D | Kassette, DVD, MD, HDD und USB |
| 0x0000003E | CD, DVD, MD, HDD und USB |
| 0x0000003F | Kassette, CD, DVD, MD, HDD und USB |
| 0x00000040 | Flashspeicher |
| 0x00000041 | Kassette und Flashspeicher |
| 0x00000042 | CD und Flashspeicher |
| 0x00000043 | Kassette, CD und Flashspeicher |
| 0x00000044 | DVD und Flashspeicher |
| 0x00000045 | Kassette, DVD und Flashspeicher |
| 0x00000046 | CD, DVD und Flashspeicher |
| 0x00000047 | Kasette, CD, DVD und Flashspeicher |
| 0x00000048 | MD und Flashspeicher |
| 0x00000049 | Kassette, MD und Flashspeicher |
| 0x0000004A | CD, MD und Flashspeicher |
| 0x0000004B | Kassette, CD, MD und Flashspeicher |
| 0x0000004C | DVD, MD und Flashspeicher |
| 0x0000004D | Kassette, DVD, MD und Flashspeicher |
| 0x0000004E | CD, DVD, MD und Flashspeicher |
| 0x0000004F | Kassette, CD, DVD, MD und Flashspeicher |
| 0x00000050 | HDD und Flashspeicher |
| 0x00000051 | Kassette, HDD und Flashspeicher |
| 0x00000052 | CD, HDD und Flashspeicher |
| 0x00000053 | Kassette, CD, HDD und Flashspeicher |
| 0x00000054 | DVD, HDD und Flashspeicher |
| 0x00000055 | Kassette, DVD, HDD und Flashspeicher |
| 0x00000056 | CD, DVD, HDD und Flashspeicher |
| 0x00000057 | Kasette, CD, DVD, HDD und Flashspeicher |
| 0x00000058 | MD, HDD und Flashspeicher |
| 0x00000059 | Kassette, MD, HDD und Flashspeicher |
| 0x0000005A | CD, MD, HDD und Flashspeicher |
| 0x0000005B | Kassette, CD, MD, HDD und Flashspeicher |
| 0x0000005C | DVD, MD, HDD und Flashspeicher |
| 0x0000005D | Kassette, DVD, MD, HDD und Flashspeicher |
| 0x0000005E | CD, DVD, MD, HDD und Flashspeicher |
| 0x0000005F | Kassette, CD, DVD, MD, HDD und Flashspeicher |
| 0x00000060 | USB und Flashspeicher |
| 0x00000061 | Kassette, USB und Flashspeicher |
| 0x00000062 | CD, USB und Flashspeicher |
| 0x00000063 | Kassette, CD, USB und Flashspeicher |
| 0x00000064 | DVD, USB und Flashspeicher |
| 0x00000065 | Kassette, DVD, USB und Flashspeicher |
| 0x00000066 | CD, DVD, USB und Flashspeicher |
| 0x00000067 | Kasette, CD, DVD, USB und Flashspeicher |
| 0x00000068 | MD, USB und Flashspeicher |
| 0x00000069 | Kassette, MD, USB und Flashspeicher |
| 0x0000006A | CD, MD, USB und Flashspeicher |
| 0x0000006B | Kassette, CD, MD, USB und Flashspeicher |
| 0x0000006C | DVD, MD, USB und Flashspeicher |
| 0x0000006D | Kassette, DVD, MD, USB und Flashspeicher |
| 0x0000006E | CD, DVD, MD, USB und Flashspeicher |
| 0x0000006F | Kassette, CD, DVD, MD, USB und Flashspeicher |
| 0x00000070 | HDD, USB und Flashspeicher |
| 0x00000071 | Kassette, HDD, USB und Flashspeicher |
| 0x00000072 | CD, HDD, USB und Flashspeicher |
| 0x00000073 | Kassette, CD, HDD, USB und Flashspeicher |
| 0x00000074 | DVD, HDD, USB und Flashspeicher |
| 0x00000075 | Kassette, DVD, HDD, USB und Flashspeicher |
| 0x00000076 | CD, DVD, HDD, USB und Flashspeicher |
| 0x00000077 | Kasette, CD, DVD, HDD, USB und Flashspeicher |
| 0x00000078 | MD, HDD, USB und Flashspeicher |
| 0x00000079 | Kassette, MD, HDD, USB und Flashspeicher |
| 0x0000007A | CD, MD, HDD, USB und Flashspeicher |
| 0x0000007B | Kassette, CD, MD, HDD, USB und Flashspeicher |
| 0x0000007C | DVD, MD, HDD, USB und Flashspeicher |
| 0x0000007D | Kassette, DVD, MD, HDD, USB und Flashspeicher |
| 0x0000007E | CD, DVD, MD, HDD, USB und Flashspeicher |
| 0x0000007F | Kassette, CD, DVD, MD, HDD, USB und Flashspeicher |
| 0xFFFFFFFF | Nicht definiert |

<a id="table-tantenne"></a>
### TANTENNE

Dimensions: 75 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00000000 | Alle Antennen |
| 0x00000001 | AM/FM Antenne |
| 0x00000002 | GPS Antenne |
| 0x00000003 | AM/FM Antenne und GPS Antenne |
| 0x00000004 | DAB L-BAND Antenne |
| 0x00000005 | AM/FM Antenne und DAB L-BAND Antenne |
| 0x00000006 | GPS Antenne und DAB L-BAND Antenne |
| 0x00000007 | AM/FM Antenne, GPS Antenne und DAB L-BAND Antenne |
| 0x00000008 | DAB BAND III Antenne |
| 0x00000009 | AM/FM Antenne und DAB BAND III Antenne |
| 0x0000000A | GPS Antenne und DAB BAND III Antenne |
| 0x0000000B | AM/FM Antenne, GPS Antenne und DAB BAND III Antenne |
| 0x0000000C | DAB L-BAND Antenne und DAB BAND III Antenne |
| 0x0000000D | AM/FM Antenne, DAB L-BAND Antenne und DAB BAND III Antenne |
| 0x0000000E | GPS Antenne, DAB L-BAND Antenne und DAB BAND III Antenne |
| 0x0000000F | AM/FM Antenne, GPS Antenne, DAB L-BAND Antenne und DAB BAND III Antenne |
| 0x00000010 | VICS FM Antenne |
| 0x00000011 | AM/FM Antenne und VICS FM Antenne |
| 0x00000012 | GPS Antenne und VICS FM Antenne |
| 0x00000013 | AM/FM Antenne, GPS Antenne und VICS FM Antenne |
| 0x00000014 | DAB L-BAND Antenne und VICS FM Antenne |
| 0x00000015 | AM/FM Antenne, DAB L-BAND Antenne und VICS FM Antenne |
| 0x00000016 | GPS Antenne, DAB L-BAND Antenne und VICS FM Antenne |
| 0x00000017 | AM/FM Antenne, GPS Antenne, DAB L-BAND Antenne und VICS FM Antenne |
| 0x00000018 | DAB BAND III Antenne und VICS FM Antenne |
| 0x00000019 | AM/FM Antenne, DAB BAND III Antenne und VICS FM Antenne |
| 0x0000001A | GPS Antenne, DAB BAND III Antenne und VICS FM Antenne |
| 0x0000001B | AM/FM Antenne, GPS Antenne, DAB BAND III Antenne und VICS FM Antenne |
| 0x0000001C | DAB L-BAND Antenne, DAB BAND III Antenne und VICS FM Antenne |
| 0x0000001D | AM/FM Antenne, DAB L-BAND Antenne, DAB BAND III Antenne und VICS FM Antenne |
| 0x0000001E | GPS Antenne, DAB L-BAND Antenne, DAB BAND III Antenne und VICS FM Antenne |
| 0x0000001F | AM/FM Antenne, GPS Antenne, DAB L-BAND Antenne, DAB BAND III Antenne und |
| 0x00000020 | VICS Beacon Antenne |
| 0x00000021 | AM/FM Antenne und VICS Beacon Antenne |
| 0x00000022 | GPS Antenne und VICS Beacon Antenne |
| 0x00000023 | AM/FM Antenne, GPS Antenne und VICS Beacon Antenne |
| 0x00000024 | DAB L-BAND Antenne und VICS Beacon Antenne |
| 0x00000025 | AM/FM Antenne, DAB L-BAND Antenne und VICS Beacon Antenne |
| 0x00000026 | GPS Antenne, DAB L-BAND Antenne und VICS Beacon Antenne |
| 0x00000027 | AM/FM Antenne, GPS Antenne, DAB L-BAND Antenne und VICS Beacon Antenne |
| 0x00000028 | DAB BAND III Antenne und VICS Beacon Antenne |
| 0x00000029 | AM/FM Antenne, DAB BAND III Antenne und VICS Beacon Antenne |
| 0x0000002A | GPS Antenne, DAB BAND III Antenne und VICS Beacon Antenne |
| 0x0000002B | AM/FM Antenne, GPS Antenne, DAB BAND III Antenne und VICS Beacon Antenne |
| 0x0000002C | DAB L-BAND Antenne, DAB BAND III Antenne und VICS Beacon Antenne |
| 0x0000002D | AM/FM Antenne, DAB L-BAND Antenne, DAB BAND III Antenne und VICS Beacon Antenne |
| 0x0000002E | GPS Antenne, DAB L-BAND Antenne, DAB BAND III Antenne und VICS Beacon Antenne |
| 0x0000002F | AM/FM Antenne, GPS Antenne, DAB L-BAND Antenne, DAB BAND III Antenne und VICS Beacon Antenne |
| 0x00000030 | VICS FM Antenne und VICS Beacon Antenne |
| 0x00000031 | AM/FM Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x00000032 | GPS Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x00000033 | AM/FM Antenne, GPS Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x00000034 | DAB L-BAND Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x00000035 | AM/FM Antenne, DAB L-BAND Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x00000036 | GPS Antenne, DAB L-BAND Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x00000037 | AM/FM Antenne, GPS Antenne, DAB L-BAND Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x00000038 | DAB BAND III Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x00000039 | AM/FM Antenne, DAB BAND III Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x0000003A | GPS Antenne, DAB BAND III Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x0000003B | AM/FM Antenne, GPS Antenne, DAB BAND III Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x0000003C | DAB L-BAND Antenne, DAB BAND III Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x0000003D | AM/FM Antenne, DAB L-BAND Antenne, DAB BAND III Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x0000003E | GPS Antenne, DAB L-BAND Antenne, DAB BAND III Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x0000003F | AM/FM Antenne, GPS Antenne, DAB L-BAND Antenne, DAB BAND III Antenne, VICS FM Antenne und VICS Beacon Antenne |
| 0x00000040 | TV1 Antenne |
| 0x00000080 | TV2 Antenne |
| 0x000000C0 | TV1 und TV2 Antenne |
| 0x00000100 | TV3 Antenne |
| 0x00000140 | TV1 und TV3 Antenne |
| 0x00000180 | TV2 und TV3 Antenne |
| 0x000001C0 | TV1, TV2 und TV3 Antenne |
| 0x00000200 | SDARS Antenne |
| 0x00000400 | Bluetooth Antenne |
| 0x00000800 | FM2 Phasendiversity |
| 0xFFFFFFFF | Nicht definiert |

<a id="table-tantennefehlerart"></a>
### TANTENNEFEHLERART

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kurzschluss nach Plus |
| 0x01 | Kurzschluss nach Masse |
| 0x02 | Leitungsunterbrechung |
| 0x03 | Falscher Antennfu&#223; oder Diversity |
| 0xFF | Nicht definiert |

<a id="table-tnavicalibration"></a>
### TNAVICALIBRATION

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Positionierprozess kalibriert |
| 0x01 | Positionierprozess nicht kalibriert |
| 0xFF | Nicht definiert |

<a id="table-tkeynr"></a>
### TKEYNR

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Schlüssel 1 |
| 0x02 | Schlüssel 2 |
| 0x03 | Schlüssel 3 |
| 0x04 | Schlüssel 4 |
| 0x05 | Schlüssel 5 |
| 0x06 | Schlüssel 6 |
| 0x07 | Schlüssel 7 |
| 0x08 | Schlüssel 8 |
| 0x09 | Schlüssel 9 |
| 0x0A | Schlüssel 10 |
| 0x0B | Schlüssel 11 |
| 0x0C | Schlüssel 12 |
| 0x0D | Schlüssel 13 |
| 0x0E | Schlüssel 14 |
| 0x0F | Schlüssel 15 |
| 0xFF | Alle Schlüssel |

<a id="table-tsdarschanneltunesuccess"></a>
### TSDARSCHANNELTUNESUCCESS

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Kanaleinstellung erfolgreich |
| 1 | Kanal nicht aboniert |
| 2 | Kanal ungueltig |
| 3 | Kanaleinstellung läuft |
| 255 | nicht definiert |

<a id="table-tformattingstatus"></a>
### TFORMATTINGSTATUS

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Formatierungsprozess nicht gestartet |
| 0x01 | Formatierungsprozess läuft |
| 0x02 | Formatierungsprozess beendet ohne Fehler |
| 0x03 | Formatierungsprozess beendet mit Fehler |
| 0xFF | Nicht definiert |

<a id="table-thddpartition"></a>
### THDDPARTITION

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Alle Partitionen |
| 0x01 | Partition 1 (Navi DB) |
| 0x02 | Partition 2 (Vorschlagsnote) |
| 0x03 | Partition 3 (IBA, Logistikdaten, speech) |
| 0x04 | Partition 4 (Benutzerdaten) |
| 0x05 | Partition 5 (entertainment server) |
| 0x06 | Partition 6 (reserviert für Entwicklung) |
| 0xFF | Nicht definiert |

<a id="table-taudiosystem"></a>
### TAUDIOSYSTEM

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | STEREO |
| 0x01 | HIFI |
| 0x02 | TOP-HIFI |
| 0x03 | M Individual Sound |
| 0xFF | Nicht definiert |

<a id="table-tsearchingprocess"></a>
### TSEARCHINGPROCESS

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Suche nicht gestartet |
| 0x01 | Suche läuft |
| 0x02 | Suche beendet und bester Sender gefunden |
| 0x03 | Suche beendet und kein bester Sender gefunden |
| 0x04 | Test unterbrochen |
| 0xFF | Nicht definiert |

<a id="table-tmicrophone"></a>
### TMICROPHONE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Mikrofon 1 |
| 0x02 | Mikrofon 2 |
| 0xFF | Nicht definiert |

<a id="table-tmicrophonetest"></a>
### TMICROPHONETEST

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Test nicht gestartet |
| 0x01 | Test läuft |
| 0x02 | Test beendet und Signal erkannt |
| 0x03 | Test beendet und Signal nicht erkannt |
| 0x04 | Test unterbrochen |
| 0xFF | Nicht definiert |

<a id="table-tsdarsfactorysuccessful"></a>
### TSDARSFACTORYSUCCESSFUL

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Wiederherstellung nicht gestartet |
| 1 | Wiederherstellung läuft |
| 2 | Wiederherstellung beendet ohne Fehler |
| 3 | Wiederherstellung konnte nicht beendet werden |
| 255 | nicht definiert |

<a id="table-tinsertedmedium"></a>
### TINSERTEDMEDIUM

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kein Medium eingelegt |
| 0x01 | Medium Erkennung wird durchgeführt |
| 0x02 | CD Medium ist eingelegt |
| 0x03 | DVD Medium ist eingelegt |
| 0x04 | Flashspeicher Medium ist eingelegt |
| 0xFF | Nicht definiert |

<a id="table-tactivationstatevicsbeacondiagnosis"></a>
### TACTIVATIONSTATEVICSBEACONDIAGNOSIS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Deaktiviert |
| 1 | Aktiviert |
| 255 | nicht definiert |

<a id="table-tantennadiag"></a>
### TANTENNADIAG

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Antennendiagnose IO |
| 0x01 | Antennendiagnose NIO |
| 0xFF | Nicht definiert |

<a id="table-thwlieferant"></a>
### THWLIEFERANT

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Harman Becker |
| 0x01 | Siemens VDO |
| 0x02 | Visteon |
| 0x03 | Alpine |
| 0x04 | Lear |
| 0x05 | Fuba |
| 0xFF | Nicht definiert |

<a id="table-thweinheit"></a>
### THWEINHEIT

Dimensions: 1 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0xFF | Nicht definiert |

<a id="table-tradonlead"></a>
### TRADONLEAD

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | aus |
| 0x01 | ein |
| 0xFF | Nicht definiert |

<a id="table-tteststatus"></a>
### TTESTSTATUS

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Test nicht gestartet |
| 0x01 | Test läuft |
| 0x02 | Test beendet ohne Fehler |
| 0x03 | Test beendet mit Fehlern |
| 0x04 | Test unterbrochen |
| 0xFF | Nicht definiert |

<a id="table-taudiokanal"></a>
### TAUDIOKANAL

Dimensions: 27 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00000000 | Alle Kanäle |
| 0x00000001 | Links vorne (Standardkanal, speziell Mitteltöner wenn getrennte Hoch/Mitteltöner) |
| 0x00000002 | Rechts vorne (Standardkanal, speziell Mitteltöner wenn getrennte Hoch/Mitteltöner) |
| 0x00000004 | Center vorne (Erweiterter Kanal, speziell Mitteltöner wenn getrennte Hoch/Mitteltöner) |
| 0x00000008 | Seite links (Erweiterter Kanal, speziell Mitteltöner wenn getrennte Hoch/Mitteltöner) |
| 0x00000010 | Seite rechts (Erweiterter Kanal, speziell Mitteltöner wenn getrennte Hoch/Mitteltöner) |
| 0x00000020 | Links hinten (Standardkanal, speziell Mitteltöner wenn getrennte Hoch/Mitteltöner) |
| 0x00000040 | Rechts hinten (Standardkanal, speziell Mitteltöner wenn getrennte Hoch/Mitteltöner) |
| 0x00000080 | Links vorne Bass (Erweiterter Kanal) |
| 0x00000100 | Rechts vorne Bass (Erweiterter Kanal) |
| 0x00000200 | Links hinten Bass (Erweiterter Kanal) |
| 0x00000400 | Rechts hinten Bass (Erweiterter Kanal) |
| 0x00000800 | Center hinten (Erweiterter Kanal, speziell Mitteltöner wenn getrennte Hoch/Mitteltöner) |
| 0x00001000 | Linker Kopfhörer links |
| 0x00002000 | Linker Kopfhörer rechts |
| 0x00004000 | Rechter Kopfhörer links |
| 0x00008000 | Rechter Kopfhörer rechts |
| 0x00010000 | Links vorne (Erweiterter Kanal, speziell Hochtöner wenn getrennte Hoch/Mitteltöner) |
| 0x00020000 | Rechts vorne (Erweiterter Kanal, speziell Hochtöner wenn getrennte Hoch/Mitteltöner) |
| 0x00040000 | Center vorne (Erweiterter Kanal, speziell Hochtöner wenn getrennte Hoch/Mitteltöner) |
| 0x00080000 | Seite links (Erweiterter Kanal, speziell Hochtöner wenn getrennte Hoch/Mitteltöner) |
| 0x00100000 | Seite rechts (Erweiterter Kanal, speziell Hochtöner wenn getrennte Hoch/Mitteltöner) |
| 0x00200000 | Links hinten (Erweiterter Kanal, speziell Hochtöner wenn getrennte Hoch/Mitteltöner) |
| 0x00400000 | Rechts hinten (Erweiterter Kanal, speziell Hochtöner wenn getrennte Hoch/Mitteltöner) |
| 0x00800000 | Center hinten (Erweiterter Kanal, speziell Hochtöner wenn getrennte Hoch/Mitteltöner) |
| 0x00000003 | Kombination  Kanäle |
| 0xFFFFFFFF | Nicht definiert |

<a id="table-tkanalfehlerart"></a>
### TKANALFEHLERART

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kurzschluss nach Plus |
| 0x01 | Kurzschluss nach Masse |
| 0x02 | Leitungsunterbrechung |
| 0x03 | Au&#223;erhalb Toleranz |
| 0xFF | Nicht definiert |

<a id="table-tsignaldab"></a>
### TSIGNALDAB

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Kein Signal |
| 0x01 | gueltiges Signal |
| 0xFF | Nicht definiert |

<a id="table-tsignalart"></a>
### TSIGNALART

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Realbild |
| 0x02 | Testbild |
| 0x03 | Signal abschalten |
| 0x04 | Testbild mit Alive Counter (ACNT) |
| 0x05 | Testbild mit stehendem ACNT |
| 0x06 | Testbild mit leicht gestörtem ACNT |
| 0x07 | Testbild mit stark gestörtem ACNT |
| 0x08 | Testbild mit leicht springendem ACNT |
| 0x09 | Testbild mit stark springendem ACNT |

<a id="table-tvideoausgang"></a>
### TVIDEOAUSGANG

Dimensions: 33 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | Alle Ausgänge |
| 0x0001 | Ausgang 1 |
| 0x0002 | Ausgang 2 |
| 0x0003 | Ausgang 1 und 2 |
| 0x0004 | Ausgang 3 |
| 0x0005 | Ausgang 1 und 3 |
| 0x0006 | Ausgang 2 und 3 |
| 0x0007 | Ausgang 1, 2 und 3 |
| 0x0008 | Ausgang 4 |
| 0x0009 | Ausgang 1 und 4 |
| 0x000A | Ausgang 2 und 4 |
| 0x000B | Ausgang 1, 2 und 4 |
| 0x000C | Ausgang 3 und 4 |
| 0x000D | Ausgang 1, 2 und 4 |
| 0x000E | Ausgang 2, 3 und 4 |
| 0x000F | Ausgang 1, 2, 3 und 4 |
| 0x0010 | Ausgang 5 |
| 0x0011 | Ausgang 1 und 5 |
| 0x0012 | Ausgang 2 und 5 |
| 0x0013 | Ausgang 1,2 und 5 |
| 0x0014 | Ausgang 3 und 5 |
| 0x0015 | Ausgang 1,3 und 5 |
| 0x0016 | Ausgang 2,3 und 5 |
| 0x0017 | Ausgang 1, 2 und 3 und 5 |
| 0x0018 | Ausgang 4 und 5 |
| 0x0019 | Ausgang 1, 4 und 5 |
| 0x001A | Ausgang 2, 4 und 5 |
| 0x001B | Ausgang 1, 2, 4 und 5 |
| 0x001C | Ausgang 3, 4 und 5 |
| 0x001D | Ausgang 1, 2, 4 und 5 |
| 0x001E | Ausgang 2, 3, 4 und 5 |
| 0x001F | Ausgang 1, 2, 3, 4 und 5 |
| 0xFFFF | Nicht definiert |

<a id="table-ttp"></a>
### TTP

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | TP aus |
| 0x01 | TP ein |
| 0x02 | TP keine Änderung |
| 0xFF | Nicht definiert |

<a id="table-taf"></a>
### TAF

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | AF aus |
| 0x01 | AF ein |
| 0x02 | AF keine Änderung |
| 0xFF | Nicht definiert |

<a id="table-trds"></a>
### TRDS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | RDS aus |
| 0x01 | RDS ein |
| 0x02 | RDS keine Änderung |
| 0xFF | Nicht definiert |

<a id="table-tonlinestatetable"></a>
### TONLINESTATETABLE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Online-Status OK |
| 0x01 | Daten nicht abrufbar |
| 0xFF | Nicht definiert |

<a id="table-thddsmartvalues"></a>
### THDDSMARTVALUES

Dimensions: 15 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0001 | Lesefehlerrate |
| 0x0002 | Allgemeiner Datendurchsatz |
| 0x0003 | Durchschnitt der Startzeit [msec] |
| 0x0004 | Anzahl der Start/Stop-Vorgänge |
| 0x0005 | Anzahl der verbrauchten Reserve-Sektoren |
| 0x0007 | Positionierungsproblemrate |
| 0x0008 | Positionierungsdurchsatz |
| 0x0009 | Laufleistung in Stunden (inklusive Standby) |
| 0x000A | Anzahl Wiederholungen Rotationsstart |
| 0x000C | Anzahl Einschaltvorgänge |
| 0x00C0 | Anzahl Not-Auschaltvorgänge |
| 0x00C1 | Anzahl Parkvorgänge |
| 0x00E7 | Temperatur des Laufwerkes |
| 0x00C5 | Anzahl aktuell instabiler Sektoren |
| 0xFFFF | Nicht definiert |

<a id="table-tnavimapstatus"></a>
### TNAVIMAPSTATUS

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Navikarte vorhanden und aktiviert |
| 0x01 | Navikarte deaktiviert |
| 0x02 | Navikarte nicht vorhanden oder gelöscht |
| 0x03 | Navikarte wird gerade deaktiviert... |
| 0x04 | Navikarte wird gerade gelöscht... |
| 0xFF | Nicht definiert |

<a id="table-tgeartype"></a>
### TGEARTYPE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Rückwärtsgang |
| 0x01 | Vorwärtsgang |
| 0x02 | Leerlauf |
| 0xFF | Nicht definiert |

<a id="table-tdirectionsource"></a>
### TDIRECTIONSOURCE

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Getriebe |
| 0xFF | Nicht definiert |

<a id="table-tprovisioningstatus"></a>
### TPROVISIONINGSTATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | IDLE, wurde nicht gestartet |
| 0x01 | ACTIVE, läuft noch |
| 0x02 | SUCCESS, alles OK |
| 0x03 | FAILED, mit Fehler beendet |

<a id="table-tprocessstatus"></a>
### TPROCESSSTATUS

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Prozess nicht gestartet |
| 0x01 | Prozess läuft |
| 0x02 | Prozess beendet ohne Fehler |
| 0x03 | Prozess beendet mit Fehlern |
| 0x04 | Prozess unterbrochen |
| 0xFF | Nicht definiert |

<a id="table-tnavisimulationmodeactivationstatus"></a>
### TNAVISIMULATIONMODEACTIVATIONSTATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Navi simulation mode deactivated |
| 0x01 | Navi simulation mode activated |
| 0xFF | Nicht definiert |

<a id="table-tab-exchangingstatus"></a>
### TAB_EXCHANGINGSTATUS

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Exchanging process not started |
| 0x01 | Exchanging process is running |
| 0x02 | Exchanging process finished without errors |
| 0x03 | Exchanging process finished with errors |
| 0xFF | Nicht definiert |

<a id="table-troutedownload"></a>
### TROUTEDOWNLOAD

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Route download not started |
| 1 | Route download is running |
| 2 | Route download finished without error(s) |
| 3 | Route download finished with error(s) |
| 4 | Route download halted |
| 255 | Not defined |

<a id="table-tpoidownload"></a>
### TPOIDOWNLOAD

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | POI download not started |
| 1 | POI download is running |
| 2 | POI download finished without error(s) |
| 3 | POI download finished with error(s) |
| 4 | POI download halted |
| 255 | Not defined |

<a id="table-tatcversion"></a>
### TATCVERSION

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | no ATC diagnosis possible |
| 0x01 | ATC diagnosis with track 12 measurement |
| 0x02 | ATC diagnosis with jitter measurement |
| 0xFF | Nicht definiert |

<a id="table-thwvar-device"></a>
### THWVAR_DEVICE

Dimensions: 13 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00000000 | Headunit Stufe 1 (Radio Business) |
| 0x00000001 | Headunit Stufe 2 (Radio Professional) |
| 0x00000002 | Headunit Stufe 3 (Navigation Business) |
| 0x00000004 | Headunit Stufe 4 (Navigation Professional) |
| 0x00000008 | RearSeatEntertainment Mid |
| 0x00000010 | RearSeatEntertainment High |
| 0x00000020 | TV-Modul DVB-T |
| 0x00000040 | TV-Modul DVB-T RSE |
| 0x00000080 | TV-Modul ISDB-T |
| 0x000000A0 | TV-Modul China |
| 0x00000100 | VideoSwitch Mid |
| 0x00000200 | VideoSwitch High |
| 0xFFFFFFFF | Nicht definiert |

<a id="table-thwvar-function"></a>
### THWVAR_FUNCTION

Dimensions: 13 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00010000 | IBOC |
| 0x00020000 | DAB |
| 0x00040000 | Video-in |
| 0x00080000 | SDARS |
| 0x00100000 | Telefon |
| 0x00200000 | I-Speech |
| 0x00400000 | CD-Laufwerk |
| 0x00800000 | MSA |
| 0x01000000 | als Japan-Variante |
| 0x02000000 | als China/Korea-Variante |
| 0x04000000 | CD-Laufwerk |
| 0x08000000 | Media-USB |
| 0xFFFFFFFF | Nicht definiert |

<a id="table-tindividualdataliste"></a>
### TINDIVIDUALDATALISTE

Dimensions: 6 rows × 17 columns

| ENTRYNR | ISLAST | FROMWHERE | DIAG | CARORKEY | USECASE | TESTER_ALGO | RESERVED | INQY_LEN | INQY_DATA | RESP_LEN | RESP_DATA | WRITE_LEN | WRITE_DATA | W_RESP_LEN | W_RESP_DATA | COMMENT |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x0000 | 0x00 | 01 | 63 | 02 | 000C | 01 | 00 | 06 | 100200000001 | 00 |  | 06 | 100200000001 | 00 |  | Profil 1 ohne Adressbuch |
| 0x0001 | 0x00 | 01 | 63 | 02 | 000C | 01 | 00 | 06 | 100200000002 | 00 |  | 06 | 100200000002 | 00 |  | Profil 2 ohne Adressbuch |
| 0x0002 | 0x00 | 01 | 63 | 02 | 000C | 01 | 00 | 06 | 100200000003 | 00 |  | 06 | 100200000003 | 00 |  | Profil 3 ohne Adressbuch |
| 0x0003 | 0x00 | 01 | 63 | 02 | 000C | 01 | 00 | 06 | 100200000004 | 00 |  | 06 | 100200000004 | 00 |  | Profil Gast ohne Adressbuch |
| 0x0004 | 0x00 | 01 | 63 | 02 | 000C | 01 | 00 | 06 | 100200000005 | 00 |  | 06 | 100200000005 | 00 |  | Globales Adressbuch |
| 0x0005 | 0xFF | 01 | 63 | 02 | 000C | 01 | 00 | 06 | 100200000006 | 00 |  | 06 | 100200000006 | 00 |  | Selbstdigitalisierte Routen |

<a id="table-twakeupsource"></a>
### TWAKEUPSOURCE

Dimensions: 6 rows × 2 columns

| MASKE | TEXT |
| --- | --- |
| 0x01 | Weckursache = CAN |
| 0x02 | Weckursache = MOST |
| 0x03 | Weckursache = IPC |
| 0x04 | Weckursache = Intern |
| 0x05 | Weckursache = Reset |
| 0xFF | Weckursache = unbekannt |

<a id="table-tgpscorrelationheading"></a>
### TGPSCORRELATIONHEADING

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Correlation OK |
| 0x01 | Correlation not OK |
| 0xFF | Nicht definiert |

<a id="table-tgyrotype"></a>
### TGYROTYPE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | internal to the Head-Unit |
| 0x01 | external to the Head-Unit |
| 0xFF | Nicht definiert |

<a id="table-taccelerationsensortype"></a>
### TACCELERATIONSENSORTYPE

Dimensions: 3 rows × 2 columns

| CODE | TEXT |
| --- | --- |
| 0x00 | internal to the Head-Unit |
| 0x01 | external to the Head-Unit |
| 0xFF | not defined |

<a id="table-tmapupdate"></a>
### TMAPUPDATE

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Map update not started |
| 0x01 | Map update is running |
| 0x02 | Map update finished without error(s) |
| 0x03 | Map update finished with error(s) |
| 0x04 | Map update halted |
| 0xFF | not defined |

<a id="table-tdabtmcactivationstate"></a>
### TDABTMCACTIVATIONSTATE

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Not activated |
| 0x01 | Activated |
| 0xFF | Not defined |

<a id="table-thubconnectionstate"></a>
### THUBCONNECTIONSTATE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | HUB connected |
| 0x01 | HUB not connected |
| 0x04 | HUB not coded |
| 0xFF | not defined |

<a id="table-tdaactivationstate"></a>
### TDAACTIVATIONSTATE

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | idle, not active yet |
| 0x02 | activation in progress |
| 0x03 | activation failed |
| 0x04 | activation successful |
| 0xFF | Nicht definiert |
