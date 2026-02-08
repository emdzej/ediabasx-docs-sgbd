# vvt_anst.prg

- Jobs: [3](#jobs)
- Tables: [4](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | ME9.2.2 fuer NG-Motoren |
| ORIGIN | BMW VS-22 Martin Björnsson |
| REVISION | 1.000 |
| AUTHOR | BMW VS-22 Martin Björnsson |
| COMMENT | Sonder-SGBD für die Ansteuerung des VVT und gleichzeitigen Auslesen der Laufunruhewerte |
| PACKAGE | 1.26 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [INFO](#job-info) - Information SGBD
- [STEUERN_VVT](#job-steuern-vvt) - Stellgliedansteuerung VVT

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

<a id="job-steuern-vvt"></a>
### STEUERN_VVT

Stellgliedansteuerung VVT

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VERSTELLWINKEL | int | gibt einen absoluten Verstellwinkel an (0..180 Grd) |
| MINHUB | int | Gewünschter Minhub (Wertebereich: 0...255) |
| MAXHUB | int | Gewünschter Maxhub (Wertebereich: 0...255) |
| SCHRITT | int | Gewünschte Schrittgrösse (Wertebereich: 0...255) |
| DURCHLAUF | int | Durchlauf Minhub-Maxhub = 1 Maxhub-Minhub = 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| LUTSFI_WERTE_1 | string | Laufunruhewerte erste Durchlauf für alle Zylinder |
| LUTSFI_WERTE_2 | string |  |
| LUTSFI_WERTE_3 | string |  |
| LUTSFI_WERTE_4 | string |  |
| LUTSFI_WERTE_5 | string |  |
| LUTSFI_WERTE_6 | string |  |
| LUTSFI_WERTE_7 | string |  |
| LUTSFI_WERTE_8 | string |  |
| LUTSFI_WERTE_9 | string |  |
| LUTSFI_WERTE_10 | string |  |
| LUTSFI_WERTE_11 | string |  |
| LUTSFI_WERTE_12 | string |  |
| LUTSFI_WERTE_13 | string |  |
| LUTSFI_WERTE_14 | string |  |
| LUTSFI_WERTE_15 | string |  |
| LUTSFI_WERTE_16 | string |  |
| LUTSFI_WERTE_17 | string |  |
| LUTSFI_WERTE_18 | string |  |
| LUTSFI_WERTE_19 | string |  |
| LUTSFI_WERTE_20 | string |  |
| LUTSFI_WERTE_21 | string |  |
| LUTSFI_WERTE_22 | string |  |
| LUTSFI_WERTE_23 | string |  |
| LUTSFI_WERTE_24 | string |  |
| LUTSFI_WERTE_25 | string |  |
| LUTSFI_WERTE_26 | string |  |
| LUTSFI_WERTE_27 | string |  |
| LUTSFI_WERTE_28 | string |  |
| LUTSFI_WERTE_29 | string |  |
| LUTSFI_WERTE_30 | string |  |
| LUTSFI_WERTE_31 | string |  |
| LUTSFI_WERTE_32 | string |  |
| LUTSFI_WERTE_33 | string |  |
| LUTSFI_WERTE_34 | string |  |
| LUTSFI_WERTE_35 | string |  |
| LUTSFI_WERTE_36 | string |  |
| LUTSFI_WERTE_37 | string |  |
| LUTSFI_WERTE_38 | string |  |
| LUTSFI_WERTE_39 | string |  |
| LUTSFI_WERTE_40 | string |  |
| LUTSFI_WERTE_41 | string |  |
| LUTSFI_WERTE_42 | string |  |
| LUTSFI_WERTE_43 | string |  |
| LUTSFI_WERTE_44 | string |  |
| LUTSFI_WERTE_45 | string |  |
| LUTSFI_WERTE_46 | string |  |
| LUTSFI_WERTE_47 | string |  |
| LUTSFI_WERTE_48 | string |  |
| LUTSFI_WERTE_49 | string |  |
| LUTSFI_WERTE_50 | string |  |
| LUTSFI_WERTE_51 | string |  |
| LUTSFI_WERTE_52 | string |  |
| LUTSFI_WERTE_53 | string |  |
| LUTSFI_WERTE_54 | string |  |
| LUTSFI_WERTE_55 | string |  |
| LUTSFI_WERTE_56 | string |  |
| LUTSFI_WERTE_57 | string |  |
| LUTSFI_WERTE_58 | string |  |
| LUTSFI_WERTE_59 | string |  |
| LUTSFI_WERTE_60 | string |  |
| LUTSFI_WERTE_61 | string |  |
| LUTSFI_WERTE_62 | string |  |
| LUTSFI_WERTE_63 | string |  |
| LUTSFI_WERTE_64 | string |  |
| LUTSFI_WERTE_65 | string |  |
| LUTSFI_WERTE_66 | string |  |
| LUTSFI_WERTE_67 | string |  |
| LUTSFI_WERTE_68 | string |  |
| LUTSFI_WERTE_69 | string |  |
| LUTSFI_WERTE_70 | string |  |
| LUTSFI_WERTE_71 | string |  |
| LUTSFI_WERTE_72 | string |  |
| LUTSFI_WERTE_73 | string |  |
| LUTSFI_WERTE_74 | string |  |
| LUTSFI_WERTE_75 | string |  |
| LUTSFI_WERTE_76 | string |  |
| LUTSFI_WERTE_77 | string |  |
| LUTSFI_WERTE_78 | string |  |
| LUTSFI_WERTE_79 | string |  |
| LUTSFI_WERTE_80 | string |  |
| LUTSFI_WERTE_81 | string |  |
| LUTSFI_WERTE_82 | string |  |
| LUTSFI_WERTE_83 | string |  |
| LUTSFI_WERTE_84 | string |  |
| LUTSFI_WERTE_85 | string |  |
| LUTSFI_WERTE_86 | string |  |
| LUTSFI_WERTE_87 | string |  |
| LUTSFI_WERTE_88 | string |  |
| LUTSFI_WERTE_89 | string |  |
| LUTSFI_WERTE_90 | string |  |
| LUTSFI_WERTE_91 | string |  |
| LUTSFI_WERTE_92 | string |  |
| LUTSFI_WERTE_93 | string |  |
| LUTSFI_WERTE_94 | string |  |
| LUTSFI_WERTE_95 | string |  |
| LUTSFI_WERTE_96 | string |  |
| LUTSFI_WERTE_97 | string |  |
| LUTSFI_WERTE_98 | string |  |
| LUTSFI_WERTE_99 | string |  |
| LUTSFI_WERTE_100 | string |  |
| LUTSFI_WERTE_101 | string |  |
| LUTSFI_WERTE_102 | string |  |
| LUTSFI_WERTE_103 | string |  |
| LUTSFI_WERTE_104 | string |  |
| LUTSFI_WERTE_105 | string |  |
| LUTSFI_WERTE_106 | string |  |
| LUTSFI_WERTE_107 | string |  |
| LUTSFI_WERTE_108 | string |  |
| LUTSFI_WERTE_109 | string |  |
| LUTSFI_WERTE_110 | string |  |
| LUTSFI_WERTE_111 | string |  |
| LUTSFI_WERTE_112 | string |  |
| LUTSFI_WERTE_113 | string |  |
| LUTSFI_WERTE_114 | string |  |
| LUTSFI_WERTE_115 | string |  |
| LUTSFI_WERTE_116 | string |  |
| LUTSFI_WERTE_117 | string |  |
| LUTSFI_WERTE_118 | string |  |
| LUTSFI_WERTE_119 | string |  |
| LUTSFI_WERTE_120 | string |  |
| LUTSFI_WERTE_121 | string |  |
| LUTSFI_WERTE_122 | string |  |
| LUTSFI_WERTE_123 | string |  |
| LUTSFI_WERTE_124 | string |  |
| LUTSFI_WERTE_125 | string |  |
| LUTSFI_WERTE_126 | string |  |
| LUTSFI_WERTE_127 | string |  |
| LUTSFI_WERTE_128 | string |  |
| LUTSFI_WERTE_129 | string |  |
| LUTSFI_WERTE_130 | string |  |
| LUTSFI_WERTE_131 | string |  |
| LUTSFI_WERTE_132 | string |  |
| LUTSFI_WERTE_133 | string |  |
| LUTSFI_WERTE_134 | string |  |
| LUTSFI_WERTE_135 | string |  |
| LUTSFI_WERTE_136 | string |  |
| LUTSFI_WERTE_137 | string |  |
| LUTSFI_WERTE_138 | string |  |
| LUTSFI_WERTE_139 | string |  |
| LUTSFI_WERTE_140 | string |  |
| LUTSFI_WERTE_141 | string |  |
| LUTSFI_WERTE_142 | string |  |
| LUTSFI_WERTE_143 | string |  |
| LUTSFI_WERTE_144 | string |  |
| LUTSFI_WERTE_145 | string |  |
| LUTSFI_WERTE_146 | string |  |
| LUTSFI_WERTE_147 | string |  |
| LUTSFI_WERTE_148 | string |  |
| LUTSFI_WERTE_149 | string |  |
| LUTSFI_WERTE_150 | string |  |
| LUTSFI_WERTE_151 | string |  |
| LUTSFI_WERTE_152 | string |  |
| LUTSFI_WERTE_153 | string |  |
| LUTSFI_WERTE_154 | string |  |
| LUTSFI_WERTE_155 | string |  |
| LUTSFI_WERTE_156 | string |  |
| LUTSFI_WERTE_157 | string |  |
| LUTSFI_WERTE_158 | string |  |
| LUTSFI_WERTE_159 | string |  |
| LUTSFI_WERTE_160 | string |  |
| LUTSFI_WERTE_161 | string |  |
| LUTSFI_WERTE_162 | string |  |
| LUTSFI_WERTE_163 | string |  |
| LUTSFI_WERTE_164 | string |  |
| LUTSFI_WERTE_165 | string |  |
| LUTSFI_WERTE_166 | string |  |
| LUTSFI_WERTE_167 | string |  |
| LUTSFI_WERTE_168 | string |  |
| LUTSFI_WERTE_169 | string |  |
| LUTSFI_WERTE_170 | string |  |
| LUTSFI_WERTE_171 | string |  |
| LUTSFI_WERTE_172 | string |  |
| LUTSFI_WERTE_173 | string |  |
| LUTSFI_WERTE_174 | string |  |
| LUTSFI_WERTE_175 | string |  |
| LUTSFI_WERTE_176 | string |  |
| LUTSFI_WERTE_177 | string |  |
| LUTSFI_WERTE_178 | string |  |
| LUTSFI_WERTE_179 | string |  |
| LUTSFI_WERTE_180 | string |  |
| LUTSFI_WERTE_181 | string |  |
| LUTSFI_WERTE_182 | string |  |
| LUTSFI_WERTE_183 | string |  |
| LUTSFI_WERTE_184 | string |  |
| LUTSFI_WERTE_185 | string |  |
| LUTSFI_WERTE_186 | string |  |
| LUTSFI_WERTE_187 | string |  |
| LUTSFI_WERTE_188 | string |  |
| LUTSFI_WERTE_189 | string |  |
| LUTSFI_WERTE_190 | string |  |
| LUTSFI_WERTE_191 | string |  |
| LUTSFI_WERTE_192 | string |  |
| LUTSFI_WERTE_193 | string |  |
| LUTSFI_WERTE_194 | string |  |
| LUTSFI_WERTE_195 | string |  |
| LUTSFI_WERTE_196 | string |  |
| LUTSFI_WERTE_197 | string |  |
| LUTSFI_WERTE_198 | string |  |
| LUTSFI_WERTE_199 | string |  |
| LUTSFI_WERTE_200 | string |  |
| LUTSFI_WERTE_201 | string |  |
| LUTSFI_WERTE_202 | string |  |
| LUTSFI_WERTE_203 | string |  |
| LUTSFI_WERTE_204 | string |  |
| LUTSFI_WERTE_205 | string |  |
| LUTSFI_WERTE_206 | string |  |
| LUTSFI_WERTE_207 | string |  |
| LUTSFI_WERTE_208 | string |  |
| LUTSFI_WERTE_209 | string |  |
| LUTSFI_WERTE_210 | string |  |
| LUTSFI_WERTE_211 | string |  |
| LUTSFI_WERTE_212 | string |  |
| LUTSFI_WERTE_213 | string |  |
| LUTSFI_WERTE_214 | string |  |
| LUTSFI_WERTE_215 | string |  |
| LUTSFI_WERTE_216 | string |  |
| LUTSFI_WERTE_217 | string |  |
| LUTSFI_WERTE_218 | string |  |
| LUTSFI_WERTE_219 | string |  |
| LUTSFI_WERTE_220 | string |  |
| LUTSFI_WERTE_221 | string |  |
| LUTSFI_WERTE_222 | string |  |
| LUTSFI_WERTE_223 | string |  |
| LUTSFI_WERTE_224 | string |  |
| LUTSFI_WERTE_225 | string |  |
| LUTSFI_WERTE_226 | string |  |
| LUTSFI_WERTE_227 | string |  |
| LUTSFI_WERTE_228 | string |  |
| LUTSFI_WERTE_229 | string |  |
| LUTSFI_WERTE_230 | string |  |
| LUTSFI_WERTE_231 | string |  |
| LUTSFI_WERTE_232 | string |  |
| LUTSFI_WERTE_233 | string |  |
| LUTSFI_WERTE_234 | string |  |
| LUTSFI_WERTE_235 | string |  |
| LUTSFI_WERTE_236 | string |  |
| LUTSFI_WERTE_237 | string |  |
| LUTSFI_WERTE_238 | string |  |
| LUTSFI_WERTE_239 | string |  |
| LUTSFI_WERTE_240 | string |  |
| LUTSFI_WERTE_241 | string |  |
| LUTSFI_WERTE_242 | string |  |
| LUTSFI_WERTE_243 | string |  |
| LUTSFI_WERTE_244 | string |  |
| LUTSFI_WERTE_245 | string |  |
| LUTSFI_WERTE_246 | string |  |
| LUTSFI_WERTE_247 | string |  |
| LUTSFI_WERTE_248 | string |  |
| LUTSFI_WERTE_249 | string |  |
| LUTSFI_WERTE_250 | string |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [KONZEPT_TABELLE](#table-konzept-tabelle) (4 × 2)

<a id="table-sg-diagnosekonzept"></a>
### SG_DIAGNOSEKONZEPT

Dimensions: 4 rows × 2 columns

| RANG | KONZEPT_TEXT |
| --- | --- |
| 1 | BMW-FAST |
| 2 | KWP2000* |
| - | KWP2000 |
| - | DS2 |

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

<a id="table-authentisierung"></a>
### AUTHENTISIERUNG

Dimensions: 4 rows × 2 columns

| AUTH_NR | AUTH_TEXT |
| --- | --- |
| 0x01 | Simple |
| 0x02 | Symetrisch |
| 0x03 | Asymetrisch |
| 0xFF | Keine |

<a id="table-konzept-tabelle"></a>
### KONZEPT_TABELLE

Dimensions: 4 rows × 2 columns

| NR | KONZEPT_TEXT |
| --- | --- |
| 0x0F | BMW-FAST |
| 0x0D | KWP2000* |
| 0x0C | KWP2000 |
| 0x06 | DS2 |
