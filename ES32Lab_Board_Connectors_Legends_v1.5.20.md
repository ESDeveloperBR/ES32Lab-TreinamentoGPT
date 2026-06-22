# ES32Lab GPT - Conectores E Legendas Da Placa ES32Lab v1.5.20

Versao do conhecimento: `0.9.0`
Atualizado em: `2026-06-20`
Resumo da versao: acompanha a inclusao da Shield 4IN-4Relay Optoacoplada e mantem catalogo fisico da ES32Lab v1.5.20.

Este arquivo deve ser usado quando o usuario perguntar sobre conectores fisicos, legendas impressas, jumpers, pinagem, face superior, face inferior, shields inferiores, alimentacao, barramentos ou localizacao de recursos na ES32Lab.

Este catalogo lista conectores e legendas da placa. Componentes eletronicos discretos, como resistores, capacitores e CIs identificados por codigos como `R2`, `C13`, `U5` ou `U6`, nao fazem parte deste arquivo.

Regra importante:

- conectores da face superior e da face inferior nao devem ser misturados;
- mesmo que existam furos, vias ou sinais interligados entre os dois lados da PCB, a IA deve informar corretamente a face fisica do conector citado;
- quando a pergunta for sobre codigo, consulte tambem `API_Catalog.json`, `Code_Generation_Rules.md` e `ES32Lab_Defaults_And_Best_Practices.md`;
- quando a pergunta for sobre sensores, perifericos ou shields externos validados, consulte tambem `Validated_Hardware_Catalog.md`.

## Versao Da Placa

- Versao da placa: `1.5.20`.
- Origem da versao: legenda inferior da PCB.
- A partir da versao `1.5.20`, a legenda dos bornes da ponte H deve ser tratada como corrigida para a documentacao atual.
- Em placas anteriores a `1.5.20`, pode existir legenda antiga nos bornes da ponte H, como `MOTOR1` e `MOTOR2`; nesse caso, seguir as regras de compatibilidade registradas em `ES32Lab_Defaults_And_Best_Practices.md` e `Code_Generation_Rules.md`.

## Convencoes

- `HDR-M-2.54`: conector macho, passo 2,54 mm.
- `HDR-F-2.54`: conector femea, passo 2,54 mm.
- `Pxx`: pino/GPIO do ESP32 conforme legenda da ES32Lab.
- `EXx`: pino do expansor I2C onboard.
- `3V3`: alimentacao de 3,3 V.
- `+5V`: alimentacao de 5 V.
- `GND`: terra.

# 1. Face Superior Da PCB

## 1.1 Alimentacao E Chaves

### Botao Power

- Componente: `PS-22F03`.
- Tipo: chave ou botao power.
- Cor: vermelho.
- Face da PCB: superior.
- Legenda associada: `POWER`.
- Funcao: liga/desliga a alimentacao da placa.

### Botao BAT RESET

- Componente: `KEY-6x6mm H15mm`.
- Tipo: botao tactil.
- Cor: preto.
- Face da PCB: superior.
- Legenda associada: `BAT RESET`.
- Funcao: reset ou reativacao do circuito de baterias.
- Observacao: pode ser necessario pressionar `BAT RESET` apos troca de baterias sem fonte externa conectada.

### Conector Power DC IN 9V

- Componente: `DC-005-2.5A-2.0`.
- Tipo: conector DC femea.
- Cor: preto.
- Face da PCB: superior.
- Legendas associadas:
  - `Power DC IN`
  - `VIN_9V`
  - `+9V/GND-`
- Pinos:
  - `+9V`: pino central.
  - `GND`: contato lateral do conector.
- Funcao: entrada de alimentacao externa pelo conector DC.
- Seguranca: a alimentacao externa da ES32Lab nao deve ultrapassar 9 V, com positivo no pino central.

### Borne Vermelho - Entrada 9 V

- Componente: `CONN-TH_P5.00_KF301-5.0-2P`.
- Tipo: borne de 2 pinos.
- Cor: vermelho.
- Face da PCB: superior.
- Legenda associada: `+9V/GND`.
- Pinos:
  - `+9V`: pino da esquerda.
  - `GND`: pino da direita.
- Funcao: entrada de alimentacao externa de ate 9 V.

### Borne Verde - Baterias BAT S1 E BAT S2

