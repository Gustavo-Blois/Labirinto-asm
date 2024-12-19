# Simple Simulator - Documentação

Este projeto implementa um simulador de CPU com uma máquina de controle que segue um ciclo de execução baseado nos estados de **Busca**, **Decodificação** e **Execução**. A máquina de controle transita entre esses estados utilizando um **switch-case**, com a inclusão de ciclos complementares, como **Reset** e **Halt**. Cada ciclo e operação são processados de forma modular, com subciclos dedicados ao tratamento de instruções específicas.

## Sumário

- [Estrutura do Código](#estrutura-do-código)
- [Definições de Estados](#definições-de-estados)
- [Decodificação de Instruções](#decodificação-de-instruções)
- [Instruções Utilizadas](#instruções-utilizadas)
- [Execução Condicional](#execução-condicional)
- [Componentes do Sistema](#componentes-do-sistema)
  - [Multiplexadores (MUX)](#multiplexadores-mux)
  - [Unidade Lógica e Aritmética (ULA)](#unidade-lógica-e-aritmética-ula)
- [Operações Auxiliares](#operações-auxiliares)
- [Detalhes dos Multiplexadores](#detalhes-dos-multiplexadores)
- [Operações da ULA](#operações-da-ula)
- [Processamento do Arquivo CPU.MIF](#processamento-do-arquivo-cpumif)
  - [Funcionalidades](#funcionalidades)
    - [Função `le_arquivo`](#função-le_arquivo)
    - [Função `processa_linha`](#função-processa_linha)
    - [Função `pega_pedaco`](#função-pega_pedaco)

## Estrutura do Código

O código é estruturado de forma modular, com componentes principais para controle do fluxo, manipulação dos dados e execução das instruções. A máquina de controle organiza o fluxo de execução em ciclos, com funções específicas para cada operação.

### Definições de Estados

A máquina de controle define os seguintes estados principais:

- **STATE_FETCH**: Responsável pela busca da próxima instrução na memória.
- **STATE_EXECUTE**: Realiza a execução da instrução atual.
- **STATE_EXECUTE2**: Estado auxiliar utilizado em algumas instruções para operações adicionais.
- **STATE_HALTED**: Indica que a execução foi interrompida ou concluída.

### Decodificação de Instruções

As instruções são decodificadas a partir do campo **opcode**, com suporte para operações como controle de fluxo, manipulação de pilha, manipulação de flags e operações auxiliares.

- **Controle de fluxo**: Instruções como **JMP** e **CALL** alteram o fluxo de execução.
- **Manipulação de pilha**: Instruções como **PUSH**, **POP** e **RTS** manipulam a pilha.
- **Manipulação de flags**: Instruções como **SETC** alteram o valor dos flags de controle (**FR**).
- **Operações auxiliares**: Como **NOP**, **HALT**, e **BREAKP**, para controle do processo.

Algumas instruções dependem do valor dos registradores de flags (**FR**) para determinar se a operação será realizada, como instruções condicionais que verificam se o valor é **maior que**, **menor que**, **igual** ou **overflow**.

## Instruções Utilizadas

### Definições de Estados

- **STATE_FETCH**: Busca a próxima instrução da memória.
- **STATE_EXECUTE**: Executa a instrução que foi buscada.
- **STATE_EXECUTE2**: Estado auxiliar para instruções específicas.
- **STATE_HALTED**: Pausa ou finaliza a execução.

### Decodificação das Instruções

As instruções são interpretadas a partir do **opcode** e executadas de acordo com seu tipo:

- **Controle de fluxo**: **JMP**, **CALL**.
- **Manipulação de pilha**: **PUSH**, **POP**, **RTS**.
- **Manipulação de flags**: **SETC**.
- **Operações auxiliares**: **NOP**, **HALT**, **BREAKP**.

## Execução Condicional

Algumas instruções exigem verificações adicionais com base nos valores dos registradores de flags (**FR**), como operações condicionais de comparação.

## Componentes do Sistema

### Multiplexadores (MUX)

Os multiplexadores são utilizados para selecionar dados de diferentes fontes para operações ou armazenamento:

- **selM1**: Seleciona o endereço de memória a ser acessado. As opções incluem **PC**, **MAR**, **M4**, **SP**.
- **selM2**: Seleciona a origem dos dados para operações ou armazenamento. As opções incluem **ULA**, **DATA_OUT**, **M4**, **SP**.
- **selM3**: Seleciona os dados de entrada da ULA. Pode ser um registrador ou os flags (**FR**).
- **selM5** e **selM6**: Usados para direcionar valores para o **PC**, **memória** ou **flags**.

### Unidade Lógica e Aritmética (ULA)

A ULA realiza operações aritméticas e lógicas entre os valores selecionados pelos multiplexadores. O resultado dessas operações é armazenado no registrador **resultadoUla.result**, enquanto os **flags** são atualizados em **resultadoUla.auxFR**.

## Operações Auxiliares

- **SETC**: Define diretamente o valor do bit **Carry**.
- **HALT**: Finaliza a execução.
- **NOP**: Não realiza operação.
- **BREAKP**: Pausa a execução até interação do usuário.

## Detalhes dos Multiplexadores

Os multiplexadores têm as seguintes funções no sistema:

- **selM1**: Define o endereço a ser acessado na memória.
- **selM2**: Seleciona a origem de dados para o armazenamento ou para operações.
- **selM3**: Selecione os dados de entrada da ULA.
- **selM5 e selM6**: Controlam o direcionamento dos dados para o **PC**, memória ou flags.

## Operações da ULA

A ULA é responsável por realizar operações aritméticas e lógicas entre os dados fornecidos pelos multiplexadores. Após cada operação, o resultado é armazenado e os flags de condição (**FR**) são atualizados conforme o tipo de operação realizada.

## Processamento do Arquivo CPU.MIF

O módulo de processamento de arquivo **CPU.MIF** é responsável por tratar dados de memória lidos de um arquivo específico. Ele lida com a leitura, tratamento e armazenamento dos dados em uma estrutura de memória interna.

### Funcionalidades

#### Função `le_arquivo`
**Descrição**: Lê o arquivo **TestaCPU.mif**, processa os dados e armazena no vetor de memória **MEMORY**.

- Abre o arquivo em modo leitura.
- Remove cabeçalhos não relevantes.
- Processa cada linha do arquivo para extrair dados binários.
- Armazena os valores no vetor de memória de tamanho **TAMANHO_MEMORIA**.
- Gera mensagens de erro para linhas inválidas.

#### Função `processa_linha`
**Descrição**: Processa uma linha do arquivo, convertendo os dados binários para valores numéricos.

- Localiza o separador **:** na linha.
- Lê os 16 bits subsequentes como um número binário.
- Retorna -1 se a linha for inválida (formato incorreto).

#### Função `pega_pedaco`
**Descrição**: Extrai um subconjunto de bits de uma instrução (IR) entre as posições a e b.

- Aplica operações de **bitwise (>>, &)** para isolar os bits desejados.
