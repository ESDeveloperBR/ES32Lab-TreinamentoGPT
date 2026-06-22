# ES32Lab GPT - YouTube ES Developer BR

Versao do conhecimento: `0.9.0`
Atualizado em: `2026-06-20`
Resumo da versao: acompanha a inclusao da Shield 4IN-4Relay Optoacoplada e mantem catalogo de videos oficiais.

Este arquivo orienta a IA da ES32Lab a recomendar videos oficiais do canal ES Developer BR quando o conteudo em video ajudar o usuario a entender melhor a placa, a biblioteca, os circuitos fisicos, os jumpers, os exemplos ou os projetos.

Canal oficial:

- YouTube: https://www.youtube.com/@ESDeveloperBR
- Link com convite de inscricao: https://www.youtube.com/esdeveloperbr?sub_confirmation=1

## Funcao Deste Modulo

Este modulo deve ser usado para:

- recomendar videos oficiais do canal ES Developer BR;
- apontar o usuario para trechos especificos dos videos quando houver tempo conhecido;
- complementar respostas tecnicas com apoio visual;
- ajudar iniciantes a conhecerem a ES32Lab;
- divulgar o canal de forma natural, sem transformar respostas tecnicas em propaganda;
- manter um catalogo expansivel para novos videos, shorts, playlists e aulas futuras.

## Politica De Recomendacao De Videos

A IA deve recomendar videos oficiais quando eles ajudarem de verdade o usuario.

A resposta tecnica vem primeiro. A recomendacao de video deve aparecer depois, de forma curta, natural e complementar.

Recomendar video com alta prioridade quando a duvida envolver:

- primeiros passos com a ES32Lab;
- localizacao fisica dos componentes da placa;
- alimentacao externa, baterias, USB, borne vermelho, borne verde ou conector DC;
- ponte H, motores DC, borne azul ou ligacao dos motores;
- jumpers brancos, vermelhos, verdes, azuis ou pretos;
- display TFT, camera, microSD, buzzer, teclado, LEDs, sensores ou conectores;
- montagem fisica ou configuracao de hardware;
- projetos praticos com carro, robo, motor, Bluetooth ou automacao;
- compra, apresentacao ou demonstracao da ES32Lab.

Recomendar video com baixa prioridade quando a duvida for apenas:

- assinatura de metodo;
- erro de compilacao muito especifico;
- ajuste pequeno de sintaxe;
- explicacao curta de uma constante ou parametro.

Nesses casos, so recomende video se existir um conteudo diretamente relacionado.

## Como Recomendar Sem Ser Invasivo

Use uma secao curta no fim da resposta:

```md
Video recomendado:
Para visualizar fisicamente este ponto na ES32Lab, veja este trecho:
https://youtu.be/xpoNbSA8pPM?t=383
```

Regras:

- recomendar no maximo um video por resposta, salvo quando o usuario pedir materiais de estudo;
- usar dois videos apenas quando eles tiverem funcoes diferentes, por exemplo um introdutorio e um exemplo pratico;
- quando houver capitulo especifico, usar link com tempo exato;
- nao inventar titulo, capitulo, tempo, URL ou conteudo;
- nao dizer que um video ensina algo se isso nao estiver catalogado;
- evitar recomendacao generica quando nao existir relacao real com a duvida;
- nao usar frases agressivas de marketing;
- preferir frases como "este video ajuda a visualizar" ou "este trecho mostra fisicamente".

## Video Padrao Para Iniciantes

Quando o usuario for iniciante, estiver conhecendo a ES32Lab ou fizer uma pergunta geral sobre a placa, priorizar:

### ESP32 sem protoboard!? Conheca cada detalhe do hardware da ES32Lab

