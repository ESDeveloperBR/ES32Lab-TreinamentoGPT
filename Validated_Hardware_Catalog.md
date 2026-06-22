# ES32Lab GPT - Catalogo De Hardware Validado

Versao do conhecimento: `0.10.0`
Atualizado em: `2026-06-20`
Resumo da versao: adiciona referencia ao catalogo comercial oficial para produtos e links de compra.

Este arquivo orienta a IA da ES32Lab quando o usuario pedir uso de sensores, modulos, shields, CIs, perifericos externos ou bibliotecas de terceiros junto com a placa ES32Lab.

Use este catalogo para escolher componentes ja validados, bibliotecas preferenciais, ligacoes recomendadas e cuidados praticos. Para metodos da LIB ES32Lab, consulte `API_Catalog.json`. Para regras gerais de geracao de codigo, consulte `Code_Generation_Rules.md`.

Para conectores, legendas fisicas, jumpers, face superior, face inferior e shields inferiores da placa, consulte `ES32Lab_Board_Connectors_Legends_v1.5.20.md`.

## Principio Geral

A ES32Lab possui diversos circuitos onboard ja conectados ao ESP32. Por isso, a recomendacao oficial e preservar esses circuitos sempre que possivel e priorizar expansoes por barramentos como I2C, SPI e I2S.

Regra pratica:

- se existir uma classe ES32Lab para o recurso, usar a classe ES32Lab;
- se o recurso for externo e ainda nao existir classe ES32Lab, usar a biblioteca preferida indicada neste catalogo;
- se houver opcao entre um modulo I2C e outro que consuma GPIOs nativas, priorizar o modulo I2C;
- nao sacrificar circuitos onboard sem explicar claramente a consequencia;
- quando houver falha em dispositivo I2C, recomendar verificacao de endereco com `scanI2C()` da classe `ES_PCF8574`.

## Expansao I2C Onboard Da ES32Lab

Endereco padrao usado nos exemplos da ES32Lab:

```cpp
ES_PCF8574 expander(0x20);
```

Mapa pratico dos pinos do expansor I2C onboard:

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

Quando os jumpers brancos da ponte H estiverem conectados, considerar `EX4`, `EX5`, `EX6` e `EX7` ocupados pelo controle dos motores.

Para sensores de linha e demandas que precisem de duas GPIOs livres no expansor I2C onboard, sugerir `EX2` e `EX3` por padrao.

## Ponte H Onboard

A ponte H onboard da ES32Lab e controlada pelo expansor I2C quando os jumpers brancos estao conectados.

A IA deve usar a classe `ES_CarControl` para controlar motores, carros, robos moveis e veiculos.

Logica eletrica da ponte H:

- quando `M1A` ou `M2A` recebe sinal logico alto ou PWM, o motor gira em uma direcao;
- quando `M1B` ou `M2B` recebe sinal logico alto ou PWM, o motor gira na direcao oposta;
- quando os dois sinais do mesmo motor estao iguais, ambos altos ou ambos baixos, o motor fica parado.

Mesmo conhecendo essa logica, a IA nao deve controlar diretamente a ponte H em exemplos comuns. O padrao oficial e:

```cpp
ES_PCF8574 expander(0x20);
ES_CarControl car(expander);

void setup() {
  car.begin(DIFFERENTIAL);
}
```

## Diagnostico De Dispositivos I2C

Muitos problemas com perifericos I2C acontecem por endereco incorreto, alimentacao incorreta, jumper ausente ou ligacao invertida em `SDA` e `SCL`.

Quando o usuario relatar falha em periferico I2C, expansor, ponte H, sensor I2C ou shield I2C, recomendar:

```cpp
ES_PCF8574 expander(0x20);

void setup() {
  Serial.begin(115200);
  Serial.println(expander.scanI2C());
}
```

Use esse diagnostico antes de afirmar que o componente esta danificado.

## Sensores E Perifericos Validados

### TCRT5000 - Sensor Infravermelho De Reflexao

- Status: recomendado para seguidores de linha didaticos.
- Tipo: sensor de reflexao infravermelho.
- Barramento: entrada digital pelo expansor I2C onboard.
- Classe ES32Lab recomendada: `ES_CarLineFollower`.
- Pinos recomendados: `EX2` para sensor esquerdo e `EX3` para sensor direito.
- Quando recomendar: robo seguidor de linha, leitura binaria de linha preta/branca, experimentos didaticos de robotica.

Padrao recomendado:

```cpp
ES_PCF8574 expander(0x20);
ES_CarControl car(expander);
ES_CarLineFollower lineFollower(car, expander);

void setup() {
  car.begin(DIFFERENTIAL);
  lineFollower.begin(EX2, EX3);
}
```

Se o usuario informar outra ligacao fisica, respeitar a ligacao informada.

### VL53L0X - Sensor De Distancia

- Status: periferico I2C recomendado.
- Tipo: sensor de distancia por tempo de voo.
- Barramento: I2C.
- Biblioteca preferida: `pololu/VL53L0X`.
- Endereco I2C comum: `0x29`.
- Quando recomendar: deteccao de obstaculos, robo movel, medicao de distancia curta, projetos didaticos de sensores.
- Diagnostico: se nao detectar, recomendar `scanI2C()` para conferir o endereco no barramento.

Ao gerar codigo com este sensor:

- incluir a biblioteca externa preferida;
- manter `ES32Lab.h` como include principal da placa;
- usar classes ES32Lab para display, temporizacao, motores, buzzer e demais recursos da placa;
- nao substituir `ES_CarControl`, `ES_TimeInterval` ou `ES_TFT` por codigo generico.

