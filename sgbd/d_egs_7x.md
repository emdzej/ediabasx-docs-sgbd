# d_egs_7x.grp

- Jobs: [2](#jobs)
- Tables: [0](#tables)

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [IDENTIFIKATION](#job-identifikation) - Zuordnung von ADR_VAR_DIAG Steuergeräteadresse ADR  (Hex) Variantenindex      VAR  (Hex) = systemNameOrEngineType ( SNOET ) Diagnoseindex       DIAG (Hex) = vehicleManufacturerDiagnosticIndex ( VMDI ) Zuordnung von ADR_INDEX Steuergeräteadresse ADR   XX      (Hex) SGBD-Index 22 3F30  INDEX XXXX  (Hex) zu Steuergerätebeschreibungsdatei SGBD Gruppendatei                   GRUPPE Steuergeräteklartext           STEUERGERAET KWP2000: $1A ReadECUIdentification UDS: $22   ReadDataByIdentifier $3F30 Sub-Parameter SGBD-Index

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

<a id="job-identifikation"></a>
### IDENTIFIKATION

Zuordnung von ADR_VAR_DIAG Steuergeräteadresse ADR  (Hex) Variantenindex      VAR  (Hex) = systemNameOrEngineType ( SNOET ) Diagnoseindex       DIAG (Hex) = vehicleManufacturerDiagnosticIndex ( VMDI ) Zuordnung von ADR_INDEX Steuergeräteadresse ADR   XX      (Hex) SGBD-Index 22 3F30  INDEX XXXX  (Hex) zu Steuergerätebeschreibungsdatei SGBD Gruppendatei                   GRUPPE Steuergeräteklartext           STEUERGERAET KWP2000: $1A ReadECUIdentification UDS: $22   ReadDataByIdentifier $3F30 Sub-Parameter SGBD-Index

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| VARIANTE | string | Name der SGBD |

## Tables

No tables found.