- Componente: `CONN-TH_P5.00_KF301-5.0-2P`.
- Tipo: borne de 2 pinos.
- Cor: verde.
- Face da PCB: superior.
- Legendas associadas:
  - `BAT1 S1`
  - `+ BAT S1 -`
  - `BAT2`
  - `+ BAT S2 -`
- Estrutura:
  - `BAT1`: `+` na esquerda e `-` na direita.
  - `BAT2`: `+` na esquerda e `-` na direita.
- Funcao: conexao das baterias da placa.
- Observacao: a placa trabalha com duas baterias de ion-litio de 4,2 V no circuito de carga/descarga.

## 1.2 Motores E Ponte H

### Borne Azul - Motor 0 DC

- Componente: `CONN-TH_P5.00_KF301-5.0-2P`.
- Tipo: borne de 2 pinos.
- Cor: azul.
- Face da PCB: superior.
- Legendas associadas:
  - `Motor0 DC`
  - `MOTOR0`
- Pinos:
  - terminal A do motor 0.
  - terminal B do motor 0.
- Funcao: conexao do motor DC 0 a ponte H onboard.
- Observacao de codigo: na classe `ES_CarControl`, este motor deve ser tratado como motor de indice `0`.

### Borne Azul - Motor 1 DC

- Componente: `CONN-TH_P5.00_KF301-5.0-2P`.
- Tipo: borne de 2 pinos.
- Cor: azul.
- Face da PCB: superior.
- Legendas associadas:
  - `Motor1 DC`
  - `MOTOR1`
- Pinos:
  - terminal A do motor 1.
  - terminal B do motor 1.
- Funcao: conexao do motor DC 1 a ponte H onboard.
- Observacao de codigo: na classe `ES_CarControl`, este motor deve ser tratado como motor de indice `1`.

### Jumper BRID-H

- Componente: `HDR-M-2.54-Branco-1X4`.
- Tipo: conector macho 1x4.
- Cor: branco.
- Face da PCB: superior.
- Legenda associada: `BRID-H`.
- Pinos/legendas:
  - `M1A`
  - `M1B`
  - `M2A`
  - `M2B`
- Funcao: conecta a ponte H ao expansor I2C onboard.
- Observacao: quando os jumpers brancos da ponte H estiverem conectados, `EX4`, `EX5`, `EX6` e `EX7` ficam ocupados pelo controle dos motores.

## 1.3 Conectores ESP32 / Shields

### ESP32 DEVKIT V1

- Componente: dois conectores `HDR-F-2.54_1X15`.
- Tipo: conectores femea 1x15.
- Cor: preto.
- Face da PCB: superior.
- Legendas associadas:
  - `ESP32 DEVKIT V1`
  - `ESP32_DEVKITV1`
- Pinos/legendas extraidas:
  - `P00`
  - `RX0`
  - `P04`
  - `P12`
  - `P14`
  - `P16`
  - `P18`
  - `P21`
  - `P23`
  - `P26`
  - `P32`
  - `P34`
  - `P36`
  - `TX0`
  - `P02`
  - `P05`
  - `P13`
  - `P15`
  - `P17`
  - `P19`
  - `P22`
  - `P25`
  - `P27`
  - `P33`
  - `P35`
  - `P39`
- Observacao: este encaixe aceita placas compativeis com ESP32 DEVKIT V1.

### ESP32 NODEMCU 32S

- Componente: dois conectores `HDR-F-2.54_1X19`.
- Tipo: conectores femea 1x19.
- Cor: preto.
- Face da PCB: superior.
- Legendas associadas:
  - `ESP32 NODEMCU 32S`
  - `ESP32_NODEMCU_32S`
  - `USB`
- Fileira de pinos 1:
  - `GND`
  - `3V3`
  - `23`
  - `22`
  - `1`
  - `3`
  - `21`
  - `19`
  - `18`
  - `5`
  - `17`
  - `16`
  - `4`
  - `2`
  - `15`
- Fileira de pinos 2:
  - `EN`
  - `36`
  - `39`
  - `34`
  - `35`
  - `32`
  - `33`
  - `25`
  - `26`
  - `27`
  - `14`
  - `12`
  - `13`
  - `GND`
  - `Vin`
- Observacao: este encaixe aceita placas compativeis com ESP32 NodeMCU 32S.

## 1.4 GPIOs Digitais E Analogicas

### GPIOs Digitais

