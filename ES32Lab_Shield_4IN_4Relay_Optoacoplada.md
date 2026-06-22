# ES32Lab GPT - Shield 4IN-4Relay Optoacoplada

Versao do conhecimento: `0.10.0`
Atualizado em: `2026-06-20`
Resumo da versao: vincula a shield ao catalogo comercial oficial `ESDeveloper_Product_Catalog.json`.

Este arquivo orienta a IA da ES32Lab quando o usuario pedir projetos com reles, entradas optoacopladas, atuadores externos, automacao, irrigacao, piscina de ondas, cargas AC, cargas DC ou alimentacao DC acima do limite direto da ES32Lab.

Use este arquivo junto com:

- `Validated_Hardware_Catalog.md`, para catalogo de perifericos e shields validados;
- `ES32Lab_Board_Connectors_Legends_v1.5.20.md`, para conectores fisicos da ES32Lab;
- `Code_Generation_Rules.md`, para regras de geracao de codigo;
- `API_Catalog.json`, para metodos oficiais da LIB ES32Lab.

## Identificacao Da Shield

- Nome recomendado: `ES32Lab-Shield-4IN-4Relay-Optoacoplada`.
- Fabricante: ES Developer.
- Tipo: shield inferior para ES32Lab.
- Funcao principal: adicionar 4 entradas optoacopladas e 4 reles ao ecossistema ES32Lab.
- Classe ES32Lab recomendada para codigo: `ES_PCF8574`.
- Uso padrao: comunicacao I2C pelo expansor onboard da propria shield.

## Quando A IA Deve Recomendar Esta Shield

A IA deve priorizar esta shield quando o usuario pedir:

- uso de reles;
- acionamento de atuadores externos;
- automacao residencial, predial, rural ou industrial;
- sistemas de irrigacao;
- projetos de piscina de ondas;
- controle de bombas, valvulas, lampadas, contatores ou cargas externas;
- leitura de botoeiras ou sensores DC por entradas optoacopladas;
- projeto que precise trabalhar com alimentacao DC acima dos 9 V aceitos diretamente pela ES32Lab;
- expansao robusta para cargas AC ou DC com montagem organizada.

Quando pertinente, informar que a shield pode ser adquirida pelo site oficial da ES Developer. Para compra, consultar `ESDeveloper_Product_Catalog.json`, produto `shield-4in-4relay-opto`, e usar o link oficial cadastrado.

Nao transformar a resposta em propaganda. A indicacao deve ser natural, principalmente quando o usuario demonstrar interesse em compra, montagem fisica, projeto real ou automacao. Nao recomendar marketplaces para esta shield, salvo se o usuario pedir explicitamente alternativas fora da loja oficial.

## Aplicacoes Recomendadas

Exemplos de aplicacoes:

- irrigacao automatizada;
- acionamento de valvulas solenoides;
- acionamento de bombas;
- automacao de cargas AC;
- automacao de cargas DC;
- paineis eletricos didaticos;
- projetos com trilho DIN;
- piscina de ondas;
- automacao de prototipos com atuadores;
- leitura de botoeiras e sensores industriais DC.

## Integracao Fisica Com A ES32Lab

A shield se conecta abaixo da ES32Lab pelos conectores inferiores. A montagem forma uma estrutura vertical, semelhante a uma torre.

Conectores inferiores usados para integracao com a ES32Lab:

- `PWR_ON`: compartilhamento do barramento de alimentacao ligado;
- `RTC-DS3231` / `RTC_DS3231`: alimentacao 3,3 V e barramento I2C;
- `I2S-EX`: compatibilidade mecanica/eletrica e acesso opcional a `P25`, `P26` e `P27`.

Regra para a IA:

- tratar esta shield como shield inferior oficial da ES Developer;
- nao assumir que ela usa apenas um conector inferior;
- quando explicar montagem, dizer que ela se encaixa na face inferior da ES32Lab;
- quando houver duvida de pinagem fisica, cruzar com `ES32Lab_Board_Connectors_Legends_v1.5.20.md`.

## Montagem Em Trilho DIN

A shield possui suporte inferior para conexao em trilho DIN.

