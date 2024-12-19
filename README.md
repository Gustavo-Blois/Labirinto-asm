
# Cracker Run - Assembly Game

Este projeto foi desenvolvido como parte da disciplina Organização e Arquitetura de Computadores (SSC0513), oferecida pelo Instituto de Ciências Matemáticas e de Computação (ICMC) da Universidade de São Paulo (USP), sob a orientação do professor Dr. Eduardo do Valle Simões. 

## Descrição

- O projeto é um jogo de labirinto no qual o objetivo é o jogador pegar um payload e inserir ele na rede da federal.

- Para iniciar o jogo, pressione a tecla Backspace. A movimentação pelo mapa é realizada utilizando as teclas "A", "W", "S" e "D".

- O jogo foi projetado para ser executado no Simulador de Processador (https://proc.giroto.dev/) ou no Simple Simulator.

- Link do vídeo de apresentação: https://www.youtube.com/watch?v=KevaJqtyBBI

## Como jogar

Utilize-se preferencialmente o Simulador de Processador, disponível em: https://proc.giroto.dev/.

### Passo a Passo

    1. Baixe os arquivos charmap.mif e Cracker_Run.asm deste repositório.

    2. Em seguida, acesse o Simulador de Processador, disponível em: https://proc.giroto.dev/

    3. No simulador, importe para o campo Charmap o arquivo charmap.mif e, no campo File, importe o arquivo Cracker_Run.asm.

    4. Clique em BUILD para compilar o código e ajuste a frequência conforme sua preferência.

    5. Clique em RUN para iniciar o jogo.

    6. Agora, divirta-se tentando hackear a rede da federal!

## Telas

#### Incial
![Tela Inicial](https://raw.githubusercontent.com/Guilherme2281/fig/refs/heads/main/Tela%20inicial.png)
*Figura 1: Tela Inicial.*


#### Jogo
![Labirinto](https://raw.githubusercontent.com/Guilherme2281/figuras/refs/heads/main/jogo.png?token=GHSAT0AAAAAAC32JO6JVPU6XTOQ2T65EFCOZ3DOSSA)
*Figura 2: Labirinto do jogo.*

#### Concluiu o objetivo
![Tela de ganhador](https://raw.githubusercontent.com/Guilherme2281/fig/refs/heads/main/Objetivo%20com%20concluido.png)
*Figura 3: Fim de jogo.*

## Processador

- O jogo foi desenvolvido para ser executado no processador ICMC desenvolvido pelo professor Dr. Eduardo do Valle Simões, cuja a arquitetura é apresentada na Figura 4. 

- A implementação em linguagem C desse processador está contida na pasta Simulador.

- Mais informações sobre este processador podem ser encontradas no link: https://github.com/simoesusp/Processador-ICMC


![Processador](https://raw.githubusercontent.com/Guilherme2281/fig/refs/heads/main/processador.png)

*Figura 4: Arquitetura do processador ICMC.*


## Autores

- Breno Wingeter de Castilho - N°USP: 15573522

- Guilherme Magalhães Viana - N°USP: 14614394

- Gustavo Blois - N°USP: 13688162

- Ligia Keiko Carvalho - N°USP: 13242363