- Componente: `HDR-M-2.54-Preto-2X11`.
- Tipo: conector macho 2x11.
- Cor: preto.
- Face da PCB: superior.
- Legendas associadas:
  - `GPIO Digitais`
  - `DIGITAL`
- Pinos/legendas da esquerda:
  - `EN`
  - `P00`
  - `RX0`
  - `P04`
  - `P12`
  - `P14`
  - `P16`
  - `P18`
  - `P21`
  - `P23`
  - `P26`
- Pinos/legendas da direita:
  - `GND`
  - `TX0`
  - `P02`
  - `P05`
  - `P13`
  - `P15`
  - `P17`
  - `P19`
  - `P22`
  - `P25`
  - `P27`

### GPIOs Analogicas

- Componente: `HDR-M-2.54-Preto-2X3`.
- Tipo: conector macho 2x3.
- Cor: preto.
- Face da PCB: superior.
- Legenda associada: `ANALOG`.
- Pinos/legendas da esquerda:
  - `P32`
  - `P34`
  - `P36`
- Pinos/legendas da direita:
  - `P33`
  - `P35`
  - `P39`

## 1.5 Fontes Auxiliares

### Fonte +5V

- Componente: `HDR-M-2.54-Amarelo-1X4`.
- Tipo: conector macho 1x4.
- Cor: amarelo.
- Face da PCB: superior.
- Legenda associada: `+5V`.
- Pinos: quatro pinos `+5V`.
- Funcao: distribuicao de alimentacao 5 V.

### Fonte +3V3

- Componente: `HDR-M-2.54-Vermelho-1X4`.
- Tipo: conector macho 1x4.
- Cor: vermelho.
- Face da PCB: superior.
- Legenda associada: `+3V3`.
- Pinos: quatro pinos `+3V3`.
- Funcao: distribuicao de alimentacao 3,3 V.

### GND

- Componente: `HDR-M-2.54-Preto-1X4`.
- Tipo: conector macho 1x4.
- Cor: preto.
- Face da PCB: superior.
- Legenda associada: `GND`.
- Pinos: quatro pinos `GND`.
- Funcao: distribuicao de terra/GND.

## 1.6 Jumpers Vermelhos De Alimentacao Onboard

Os jumpers vermelhos ligam ou desligam a tensao de 3,3 V de determinados conectores ou circuitos onboard da ES32Lab.

### Jumper 3V3/BLK

- Componente: `HDR-M-2.54-Vermelho-1X2`.
- Tipo: conector macho 1x2.
- Cor: vermelho.
- Face da PCB: superior.
- Legenda associada: `3V3/BLK`.
- Pinos:
  - `3V3`
  - `BLK`
- Funcao: alimentacao/luz do display TFT.

### Jumper RTC/3V3

- Componente: `HDR-M-2.54-Vermelho-1X2`.
- Tipo: conector macho 1x2.
- Cor: vermelho.
- Face da PCB: superior.
- Legenda associada: `RTC/3V3`.
- Pinos:
  - `RTC`
  - `3V3`
- Funcao: liga/desliga a alimentacao 3,3 V do conector RTC superior e dos conectores RTC inferiores.

### Jumper 3V3/EXP

- Componente: `HDR-M-2.54-Vermelho-1X2`.
- Tipo: conector macho 1x2.
- Cor: vermelho.
- Face da PCB: superior.
- Legenda associada: `3V3/EXP`.
- Pinos:
  - `3V3`
  - `EXP`
- Funcao: liga/desliga a alimentacao 3,3 V do expansor de GPIOs onboard.

## 1.7 Jumpers Verdes De Sinais Onboard

Os jumpers verdes conectam circuitos onboard da ES32Lab a GPIOs do ESP32. Se o usuario precisar da GPIO para outra aplicacao, pode remover o jumper correspondente.

### Jumper P34/VOLT

- Componente: `HDR-M-2.54-Verde-1X2`.
- Tipo: conector macho 1x2.
- Cor: verde.
- Face da PCB: superior.
- Legenda associada: `P34/VOLT`.
- Pinos:
  - `P34`
  - `VOLT`
- Funcao: conecta `P34` ao sensor de tensao onboard.

### Jumper P33/KEY

- Componente: `HDR-M-2.54-Verde-1X2`.
- Tipo: conector macho 1x2.
- Cor: verde.
- Face da PCB: superior.
- Legenda associada: `P33/KEY`.
- Pinos:
  - `P33`
  - `KEY`