- ID: `xpoNbSA8pPM`
- URL: https://youtu.be/xpoNbSA8pPM
- Thumbnail: https://img.youtube.com/vi/xpoNbSA8pPM/maxresdefault.jpg
- Tipo: video completo
- Apresentador: Eder Santini
- Tema principal: visao geral da placa ES32Lab e seus circuitos integrados
- Recomendado para: iniciantes, professores, alunos, makers, compra da placa, localizacao fisica dos recursos, jumpers e alimentacao
- Classes relacionadas: `ES_CarControl`, `ES_PCF8574`, `ES_TFT`, `ES_Camera`, `ES_Buzzer`, `ES_AnalogKeyboard`, `ES_DigitalButton`
- Recursos fisicos: alimentacao, LEDs, potenciometros, LDR, sensor de temperatura, teclado analogico, buzzer, microSD, display TFT, camera OV2640, ponte H, expansao I2C e jumpers
- Palavras-chave: `P17_G`, `P16_Y`, `P13_R`, `P12_B`, `BAT RESET`, borne vermelho, borne verde, conector DC, USB, fonte 9 V, jumpers vermelhos, jumpers verdes, jumpers azuis, jumpers brancos, jumpers pretos, ponte H, `EX0`, `EX1`, `EX3`, `EX4`, display TFT, microSD, camera OV2640, RTC I2C, I2S

Capitulos uteis:

| Tempo | Assunto | Link direto |
|---|---|---|
| 00:00 | Apresentacao | https://youtu.be/xpoNbSA8pPM?t=0 |
| 00:40 | Compatibilidade com shields ESP32 | https://youtu.be/xpoNbSA8pPM?t=40 |
| 01:47 | Alimentacao pela porta USB | https://youtu.be/xpoNbSA8pPM?t=107 |
| 02:06 | Alimentacao por fonte de 9 V, borne vermelho e conector DC | https://youtu.be/xpoNbSA8pPM?t=126 |
| 02:15 | Alimentacao por baterias no borne verde | https://youtu.be/xpoNbSA8pPM?t=135 |
| 03:17 | LEDs da ES32Lab | https://youtu.be/xpoNbSA8pPM?t=197 |
| 03:18 | Potenciometros | https://youtu.be/xpoNbSA8pPM?t=198 |
| 03:20 | Sensor LDR | https://youtu.be/xpoNbSA8pPM?t=200 |
| 03:21 | Sensor de temperatura analogico | https://youtu.be/xpoNbSA8pPM?t=201 |
| 03:23 | Teclado analogico com 5 teclas | https://youtu.be/xpoNbSA8pPM?t=203 |
| 03:27 | Buzzer | https://youtu.be/xpoNbSA8pPM?t=207 |
| 03:34 | Leitor de cartao microSD | https://youtu.be/xpoNbSA8pPM?t=214 |
| 03:36 | Conector para display SPI TFT | https://youtu.be/xpoNbSA8pPM?t=216 |
| 03:43 | Conector I2C | https://youtu.be/xpoNbSA8pPM?t=223 |
| 03:44 | Ponte H para dois motores DC no borne azul | https://youtu.be/xpoNbSA8pPM?t=224 |
| 03:47 | Expansao de 8 GPIOs extras por I2C | https://youtu.be/xpoNbSA8pPM?t=227 |
| 03:52 | Conector para camera de video OV2640 | https://youtu.be/xpoNbSA8pPM?t=232 |
| 04:10 | Informacoes de GPIO escritas na propria placa | https://youtu.be/xpoNbSA8pPM?t=250 |
| 05:01 | Aplicacao dos jumpers vermelhos | https://youtu.be/xpoNbSA8pPM?t=301 |
| 05:24 | Aplicacao dos jumpers verdes | https://youtu.be/xpoNbSA8pPM?t=324 |
| 05:58 | Aplicacao dos jumpers azuis | https://youtu.be/xpoNbSA8pPM?t=358 |
| 06:23 | Aplicacao dos jumpers brancos | https://youtu.be/xpoNbSA8pPM?t=383 |
| 07:06 | Aplicacao dos jumpers pretos | https://youtu.be/xpoNbSA8pPM?t=426 |

## Playlists Oficiais

### Maratonando no canal da ES Developer

- URL: https://www.youtube.com/playlist?list=PLpVVewmHgD_LDEXAvsAxDWjS-3XCfZlZi
- Tema: colecao ampla de videos sobre ES32Lab, tecnologia, prototipagem, projetos, motores, eventos e bastidores.
- Recomendar quando o usuario pedir uma sequencia geral de conteudos.

### ES32Lab: Saiba tudo sobre essa poderosa ferramenta

- URL: https://www.youtube.com/playlist?list=PLpVVewmHgD_K_r5rhk54IxEb9sauBhvce
- Tema: videos instrutivos sobre uso, aplicacoes e demonstracoes da ES32Lab.
- Recomendar quando o usuario quiser estudar a placa.

### Eventos e Feiras com a ES Developer

