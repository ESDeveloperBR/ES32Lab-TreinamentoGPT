# ES32Lab GPT - Indice De Exemplos Oficiais

Versao do conhecimento: `0.9.0`
Atualizado em: `2026-06-20`
Resumo da versao: acompanha a inclusao da Shield 4IN-4Relay Optoacoplada sem alterar indice de exemplos.

Este arquivo relaciona os exemplos oficiais da LIB ES32Lab com temas que o usuario pode pedir para a IA.

Quando o usuario solicitar um codigo, a IA deve usar este indice para indicar exemplos oficiais relacionados.

## LEDs

### LED piscando

- Arquivo: `examples/LEDs/ledBlink/ledBlink.ino`
- Tema: piscar LED, saida digital, `pinMode`, `digitalWrite`
- Classes relacionadas: nenhuma obrigatoria
- Constantes relacionadas: `P17_G`, `P_LED_GREEN`

### LED verde piscando

- Arquivo: `examples/LEDs/ledBlinkGreen/ledBlinkGreen.ino`
- Tema: LED verde da ES32Lab
- Constantes relacionadas: `P17_G`, `P_LED_GREEN`

### LED com potenciometro

- Arquivo: `examples/LEDs/Potentiometer-TimeLedBlink/Potentiometer-TimeLedBlink.ino`
- Tema: LED, potenciometro, intervalo de tempo
- Classes relacionadas: `ES_TimeInterval`
- Constantes relacionadas: `P_POT1`, `P_POT2`

## Potenciometros

- Arquivo: `examples/Potentiometer/Potentiometer-Reading/Potentiometer-Reading.ino`
- Tema: leitura analogica, potenciometro
- Constantes relacionadas: `P_POT1`, `P_POT2`

- Arquivo: `examples/Potentiometer/Potentiometer-TimeLedBlink/Potentiometer-TimeLedBlink.ino`
- Tema: usar potenciometro para controlar tempo
- Classes relacionadas: `ES_TimeInterval`

## Teclado Analogico

- Arquivo: `examples/AnalogKeyboard/AnalogKeyboard-PressKey/AnalogKeyboard-PressKey.ino`
- Tema: detectar pressionamento de tecla
- Classe relacionada: `ES_AnalogKeyboard`

- Arquivo: `examples/AnalogKeyboard/AnalogKeyboard-ReleaseKey/AnalogKeyboard-ReleaseKey.ino`
- Tema: detectar tecla solta
- Classe relacionada: `ES_AnalogKeyboard`

- Arquivo: `examples/AnalogKeyboard/AnalogKeyboard-DebugRead/AnalogKeyboard-DebugRead.ino`
- Tema: diagnostico/calibracao do teclado analogico
- Classe relacionada: `ES_AnalogKeyboard`

## Botao Digital

- Arquivo: `examples/DigitalButton/DigitalButton.ino`
- Tema: botao em GPIO nativa, press, hold, release
- Classe relacionada: `ES_DigitalButton`

## Temporizacao

- Arquivo: `examples/TimeInterval/TimeInterval-intervalMillis/TimeInterval-intervalMillis.ino`
- Tema: executar tarefa por intervalo sem delay
- Classe relacionada: `ES_TimeInterval`

- Arquivo: `examples/TimeInterval/TimeInterval-intervalMicros/TimeInterval-intervalMicros.ino`
- Tema: intervalo em microssegundos
- Classe relacionada: `ES_TimeInterval`

- Arquivo: `examples/TimeInterval/TimeInterval-stopwatchStartMicros/TimeInterval-stopwatchStartMicros.ino`
- Tema: cronometro com microssegundos
- Classe relacionada: `ES_TimeInterval`

## Buzzer

- Arquivo: `examples/Buzzer/ES_Buzzer_HappyBirthday/ES_Buzzer_HappyBirthday.ino`
- Tema: tocar melodia no buzzer
- Classe relacionada: `ES_Buzzer`

- Arquivo: `examples/Buzzer/ES_Buzzer_controlVolumeSpeed/ES_Buzzer_controlVolumeSpeed.ino`
- Tema: volume e velocidade
- Classe relacionada: `ES_Buzzer`

- Arquivo: `examples/Buzzer/ES_Buzzer_controlPitchSpeed/ES_Buzzer_controlPitchSpeed.ino`
- Tema: pitch e velocidade
- Classe relacionada: `ES_Buzzer`

## Expansor I2C PCF8574

- Arquivo: `examples/i2C_Expander/i2C_scanI2C/i2C_scanI2C.ino`
- Tema: localizar dispositivos I2C
- Classe relacionada: `ES_PCF8574`

- Arquivo: `examples/i2C_Expander/i2C_digitalWriteExpander/i2C_digitalWriteExpander.ino`
- Tema: saida digital pelo expansor
- Classe relacionada: `ES_PCF8574`

- Arquivo: `examples/i2C_Expander/i2C_digitalReadExpander/i2C_digitalReadExpander.ino`
- Tema: entrada digital pelo expansor
- Classe relacionada: `ES_PCF8574`

- Arquivo: `examples/i2C_Expander/i2C_button/i2C_button.ino`
- Tema: botao no expansor
- Classe relacionada: `ES_PCF8574`

- Arquivo: `examples/i2C_Expander/i2C_pwm/i2C_pwm.ino`
- Tema: PWM simulado no PCF8574
- Classe relacionada: `ES_PCF8574`

