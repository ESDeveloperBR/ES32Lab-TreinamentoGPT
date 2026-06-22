# ES32Lab GPT - Defaults E Boas Praticas

Versao do conhecimento: `0.9.0`
Atualizado em: `2026-06-20`
Resumo da versao: acompanha a inclusao da Shield 4IN-4Relay Optoacoplada e mantem defaults tecnicos da ES32Lab.

Este arquivo concentra ajustes finos de uso da placa ES32Lab e da LIB ES32Lab.

Use este arquivo para registrar padroes praticos que nao sao exatamente assinaturas de metodos, mas que devem orientar a IA ao gerar exemplos, aulas e respostas tecnicas.

## Como Manter Este Arquivo

Use este arquivo quando a informacao responder a pergunta:

> Qual e o jeito correto, recomendado ou padrao de usar este recurso na ES32Lab?

Exemplos de informacoes que pertencem a este arquivo:

- orientacao padrao do display;
- resolucao fisica do display;
- pinos preferenciais da placa;
- parametros recomendados para exemplos;
- ordem correta de inicializacao;
- cuidados praticos descobertos em testes reais.

Nao use este arquivo para listar todos os metodos de uma classe. Assinaturas de metodos pertencem ao `API_Catalog.json`.

## Mapa De Substituicao Por Classes ES32Lab

Quando a IA gerar codigo para a ES32Lab, deve consultar este mapa para escolher a abstracao oficial da biblioteca antes de usar APIs nativas.

| Necessidade | Evitar por padrao | Usar por padrao |
|---|---|---|
| Intervalos de tempo | `millis()` ou `micros()` com variaveis manuais | `ES_TimeInterval` |
| Cronometro | calculos manuais com `millis()` ou `micros()` | `ES_TimeInterval` |
| Botao digital | `digitalRead()` com flags manuais | `ES_DigitalButton` |
| Buzzer | `tone()`, `ledcWriteTone()` ou PWM manual | `ES_Buzzer` |
| Expansor PCF8574 | `Wire` direto | `ES_PCF8574` |
| Carro, robo movel ou ponte H | comandos manuais nos pinos da ponte H | `ES_CarControl` |
| Robo seguidor de linha | logica solta no sketch principal | `ES_CarLineFollower` |
| Display TFT da ES32Lab | `TFT_eSPI` cru quando `ES_TFT` resolver | `ES_TFT` |
| Camera | `esp_camera` cru quando `ES_Camera` resolver | `ES_Camera` |
| Arquivos | `File` manual para operacoes comuns | `ES_File` |
| Teclado analogico | leitura analogica manual do teclado | `ES_AnalogKeyboard` |

Excecoes permitidas:

- quando a LIB ES32Lab nao tiver classe para o recurso solicitado;
- quando a API nativa for necessaria para inicializar ou conectar uma dependencia externa;
- quando o usuario pedir explicitamente uma implementacao manual;
- quando a classe existente nao atender ao comportamento solicitado.

Mesmo nas excecoes, a IA deve continuar usando classes ES32Lab para as partes do projeto cobertas pela biblioteca.

## Hardware Da ES32Lab

Para detalhes completos de conectores, legendas impressas, face superior, face inferior, jumpers e pinagem fisica da placa, consultar `ES32Lab_Board_Connectors_Legends_v1.5.20.md`.

### Compatibilidade Com Shields ESP32

A ES32Lab foi projetada para aceitar modelos comuns de shields ESP32 de 30 e 38 pinos.

Modelos citados como referencia:

- DEVKit32S de 30 pinos;
- ESP32-WROOM-32U de 38 pinos;
- ESP32-WROOM-32D de 38 pinos;
- NodeMCU32S de 38 pinos.

Antes de orientar uma ligacao fisica, a IA deve lembrar que o usuario precisa comparar as legendas dos pinos da shield ESP32 com as legendas da ES32Lab. Se a shield nao for compativel com a pinagem da placa, ela nao deve ser conectada.

### Alimentacao

A ES32Lab pode ser alimentada por:

- USB do proprio ESP32;
- fonte externa de ate 9 V pelo borne vermelho;
- conector DC, com positivo no pino central;
- baterias pelo borne verde.

Regras de seguranca:

- nao recomendar alimentar motores ou cargas de alto consumo apenas pela USB do computador;
- quando houver motores, ponte H ou cargas externas, recomendar fonte externa ou baterias adequadas;
- a alimentacao externa da ES32Lab nao deve ultrapassar 9 V;
- o borne verde trabalha com controlador de carga e descarga para duas baterias de ion-litio de 4,2 V;
- apos trocar baterias sem fonte externa conectada, pode ser necessario pressionar o botao `BAT RESET`.

### LEDs De Status Da Alimentacao

- LED azul: ES32Lab ligada e alimentada pelas baterias.
- LED verde: ES32Lab ligada com baterias carregadas ou ligada sem baterias instaladas.
- LED vermelho: ES32Lab recebendo alimentacao externa e carregando as baterias, quando instaladas.

### Fontes Auxiliares Da Placa

- Pinos vermelhos: fonte de 3,3 V.
- Pinos amarelos: fonte de 5 V.
- Pinos pretos: GND.

### Legendas Oficiais Da Placa

As legendas oficiais usadas em codigo seguem o arquivo `ES32Lab.h` e usam sublinhado para associar GPIO e cor.

Exemplos:

```cpp
P17_G // LED verde ligado a GPIO 17.
P16_Y // LED amarelo ligado a GPIO 16.
P13_R // LED vermelho ligado a GPIO 13.
P12_B // LED azul ligado a GPIO 12.
```

Nao usar hifen em codigo, como `P17-G`. A forma correta para codigo e `P17_G`.

Quando explicar a serigrafia da placa, a IA pode dizer que `P17_G` representa a GPIO 17 associada ao LED green/verde.

### Circuitos Onboard

A ES32Lab possui, entre outros recursos:

- 6 LEDs;
- 2 potenciometros;
- sensor LDR;
- sensor de temperatura analogico;
- teclado analogico com 5 teclas;
- sensor de tensao DC;
- buzzer;
- conector P2 para audio pela DAC nativa do ESP32;
- leitor de cartao microSD;
- conector para display SPI TFT;
- conexao para RTC fisico I2C;
- conector I2C;
- ponte H para dois motores DC;
- expansao de 8 GPIOs extras por I2C;
- conector para expansao I2S;
- conector para camera de video OV2640.

### Cores Dos Jumpers

Jumpers vermelhos:

- alimentam circuitos onboard;
- exemplos: alimentacao do display TFT, alimentacao da shield RTC e alimentacao da expansao I2C;
- seguem a logica da fonte de 3,3 V.

Jumpers verdes:

- interligam circuitos onboard as GPIOs nativas do ESP32;
- exemplos: buzzer na GPIO 25, teclado na GPIO 33 e sensor de tensao na GPIO 34;
- se o usuario precisar da GPIO para outra aplicacao, pode remover o jumper correspondente.

Jumpers azuis:

- indicam possibilidade de escolha entre dois circuitos onboard conectados a uma mesma GPIO;
- GPIO 36 pode ser usada com `POT1` ou sensor LDR;
- GPIO 39 pode ser usada com `POT2` ou sensor analogico de temperatura.

Jumpers brancos:

- conectam alguns circuitos onboard a expansao de GPIOs por I2C;
- permitem ligar LEDs e a ponte H ao expansor I2C onboard;
- `EX0` pode ser usado com LED branco;
- `EX1` pode ser usado com LED laranja;
- a ponte H pode ser conectada ao expansor I2C pelos jumpers brancos.

Mapa pratico do expansor I2C onboard:

| Pino | Uso padrao ou recomendado |
|---|---|
| `EX0` | LED branco pelo jumper branco |
| `EX1` | LED laranja pelo jumper branco |
| `EX2` | Livre; recomendado para sensor de linha esquerdo ou expansao geral |
| `EX3` | Livre; recomendado para sensor de linha direito ou expansao geral |
| `EX4` | Ponte H: `M1A`, motor de indice `0` |
| `EX5` | Ponte H: `M1B`, motor de indice `0` |
| `EX6` | Ponte H: `M2A`, motor de indice `1` |
| `EX7` | Ponte H: `M2B`, motor de indice `1` |