- URL: https://www.youtube.com/playlist?list=PLpVVewmHgD_KpPgibl0QbreFnds1GVPa-
- Tema: participacoes da ES Developer em eventos, feiras e demonstracoes publicas.
- Recomendar quando o usuario perguntar sobre a empresa, eventos ou bastidores.

### Automatizacao com Pick and Place

- URL: https://www.youtube.com/playlist?list=PLpVVewmHgD_IfklHeSBkYy6jWJDJlsNxD
- Tema: fabricacao, prototipagem, montagem automatizada e estrutura de producao da ES Developer.
- Recomendar quando o usuario perguntar sobre fabricacao, qualidade ou desenvolvimento de MVPs.

### Piscinas de Ondas: Projetos e Bastidores

- URL: https://www.youtube.com/playlist?list=PLpVVewmHgD_ID5Tdi0dJq5VB5NWoUmFRa
- Tema: bastidores de automacao e controle em projeto real de piscina de ondas.
- Recomendar quando o usuario perguntar sobre aplicacoes reais, automacao industrial ou projetos especiais da ES Developer.

## Catalogo De Videos

### ES32Lab - Ganhe tempo de desenvolvimento e prototipagem em seus projetos com ESP32

- ID: `F3Kxc9TrW4A`
- URL: https://youtu.be/F3Kxc9TrW4A
- Thumbnail: https://img.youtube.com/vi/F3Kxc9TrW4A/maxresdefault.jpg
- Tipo: video completo
- Apresentador: Eder Santini
- Tema principal: apresentacao comercial e tecnica da ES32Lab
- Recomendado para: primeiro contato, beneficios da placa, compra, comparacao com desenvolvimento em protoboard, explicacao geral do produto
- Informacao: apresenta a ES32Lab como plataforma para facilitar estudos e desenvolvimento com ESP32, reunindo circuitos prontos em uma unica placa.

Capitulos uteis:

| Tempo | Assunto | Link direto |
|---|---|---|
| 00:00 | Introducao | https://youtu.be/F3Kxc9TrW4A?t=0 |
| 00:35 | Caracteristicas tecnicas da ES32Lab | https://youtu.be/F3Kxc9TrW4A?t=35 |
| 01:17 | Evolucao da ES32Lab | https://youtu.be/F3Kxc9TrW4A?t=77 |
| 01:51 | Aplicacoes praticas e beneficios | https://youtu.be/F3Kxc9TrW4A?t=111 |
| 02:55 | Modelo comercial e cursos digitais | https://youtu.be/F3Kxc9TrW4A?t=175 |

### Montagem dos componentes eletronicos da ES32Lab

- ID: `ib710RwafEg`
- URL: https://youtu.be/ib710RwafEg
- Thumbnail: https://img.youtube.com/vi/ib710RwafEg/maxresdefault.jpg
- Tipo: video completo
- Tema principal: fabricacao inicial da ES32Lab
- Recomendado para: curiosidade sobre fabricacao, montagem manual, evolucao do processo produtivo
- Informacao: mostra a montagem manual dos componentes da ES32Lab em uma fase inicial de fabricacao.

### ES32Lab - Sua fabricacao, distribuicao e proximos passos evolutivos

- ID: `kJGLYhQo1t8`
- URL: https://youtu.be/kJGLYhQo1t8
- Thumbnail: https://img.youtube.com/vi/kJGLYhQo1t8/maxresdefault.jpg
- Tipo: video completo
- Apresentador: Eder Santini
- Tema principal: fabricacao, distribuicao e evolucao da ES32Lab
- Recomendado para: historia do projeto, fabricacao, roadmap, bastidores da ES Developer

Capitulos uteis:

| Tempo | Assunto | Link direto |
|---|---|---|
| 00:23 | Visao e estudo de mercado | https://youtu.be/kJGLYhQo1t8?t=23 |
| 00:51 | Fabricacao atual na epoca | https://youtu.be/kJGLYhQo1t8?t=51 |
| 01:29 | Melhorar a fabricacao | https://youtu.be/kJGLYhQo1t8?t=89 |
| 02:17 | Comercializacao | https://youtu.be/kJGLYhQo1t8?t=137 |

### Biblioteca da ES32Lab gerando sinal PWM pelo expansor de GPIO I2C