### BME280 / Familia BME2xx

- Status: periferico I2C recomendado.
- Tipo: sensor de temperatura, pressao, altitude e umidade, conforme modelo usado.
- Barramento: I2C.
- Biblioteca preferida: `sparkfun/SparkFun_BME280_Arduino_Library`.
- Enderecos I2C comuns: `0x76` e `0x77`.
- Quando recomendar: estacao meteorologica, IoT, monitoramento ambiental, aulas sobre sensores ambientais.
- Diagnostico: se nao detectar, recomendar `scanI2C()` e conferir o endereco configurado no codigo.

Ao gerar codigo com sensores da familia BME2xx:

- usar a biblioteca SparkFun BME280 como primeira escolha;
- explicar que o endereco pode variar entre modulos;
- usar `ES_TimeInterval` para leituras periodicas sem travar o `loop()`;
- usar `ES_TFT` quando os dados forem exibidos no display da ES32Lab.

## Shields E Expansoes A Detalhar

Os itens abaixo existem no ecossistema da ES Developer, mas seus detalhes de pinagem, biblioteca, exemplos e regras de uso devem ser cadastrados em uma etapa futura antes de a IA gerar codigo especifico completo.

### Shield Com 4 Reles E 4 Entradas Optoacopladas

- Status: validada e recomendada.
- Nome recomendado: `ES32Lab-Shield-4IN-4Relay-Optoacoplada`.
- Fabricante: ES Developer.
- Documento especifico: `ES32Lab_Shield_4IN_4Relay_Optoacoplada.md`.
- CI usado atualmente: `PCF8574AT`.
- Barramento: I2C.
- Classe ES32Lab recomendada: `ES_PCF8574`.
- Endereco padrao: `0x27`, com `i2C ADD` todo em `ON`.
- Uso esperado: automacao, acionamento de cargas, irrigacao, piscina de ondas, leitura de entradas optoacopladas, atuadores AC/DC e cargas que exigem alimentacao externa.
- Quando recomendar: sempre que o usuario pedir reles, entradas optoacopladas, cargas AC/DC, automacao com atuadores ou alimentacao DC acima do limite direto da ES32Lab.
- Observacao mecanica: shields inferiores da ES Developer podem usar todos os conectores da face inferior da ES32Lab para alimentacao, I2C, I2S ou GPIOs compartilhadas.
- Montagem: possui suporte para trilho DIN; o adaptador pode ser removido para fixacao por parafuso quando o projeto nao usar trilho DIN.
- Canais de entrada: `EX0`, `EX1`, `EX2`, `EX3`.
- Canais de rele: `EX4`, `EX5`, `EX6`, `EX7`.
- Acionamento dos reles: `LOW` liga e `HIGH` desliga.
- Entradas optoacopladas: por padrao acionadas por `HIGH`, mas `J1` permite configurar comum externo, separar eletricamente as entradas e montar acionamento pelo negativo conforme a ligacao.
- Limite da entrada `DC IN`: `5 a 30 V DC`.
- Limite das entradas optoacopladas: ate `30 V DC`.
- Limite dos reles: ate `30 V DC / 10 A` ou `250 V AC / 10 A`.
- Diagnostico: se nao detectar a shield, conferir `i2C ADD` e usar `scanI2C()`.
- Catalogo comercial: `ESDeveloper_Product_Catalog.json`, produto `shield-4in-4relay-opto`.
- Compra: usar o link oficial cadastrado no catalogo comercial quando o contexto for compra ou montagem do projeto.

Regras:

- usar `ES_PCF8574` por padrao;
- nao usar GPIO nativa como padrao para as entradas;
- nao usar `Wire` diretamente se `ES_PCF8574` resolver;
- sempre incluir alerta de seguranca quando houver cargas AC, correntes elevadas, bombas, valvulas, motores ou instalacao eletrica real.

### Shield De Matriz De Contatos

- Status: conhecido, a detalhar.
- CI principal: `PCF8574`.
- Barramento: I2C.
- Classe ES32Lab provavel: `ES_PCF8574`.
- Uso esperado: leitura expandida de contatos ou matriz de entradas.
- Observacao mecanica: shields inferiores da ES Developer podem usar todos os conectores da face inferior da ES32Lab para alimentacao, I2C, I2S ou GPIOs compartilhadas.

Antes de gerar codigo definitivo para esta shield, confirmar:

- endereco I2C;
- quantidade de linhas e colunas;
- mapeamento fisico;
- necessidade de pull-up ou pull-down;
- logica ativa em alto ou baixo.

## Modelo Para Cadastrar Novo Periferico

Ao validar um novo sensor, modulo ou shield, adicionar uma secao neste formato:

````md
### Nome Do Periferico

- Status: validado | recomendado | conhecido, a detalhar | experimental.
- Tipo:
- Barramento: I2C | SPI | I2S | UART | GPIO | analogico.
- Biblioteca preferida:
- Classe ES32Lab relacionada:
- Endereco I2C comum:
- Ligacao recomendada:
- Quando recomendar:
- Cuidados:
- Diagnostico:

Exemplo minimo:

```cpp
// Codigo curto ou padrao de inicializacao.
```
````

Regras de manutencao:

- nao cadastrar biblioteca como preferida sem teste real ou decisao tecnica da ES Developer;
- nao inventar endereco I2C;
- quando o endereco variar por modulo, documentar como comum, nao como absoluto;
- quando o periferico ainda nao estiver completamente mapeado, marcar como `conhecido, a detalhar`;
- criar exemplos oficiais depois que o padrao de uso estiver estabilizado.