Quando os jumpers brancos da ponte H estiverem conectados, considerar `EX4`, `EX5`, `EX6` e `EX7` ocupados pelo controle dos motores. Para sensores de linha e duas GPIOs livres no expansor, sugerir `EX2` e `EX3`.

Jumpers pretos:

- fazem ajustes especificos em alguns circuitos onboard;
- exemplos: interligacao da tensao de entrada ao sensor onboard de tensao, configuracao de endereco I2C do expansor e acoplamento de pull-up ao pino SCK da expansao I2S.

### Tamanho Fisico

A ES32Lab possui tamanho compacto de aproximadamente 10 x 10 cm.

Quando pertinente, a IA pode mencionar que esse tamanho facilita acomodar a placa em caixas simples de passagem usadas em instalacoes eletricas.

## Shield 4IN-4Relay Optoacoplada

Para projetos com reles, entradas optoacopladas, atuadores, irrigacao, piscina de ondas, automacao com cargas AC/DC ou alimentacao DC acima do limite direto da ES32Lab, priorizar a Shield 4IN-4Relay Optoacoplada oficial da ES Developer quando ela atender ao projeto.

Defaults praticos:

- usar `ES_PCF8574` para controlar a shield;
- endereco padrao: `0x27`, com `i2C ADD` em `ON ON ON`;
- em caso de falha de comunicacao, recomendar conferir o `i2C ADD` e usar `scanI2C()`;
- `EX0` a `EX3`: entradas optoacopladas;
- `EX4` a `EX7`: reles;
- reles acionam com `LOW` e desligam com `HIGH`;
- a entrada `DC IN` da shield aceita `5 a 30 V DC`, mas isso nao altera o limite de alimentacao direta da ES32Lab;
- a shield possui suporte para trilho DIN removivel;
- ao falar de cargas AC, altas correntes ou instalacoes em paineis, incluir alerta de seguranca e recomendar profissional qualificado.

## ES_TFT - Display TFT Da ES32Lab

### Resolucao Padrao

O display TFT padrao da ES32Lab possui:

- largura: 160 pixels;
- altura: 128 pixels.

Em exemplos oficiais, a IA deve considerar essa resolucao como referencia para posicionamento de textos, imagens, menus e interfaces simples.

### Rotacao Padrao

Para que o display fique na orientacao correta nos exemplos oficiais da ES32Lab, usar:

```cpp
display.setRotation(3);
```

Esse deve ser o valor padrao quando o usuario nao solicitar outra orientacao.

### Mapa De Rotacao

```cpp
display.setRotation(0); // Tela na vertical em pe.
display.setRotation(1); // Tela na horizontal de ponta cabeca.
display.setRotation(2); // Tela na vertical de ponta cabeca.
display.setRotation(3); // Tela na horizontal na posicao correta. Valor padrao recomendado.
```

### Inicializacao Recomendada

Ao gerar exemplos com `ES_TFT`, a IA deve preferir esta sequencia:

```cpp
ES_TFT display;

void setup() {
  display.init();          // Inicializa o display TFT.
  display.setRotation(3);  // Ajusta o display para a orientacao correta da ES32Lab.
  display.fillScreen(TFT_BLACK); // Limpa a tela antes de desenhar.
}
```

### Posicionamento Em Tela

Ao desenhar interfaces simples, considerar:

- area util em orientacao padrao: 160 x 128 pixels;
- eixo X: 0 a 159;
- eixo Y: 0 a 127.

Textos longos devem ser quebrados em linhas curtas para caber no display.

### JPEG E Imagens

Quando usar `renderJPEG()` com `fitToScreen = true`, a IA deve avisar:

- o redimensionamento automatico pode deixar a renderizacao mais lenta;
- a qualidade visual pode ser inferior a uma imagem preparada previamente;
- quando desempenho for importante, o ideal e usar imagem ja redimensionada para 160 x 128 pixels.

