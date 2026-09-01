# ES32Lab GPT - Defaults E Boas Praticas

Versao do conhecimento: `0.13.2`
Atualizado em: `2026-09-01`
Resumo da versao: adiciona orientacoes praticas de Arduino IDE, instalacao, upload BOOT/EN e Monitor Serial.

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
| Sensor de distancia VL53L0X | biblioteca externa ou Wire direto | `ES_VL53L0X` |

Excecoes permitidas:

- quando a LIB ES32Lab nao tiver classe para o recurso solicitado;
- quando a API nativa for necessaria para inicializar ou conectar uma dependencia externa;
- quando o usuario pedir explicitamente uma implementacao manual;
- quando a classe existente nao atender ao comportamento solicitado.

Mesmo nas excecoes, a IA deve continuar usando classes ES32Lab para as partes do projeto cobertas pela biblioteca.

## Ambientes De Desenvolvimento

### Arduino IDE

Quando o usuario estiver usando Arduino IDE com o pacote `esp32 por Espressif Systems` versao `3.3.11` ou superior, orientar a selecao da placa oficial:

```text
ES Developer ES32Lab
```

Essa deve ser a recomendacao padrao para Arduino IDE. Nao recomendar `ESP32 Dev Module`, `NodeMCU-32S` ou equivalentes como primeira opcao quando a placa oficial estiver disponivel.

Use placas genericas apenas como compatibilidade para versoes antigas do pacote ESP32, ambientes temporarios, testes especificos ou quando o usuario ainda nao tiver acesso a definicao oficial.

Com a placa oficial selecionada, os aliases da variant sao fornecidos pelo proprio core Arduino-ESP32. A LIB ES32Lab continua compativel e deve evitar duplicar definicoes de GPIO quando detectar essa condicao.

Video tutorial oficial recomendado para iniciantes:

https://youtu.be/RfHCgr7BZb4

Ao orientar instalacao da Arduino IDE, usar como referencia publica principal a pagina oficial:

https://www.arduino.cc/en/software

O video demonstra a instalacao no Windows pela Microsoft Store, mas a pagina oficial da Arduino IDE tambem pode ser indicada como caminho geral de download.

Quando a resposta tratar da ferramenta de compilacao, configuracao e gravacao, usar a expressao `Arduino IDE`. Evitar dizer apenas `Arduino` quando o contexto for o software, pois isso pode confundir o usuario iniciante com uma placa Arduino.

Para instalar o suporte ao ESP32 na Arduino IDE 2.x:

1. Abrir o Gerenciador de Placas.
2. Pesquisar por `ESP32`.
3. Instalar `ESP32 by Espressif Systems`.
4. Usar a versao atual compativel sempre que possivel.

No fluxo basico atual da Arduino IDE 2.x, nao orientar a inclusao manual de URL JSON adicional apenas para instalar o pacote ESP32, salvo se o usuario estiver em um ambiente antigo ou pedir esse procedimento explicitamente.

Se a ES32Lab nao aparecer no seletor de placas:

1. Conferir se `ESP32 by Espressif Systems` esta instalado.
2. Conferir se o pacote esta atualizado.
3. Atualizar o pacote, se necessario.
4. Lembrar que a definicao oficial `ES Developer ES32Lab` esta disponivel a partir da versao `3.3.11`.

Depois de selecionar a placa correta, orientar tambem a selecao da porta COM correspondente a conexao USB usada pelo ESP32/ES32Lab. Nao inventar uma porta COM especifica, pois ela depende do computador do usuario.

Para instalar a biblioteca ES32Lab pela Arduino IDE:

1. Abrir o Gerenciador de Bibliotecas.
2. Pesquisar por `ES32Lab`.
3. Clicar em Instalar.
4. Quando a Arduino IDE solicitar dependencias necessarias, confirmar a instalacao.

Com a biblioteca instalada, os exemplos oficiais ficam em:

```text
Arquivo -> Exemplos -> ES32Lab
```

Para validar uma instalacao inicial, a IA pode sugerir abrir e compilar um exemplo oficial simples ou demonstrativo. O video usa `Games -> Space Invader` como exemplo de compilacao, mas isso nao deve transformar Space Invader no tema principal do tutorial.

Explique para iniciantes a diferenca entre os botoes principais:

- Verificar/compilar: compila o codigo sem gravar na placa.
- Enviar: compila e grava o programa na placa selecionada.

### Erro De Gravacao Com BOOT E EN

Quando o codigo compila, mas o ESP32 nao entra automaticamente em modo de gravacao/download, orientar o procedimento manual:

1. Manter `BOOT` pressionado.
2. Pressionar e soltar `EN`.
3. Aguardar aproximadamente 1 segundo.
4. Soltar `BOOT`.
5. Tentar enviar o programa novamente.
6. Depois da gravacao, pressionar `EN` para reiniciar a placa e executar o programa.

Dependendo da placa ESP32, `BOOT` pode aparecer como `IO0`, e `EN` pode aparecer como `RESET`, `RST` ou `ENABLE`. A posicao fisica dos botoes pode variar conforme fabricante e modelo.