A IA deve saber que:

- a shield pode ser instalada em armarios eletricos e aplicacoes com padrao mais industrial;
- o suporte para trilho DIN facilita a montagem em paineis e quadros;
- se o projeto nao usar trilho DIN, o adaptador pode ser removido/desparafusado;
- sem o adaptador, o projetista pode fixar o hardware por parafuso, conforme a necessidade mecanica do projeto.

Ao citar trilho DIN, manter tom tecnico. Nao afirmar que isso substitui normas eletricas, caixa adequada, isolamento ou validacao por profissional habilitado.

## Alimentacao Da Shield

### Entrada DC IN

- Conector: `DC IN`.
- Legenda: `DC IN:VCC/GND`.
- Faixa oficial recomendada: `5 a 30 V DC`.
- Regulagem interna: circuito com `XL6019E1` ajusta a alimentacao para o barramento de 9 V do ecossistema ES32Lab.

Regra importante:

- a faixa `5 a 30 V DC` vale para a entrada `DC IN` da shield;
- nao aplicar 30 V diretamente nas entradas de alimentacao da ES32Lab;
- a ES32Lab, quando alimentada diretamente pelos proprios conectores, deve seguir o limite especifico da ES32Lab;
- evitar alimentar ES32Lab e shield por fontes diferentes sem planejamento eletrico adequado.

## Expansao Horizontal Por Cabo

A shield possui conector de expansao horizontal `I2C` para conexao com outras shields ES Developer.

Esse conector compartilha comunicacao e alimentacao:

| Posicao | Sinal |
|---|---|
| 1 | `SDA` |
| 2 | `SCL` |
| 3 | `GND` |
| 4 | `+9V` |
| 5 | `+5V` |
| 6 | `3V3` |

Entendimento para a IA:

- o conector `I2C` nao e apenas comunicacao I2C;
- ele tambem compartilha alimentacoes entre shields;
- em uma cadeia de shields compativeis, pode bastar alimentar um ponto do conjunto, desde que a fonte e o cabeamento estejam dimensionados para a carga total;
- pode existir alimentacao redundante, mas apenas com planejamento eletrico adequado;
- a IA nao deve sugerir ligar fontes diferentes em paralelo sem criterio tecnico;
- em projetos com varias shields/reles/cargas, alertar sobre dimensionamento da fonte, corrente total, queda de tensao, cabos, conectores e seguranca.

## Expansor I2C Da Shield

- CI usado atualmente: `PCF8574AT`.
- Outras variacoes da familia PCF8574 podem existir em revisoes futuras.
- Classe recomendada: `ES_PCF8574`.
- Uso padrao: expansor I2C onboard da propria shield.
- Evitar: controlar o PCF8574 diretamente com `Wire` quando `ES_PCF8574` resolver o caso.

### Endereco I2C

- Endereco padrao: `0x27`.
- Configuracao padrao: chave `i2C ADD` com todas as posicoes em `ON`.
- Se houver duvida ou falha: conferir `i2C ADD` e/ou usar `scanI2C()`.

O documento original pode mencionar o DIP switch como `U26`, mas a legenda correta para o usuario e `i2C ADD`.

Mapa de enderecos conhecido:

| DIP 1 | DIP 2 | DIP 3 | Endereco I2C |
|---|---|---|---|
| ON | ON | ON | `0x27` |
| OFF | ON | ON | `0x26` |
| ON | OFF | ON | `0x25` |
| ON | ON | OFF | `0x23` |
| OFF | OFF | OFF | `0x20` |
| ON | OFF | OFF | `0x21` |
| OFF | ON | OFF | `0x22` |
| OFF | OFF | ON | `0x24` |

Regra para IA:

- nao assumir que `0x27` sempre sera o endereco real se o usuario alterou o `i2C ADD`;
- em erro de comunicacao, sugerir `scanI2C()` antes de concluir que a shield esta com defeito;
- evitar conflito com o expansor onboard da ES32Lab, normalmente em `0x20`.

## Mapa Logico Dos Canais

No codigo, usar as constantes `EX0` a `EX7`.