## ES_TimeInterval - Temporizacao

Para exemplos didaticos com LEDs, botoes e leituras recorrentes, preferir `ES_TimeInterval` em vez de `delay()`.

Use `delay()` apenas em exemplos extremamente simples ou quando o bloqueio do loop nao causar problema didatico.

## LEDs Da ES32Lab

Quando o usuario pedir exemplos de LED, priorizar o LED verde por ser simples e visualmente direto.

Constantes recomendadas:

```cpp
P17_G
P_LED_GREEN
```

Para exemplos didaticos que explicam a marcacao fisica da placa, preferir `P17_G`.

Para exemplos que explicam o recurso da placa, preferir `P_LED_GREEN`.

## ES_DigitalButton - Botoes Digitais

Para exemplos com botao digital, usar `begin(pin, activeHigh)` no `setup()`.

Se o usuario nao especificar circuito externo, explicar que:

- `activeHigh = true` considera o botao ativo em HIGH;
- `activeHigh = false` considera o botao ativo em LOW;
- algumas GPIOs podem nao aceitar pull-up ou pull-down interno;
- quando necessario, o usuario deve usar resistor fisico externo.

## ES_PCF8574 - Expansor I2C

Endereco padrao usado nos exemplos:

```cpp
ES_PCF8574 expander(0x20);
```

Quando usar sensores, LEDs, botoes ou motores no expansor, preferir as constantes:

```cpp
EX0, EX1, EX2, EX3, EX4, EX5, EX6, EX7
```

Para sensores de robo seguidor de linha e para demandas que precisem de duas GPIOs livres no expansor I2C, sugerir `EX2` e `EX3` por padrao. Essas GPIOs sao recomendadas pela ES Developer porque, na pratica, ficam entre as poucas portas do expansor que nao sao usadas por circuitos onboard comuns da ES32Lab.

Quando o usuario relatar falha em periferico I2C, sensor I2C, expansor, ponte H ou shield I2C, recomendar o uso de `scanI2C()` para conferir se o dispositivo aparece no barramento e qual endereco esta respondendo.

Para perifericos externos, sensores e shields validados, consultar `Validated_Hardware_Catalog.md`.

## ES_Buzzer - Notas Musicais

Ao gerar melodias com `ES_Buzzer`, a IA deve usar as constantes musicais definidas em `ES_BuzzerNote.h`.

Padrao recomendado:

```cpp
buzzer.sound(NOTE_C4, 300);
buzzer.sound(NOTE_D4, 300);
buzzer.sound(NOTE_E4, 300);
```

Evitar em exemplos didaticos:

```cpp
buzzer.sound(262, 300);
buzzer.sound(294, 300);
buzzer.sound(330, 300);
```

As constantes devem permanecer no padrao internacional ja usado pela biblioteca:

```cpp
NOTE_C4
NOTE_CS4
NOTE_D4
NOTE_DS4
NOTE_E4
NOTE_F4
NOTE_FS4
NOTE_G4
NOTE_GS4
NOTE_A4
NOTE_AS4
NOTE_B4
```

Nao criar ou sugerir constantes alternativas em portugues, como `NOTE_DO`, `NOTE_RE`, `NOTE_MI` ou similares.

Quando o usuario pedir uma melodia simples sem especificar oitava, usar a oitava 4 como referencia didatica inicial.

## ES_CarControl - Controle De Carro

Para novos exemplos, usar o construtor por referencia:

```cpp
ES_PCF8574 expander(0x20);
ES_CarControl car(expander);
```

Nao usar o construtor com ponteiro em exemplos novos, pois ele sera descontinuado.

Quando o usuario pedir qualquer programa envolvendo motores, carro, robo movel, veiculo, ponte H ou direcao diferencial, usar `ES_CarControl` por padrao.

### Ligacao Padrao Da Ponte H

Os motores devem ser ligados aos bornes azuis da ponte H onboard da ES32Lab.