Nao afirmar que todo erro de upload e resolvido com `BOOT + EN`. Esse procedimento e adequado para o caso comum em que o ESP32 nao entrou corretamente em modo de download. Para outros erros, pedir a mensagem completa da Arduino IDE e seguir o diagnostico.

### Monitor Serial E Baud Rate

Quando o Monitor Serial mostrar caracteres estranhos, ilegiveis ou dados baguncados, conferir primeiro se a velocidade do Monitor Serial e a mesma configurada no programa.

Exemplo comum:

- Programa com `Serial.begin(115200)`.
- Monitor Serial configurado em `9600`.

Nesse caso, ajustar o Monitor Serial para `115200` costuma corrigir a exibicao. Nao afirmar que todo problema de Monitor Serial e baud rate; se persistir, pedir o codigo, a configuracao usada e a saida exibida.

### PlatformIO / VS Code

No momento desta diretriz, a ES32Lab ainda nao possui definicao oficial no repositorio PlatformIO. Enquanto isso nao estiver disponivel, usar temporariamente `nodemcu-32s` como board de compatibilidade.

Configuracao padrao temporaria para projetos ES32Lab no PlatformIO:

```ini
[env:nodemcu-32s]
platform = espressif32
board = nodemcu-32s
framework = arduino

monitor_speed = 115200
lib_ldf_mode = deep+

lib_deps =
    esdeveloper/ES32Lab
    esdeveloper/TFT_eSPI_ES32Lab
```

Bibliotecas externas validadas ou necessarias ao projeto devem ser adicionadas abaixo das bibliotecas oficiais, sem substituir `esdeveloper/ES32Lab` nem `esdeveloper/TFT_eSPI_ES32Lab`.

Quando a ES32Lab entrar oficialmente no PlatformIO, esta secao deve ser atualizada para usar o board oficial.

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

## ES_AnalogKeyboard - Teclado Analogico

Para o teclado analogico onboard da ES32Lab, usar a classe `ES_AnalogKeyboard`.

Defaults praticos:

- pino padrao: `P_KEYBOARD`;
- GPIO fisica associada: GPIO 33;
- tolerancia padrao: `20%`, configurada no construtor;
- exemplo oficial de diagnostico: `examples/AnalogKeyboard/AnalogKeyboard-DebugRead/AnalogKeyboard-DebugRead.ino`.

Valores esperados das teclas individuais:

| Tecla | Valor esperado |
|---|---:|
| `KEY_CENTER` | `0` |
| `KEY_UP` | `769` |
| `KEY_RIGHT` | `1585` |
| `KEY_DOWN` | `2400` |
| `KEY_LEFT` | `3323` |

Quando o usuario relatar que o teclado nao funciona, a IA deve orientar diagnostico antes de reescrever a logica do codigo:

1. Rodar o exemplo oficial `AnalogKeyboard-DebugRead`.
2. Segurar cada tecla por pelo menos tres leituras.
3. Comparar `Min`, `Max` e `Media` com os valores esperados.
4. Se os valores aparecem mas ficam um pouco fora da faixa, testar uma tolerancia maior no construtor, como `25` ou `30`, com cuidado para nao sobrepor faixas entre teclas.
5. Se a leitura fica travada, sempre `0`, sempre `4095`, sem variacao ou com ruido extremo, verificar jumper verde do teclado, alimentacao, GND, GPIO `P_KEYBOARD`/GPIO 33 e testar outro ESP32.
6. Se outro ESP32 funcionar na mesma ES32Lab, tratar como forte indicio de problema na GPIO analogica do ESP32 original.

Exemplo de ajuste de tolerancia:

```cpp
ES_AnalogKeyboard keyboard(P_KEYBOARD, 25);
```

Teste em outro pino analogico so deve ser sugerido quando o usuario puder fazer a ligacao fisica por jumper de forma consciente. Nesse caso, usar um pino analogico valido e instanciar a classe com esse pino:

```cpp
ES_AnalogKeyboard keyboard(P32, 20);
```

Observacao importante: `KEY_CENTER` vale `0`, entao a tolerancia percentual nao cria uma faixa positiva ao redor de zero. Se a tecla central nao chegar perto de zero, priorizar diagnostico com `debugRead()` e verificacao fisica.

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

## ES_VL53L0X - Sensor De Distancia VL53L0X

Para sensores VL53L0X, usar a classe oficial `ES_VL53L0X`.

Defaults praticos:

- endereco I2C padrao: `0x29`;
- offset inicial recomendado para exemplos gerados: `50 mm`;
- barramento padrao: `Wire`;
- unidade de leitura: milimetros;
- valor invalido de leitura: `ES_VL53L0X_INVALID_DISTANCE` (`65535`);
- exemplo inicial: `examples/SensorDistance/SensorDistanceSimple/SensorDistanceSimple.ino`;
- exemplo com estabilidade/velocidade de leitura: `examples/SensorDistance/SensorDistanceTimingBudget/SensorDistanceTimingBudget.ino`.

Padrao recomendado:

```cpp
ES_VL53L0X distance;

void setup() {
  Serial.begin(115200);
  distance.setTimeout(500);
  distance.setDistanceOffset(50); // Calibracao inicial recomendada em mm.
  distance.begin(); // Usa o endereco padrao 0x29.
}
```

Para codigos gerados ao usuario com leitura recorrente, preferir `ES_TimeInterval` em vez de `delay()`. Usar `distance.setDistanceOffset(50)` como ponto de partida calibravel; se a montagem, lente, case ou sensor exigir outro valor, orientar o usuario a ajustar. Os exemplos oficiais didaticos podem manter pequenos `delay()` quando isso simplificar a leitura no Monitor Serial.

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


## Diagnostico De Versao Da LIB ES32Lab

Considere como versao corrente da biblioteca ES32Lab a `0.15.2`, com `ES32LAB_VERSION` retornando `0.15.2 update 24/06/2026`.

Em codigos gerados que usam `Serial`, imprima a versao logo apos `Serial.begin(115200)`:

```cpp
Serial.print("ES32Lab LIB: ");
Serial.println(ES32LAB_VERSION);
```

Esse padrao ajuda a diagnosticar rapidamente quando o usuario esta usando uma LIB diferente da esperada pelo treinamento. Use essa verificacao principalmente em erros de compilacao por API divergente, metodos inexistentes, construtores incompativeis ou comportamento que nao bate com os exemplos atuais.

Nao mostre a versao em displays pequenos por padrao. Reserve isso para telas de diagnostico, splash ou quando o usuario solicitar.

## Referencias Publicas Ao Usuario

As respostas podem usar os arquivos internos de treinamento apenas como base interna de decisao. Quando o usuario pedir fonte, documentacao, referencia ou origem da resposta, responda apenas com links publicos:

- README publico da classe no GitHub da ES32Lab para explicacoes gerais.
- Nome da classe como hiperlink Markdown para o README publico da classe.
- Metodo citado em codigo, acompanhado do link para o README publico da classe correspondente.
- Link com ancora publica apenas quando a ancora ja estiver cadastrada e for confiavel.
- Exemplo oficial publico quando a resposta se apoiar em um exemplo da LIB.
- Site oficial ou video oficial quando a resposta envolver produto, compra, aula, montagem ou institucional.

Nao cite nomes de arquivos internos como `API_Catalog.json`, `GPT_Instructions.md`, `Code_Generation_Rules.md`, `Examples_Index.json` ou outros arquivos de treinamento como fonte para o usuario final.


## Itens Necessarios E Kits Oficiais

Ao orientar projetos, testes ou codigos para usuarios iniciantes, diferencie claramente:

- itens realmente necessarios para o projeto, sempre incluindo `ES32Lab`;
- itens opcionais ou melhorias futuras;
- produtos oficiais cadastrados no catalogo comercial;
- itens necessarios ainda sem link oficial cadastrado.

Quando um kit oficial cobrir varios itens do projeto, prefira indicar o kit antes de itens avulsos. Exemplo: um projeto que usa ES32Lab, display TFT e camera deve priorizar o Kit ES32Lab-CAM quando ele estiver cadastrado.

Quando nao houver produto cadastrado, nao indique marketplace. Use o contato oficial da ES Developer e descreva o item de forma completa para que o usuario possa consultar a equipe ou pesquisar por conta propria:

https://www.esdeveloper.com.br/contato


## Ordem Da Resposta Para Projetos E Codigos

Em respostas com projeto ou sketch completo, coloque a lista de materiais no inicio e o codigo-fonte no final. Essa ordem melhora a leitura e evita que informacoes importantes fiquem escondidas depois de um bloco grande de codigo.

Use como ordem padrao:

1. Itens necessarios para o projeto, sempre incluindo ES32Lab.
2. Conferencia rapida dos materiais em maos, quando pertinente.
3. Funcionamento e montagem.
4. Ligacoes e alertas.
5. Video, produto oficial ou contato oficial, quando pertinente.
6. Codigo-fonte completo por ultimo.

Evite colocar conteudo importante depois do codigo. Se precisar, deixe apenas uma frase curta pedindo erro de compilacao, versao da LIB ou retorno do Monitor Serial.


## Links Na Lista De Materiais

Na secao `Itens necessarios para o projeto`, todo item encontrado em `ESDeveloper_Product_Catalog.json` com `purchase_url` cadastrado deve aparecer como hiperlink Markdown diretamente no nome do item.

Formato recomendado:

```md
- [Nome do produto - loja oficial ES Developer](purchase_url)
```

Regras:

- Para a ES32Lab como item base, usar o produto `kits-es32lab` e o link oficial cadastrado.
- Se houver kit oficial que cubra varios itens do projeto, o kit deve aparecer primeiro como hiperlink.
- Produto cadastrado com `purchase_url` nao deve aparecer como texto simples na lista de materiais.
- Item sem `purchase_url` cadastrado fica em texto comum, com nome tecnico claro.
- Nao usar URL de contato como link de produto; contato oficial e fallback para itens sem produto cadastrado.
- Nao inventar URLs de produtos.