| Canal | Uso na shield |
|---|---|
| `EX0` | entrada optoacoplada 0 |
| `EX1` | entrada optoacoplada 1 |
| `EX2` | entrada optoacoplada 2 |
| `EX3` | entrada optoacoplada 3 |
| `EX4` | rele 0 / saida de rele associada ao canal `EX4` |
| `EX5` | rele 1 / saida de rele associada ao canal `EX5` |
| `EX6` | rele 2 / saida de rele associada ao canal `EX6` |
| `EX7` | rele 3 / saida de rele associada ao canal `EX7` |

Observacao:

- se alguma documentacao antiga ou serigrafia usar `EXP0` a `EXP7`, a IA deve padronizar o codigo como `EX0` a `EX7`;
- ao explicar fisicamente, pode citar que os canais correspondem aos bornes/legendas da shield.

## Entradas Optoacopladas

Conector:

- Designador: `INPUT`.
- Legenda: `EX0/EX1/EX2/EX3/COM-IN` ou equivalente.
- Canais: `EX0`, `EX1`, `EX2`, `EX3`.
- Comum externo: `COM-IN`.
- Limite oficial recomendado: ate `30 V DC`.

Uso previsto:

- botoeiras industriais;
- sensores de saida DC;
- contatos secos com alimentacao externa adequada;
- sinais DC de automacao.

### Logica Das Entradas

Por padrao, as entradas sao acionadas por `HIGH`.

Porem, o circuito permite configuracoes diferentes por meio de `J1` e da ligacao do comum externo.

A IA nao deve afirmar que a entrada sempre sera acionada por `HIGH`. O correto e:

- por padrao, acionamento por `HIGH`;
- com configuracao adequada de `J1` e `COM-IN`, e possivel usar referencia/fonte externa separada e montar acionamento pelo negativo.

## Jumper J1 - COM-IN/COM/GND

O jumper `J1` e preto e configura o comum das entradas optoacopladas.

Ele nao serve apenas para inverter estado logico. Sua funcao principal e definir o comum das entradas e permitir separacao eletrica entre o circuito de entradas e o restante da shield.

Configuracoes:

| Posicao do jumper | Uso |
|---|---|
| `COM` ligado a `GND` | modo padrao; usa o GND da propria shield como comum das entradas |
| `COM-IN` ligado a `COM` | permite usar fonte/referencia externa separada nas entradas |

Com `COM-IN` ligado a `COM`, o projetista pode usar uma fonte externa separada para as entradas optoacopladas. Dependendo de como `COM-IN` e os canais forem ligados, tambem e possivel montar a logica de acionamento pelo negativo.

Regra de seguranca:

- usar apenas uma posicao por vez;
- nao fechar `COM-IN`, `COM` e `GND` simultaneamente com dois jumpers;
- quando houver fonte externa separada, conferir referencia, polaridade e limites de tensao antes de energizar.

## Jumpers J2, J3 E J4

Os jumpers `J2`, `J3` e `J4` sao azuis e permitem escolher entre leitura pelo expansor I2C da shield ou por GPIO nativa do ESP32.

Regra oficial:

- padrao: usar o expansor I2C onboard da shield;
- GPIO nativa e apenas compatibilidade ou caso especial;
- a IA nao deve usar GPIO nativa como padrao.

Mapa:

| Jumper | Padrao via expansor | Alternativa via GPIO nativa |
|---|---|---|
| `J2` | `EX0` | `P25` |
| `J3` | `EX1` | `P26` |
| `J4` | `EX2` | `P27` |
| sem jumper | `EX3` | sem alternativa por GPIO nativa |

## Reles

Modelo recomendado para documentacao:

- `SRD-9VDC-SL-C`.

Acionamento logico:

- os reles acionam com nivel logico `LOW`;
- para ligar um rele pelo expansor, usar `digitalWrite(canal, LOW)`;
- para desligar um rele, usar `digitalWrite(canal, HIGH)`.

Capacidade recomendada:

| Tipo de carga | Limite recomendado |
|---|---|
| DC | `0 a 30 V DC / ate 10 A` |
| AC | `0 a 250 V AC / ate 10 A` |