- Arquivo: `examples/i2C_Expander/i2C_motorControlSimple/i2C_motorControlSimple.ino`
- Tema: motor via expansor
- Classe relacionada: `ES_PCF8574`

## Controle De Carro

- Arquivo: `examples/CarControl/differentialSteering_CommandTest/differentialSteering_CommandTest.ino`
- Tema: carro com direcao diferencial
- Classe relacionada: `ES_CarControl`

- Arquivo: `examples/CarControl/frontalSteering_CommandTest/frontalSteering_CommandTest.ino`
- Tema: carro com direcao frontal
- Classe relacionada: `ES_CarControl`

- Arquivo: `examples/CarControl/differentialSteering_Bluetooth/differentialSteering_Bluetooth.ino`
- Tema: carro Bluetooth com direcao diferencial
- Classe relacionada: `ES_CarControl`

- Arquivo: `examples/CarControl/frontalSteering_Bluetooth/frontalSteering_Bluetooth.ino`
- Tema: carro Bluetooth com direcao frontal
- Classe relacionada: `ES_CarControl`

## Robo Seguidor De Linha

- Arquivo: `examples/CarLineFollower/CarLineFollower_Simple/CarLineFollower_Simple.ino`
- Tema: robo seguidor de linha simples
- Classe relacionada: `ES_CarLineFollower`

- Arquivo: `examples/CarLineFollower/CarLineFollower_DisplayKeyboard/CarLineFollower_DisplayKeyboard.ino`
- Tema: robo seguidor de linha com display e teclado
- Classes relacionadas: `ES_CarLineFollower`, `ES_TFT`, `ES_AnalogKeyboard`

## Arquivos

- Arquivo: `examples/File/ES_File-ListAllFiles/ES_File-ListAllFiles.ino`
- Tema: listar arquivos
- Classe relacionada: `ES_File`

- Arquivo: `examples/File/ES_File-Print/ES_File-Print.ino`
- Tema: escrever em arquivo
- Classe relacionada: `ES_File`

- Arquivo: `examples/File/ES_File-ReadFile/ES_File-ReadFile.ino`
- Tema: ler arquivo inteiro
- Classe relacionada: `ES_File`

- Arquivo: `examples/File/ES_File-ReadLine/ES_File-ReadLine.ino`
- Tema: ler linha especifica
- Classe relacionada: `ES_File`

- Arquivo: `examples/File/ES_File-Navigation/ES_File-Navigation.ino`
- Tema: navegar entre arquivos
- Classe relacionada: `ES_File`

## Display TFT

- Arquivo: `examples/Display-TFT/BasicCommands/BasicCommands.ino`
- Tema: comandos basicos do display
- Classe relacionada: `ES_TFT`

- Arquivo: `examples/Display-TFT/Text-DrawString/Text-DrawString.ino`
- Tema: escrever texto no display
- Classe relacionada: `ES_TFT`

- Arquivo: `examples/Display-TFT/Text-PrintAndPrintln/Text-PrintAndPrintln.ino`
- Tema: print e println no display
- Classe relacionada: `ES_TFT`

- Arquivo: `examples/Display-TFT/DrawLine/DrawLine.ino`
- Tema: desenhar linhas
- Classe relacionada: `ES_TFT`

- Arquivo: `examples/Display-TFT/DrawRectangles/DrawRectangles.ino`
- Tema: desenhar retangulos
- Classe relacionada: `ES_TFT`

- Arquivo: `examples/Display-TFT/DrawCircleAndEllipse/DrawCircleAndEllipse.ino`
- Tema: desenhar circulos e elipses
- Classe relacionada: `ES_TFT`

- Arquivo: `examples/Display-TFT/PhotoViewerAnalogKeyboard/PhotoViewerAnalogKeyboard.ino`
- Tema: visualizador de fotos com teclado analogico
- Classes relacionadas: `ES_TFT`, `ES_File`, `ES_AnalogKeyboard`

## Camera

- Arquivo: `examples/Camera/Camera-DisplayTFT/Camera-DisplayTFT.ino`
- Tema: exibir camera no display
- Classes relacionadas: `ES_Camera`, `ES_TFT`

- Arquivo: `examples/Camera/Camera-SaveFrameToSD/Camera-SaveFrameToSD.ino`
- Tema: salvar frame da camera no SD
- Classes relacionadas: `ES_Camera`, `ES_File`

- Arquivo: `examples/Camera/Camera-StreamHTTP/Camera-StreamHTTP.ino`
- Tema: stream HTTP da camera
- Classe relacionada: `ES_Camera`

## Projetos Completos

- Arquivo: `examples/FullProjects/carRCBluetoothDifferentialSteering-ES_CarControl/carRCBluetoothDifferentialSteering-ES_CarControl.ino`
- Tema: carro Bluetooth completo com ES_CarControl
- Classe relacionada: `ES_CarControl`

- Arquivo: `examples/FullProjects/carRCBluetoothFrontalSteering-ES_CarControl/carRCBluetoothFrontalSteering-ES_CarControl.ino`
- Tema: carro Bluetooth com direcao frontal
- Classe relacionada: `ES_CarControl`

- Arquivo: `examples/FullProjects/CarLineFollower_DisplayKeyboard/CarLineFollower_DisplayKeyboard.ino`
- Tema: robo seguidor de linha com display e teclado
- Classes relacionadas: `ES_CarLineFollower`, `ES_CarControl`, `ES_TFT`, `ES_AnalogKeyboard`