- Funcao: conecta `P33` ao teclado analogico.

### Jumper BUZZER/P25

- Componente: `HDR-M-2.54-Verde-1X2`.
- Tipo: conector macho 1x2.
- Cor: verde.
- Face da PCB: superior.
- Legenda associada: `BUZZER/P25`.
- Pinos:
  - `BUZZER`
  - `P25`
- Funcao: conecta o buzzer a `P25`.

## 1.8 Jumpers Azuis De Selecao Analogica

Os jumpers azuis selecionam qual circuito onboard compartilha uma determinada GPIO analogica do ESP32. Se a GPIO for necessaria para outra aplicacao, o jumper pode ser removido.

### Jumper POT1/P36/LDR

- Componente: `HDR-M-2.54-Azul-1X3`.
- Tipo: conector macho 1x3.
- Cor: azul.
- Face da PCB: superior.
- Legenda associada: `POT1/P36/LDR`.
- Pinos:
  - `POT1`
  - `P36`
  - `LDR`
- Funcao: seleciona o uso de `P36` entre potenciometro 1 e LDR.

### Jumper POT2/P39/THER

- Componente: `HDR-M-2.54-Azul-1X3`.
- Tipo: conector macho 1x3.
- Cor: azul.
- Face da PCB: superior.
- Legenda associada: `POT2/P39/THER`.
- Pinos:
  - `POT2`
  - `P39`
  - `THER`
- Funcao: seleciona o uso de `P39` entre potenciometro 2 e sensor de temperatura analogico.

## 1.9 Jumpers Brancos Do Expansor

Os jumpers brancos conectam a expansao de GPIOs I2C onboard a outros circuitos onboard da ES32Lab. Se alguma GPIO da expansao for necessaria para outra aplicacao, o jumper correspondente pode ser removido.

### Jumper EX0/WHI

- Componente: `HDR-M-2.54-Branco-1X2`.
- Tipo: conector macho 1x2.
- Cor: branco.
- Face da PCB: superior.
- Legenda associada: `EX0/WHI`.
- Pinos:
  - `EX0`
  - `WHI`
- Funcao: conecta `EX0` ao LED branco.
- Observacao: por padrao, esse jumper pode ficar desconectado para evitar acionamento visual indesejado quando `EX0` nao estiver sendo usado no codigo.

### Jumper EX1/ORA

- Componente: `HDR-M-2.54-Branco-1X2`.
- Tipo: conector macho 1x2.
- Cor: branco.
- Face da PCB: superior.
- Legenda associada: `EX1/ORA`.
- Pinos:
  - `EX1`
  - `ORA`
- Funcao: conecta `EX1` ao LED laranja.
- Observacao: por padrao, esse jumper pode ficar desconectado para evitar acionamento visual indesejado quando `EX1` nao estiver sendo usado no codigo.

## 1.10 Jumpers Pretos E Enderecamento

Os jumpers pretos fazem ajustes especificos em circuitos onboard da ES32Lab.

### Jumper PWR/VOLT

- Componente: `HDR-M-2.54-Preto-1X2`.
- Tipo: conector macho 1x2.
- Cor: preto.
- Face da PCB: superior.
- Legenda associada: `PWR/VOLT`.
- Pinos:
  - `PWR`
  - `VOLT`
- Funcao: interliga a tensao de entrada ao sensor onboard de tensao.

### Jumper SCK/R10K

- Componente: `HDR-M-2.54-Preto-1X2`.
- Tipo: conector macho 1x2.
- Cor: preto.
- Face da PCB: superior.
- Legenda associada: `SCK/R10K`.
- Pinos:
  - `SCK`
  - `R10K`
- Funcao: acoplamento de pull-up ao pino `SCK` da expansao I2S.

### Jumper ADD

- Componentes: `HDR-M-2.54-Preto-1X3` e `HDR-M-2.54-Preto-2X3`.
- Tipo: conectores macho equivalentes a um conjunto 3x3.
- Cor: preto.
- Face da PCB: superior.
- Legendas associadas:
  - `ADD`
  - `Mudar Endereco`
- Funcao: alteracao/configuracao de endereco I2C do expansor onboard.

Estrutura:

| Coluna | Pinos |
|---|---|
| Esquerda | `3V3`, `3V3`, `3V3` |
| Central | `A2`, `A1`, `A0` |
| Direita | `GND`, `GND`, `GND` |