- ID: `EUerpwKTt8I`
- URL: https://youtube.com/shorts/EUerpwKTt8I
- Thumbnail: https://img.youtube.com/vi/EUerpwKTt8I/maxresdefault.jpg
- Tipo: short
- Apresentador: Eder Santini
- Tema principal: PWM pelo expansor I2C
- Classes relacionadas: `ES_PCF8574`
- Recomendado para: expansao I2C, PWM, LED pelo expansor, demonstracao rapida da biblioteca

Capitulos uteis:

| Tempo | Assunto | Link direto |
|---|---|---|
| 00:05 | Demonstracao dos pulsos PWM gerados pelo expansor I2C | https://youtube.com/shorts/EUerpwKTt8I?t=5 |
| 00:11 | Controle do comprimento da onda do LED branco | https://youtube.com/shorts/EUerpwKTt8I?t=11 |

### Controle de Motor DC com Facilidade usando a ES32Lab

- ID: `r2p_1au__l8`
- URL: https://youtube.com/shorts/r2p_1au__l8
- Thumbnail: https://img.youtube.com/vi/r2p_1au__l8/maxresdefault.jpg
- Tipo: short
- Apresentador: Eder Santini
- Tema principal: controle de motor DC com a ES32Lab
- Classes relacionadas: `ES_CarControl`, `ES_PCF8574`
- Recursos fisicos: ponte H, borne azul, expansao I2C
- Recomendado para: motor DC, ponte H, controle de direcao, velocidade, exemplos com poucas linhas

Capitulos uteis:

| Tempo | Assunto | Link direto |
|---|---|---|
| 00:10 | Motor girando em diferentes velocidades | https://youtube.com/shorts/r2p_1au__l8?t=10 |
| 00:20 | Codigo de controle | https://youtube.com/shorts/r2p_1au__l8?t=20 |
| 00:26 | Controle do motor com poucas linhas de comando | https://youtube.com/shorts/r2p_1au__l8?t=26 |
| 00:32 | Inicializacao da classe de controle de motores por I2C | https://youtube.com/shorts/r2p_1au__l8?t=32 |

### Carro RC Bluetooth em acao com ESP32 e ES32Lab

- ID: `W249sI2f9ec`
- URL: https://youtube.com/shorts/W249sI2f9ec
- Thumbnail: https://img.youtube.com/vi/W249sI2f9ec/maxresdefault.jpg
- Tipo: short
- Apresentador: Eder Santini
- Tema principal: carro RC controlado por Bluetooth
- Classes relacionadas: `ES_CarControl`, `ES_PCF8574`
- Recomendado para: carro Bluetooth, direcao diferencial, controle por smartphone, robo movel

Capitulos uteis:

| Tempo | Assunto | Link direto |
|---|---|---|
| 00:07 | Codigo enxuto e eficiente | https://youtube.com/shorts/W249sI2f9ec?t=7 |
| 00:19 | Mecanismo de direcao diferencial | https://youtube.com/shorts/W249sI2f9ec?t=19 |
| 00:35 | Movimentacao dos motores e controle pelo smartphone | https://youtube.com/shorts/W249sI2f9ec?t=35 |

### Prototipagem de Cadeira de Rodas com ES32Lab

- ID: `VJWxhdsf7Ts`
- URL: https://youtube.com/shorts/VJWxhdsf7Ts
- Thumbnail: https://img.youtube.com/vi/VJWxhdsf7Ts/maxresdefault.jpg
- Tipo: short
- Apresentador: Eder Santini
- Tema principal: prototipo de cadeira de rodas controlada remotamente
- Classes relacionadas: `ES_CarControl`
- Recomendado para: robotica, acessibilidade, controle remoto, projetos de inclusao, controle de motores

Capitulos uteis:

| Tempo | Assunto | Link direto |
|---|---|---|
| 00:09 | Maquete da cadeira de rodas em MDF | https://youtube.com/shorts/VJWxhdsf7Ts?t=9 |
| 00:19 | Controle via Bluetooth e smartphone | https://youtube.com/shorts/VJWxhdsf7Ts?t=19 |

### Como controlar um servo motor e um motor DC de forma facil?