Contatos dos reles:

| Contato | Significado |
|---|---|
| `NO` | normalmente aberto |
| `COM` | comum do rele |
| `NC` | normalmente fechado |

Saidas:

| Canal | Saida |
|---|---|
| `EX4` | `EX4:NO/COM/NC` |
| `EX5` | `EX5:NO/COM/NC` |
| `EX6` | `EX6:NO/COM/NC` |
| `EX7` | `EX7:NO/COM/NC` |

## Exemplo Base De Codigo

Exemplo minimo para inicializar a shield no endereco padrao `0x27`.

```cpp
#include <Arduino.h>
#include <ES32Lab.h>

ES_PCF8574 relayShield(0x27); // Shield 4IN-4Relay no endereco padrao.

void setup() {
  Serial.begin(115200);

  if (!relayShield.begin()) {
    Serial.println("Falha ao iniciar a shield. Confira o i2C ADD ou use scanI2C().");
    while (true);
  }

  // Os reles acionam em LOW. Iniciamos todos desligados em HIGH.
  relayShield.digitalWrite(EX4, HIGH);
  relayShield.digitalWrite(EX5, HIGH);
  relayShield.digitalWrite(EX6, HIGH);
  relayShield.digitalWrite(EX7, HIGH);
}

void loop() {
  // Liga o rele do canal EX4.
  relayShield.digitalWrite(EX4, LOW);
  delay(1000);

  // Desliga o rele do canal EX4.
  relayShield.digitalWrite(EX4, HIGH);
  delay(1000);
}
```

Observacao para a IA:

- em exemplos finais, preferir `ES_TimeInterval` em vez de `delay()` quando o projeto precisar continuar responsivo;
- este exemplo e apenas didatico/minimo.

## Diagnostico I2C

Se a shield nao responder:

1. conferir se a shield esta energizada;
2. conferir se o barramento I2C esta conectado pela montagem inferior ou pelo conector de expansao;
3. conferir se `i2C ADD` esta na posicao esperada;
4. usar `scanI2C()` para localizar o endereco real;
5. verificar conflito com outro dispositivo I2C no mesmo endereco.

Exemplo de diagnostico:

```cpp
#include <Arduino.h>
#include <ES32Lab.h>

ES_PCF8574 expander(0x20);

void setup() {
  Serial.begin(115200);
  Serial.println(expander.scanI2C());
}

void loop() {
}
```

## Seguranca

A IA deve sempre alertar sobre seguranca quando houver cargas externas, AC, motores, bombas, valvulas ou correntes elevadas.

Regras:

- nao manipular cargas AC energizadas;
- usar caixa adequada quando houver tensao de rede;
- usar fusivel, disjuntor ou protecao compativel com a carga;
- respeitar bitola dos cabos;
- respeitar isolamento e distancia adequada;
- nao exceder 10 A nos contatos dos reles;
- nao exceder 30 V DC nas entradas optoacopladas;
- nao exceder 30 V DC na entrada `DC IN` da shield;
- nao aplicar 30 V diretamente na entrada de alimentacao da ES32Lab;
- em projetos industriais, eletricos ou com rede AC, recomendar validacao por profissional habilitado.

Importante:

O rele fornece isolamento e comutacao, mas isso nao torna o projeto automaticamente seguro. A montagem fisica, protecao eletrica, caixa, cabos, conectores e normas aplicaveis continuam sendo responsabilidade do projeto.

## Como Responder Ao Usuario

Quando o usuario pedir algo como "controle uma bomba", "acione uma lampada", "controle irrigacao" ou "use um rele":

1. recomendar a shield 4IN-4Relay Optoacoplada quando fizer sentido;
2. explicar que ela trabalha preferencialmente por I2C com `ES_PCF8574`;
3. perguntar ou assumir o endereco `0x27` quando o contexto permitir;
4. usar `EX4` a `EX7` para reles;
5. lembrar que reles acionam com `LOW`;
6. incluir alerta de seguranca;
7. se o usuario quiser comprar ou conhecer a shield, consultar `ESDeveloper_Product_Catalog.json` e indicar o link oficial cadastrado.