Configuracoes de endereco I2C do expansor:

| Endereco | A2 | A1 | A0 |
|---|---|---|---|
| `0x20` | `GND` | `GND` | `GND` |
| `0x21` | `GND` | `GND` | `3V3` |
| `0x22` | `GND` | `3V3` | `GND` |
| `0x23` | `GND` | `3V3` | `3V3` |
| `0x24` | `3V3` | `GND` | `GND` |
| `0x25` | `3V3` | `GND` | `3V3` |
| `0x26` | `3V3` | `3V3` | `GND` |
| `0x27` | `3V3` | `3V3` | `3V3` |

## 1.11 Expansor I2C Onboard

### EXPANDER

- Componente: `HDR-M-2.54-Preto-1X9`.
- Tipo: conector macho 1x9.
- Cor: preto.
- Face da PCB: superior.
- Legenda associada: `EXPANDER`.
- Pinos:
  - `INT`
  - `EX0`
  - `EX1`
  - `EX2`
  - `EX3`
  - `EX4`
  - `EX5`
  - `EX6`
  - `EX7`
- Funcao: expansao de GPIOs extras por I2C.

## 1.12 Conexao I2C Superior

### I2C

- Componente: `HDR-F-2.54_1X4`.
- Tipo: conector femea 1x4.
- Cor: preto.
- Face da PCB: superior.
- Legenda associada: `I2C`.
- Pinos:
  - `3V3`
  - `GND`
  - `SCL`
  - `SDA`
- Funcao: conexao de perifericos I2C externos.

## 1.13 RTC Superior

### RTC

- Componente: `HDR-F-2.54_1X6`.
- Tipo: conector femea 1x6.
- Cor: preto.
- Face da PCB: superior.
- Legenda associada: `RTC`.
- Pinos:
  - `32K`
  - `SQW`
  - `SCL`
  - `SDA`
  - `VCC`: 3,3 V.
  - `GND`
- Observacao: idealizado inicialmente para modulo RTC, mas pode ser usado por outros modulos I2C conforme a necessidade do projeto.

## 1.14 Display TFT E SPI

### Display TFT 1.8 SPI 128x160 SD

- Componentes: `HDR-F-2.54_1X8` e `HDR-F-2.54_1X4`.
- Tipo: conectores femea 1x8 e 1x4.
- Cor: preto.
- Face da PCB: superior.
- Legenda associada: `Display TFT 1.8 128x160`.
- Pinos do conector 1x8:
  - `3V3`
  - `GND`
  - `CS/P15`
  - `RST`
  - `A0/P02`
  - `DA/P23`
  - `CL/P18`
  - `LED`
- Pinos do conector 1x4:
  - `CS/P05`
  - `MOSI/P23`
  - `MISO/P19`
  - `SCK/P18`
- Funcao: sinais SPI associados ao display TFT e ao cartao SD.

### Display TFT SPI ST7735

- Componente: `HDR-F-2.54_1X8`.
- Tipo: conector femea 1x8.
- Cor: preto.
- Face da PCB: superior.
- Legenda associada: `TFT_SPI_ST7735`.
- Pinos:
  - `BLK`
  - `CS/P15`
  - `DC/P02`
  - `RST`
  - `SDA/P23`
  - `SCL/P18`
  - `3V3`
  - `GND`
- Funcao: conexao do display TFT SPI ST7735.

## 1.15 Camera

### CAM-OV2640

- Componente: `HDR-F-2.54_2x9`.
- Tipo: conector femea 2x9.
- Cor: preto.
- Face da PCB: superior.
- Legenda associada: `CAM-OV2640`.
- Fileira da esquerda:
  - `3V3`
  - `P13/VSY`
  - `P32/HRE`
  - `RST`
  - `P12/D1`
  - `P16/D3`
  - `P39/D5`
  - `P35/D7`
  - `NC`
- Fileira da direita:
  - `GND`
  - `SCL/P22`
  - `SDA/P21`
  - `D0/P04`
  - `D2/P14`
  - `D4/P36`
  - `D6/P34`
  - `DCLK/P17`
  - `PWDN`

## 1.16 I2S Superior

### I2S

- Componente: `HDR-F-2.54_1X6`.
- Tipo: conector femea 1x6.
- Cor: preto.
- Face da PCB: superior.
- Legenda associada: `I2S`.
- Pinos:
  - `+5V`
  - `GND`
  - `P26/LCK`
  - `P25/DIN`
  - `P27/BCK`
  - `SCK`