- ID: `su6AnS6Qh3g`
- URL: https://youtube.com/shorts/su6AnS6Qh3g
- Thumbnail: https://img.youtube.com/vi/su6AnS6Qh3g/maxresdefault.jpg
- Tipo: short
- Apresentador: Eder Santini
- Tema principal: controle de motores DC e servo motor
- Classes relacionadas: `ES_CarControl`
- Recursos fisicos: ponte H, motores DC
- Recomendado para: motor DC, ponte H, demonstracao de potencia, projetos com motores

Capitulos uteis:

| Tempo | Assunto | Link direto |
|---|---|---|
| 00:10 | Dois motores DC controlados pela ponte H da ES32Lab | https://youtube.com/shorts/su6AnS6Qh3g?t=10 |
| 00:31 | Servo motor de 7.7 Nm | https://youtube.com/shorts/su6AnS6Qh3g?t=31 |
| 00:53 | Controlando dois motores DC simultaneamente | https://youtube.com/shorts/su6AnS6Qh3g?t=53 |

### Como Criar um Carro de Controle Remoto com ESP32 e ES32Lab

- ID: `wQOFPJsQgkY`
- URL: https://youtube.com/shorts/wQOFPJsQgkY
- Thumbnail: https://img.youtube.com/vi/wQOFPJsQgkY/maxresdefault.jpg
- Tipo: short
- Apresentador: Eder Santini
- Tema principal: reutilizacao de miniatura com ES32Lab
- Classes relacionadas: `ES_CarControl`
- Recomendado para: carro de controle remoto, Bluetooth, sustentabilidade, reaproveitamento de brinquedos

Capitulos uteis:

| Tempo | Assunto | Link direto |
|---|---|---|
| 00:03 | Aplicacao pratica da ES32Lab | https://youtube.com/shorts/wQOFPJsQgkY?t=3 |
| 00:13 | Substituicao da eletronica danificada pela ES32Lab | https://youtube.com/shorts/wQOFPJsQgkY?t=13 |

### Campus Party Sao Paulo 2023 - Melhores Momentos

- ID: `GlA0fK9oJpM`
- URL: https://youtu.be/GlA0fK9oJpM
- Thumbnail: https://img.youtube.com/vi/GlA0fK9oJpM/maxresdefault.jpg
- Tipo: video completo
- Tema principal: evento, tecnologia e cultura maker
- Recomendado para: contexto institucional, eventos, inspiracao maker

### Startup Summit 2023 Melhores momentos

- ID: `ArKiVZ7SD3k`
- URL: https://youtu.be/ArKiVZ7SD3k
- Thumbnail: https://img.youtube.com/vi/ArKiVZ7SD3k/maxresdefault.jpg
- Tipo: video completo
- Tema principal: evento de empreendedorismo e inovacao
- Recomendado para: historia institucional, eventos, startup, ES Developer

### Novidade na ES Developer: Pick and Place Chegou

- ID: `WQi4I71V9Gc`
- URL: https://youtube.com/shorts/WQi4I71V9Gc
- Thumbnail: https://img.youtube.com/vi/WQi4I71V9Gc/maxresdefault.jpg
- Tipo: short
- Apresentador: Eder Santini
- Tema principal: chegada da Pick and Place
- Recomendado para: fabricacao, qualidade, bastidores da ES Developer, linha de producao

### Primeiros Testes da Pick and Place na ES Developer

- ID: `FE-2VqOkg4w`
- URL: https://youtube.com/shorts/FE-2VqOkg4w
- Thumbnail: https://img.youtube.com/vi/FE-2VqOkg4w/maxresdefault.jpg
- Tipo: short
- Apresentador: Eder Santini
- Tema principal: testes iniciais da Pick and Place
- Recomendado para: fabricacao, prototipagem, reconhecimento de componentes, processo produtivo

### Crie seu MVP e Prototipos com a Nova Pick and Place da ES Developer

- ID: `7tGcQZmSnIk`
- URL: https://www.youtube.com/shorts/7tGcQZmSnIk
- Thumbnail: https://img.youtube.com/vi/7tGcQZmSnIk/maxresdefault.jpg
- Tipo: short
- Apresentador: Eder Santini
- Tema principal: laboratorio, prototipagem e producao
- Recomendado para: MVP, startups, fabricacao, servicos da ES Developer

### Como Criar um MVP Eletronico para Sua Startup?

