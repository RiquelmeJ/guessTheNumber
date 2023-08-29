**Universidade Federal do Cariri**  
**Bacharelado em Ciência da Computação**  
**Alunos:** Karla Mikaelly Paz de Almeida e Riquelme Jatay Ribeiro S. Bezerra  
**Professor:** Ramon Santos Nepomuceno  
# Trabalho de Circuitos Digitais
## Índice
* [Introdução](#introdução)
* [Sobre o jogo](#sobre-o-jogo)
* [Componentes](#componentes)
   + [Decodificador](#decodificador)
   + [Multiplexador](#multiplexador)
   + [Comparador](#comparador)
## Introdução
Olá! Nesse documento, iremos explicar o funcionamento do projeto *Guess The Number* e como ocorreu a construção de cada um dos componentes.
![visão geral do projeto](https://uploaddeimagens.com.br/images/004/590/289/full/projetoGeral.png?1693225424 "visão geral do projeto")
## Sobre o jogo

O primeiro projeto da disciplina consiste em um jogo para dois jogadores construído na plataforma **Logisim**. O objetivo do jogo é adivinhar qual é o número secreto do sistema por meio de chutes e das dicas ao fim de cada rodada. Vencerá o o jogo aquele que adivinhar o número secreto primeiro. O sistema funciona da seguinte forma:
 - para iniciar o jogo, há um botão "Jogar". Cada jogador, em sua vez, deve escolher um número e digitá-lo no sistema binário por meio de um conjunto de botões. Estes, por sua vez, estão ligados em um display de sete segmentos que "converte" a entrada do jogador e a exibe no sistema hexadecimal;
 - logo após, é necessário indicar quem é o jogador da vez por meio do botão homônimo, e o multiplexador permitirá que apenas o palpite do jogador indicado seja analisado pelo comparador;
 - então o comparador, como o nome sugere, comparará a entrada enviada pelo usuário com o número secreto e indicará se o palpite foi errado (no caso, maior ou menor do que o número secreto) ou correto (igual ao número secreto) por meio de 3 saídas.

## Componentes
### Decodificador
Um display de sete segmentos é um dispositivo eletrônico que é frequentemente utilizado para exibir números decimais (em nosso caso, hexadecimais) a partir de números binários. Ele consiste em sete segmentos individuais que podem ser ativados ou desativados independentemente, permitindo a formação de diferentes combinações para representar dígitos ou alguns caracteres especiais, como letras.  
Para esse projeto, os circuitos dos segmentos foram idealizados de forma que representam dígitos de 0 a 9 eletras de A até F, contemplando todos os algarismos necessários para o sistema hexadecimal, ao ligar ou desligar os segmentos apropriados. Por exemplo, para exibir o número "1", devem ser ativados os LEDs "b" e "c".  
Os decodificadores foram projetados a partir da tabela verdade dos caracteres hexadecimais, onde cada expressão lógica gerada pela tabela verdade foi simplificada utilizando a técnica do mapa de Karnaugh e implementada por meio do produto de somas.

![circuitos dos componentes do display](https://uploaddeimagens.com.br/images/004/590/465/full/circuitosDisplay.png?1693231398 "circuitos dos componentes do display")
![decodificador](https://uploaddeimagens.com.br/images/004/590/497/full/decodificador.png?1693232459 "decodificador")
### Multiplexador
O multiplexador é responsável por selecionar um de vários sinais de entrada e encaminhá-lo para a saída, com base em um conjunto de sinais de controle. Em nosso sistema, o seletor se encaminha de controlar qual a saída desejada. Como já é notável, os três principais componentes são as entradas do usuário, o seletor e a sua saída.   
Para a produção desse componente, tomamos como base a explicação dada em aula sobre a tabela verdade e a implementação do multiplexador de 1 saída:
* quando o seletor está em 0, a primeira entrada é repassada. No caso, o 0 do seletor é barrado e chega como um na porta AND, e se o jogador tiver escolhido 0, a porta continuará inativa e repassará 0. Caso contrário, a porta é ativada e repassa o 1 na saída.  
* quando o seletor está em 1, ele é negado na primeira AND e chega como 1 na segunda, permitindo que a jogada do outro jogador defina a saída dessa.

A partir desse, montamos o multiplexador com 4 saídas. Os interruptores mais à esquerda representam as entradas dos jogadores 0 e 1 (de cima para baixo), e o interruptor mais acima seleciona qual dos palpites deve ser repassado para o comparador.

![multiplexador](https://uploaddeimagens.com.br/images/004/591/406/full/Group_1_%282%29.png?1693276175 "multiplexador")
### Comparador
Esse componente é um dos mais importantes para o funcionamento do jogo. Ele é responsável por comparar a entrada do jogador da vez (que chamaremos de A) com o "número secreto" (que chamaremos de B) e retornar a assertividade do chute. Essa parte do projeto foi baseada, em sua grande parte, na [vídeoaula](https://www.youtube.com/watch?v=tVgocuuisjA) do professor Pedro Souza.
![decodificador](https://uploaddeimagens.com.br/images/004/591/374/full/imagem_2023-08-28_221314424.png?1693271598 "decodificador")

Seu funcionamento ocorre da seguinte forma:
- **A = B:** as portas XNOR são responsáveis por comparar se as das entradas são iguais, retornando 1 se sim e 0 caso contrário. Como temos um número de 4 algarismos binários, são necessárias 4 portas para comparar estes com os 4 algarismos do "número secreto". Para que o número seja igual, as 4 portas devem retornar 1; por isso, todas estão ligadas em uma porta AND, e que acenderá a lâmpada com o rótulo "A = B" caso todos os algarismos do chute sejam iguais aos algarismos do número secreto naquela mesma posição;
- **A > B:** para este circuito, utilizamos a lógica de que é possível afirmar se um número é maior que o outro da mesma forma que no decimal, comparando uma posição por vez, daquela com maior valor significativo para o algarismo. Veja um exemplo: temos os números 324 e 224. Mesmo que seus dois últimos algarismos fossem ocultados (3** e 2**), poderíamos afirmar que o primeiro é maior do que o segundo apenas comparando seus algarismos da casa das centenas. Da mesma forma, é possível afirmar a relação de grandeza apenas comparando os algarismos mais à esquerda desses, na mesma posição. Caso esses sejam iguais, pegamos os próximos algarismos mais à esquerda após esses de ambos os números, e assim sucessivamente até chegarmos no algarismo mais à direita de cada número.
	- Veja que o próximos algarismos só serão comparados caso o algarismos anteriores sejam iguais (por isso a ligação das portas XNOR nas portas AND). E que em qualquer um dos casos, se um dos algarismos de A for maior do que o de B naquela posição, mesmo com os anteriores sendo iguais, o sistema indicará que A > B (por isso todas as portas AND dessa parte do circuito estão ligadas em uma só porta OR) por meio da respectiva lâmpada;
 - **A < B:** o funcionamento dessa parte do comparador é o mais simples em relação às anteriores. Ora, se um número X não é igual ou maior do que um número Y, obrigatoriamente X é menor do que Y. Por isso, a lâmpada que indica A < B só acenderá caso as outras duas estejam apagadas.


Veja também que todas as saídas estão ligadas em uma porta AND cada, e que há um interruptor ligado à todas elas. Esse interruptor nada mais é do que o botão "Jogar?" no sistema completo, e a saída do comparador só será exibida se esse estiver ligado.