- Funcao: expansao I2S.

## 1.17 Audio P2

### Conector P2 Audio

- Componente: `PJ-327D-5A`.
- Tipo: conector P2 de audio.
- Cor: preto.
- Face da PCB: superior.
- Legenda associada: `DAC-P25/P26`.
- Pinos/sinais associados:
  - `P25`
  - `P26`
- Funcao: saida de audio usando DAC nativo do ESP32.

# 2. Face Inferior Da PCB

## 2.1 Versao E Legendas Institucionais

### Identificacao Da Placa

- Face da PCB: inferior.
- Legenda: `Version: 1.5.20`.

## 2.2 I2S Inferior - GY-PCM5102

### I2S-GY-PCM5102

- Componente: `HDR-F-2.54_1X6`.
- Tipo: conector femea 1x6.
- Cor: preto.
- Face da PCB: inferior.
- Legenda associada: `I2S-GY-PCM5102`.
- Pinos:
  - `+5V`
  - `GND`
  - `P26/LCK`
  - `P25/DIN`
  - `P27/BCK`
  - `SCK`
- Funcao: conexao de modulo I2S GY-PCM5102 ou shields inferiores da ES Developer que usem alimentacao, sinais I2S ou GPIOs compartilhadas por esse conector.

## 2.3 PWR_ON Inferior

### PWR_ON

- Componente: `HDR-F-2.54_2X2`.
- Tipo: conector femea 2x2.
- Cor: preto.
- Face da PCB: inferior.
- Legenda associada: `PWR_ON`.
- Pinos:
  - direita: `GND`, `GND`.
  - esquerda: `ON_9V`, `ON_9V`.
- Observacao: os pinos `GND` se repetem na vertical e os pinos `ON_9V` tambem se repetem na vertical.
- Observacao adicional: `ON_9V` indica a alimentacao principal da ES32Lab apos o botao `POWER` ser acionado. O valor pode variar conforme fonte externa ou baterias. Shields inferiores da ES Developer podem usar esse conector para compartilhamento de alimentacao.

## 2.4 RTC Inferior

### RTC-DS3231 - Conector 1x6

- Componente: `HDR-F-2.54_1X6`.
- Tipo: conector femea 1x6.
- Cor: preto.
- Face da PCB: inferior.
- Legenda associada: `RTC-DS3231`.
- Pinos:
  - `32K`
  - `SQW`
  - `SCL`
  - `SDA`
  - `VCC`: 3,3 V, condicionado ao jumper `RTC/3V3`.
  - `GND`
- Funcao: conexao inferior para modulo RTC DS3231 e shields inferiores da ES Developer que usem alimentacao ou barramento I2C.

### RTC_DS3231 - Conector 1x4

- Componente: `HDR-F-2.54_1X4`.
- Tipo: conector femea 1x4.
- Cor: preto.
- Face da PCB: inferior.
- Legenda associada: `RTC_DS3231`.
- Pinos:
  - `SCL`
  - `SDA`
  - `VCC`: 3,3 V, condicionado ao jumper `RTC/3V3`.
  - `GND`
- Funcao: conexao inferior para modulo RTC DS3231 e shields inferiores da ES Developer que usem alimentacao ou barramento I2C.

## 2.5 Shields Inferiores Da ES Developer

A ES Developer possui shields projetadas para conectar abaixo da ES32Lab. Essas shields podem usar todos os conectores da face inferior para manter compatibilidade mecanica, eletrica e funcional.

As shields inferiores podem compartilhar:

- alimentacao principal pelo conector `PWR_ON`;
- alimentacao de 3,3 V e barramento I2C pelos conectores RTC inferiores;
- sinais I2S e GPIOs compartilhadas pelo conector `I2S-GY-PCM5102`;
- GND comum entre placa e shield.

Regra para a IA:

- nao assumir que uma shield inferior usa apenas um conector;
- nao gerar codigo definitivo para uma shield inferior sem documentacao especifica da shield;
- quando o usuario perguntar por uma shield inferior ainda nao catalogada, explicar que a ES Developer possui shields inferiores e pedir a documentacao ou o modelo da shield;
- quando a documentacao da shield estiver disponivel, cruzar a pinagem da shield com este arquivo.