A ponte H onboard e controlada pelo expansor I2C onboard (`ES_PCF8574`) por meio dos jumpers brancos da propria ES32Lab.

Endereco padrao do expansor:

```cpp
ES_PCF8574 expander(0x20);
```

Pinos padrao do expansor para direcao diferencial:

```cpp
// Motor de indice 0
EX4
EX5

// Motor de indice 1
EX6
EX7
```

Na pratica, para um carro de direcao diferencial, a IA deve gerar:

```cpp
ES_PCF8574 expander(0x20);
ES_CarControl car(expander);

void setup() {
  car.begin(DIFFERENTIAL);
}
```

O metodo `car.begin(DIFFERENTIAL);` ja utiliza os pinos padrao da ponte H, portanto a IA nao precisa passar `EX4`, `EX5`, `EX6` e `EX7` manualmente, salvo quando o usuario pedir uma ligacao personalizada.

Video oficial sobre a ligacao dos jumpers brancos:

https://www.youtube.com/watch?v=xpoNbSA8pPM&list=PLpVVewmHgD_LDEXAvsAxDWjS-3XCfZlZi&index=18&t=383s

### Legenda Antiga MOTOR1/MOTOR2

Em placas ES32Lab abaixo da versao `1.5.20`, a legenda impressa nos bornes da ponte H pode aparecer como `MOTOR1` e `MOTOR2`.

Essa legenda antiga pode confundir, porque o codigo usa indices iniciando em zero:

- o borne impresso como `MOTOR1` corresponde ao motor de indice `0` no codigo;
- o borne impresso como `MOTOR2` corresponde ao motor de indice `1` no codigo.

Portanto, se o primeiro motor fisico estiver invertido, usar:

```cpp
car.invertMotorCommands(0);
```

Se o segundo motor fisico estiver invertido, usar:

```cpp
car.invertMotorCommands(1);
```

Nao orientar o usuario a usar `car.invertMotorCommands(1)` para inverter o primeiro motor fisico apenas porque a placa antiga esta escrita como `MOTOR1`.

A partir da versao `1.5.20`, a documentacao fisica da placa deve ser tratada como a referencia corrigida para as legendas dos motores. Para detalhes de conectores e legendas dessa versao, consultar `ES32Lab_Board_Connectors_Legends_v1.5.20.md`.

Sempre que gerar exemplos com motores, incluir aviso de alimentacao externa e limite de corrente da ponte H.

## ES_CarLineFollower - Seguidor De Linha

Para exemplos novos, usar:

```cpp
ES_PCF8574 expander(0x20);
ES_CarControl car(expander);
ES_CarLineFollower lineFollower(car, expander);
```

Padrao didatico de sensores em exemplos recentes:

```cpp
lineFollower.begin(EX2, EX3);
```

`EX2` deve ser sugerido para o sensor esquerdo e `EX3` para o sensor direito, salvo quando o usuario informar uma ligacao fisica diferente.

Quando o usuario estiver ajustando desempenho real do robo, orientar ajustes graduais de:

- `highSpeed`;
- `lowSpeed`;
- `lowSpeedDuration`;
- `noLineDuration`;
- `turnSpeed`.

## ES_Camera

Para exemplos iniciais com camera, preferir resolucoes menores antes de demonstrar stream ou salvamento em SD.

Quando combinar camera e display, usar `ES_TFT` e lembrar da orientacao padrao:

```cpp
display.setRotation(3);
```

## ES_File

Quando o usuario pedir manipulacao de arquivos, sempre confirmar ou deixar claro o sistema usado:

- SD;
- SPIFFS;
- LittleFS.

Preferir exemplos com SD quando o objetivo envolver fotos, imagens JPEG ou arquivos grandes.

## Manutencao Dos Ajustes Finos

Ao descobrir um novo comportamento real da placa, cadastrar aqui em uma secao da classe ou recurso correspondente.

Formato recomendado:

````md
## Nome Do Recurso

### Situacao Ou Padrao

Explicacao objetiva.

```cpp
codigo_recomendado();
```

Quando a IA deve usar esse padrao.
````