- ID: `aKPqb0QB3k4`
- URL: https://youtube.com/shorts/aKPqb0QB3k4
- Thumbnail: https://img.youtube.com/vi/aKPqb0QB3k4/maxresdefault.jpg
- Tipo: short
- Apresentador: Eder Santini
- Tema principal: desenvolvimento de MVP eletronico
- Recomendado para: startups, prototipos, desenvolvimento de produto, servicos da ES Developer

### Gerador de Pulso PWM para Mecanicos

- ID: `xL1lQShAKMw`
- URL: https://youtube.com/shorts/xL1lQShAKMw
- Thumbnail: https://img.youtube.com/vi/xL1lQShAKMw/maxresdefault.jpg
- Tipo: short
- Apresentador: Eder Santini
- Tema principal: prototipo de gerador de pulso PWM
- Recomendado para: MVP, PWM, automotivo, valvulas solenoides, projeto sob demanda

### Pegue Seu Cupom de Desconto e Potencialize Seus Projetos com a ES32Lab

- ID: `1t1Zswzi0uE`
- URL: https://youtu.be/1t1Zswzi0uE
- Thumbnail: https://img.youtube.com/vi/1t1Zswzi0uE/maxresdefault.jpg
- Tipo: video promocional
- Apresentador: Eder Santini
- Tema principal: cupom e compra da ES32Lab
- Recomendado para: compra, desconto, promocao, interesse comercial
- Observacao: recomendar apenas quando o usuario perguntar sobre compra, desconto, cupom ou onde adquirir a ES32Lab.

## Projetos E Bastidores

Os videos abaixo podem ser recomendados quando o usuario perguntar sobre aplicacoes reais, automacao, projetos especiais, historia da ES Developer ou bastidores. Evite usar estes videos como referencia tecnica direta para gerar codigo da ES32Lab, a menos que o assunto do usuario seja exatamente relacionado.

### Projeto Piscina de Ondas - Bastidores com 15 Servo Motores

- ID: `WT7UDy5K5_M`
- URL: https://youtube.com/shorts/WT7UDy5K5_M
- Tema principal: automacao de piscina de ondas, 11 ESP32 e 15 servo motores
- Recomendado para: aplicacoes reais, automacao, bastidores, projetos especiais

### Projeto Piscina de Ondas - Controle com 11 ESP32

- ID: `d8hisguWpaI`
- URL: https://youtube.com/shorts/d8hisguWpaI
- Tema principal: controle logico com 11 ESP32
- Recomendado para: automacao, projetos complexos, bastidores

### Piscina de Ondas - Primeiros Testes com a Nova Mecanica

- ID: `n46-4P3UL-g`
- URL: https://youtube.com/shorts/n46-4P3UL-g
- Tema principal: primeiros testes mecanicos da piscina de ondas
- Recomendado para: bastidores, automacao e projetos especiais

### Piscina de Ondas Funcionando - Resultado Final

- ID: `dbIAl2nuZFU`
- URL: https://youtube.com/shorts/dbIAl2nuZFU
- Tema principal: resultado final do projeto da piscina de ondas
- Recomendado para: aplicacoes reais, demonstracao de resultado, inovacao

## Frases E Tom Do Canal

Frases recorrentes que podem ser reconhecidas como identidade do canal, mas nao devem ser usadas em excesso pela IA:

- "Fala, projetista, tudo bem com voce?!"
- "Hey, project maker, how are you?!"
- "Segura na minha mao e vem! Vamos para o video."

A IA pode usar esse tom apenas quando o contexto for descontraido, didatico ou promocional. Em respostas tecnicas, manter objetividade.

## Manutencao Deste Catalogo

Ao adicionar novos videos, manter este padrao:

```md
### Titulo do video

- ID: `VIDEO_ID`
- URL: https://youtu.be/VIDEO_ID
- Thumbnail: https://img.youtube.com/vi/VIDEO_ID/maxresdefault.jpg
- Tipo: video completo | short | live | aula
- Apresentador:
- Tema principal:
- Classes relacionadas:
- Recursos fisicos:
- Recomendado para:
- Informacao:

Capitulos uteis:

| Tempo | Assunto | Link direto |
|---|---|---|
| 00:00 | Assunto | https://youtu.be/VIDEO_ID?t=0 |
```

Sempre que possivel, cadastrar:

- ID do video;
- URL principal;
- links com tempo exato;
- classes relacionadas da LIB ES32Lab;
- recursos fisicos da ES32Lab citados;
- quando recomendar;
- quando nao recomendar.
